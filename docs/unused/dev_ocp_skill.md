# Developing OCP Skills

[OVOS Common Play (OCP)](glossary.md#ocp) is a full-fledged media player, compatible with the [MPRIS standard](glossary.md#mpris). Developing a skill for OCP is similar to writing any other OVOS-compatible skill except basic intents and playing media are handled for the developer. This documentation is a quick start guide for developers hoping to write an OCP skill.

## General Steps

- Create a skill class extending the OCP base class
- In the \_\_init\_\_ method indicate [the media types you want to handle](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin/blob/31701ded43a4f7ff6c02833d6aaf1bc0740257fc/ovos_plugin_common_play/ocp/status.py#L95)
- `self.voc_match(phrase, "skill_name")` to handle specific requests for your skill
- `self.remove_voc(phrase, "skill_name")` to remove matched phrases from the search request
- Implement the `ocp_search` decorator, as many as you want (they run in parallel)
  - The decorated method can return a list or be an iterator of `result_dict` (track or playlist)
  - The search function can be entirely inline or call another Python library, like [pandorinha](https://github.com/OpenJarbas/pandorinha) or [plexapi](https://github.com/pkkid/python-plexapi)
- `self.extend_timeout()` to not let OCP call for a Generic search too soon
  - Place one in each search function so it's extended every time the skill is called
- Implement a confidence score formula
  - [Values are between 0 and 100](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin/blob/31701ded43a4f7ff6c02833d6aaf1bc0740257fc/ovos_plugin_common_play/ocp/status.py#L4)
  - High confidence scores cancel other OCP skill searches
- `ocp_featured_media`, return a playlist for the OCP menu if selected from GUI
- Create a `requirements.txt` file with third-party package requirements
- Create a `skills.json` file for skill metadata

The general interface that OCP expects to receive looks something like the following:

```python
class OVOSAudioTrack(TypedDict):
    uri: str  # URL/URI of media, OCP will handle formatting and file handling
    title: str
    media_type: ovos_plugin_common_play.MediaType
    playback: ovos_plugin_common_play.PlaybackType
    match_confidence: int  # 0-100
    album: str | None  # Parsed even for movies and TV shows
    artist: str | None  # Parsed even for movies and TV shows
    length: int | str | None  # in milliseconds, if present
    image: str | None
    bg_image: str | None
    skill_icon: str | None  # Optional filename for skill icon
    skill_id: str | None  # Optional ID of skill to distinguish where results came from
```

## OCP Skill Template

```python
from os.path import join, dirname

from ovos_plugin_common_play.ocp import MediaType, PlaybackType
from ovos_utils.parse import fuzzy_match
from ovos_workshop.skills.common_play import OVOSCommonPlaybackSkill, \
    ocp_search


class MySkill(OVOSCommonPlaybackSkill):
    def __init__(...):
        super(....)
        self.supported_media = [MediaType.GENERIC,
                                MediaType.MUSIC]   # <- these are the only media_types that will be sent to your skill
        self.skill_icon = join(dirname(__file__), "ui", "pandora.jpeg")

    # score
    @staticmethod
    def calc_score(phrase, match, base_score=0, exact=False):
         # implement your own logic here, assing a val from 0 - 100 per result
        if exact:
            # this requires that the result is related
            if phrase.lower() in match["title"].lower():
                match["match_confidence"] = max(match["match_confidence"], 80)
            elif phrase.lower() in match["artist"].lower():
                match["match_confidence"] = max(match["match_confidence"], 85)
            elif phrase.lower() == match["station"].lower():
                match["match_confidence"] = max(match["match_confidence"], 70)
            else:
                return 0

        title_score = 100 * fuzzy_match(phrase.lower(),
                                        match["title"].lower())
        artist_score = 100 * fuzzy_match(phrase.lower(),
                                         match["artist"].lower())
        if artist_score > 85:
            score += artist_score * 0.85 + title_score * 0.15
        elif artist_score > 70:
            score += artist_score * 0.6 + title_score * 0.4
        elif artist_score > 50:
            score += title_score * 0.5 + artist_score * 0.5
        else:
            score += title_score * 0.8 + artist_score * 0.2
        score = min((100, score))
        return score

    @ocp_search()
    def search_my_skill(self, phrase, media_type=MediaType.GENERIC):
        # match the request media_type
        base_score = 0
        if media_type == MediaType.MUSIC:
            base_score += 10
        else:
            base_score -= 15  # some penalty for proof of concept

        explicit_request = False
        if self.voc_match(phrase, "mySkillNameVoc"):
            # explicitly requested our skill
            base_score += 50
            phrase = self.remove_voc(phrase, "mySkillNameVoc")  # clean up search str
            explicit_request = True
            self.extend_timeout(1)  # we know our skill is slow, ask OCP for more time

        for r in self.search_my_results(phrase):
            yield {
                "match_confidence": self.calc_score(phrase, r, base_score,
                                                    exact=not explicit_request),
                "media_type": MediaType.MUSIC,
                "length": r["duration"] * 1000,  # seconds to milliseconds
                "uri": r["uri"],
                "playback": PlaybackType.AUDIO,
                "image": r["image"],
                "bg_image": r["bg_image"],
                "skill_icon": self.skill_icon,
                "title": r["title"],
                "artist": r["artist"],
                "album": r["album"],
                "skill_id": self.skill_id
            }

```

## skill.json template

```json
{
  "title": "Plex OCP Skill",
  "url": "https://github.com/d-mcknight/skill-plex",
  "summary": "[OCP](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin) skill to play media from [Plex](https://plex.tv).",
  "short_description": "[OCP](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin) skill to play media from [Plex](https://plex.tv).",
  "description": "",
  "examples": [
    "Play Charles Mingus",
    "Play Jamie Cullum on Plex",
    "Play the movie Ghostbusters",
    "Play the movie Ghostbusters on Plex",
    "Play Star Trek the Next Generation on Plex",
    "Play the tv show Star Trek the Next Generation on Plex"
  ],
  "desktopFile": false,
  "warning": "",
  "systemDeps": false,
  "requirements": {
    "python": ["plexapi~=4.13", "ovos-workshop~=0.0.11"],
    "system": {},
    "skill": []
  },
  "incompatible_skills": [],
  "platforms": ["i386", "x86_64", "ia64", "arm64", "arm"],
  "branch": "master",
  "license": "BSD-3-Clause",
  "icon": "https://freemusicarchive.org/legacy/fma-smaller.jpg",
  "category": "Music",
  "categories": ["Music", "Daily"],
  "tags": ["music", "NeonAI", "NeonGecko Original", "OCP", "Common Play"],
  "credits": ["NeonGeckoCom", "NeonDaniel"],
  "skillname": "skill-plex",
  "authorname": "d-mcknight",
  "foldername": null
}
```

## Installing an OCP Skill

[OCP Skills are installed like any other OVOS skill](install_skills.md). The preferred pattern is to release a [pip](https://pypi.org) package for your OCP skill and install it directly, but skills may also be installed directly from any [pip-supported source](https://peps.python.org/pep-0508/) such as `git+https://github.com/OpenVoiceOS/skill-ovos-youtube-music`.

Once a skill has been installed a restart of the `mycroft-skills`, `ovos-skills`, or `neon-skills` service will be required.

## Need Help?

Say hi in [OpenVoiceOS Chat](https://matrix.to/#/!XFpdtmgyCoPDxOMPpH:matrix.org?via=matrix.org) and a team member would be happy to assist you.

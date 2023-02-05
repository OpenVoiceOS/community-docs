# OCP

![](https://github.com/OpenVoiceOS/ovos_assets/blob/master/Logo/ocp.png?raw=true)

[OCP](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin) stands for OpenVoiceOS Common Play, it is a full fledged
media player

## Introduction 

OCP is a [OVOSAbstractApplication](https://github.com/OpenVoiceOS/OVOS-workshop/blob/dev/ovos_workshop/app.py#L47), this
means it is a standalone but native OVOS applicatiom with full voice integration

OCP differs from a typical mycroft-core audio service in several aspects:

- Can run standalone, only needs a bus connection
- OCP provides it's own intents as if it was a skill
- OCP provides it's own GUI as if it was a skill
- mycroft-core CommonPlay skill framework is disabled when OCP loads
- OCP skills have a dedicated MycroftSkill subclass and decorators in ovos-workshop
- OCP skills act as media providers, they do not (usually) handle playback
- mycroft-core CommonPlay skills have an imperfect compatibility layer and are given lower priority over OCP skills
- OCP handles several kinds of playback, including video
- OCP has a sub-intent parser for matching requested media types
- AudioService becomes a subsystem for OCP
- OCP also has AudioService plugin component introducing a compatibility layer for skills using "old style audioservice
  api"
- OCP integrates with MPRIS, it can be controlled from external apps, eg KdeConnect in your phone
- OCP manages external MPRIS enabled players, you can voice control 3rd party apps without writing a skill for it via
  OCP

## OCP Skills

Skills provide search results, think about them as media providers/catalogs for OCP

You can find OCP skills in the [awesome-ocp-skills](https://github.com/OpenVoiceOS/awesome-ocp-skills) list 

### Skills Menu

Some skills provide featured_media, you can access these from the OCP menu

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/ocp/ocp_skills.gif)

### File Browser integration

selected files will be played in OCP

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/ocp/file_browser.gif)

folders are considered playlists

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/ocp/folder_playlist.gif)


## Configuration

### GUI

Some OCP settings are exposed via the GUI

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/ocp/ocp_timeout.gif)

### Advanced

OCP contains a audio service plugin component that acts as a compatibility layer with MycroftAI CommonPlay skills framework. 

in mycroft-core you can set OCP as `default-backend`, ovos-core is not required for OCP

For compatibility and historical reasons OCP reads it's configuration from the `"Audio"` section

```javascript
"Audio": {
    "backends": {
      "OCP": {
        "type": "ovos_common_play",
        "active": true
        // all values below are optional

        // plugin config
        // operational mode refers to the OCP integration
        // "external" - OCP is already running elsewhere, connect by bus only
        // "native" - launch OCP service from the plugin
        // "auto" - if OCP is already running connect to it, else launch it
        // you should only change this if you want to run OCP as a standalone system service
        "mode": "auto",

        // MPRIS integrations
        // integration is enabled by default, but can be disabled
        "disable_mpris": False,
        // dbus type for MPRIS, "session" or "system"
        "dbus_type": "session",
        // allow OCP to control MPRIS enabled 3rd party applications
        // voice enable them (next/prev/stop/resume..)
        // and stop them when OCP starts it's own playback
        // NOTE: OCP can be controlled itself via MPRIS independentely of this setting
        "manage_external_players": False,

        // Playback settings
        // AUTO = 0 - play each entry as considered appropriate,
        //            ie, make it happen the best way possible
        // AUDIO_ONLY = 10  - only consider audio entries
        // VIDEO_ONLY = 20  - only consider video entries
        // FORCE_AUDIO = 30 - cast video to audio unconditionally
        //                   (audio can still play in mycroft-gui)
        // FORCE_AUDIOSERVICE = 40 - cast everything to audio service backend,
        //                           mycroft-gui will not be used
        // EVENTS_ONLY = 50 - only emit ocp events,
        //                    do not display or play anything.
        //                    allows integration with external interfaces
        "playback_mode": 0,

        // ordered list of audio backend preferences,
        // when OCP selects a audio service for playback
        // this list is checked in order until a available backend is found
        "preferred_audio_services": ["vlc", "mplayer", "simple"],

        // when media playback ends "click next"
        "autoplay": True,
        // if True behaves as if the search results are part of the playlist
        //  eg:
        //   - click next in last track -> play next search result
        //   - end of playlist + autoplay -> play next search result
        "merge_search": True,

        // search params
        // minimum time to wait for skill replies,
        // after this time, if at least 1 result was
        // found, selection is triggered
        "min_timeout": 5,
        // maximum time to wait for skill replies,
        // after this time, regardless of number of
        // results, selection is triggered
        "max_timeout": 15,
        // ignore results below min_Score
        "min_score": 50,
        // stop collecting results if we get a
        // match with confidence >= early_stop_thresh
        "early_stop_thresh": 85,
        // sleep this amount before early stop,
        // allows skills that "just miss" to also be taken into account
        "early_stop_grace_period": 0.5,
        // if True emits the regular mycroft-core
        // bus messages to get results from "old style" skills
        "backwards_compatibility": True,
        // allow skills to request more time,
        // extends min_timeout for individual queries (up to max_timeout)
        "allow_extensions": True,
        // if no results for a MediaType, perform a second query with MediaType.GENERIC
        "search_fallback": True,

        // stream extractor settings
        // how to handle bandcamp streams
        // "pybandcamp", "youtube-dl"
        "bandcamp_backend": "pybandcamp",
        // how to handle youtube streams
        // "youtube-dl", "pytube", "pafy", "invidious"
        "youtube_backend": "invidious",
        // the url to the invidious instance to be used"
        // by default uses a random instance
        "invidious_host": None,
        // get final stream locally or from where invidious is hosted
        // This partially allows bypassing geoblocked content,
        // but it is a global flag, not per entry.
        "invidious_proxy": False,
        // different forks of youtube-dl are supported
        // "yt-dlp", "youtube-dl", "youtube-dlc"
        "ydl_backend": "yt-dlp",
        // how to extract live streams from a youtube channel
        // "pytube", "youtube_searcher", "redirect", "youtube-dl"
        // uses youtube auto redirect https://www.youtube.com/{channel_name}/live
        "youtube_live_backend": "redirect"
    }
}
```

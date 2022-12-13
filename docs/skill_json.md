# skill.json

Skills can include a skill.json file in the root of the skill directory

This file contains metadata about the skill and is all you need to submit a skill to some skill marketplaces (eg. Pling)

```javascript
{
  "name": "Wolfram Alpha",
  "description": "Get information from Wolfram Alpha",
  "skillname": "skill-wolfie",
  "authorname": "JarbasSkills",
  "url": "https://github.com/JarbasSkills/skill-wolfie",
  "branch": "v0.1",
  "desktopFile": false,
  "systemDeps": false,
  "download_url": "https://github.com/JarbasSkills/skill-wolfie/archive/v0.1.tar.gz",
  "examples": [
    "ask the wolf what is the speed of light",
    "How tall is Mount Everest?",
    "When was The Rocky Horror Picture Show released?",
    "What is Madonna's real name?",
    "What's 18 times 4?",
    "How many inches in a meter?"
  ],
  "lang": "en-us",
  "lang_support": {
    "pt-pt": {
      "name": "Wolfram Alpha",
      "description": "...",
      "examples": [...]
    }
  }
}
```

# Spec

On the JSON file:
* `name` is a human-readable name for the skill to be used in store listings, UI, etc.
* `description` is a human-readable short description of the skill. This should be limited to one or two sentences max
* `branch` refers to the git tag mentioned above, and can be omitted if the tag is in the URL.
* `desktop_file` should be `true` if your Skill is associated with a FreeDesktop-compliant desktop entry. Most Skills should leave this `false`.
* `systemDeps` should be `true` if your skill requirements include system packages, or `false` if not.
* `icon` can be omitted if the Skill's icon can be resolved another way by OSM.
* `folder` should be omitted unless you know your target device requires it.
* `categories` can list as many categories as you like, and the Skill will appear under each in the Skills Store.`category` refers to the Skill's *primary* category, which is the one that will appear next to its entry when clicked.
* `tags` refers to other search terms you'd like to apply to this Skill. You are encouraged to add as many tags as you feel are appropriate. These will be carefully checked as part of the review process.
* `examples` is a list of example utterances that this skill should handle
* `lang` is the language the `skill.json` and `README.md` files are written in
* `lang_support` is a dict of other supported languages to translated skill `name`, `description`, and `examples`. Missing fields will default to top-level fields

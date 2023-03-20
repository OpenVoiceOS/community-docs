# Installing New Skills

There are a few ways to install skills in ovos.  The official way is to use [osm](https://openvoiceos.github.io/community-docs/osm/)
# OVOS skills manager

Install skills from any appstore!

The [mycroft-skills-manager](https://github.com/MycroftAI/mycroft-skills-manager) alternative that is [not vendor locked](https://github.com/MycroftAI/mycroft-skills-manager/pull/75), this means you must use it responsibly! 

Do not install random skills, different appstores have different policies!

Keep in mind any skill you install can [modify mycroft-core at runtime](https://github.com/JarbasSkills/skill-monkey-patcher), and very likely has 
root access if you are running on a raspberry pi


## Supported stores

- [OVOS]() - this one is really a proof of concept for now, stay tuned!
- [Mycroft Marketplace]() - the official mycroft skills store, all skills are 
  reviewed by humans!
- [Pling]() - the official plasma bigscreen skills store, skills are accepted 
  by default and only removed if flagged as malicious
- [Andlo's skill list]() - not a real appstore, this is a web scrapped 
  automatically generated list of 900+ skills from all over github, there 
  is no review at all, it will catch [malicious skills](https://github.com/JarbasAl/skill-XPLOIT-hijack-speech)

## OpenVoiceOS Skill Manager
``` 
pip install ovos-skills-manager
```
Enable a skill store
``` 
osm enable --appstore [ovos|mycroft|pling|andlo|all]
```
Search for a skill and install it
```
osm install --search
```
[More Information](osm.md)
## Manual Install

### Finding Skills

Most skills are found throughout github.  The official skills can be found at the [OpenVoiceOS](https://github.com/OpenVoiceOS) github page.  Search the repositories for "skills".  There are a few other places they can be found. [Neon AI](https://github.com/NeonGeckoCom) has several skills, and a search through github will for sure find more.

### Installing a found skill

#### pip install

The preferred method is with `pip`. If a skill has a `setup.py` file, it can be installed this way.

The syntax is `pip install git+<github/repository.git>`.

ex. `pip install git+https://github.com/OpenVoiceOS/skill-ovos-date-time.git` should install the ovos-date-time skill

After installing skills this way, ovos skills service needs to be restarted

buildroot / raspbian

`systemctl --user restart mycroft-skills`

manjaro / other system installed services

`systemctl restart mycroft-skills`

#### git install

Skills can also be directly cloned to the skill directory, usually located at `~/.local/share/mycroft/skills/`

enter the skill directory

`cd ~/.local/share/mycroft/skills`

and clone the found skill here with git

`git clone <github/repository.git>`

ex. `git clone https://github.com/OpenVoiceOS/skill-ovos-date-time.git` will install the ovos-date-time skill.

A restart of the ovos-skills service is not required when installing this way.



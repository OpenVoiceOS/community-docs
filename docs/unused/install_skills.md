# Installing New Skills

There are a few ways to install skills in ovos.  The preferred way is with `pip` and a `setup.py` file.

## Finding Skills

Most skills are found throughout github.  The official skills can be found with a simple search in the [OVOS github page](https://github.com/orgs/OpenVoiceOS/repositories?q=skill&type=all&language=&sort=).  There are a few other places they can be found. [Neon AI](https://github.com/NeonGeckoCom) has several skills, and a search through github will for sure find more.

## Installing a found skill

### pip install

The preferred method is with `pip`. If a skill has a `setup.py` file, it can be installed this way.

The syntax is `pip install git+<github/repository.git>`.

ex. `pip install git+https://github.com/OpenVoiceOS/skill-ovos-date-time.git` should install the ovos-date-time skill

They can be installed locally also.

Clone the repository

`git clone https://github.com/OpenVoiceOS/skill-ovos-date-time`

`pip install ./skill-ovos-date-time`

After installing skills this way, ovos skills service needs to be restarted

`systemctl --user restart ovos-skills`


#### git install
This is NOT the preferred method and is here for backward compatabity with the origional `mycroft-core` skills.

Skills can also be directly cloned to the skill directory, usually located at `~/.local/share/mycroft/skills/`

enter the skill directory

`cd ~/.local/share/mycroft/skills`

and clone the found skill here with git

`git clone <github/repository.git>`

ex. `git clone https://github.com/OpenVoiceOS/skill-ovos-date-time.git` will install the ovos-date-time skill.

A restart of the ovos-skills service is not required when installing this way.

[Information on Skills](arch_skills.md)

[Configuring Skills](config_skills.md)

## Depreciated
The OVOS skills manager is in need of some love, and when official skill stores are created, this will be updated to use the new methods.  Until then, this method is **NOT** recomended, and **NOT** supported.  The following is included just as refrence.

### OVOS skills manager

Install skills from any appstore!

The [mycroft-skills-manager](https://github.com/MycroftAI/mycroft-skills-manager) alternative that is [not vendor locked](https://github.com/MycroftAI/mycroft-skills-manager/pull/75), this means you must use it responsibly!

Do not install random skills, different appstores have different policies!

Keep in mind any skill you install can [modify mycroft-core at runtime](https://github.com/JarbasSkills/skill-monkey-patcher), and very likely has
root access if you are running on a raspberry pi


### Supported stores

- [OVOS]() - this one is really a proof of concept for now, stay tuned!
- [Mycroft Marketplace]() - the official mycroft skills store, all skills are
reviewed by humans!
- [Pling]() - the official plasma bigscreen skills store, skills are accepted
by default and only removed if flagged as malicious
- [Andlo's skill list]() - not a real appstore, this is a web scrapped
automatically generated list of 900+ skills from all over github, there
is no review at all, it will catch [malicious skills](https://github.com/JarbasAl/skill-XPLOIT-hijack-speech)

### OpenVoiceOS Skill Manager
```bash
pip install ovos-skills-manager
```
Enable a skill store
```bash
osm enable --appstore [ovos|mycroft|pling|andlo|all]
```
Search for a skill and install it
```bash
osm install --search
```
See more osm commands
```bash
osm --help
osm install --help
```
[More Information](https://github.com/travellingtechie/ovos_skill_manager#readme)

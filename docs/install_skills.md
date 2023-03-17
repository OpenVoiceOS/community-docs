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
  
## Install


```bash
pip install ovos-skills-manager
```

## Usage

osm provides a few command line utilities, explained below

#### Install

Install a mycroft skill! Either pass a search query or a github url

```bash
(.venv) user@hostname:~$ osm install --help
Usage: osm install [OPTIONS]

Options:
  --skill TEXT                    skill to install
  --branch TEXT                   select skill github branch to use
  --folder TEXT                   path where skill will be installed, default
                                  /opt/mycroft/skills

  --search                        search appstores, otherwise assume it's a
                                  github url

  --appstore [ovos|mycroft|pling|andlo|default|all]
                                  search a specific appstore, default search
                                  appstores enabled in config file

  --method [all|name|url|category|author|tag|description]
                                  match this metadata field when searching
  --fuzzy / --exact               exact or fuzzy matching, default fuzzy
  --thresh INTEGER RANGE          fuzzy matching threshold from 0 (everything
                                  is a match) to 100 (exact match),  default
                                  80

  --no-ignore-case                ignore upper/lower case, default ignore
  --help                          Show this message and exit.

```

#### Enable

Enable a new skills store
```bash
(.venv) user@hostname:~$ osm enable --help
Usage: osm enable [OPTIONS]

Options:
  --appstore [ovos|mycroft|pling|andlo|all]
                                  enable a specific appstore
  --help                          Show this message and exit.

```

#### Disable

Disable a skills store
```bash
(.venv) user@hostname:~$ osm disable --help
Usage: osm disable [OPTIONS]

Options:
  --appstore [ovos|mycroft|pling|andlo|all]
                                  disable a specific appstore
  --help                          Show this message and exit.
```

#### Sync

Sync skill list for a skills store

Suggestion: set a cronjob for this
```bash
(.venv) user@hostname:~$ osm sync --help
Usage: osm sync [OPTIONS]

Options:
  --appstore [ovos|mycroft|pling|andlo|default|all]
                                  sync a specific appstore, default syncs
                                  appstores enabled in config file

  --rebuild                       rebuild skill database, if not set only sync
                                  data for new skills

  --merge                         merge skill data, if not set replaces skill
                                  entries

  --github                        augment skill data from github, by default
                                  only saves data provided directly by the
                                  appstore

  --help                          Show this message and exit.
```

#### Priority

Change priority of a skills store, this will affect order of results and 
have impact in the OSM-skill (coming soon) 
```bash
(.venv) user@hostname:~$ osm priority --help
Usage: osm priority [OPTIONS]

Options:
  --appstore [ovos|mycroft|pling|andlo]
                                  change priority of a specific appstore
  --priority INTEGER RANGE        appstore priority, from 0 (highest) to 100
                                  (lowest)

  --help                          Show this message and exit.
```

#### Print config

print current configuration of osm, config file can be found at `~/.config/OpenVoiceOS/OVOS-SkillsManager.json`
```bash
(.venv) user@hostname:~$ osm print --help
Usage: osm print [OPTIONS]

Options:
  --appstore [ovos|mycroft|pling|andlo|all|default]
                                  print config of a specific appstore
  --help                          Show this message and exit.

```

#### Search

Search skills and print results, searching can be done according any number 
of criteria, this is useful for discovery
```bash
(.venv) user@hostname:~$ osm search --help
Usage: osm search [OPTIONS]

Options:
  --query TEXT                    Search a skill with this query
  --method [all|name|url|category|author|tag|description]
                                  match this metadata field when searching
  --appstore [ovos|mycroft|pling|andlo|default|all]
                                  search a specific appstore, by default
                                  searches appstores enabled in config file

  --fuzzy / --exact               exact or fuzzy matching
  --thresh INTEGER RANGE          fuzzy matching threshold from 0 (everything
                                  is a match) to 100 (exact match)

  --no-ignore-case                ignore upper/lower case
  --help                          Show this message and exit.

```



## Manual Install

### Finding Skills

Most skills are found throughout github.  The official skills can be found at the [OpenVoiceOS](https://github.com/OpenVoiceOS) github page.  Search the repositories for "skills".  There are a few other places they can be found. [Neon AI](https://github.com/NeonGeckoCom) has several skills, and a search through github will for sure find more.

### Installing a found skill

#### pip install

The preferred method is with `pip`. If a skill has a `setup.py` file, it can be installed this way.

The syntax is `pip install git+<github/repository.git>`.

ex. `pip install git+https://github.com/OpenVoiceOS/skill-ovos-date-time.git` should install the ovos-date-time skill

After installing skills this way, ovos skills service needs to be restarted

buildroot / ovos-picroft

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

## Skill Libraries
**Editors Note** Coming soon

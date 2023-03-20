# OpenVoiceOS Skill Manager
## Install ovos-skills-manager (osm)

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

  --search                        search appstores, otherwise assume its a
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



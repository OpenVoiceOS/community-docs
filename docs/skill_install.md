# Installing New Skills

There are a few ways to install skills in ovos.  The official way is to use [opm](https://openvoiceos.github.io/community-docs/osm/)

## Manual Install

### Finding Skills

Most skills are found throughout github.  The official skills can be found at the [OpenVoiceOS](https://github.com/OpenVoiceOS) github page.  Search the repositories for "skills".  There are a few other places they can be found. [Neon AI](https://github.com/NeonGeckoCom) has several skills, and a search through github will for sure find more.

### Installing a found skill

#### pip install

The prefered method is with `pip`. If a skill has a `setup.py` file, it can be installed this way.

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

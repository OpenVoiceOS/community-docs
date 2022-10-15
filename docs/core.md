# ovos-core

[OpenVoiceOS](https://openvoiceos.com/) is an open source platform for smart speakers and other voice-centric devices.

OVOS-core is a backwards-compatible descendant of [Mycroft-core](https://github.com/MycroftAI/mycroft-core), the central component of Mycroft. It contains extensions and features not present upstream. 

All Mycroft Skills and Plugins should work normally with OVOS-core. 

OVOS-core is fully modular. Furthermore, common components have been repackaged as plugins. That means it isn't just a great assistant on its own, but also a pretty small library!


## Installing ovos-core

(NOTE: at this early stage, required system libs are presumed, and your distribution might be a question mark.)

We suggest you do this in a virtualenv:

`pip install ovos-core[all]`


## Running ovos-core

`start-mycroft.sh` is available to perform common tasks.

**Note**: MycroftAI's `dev_setup.sh` does not exist in OVOS-core.

Assuming you installed mycroft-core in your home directory, run:

- `cd ~/ovos-core`
- `./start-mycroft.sh debug`

The "debug" command will start the background services (microphone listener, skill, messagebus, and audio subsystems) as
well as bringing up a text-based Command Line Interface (CLI) you can use to interact with Mycroft and see the contents
of the various logs. Alternatively you can run `./start-mycroft.sh all` to begin the services without the command line
interface. Later you can bring up the CLI using `./start-mycroft.sh cli`.

The background services can be stopped as a group with:

- `./stop-mycroft.sh`

## Skills

Mycroft is nothing without skills. There are a handful of default skills, but most need to be installed explicitly.  
See the [Skill Repo](https://github.com/MycroftAI/mycroft-skills#welcome) to discover skills made by others.  
Please share your own interesting work!


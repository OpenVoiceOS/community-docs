# ovos-core

[OpenVoiceOS](https://openvoiceos.com/) is an open source platform for smart speakers and other voice-centric devices.

OVOS-core is a backwards-compatible descendant of [Mycroft-core](https://github.com/MycroftAI/mycroft-core), the central component of Mycroft. It contains extensions and features not present upstream. 

All Mycroft Skills and Plugins should work normally with OVOS-core. 

OVOS-core is fully modular. Furthermore, common components have been repackaged as plugins. That means it isn't just a great assistant on its own, but also a pretty small library!


## Getting Started

ovos-core is very modular, depending on where you are running ovos-core you may want to run only a subset of the services

by default ovos-core only installs the minimum components common to all services, for the purposes of this document we will assume you want a full install

if you want to finetune the components please replace `[all]` in commands below with the subset of desired extras, eg `[skills,bus]`

### Installing ovos-core

ovos-core can be installed from pypi or from source

if install fails you may need to install some system dependencies, how to do this will depend on your distro

```bash
sudo apt install build-essential python3-dev swig libssl-dev libfann-dev portaudio19-dev libpulse-dev
```

**Note**: MycroftAI's `dev_setup.sh` does not exist in OVOS-core.


#### from source

We suggest you do this in a virtualenv:

`pip install git+https://github.com/OpenVoiceOS/ovos-core[all]`

#### from pypi

`pip install ovos-core[all]`

### Running ovos-core

#### Developer launcher script

`start-mycroft.sh` is available to perform common tasks.


Assuming you installed mycroft-core in your home directory, run:

- `cd ~/ovos-core`
- `./start-mycroft.sh debug`

The "debug" command will start the background services (microphone listener, skill, messagebus, and audio subsystems) as
well as bringing up a text-based Command Line Interface (CLI) you can use to interact with Mycroft and see the contents
of the various logs. Alternatively you can run `./start-mycroft.sh all` to begin the services without the command line
interface. Later you can bring up the CLI using `./start-mycroft.sh cli`.

The background services can be stopped as a group with:

- `./stop-mycroft.sh`


#### Automatically on boot

We recommend you create system services to manage ovos instead of depending on the launcher script above

A good explanation can be found here https://github.com/j1nx/mycroft-systemd

A reference implementation can be found in [ovos-buildroot](https://github.com/OpenVoiceOS/ovos-buildroot/tree/develop/buildroot-external/rootfs-overlay/usr/lib/systemd/user)
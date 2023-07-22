# Installing OVOS
The OVOS ecosystem is very modular, depending on where you are running `ovos-core` you may want to run only a subset of the services.

By default `ovos-core` only installs the minimum components common to all services, for the purposes of this document we will assume you want a full install with a GUI.

**NOTE** The GUI requires separate packages in addition to what is required by `ovos-core`.  The [GUI installation](install_gui.md) is covered in its own section.

## Host system
OVOS requires some system dependencies, how to do this will depend on your distro.

Ubuntu/Debian based images.

```
sudo apt install build-essential python3-dev python3-pip swig libssl-dev libfann-dev portaudio19-dev libpulse-dev
```

A few packages are not necessary, but are needed to install from source and may be required for some plugins.  To add these packages run this command.

```
sudo apt install git libpulse-dev cmake libncurses-dev pulseaudio-utils pulseaudio
```

**NOTE**: MycroftAI's `dev_setup.sh` does not exist in OVOS-core.  See the community provided, **WIP**, [manual_user_install](https://github.com/OpenVoiceOS/raspbian-ovos/blob/dev/manual_user_install.sh) for a minimal, almost, replacement.

## Get started
We suggest you do this in a virtualenv.

Create and activate the virtual environment.
```
python -m venv .venv
. .venv/bin/activate
```
Update `pip` and install `wheel`

`pip install -U pip wheel`

## From PyPi

### `ovos-core`
To install a full OVOS software stack with enough skills and plugins to have a working system, the OVOS team includes a subset of packages that can be installed automatically with pip.

It is recommended to use the latest alpha versions until the `0.1.0` release as it contains all of the latest bug fixes and improvements.

**latest stable**

`ovos-core` 0.0.7 does not include the new `extras [mycroft]` so we use `[all]`.

`pip install ovos-core[all]`

**alpha version**

`pip install --pre ovos-core[mycroft]`

This should install everything needed for a basic OVOS software stack.

There are additional `extras` options available other than `[mycroft]` and can be found in the [ovos-core setup.py](https://github.com/OpenVoiceOS/ovos-core/blob/dev/setup.py) file.

[Starting OVOS](starting_intro.md)

### Individual Modules
Each module can be installed independently to only include the parts needed or wanted for a specific system.

**ovos-core**

`pip install --pre ovos-core`

[Starting Modules - core](starting_modules.md#core)

**ovos-messagebus**

`pip install --pre ovos-messagebus`

[Starting Modules - messagebus](starting_modules.md#messagebus)

**ovos-audio**

`pip install --pre ovos-audio`

[Starting Modules - audio](starting_modules.md#audio)

**dinkum-listener**

`pip install --pre ovos-dinkum-listener`

[Starting Modules - listener](starting_modules.md#listener)

**ovos-phal**

`pip install --pre ovos-phal`

[Starting Modules - phal](starting_modules.md#phal)

## From Source
We will use git to clone the repositories to a local directory.  While not specifically necessary, we are assuming this to be the users `HOME` directory.

### ovos-core
Install `ovos-core` from github source files.

`git clone https://github.com/OpenVoiceOS/ovos-core`

The `ovos-core` repository provides `extra` requirements files.  For the complete stack, we will use the `mycroft.txt` file.

`pip install ~/`ovos-core`[mycroft]`

This should install everything needed to use the basic OVOS software stack.

**NOTE** this also installs `lgpl` licenced software.

[Starting OVOS](starting_intro.md)

### Install individual modules

Some systems may not require a full install of OVOS.  Luckily, it can be installed as individual modules.

**core library**

`git clone https://github.com/OpenVoiceOS/ovos-core`

`pip install ~/ovos-core`

This is the minimal library needed as the brain of the system.  There are no skills, no messagebus, and no plugins installed yet.

[Starting Core](starting_modules.md#core)

**messagebus**

`git clone https://github.com/OpenVoiceOS/ovos-messagebus`

`pip install ~/ovos-messagebus`

This is the nervous system of OVOS needed for modules to talk to each other.

[Starting the Messagebus](starting_modules.md#messagebus)

**listener**

OVOS has updated their listener to use `ovos-dinkum-listener` instead of `ovos-listener`.  It is code from [mycroft-dinkum](https://github.com/MycroftAI/mycroft-dinkum) adopted for use with the OVOS ecosystem.  Previous listeners are still available, but not recommended.

`git clone https://github.com/OpenVoiceOS/ovos-dinkum-listener`

`pip install ~/ovos-dinkum-listener`

You now have what is needed for OVOS to use a microphone and its associated services, WakeWords, HotWords, and STT

[Starting the listener](starting_modules.md#listener)

**PHAL**

The OVOS Plugin based Hardware Abstraction Layer is what is used to allow the OVOS software to communicate with hardware devices such as the [operating system](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system) or interacting with the [Mycroft Mark 1 device](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk1).

The PHAL system consists of two interfaces.

`ovos-phal` is the basic interface that normal plugins would use.

`ovos-admin-phal` is used where superuser privileges are needed.

**Be extremely careful when installing `admin-phal` plugins as they provide full control over the host system.**

`git clone https://github.com/OpenVoiceOS/ovos-PHAL`

`pip install ~/ovos-PHAL`

This just installs the basic system that allows the plugins to work.

[Starting PHAL](starting_modules.md#phal)

**audio**

This is the service that is used by OVOS to play all of the audio.  It can be a voice response, or a stream from somewhere such as music, or a podcast.

It also installs [OVOS Common Play](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin) which can be used as a standalone media player and is required for OVOS audio playback.

`git clone https://github.com/OpenVoiceOS/ovos-audio`

`pip install ~/ovos-audio`

This will enable the default TTS (Text To Speech) engine for voice feedback from your OVOS device.  However, plenty of alternative TTS engines are available.

[Starting Audio](starting_modules.md#audio)

You now should have all of the separate components needed to run a full OVOS software stack.

[Starting the OVOS software stack](starting_intro.md)

# OpenVoiceOS

**OVOS is only available for 64Bit systems.  There are some required packages that are not available on 32Bit systems**

[OpenVoiceOS](https://openvoiceos.org/) is an open source platform for smart speakers and other voice-centric devices.

`ovos-core` is a backwards-compatible descendant of [Mycroft-core](https://github.com/MycroftAI/mycroft-core), the central component of Mycroft. It contains extensions and features not present upstream.

All Mycroft Skills and Plugins should work normally with OVOS-core.

`ovos-core` is fully modular. Furthermore, common components have been repackaged as plugins. That means it isn't just a great assistant on its own, but also a pretty small library!

## Getting Started

There a couple of ways to install and use the OVOS ecosystem.

### Prebuilt Images

The easiest and fastest way to experience what OVOS has to offer is to use one of the prebuilt images that the OVOS team has provided.

**NOTE** Images are currently only available for a RPi3b/b+/4.  More may be on the way.

#### Features across all images

- Out of the box support for most USB microphones and speakers.
- Out of the box support for ReSpeaker style HAT's.
- Out of the box support for the Mycroft SJ201 sound card.
- More hardware support to come.
- A small set of pre-installed skills so you may use your assistant right away

- [OVOS - Buildroot Edition](https://drive.google.com/drive/folders/113-zmx6ncoeLNsayseNxoaTlaAk1AfU2)
  - The most complete and advanced image OVOS provides.
  - All packages are built from scratch, optimizing along the way.
- [raspOVOS](https://ovosimages.ziggyai.online/raspbian/newest)
  - raspOVOS provides the complete OVOS ecosystem on top of the official raspbian OS lite image.
    - The "headless" image (NO GUI)
      - Can be run on a RPi3b.
      - This image will provide you with an experience similar to the origional [picroft](https://github.com/MycroftAI/enclosure-picroft)
    - The "GUI" image
      - Similar to the "headless" image, but has a GUI and specific packages installed for convenience.
      - Only runs on a RPi4, the RPi3 does not have enough power to run the GUI.

[Get started with an image](030-qs_intro.md)

### From source as a library

Images are not the only way to use OVOS.  It can be installed on almost any system as a set of Python libraries. `ovos-core` is very modular; depending on where you are running `ovos-core` you may want to run only a subset of the services

This is an advanced setup and requires access to a command shell and can take more effort to get working.

[Get started with OVOS modules](042-install_ovos_core.md)

### Docker

Docker images are also available and have been tested and working on Linux, Windows, and even Mac.

[Get started with OVOS Docker](043-install_ovos_docker.md)

### OVOS Installer

This is the newest way users can install OVOS on their system.
You can choose to install Docker containers, or install OVOS to a virtual environment.

[Get started with OVOS Installer](044-ovos_installer.md)

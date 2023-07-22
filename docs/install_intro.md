# OpenVoiceOS

[OpenVoiceOS](https://openvoiceos.org/) is an open source platform for smart speakers and other voice-centric devices.

`ovos-core` is a backwards-compatible descendant of [Mycroft-core](https://github.com/MycroftAI/mycroft-core), the central component of Mycroft. It contains extensions and features not present upstream.

All Mycroft Skills and Plugins should work normally with OVOS-core. 

`ovos-core` is fully modular. Furthermore, common components have been repackaged as plugins. That means it isn't just a great assistant on its own, but also a pretty small library!

## Getting Started

There a couple of ways to install and use the OVOS ecosystem.

### Prebuilt Images

The easiest and fastest way to experience what OVOS has to offer is to use one of the prebuilt images that the OVOS team has provided.

**NOTE** Images are currently only available for a RPi3b/b+/4.  More may be on the way.

- [Buildroot-ovos](https://drive.google.com/drive/folders/113-zmx6ncoeLNsayseNxoaTlaAk1AfU2)
  - The most complete and advanced image OVOS provides, complete with a default set of skills and a GUI.
- [raspbian-ovos](https://ovosimages.ziggyai.online/raspbian)
  - The newest image from the OVOS team.  This is a "headless" image (NO GUI), but comes with a preinstalled set of skills also.  This image will provide you with an experience similar to the origional [picroft](https://github.com/MycroftAI/enclosure-picroft)

[Get started with an image](qs_intro.md)

### From source as a library

Images are not the only way to use OVOS.  It can be installed on almost any system as a set of Python libraries. `ovos-core` is very modular; depending on where you are running `ovos-core` you may want to run only a subset of the services

This is an advanced setup and requires access to a command shell and can take more effort to get working.

[Get started with OVOS libraries](install_ovos_core.md)

### Docker

Docker images are also available and have been tested and working on Linux, Windows, and even Mac.

[Get started with OVOS Docker](install_ovos_docker.md)

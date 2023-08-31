# OVOS Quick Start Guide

So you just want to give OVOS a try? Here are the three fastest ways to get started:

- [Raspberry Pi](#raspberry-pi)
- [Docker](#docker)
- [Manual Install](#manual-install)

## Raspberry Pi

This quick start will help get an OVOS image installed and running on your Raspberry Pi. These images are all 64-bit operating systems. 32-bit operating systems on the Raspberry Pi will have limited OVOS functionality due to lack of dependency support.

**NOTE:** The OVOS GUI will not reliably run on a RPi3 and is therefore not recommended for that device.

### Download an OVOS image

OVOS provides a couple of different images specifically for the Raspberry Pi: a [headless image (RaspOVOS)](#rasberry-pi-os-latest-images) and an older/work-in-progress [full GUI image (Buildroot)](#buildroot-latest-image).

#### Raspberry Pi OS Latest Images

OVOS also provides a "Headless" image that is similar to the original `picroft` software from `MycroftAI`. It runs without a screen and works with a RPi3b/b+. It is often referred to as **RaspOVOS**.

- [headless images](https://ovosimages.ziggyai.online/raspbian/development)

[Instructions on flashing the image can be found here](flashing_images.md).

#### Buildroot Latest Image

The most advanced and featureful is the Buildroot image. If you want the full GUI, this is currently your only choice. _Please note that this image is older and running on OVOS 0.0.6. A new Buildroot image is in development but not yet available._

- [RPi4-64](https://drive.google.com/file/d/1PUtNXfZ5jMUlVAgyN-KXPdVdX6r51eBw/view?usp=share_link)

[Instructions on flashing the image can be found here](flashing_images.md).

#### Docker on Raspberry Pi

The Docker version of OVOS works well on a Raspberry Pi with any distro. It also has a minimal GUI available. For more information, see the [Docker instructions](#docker).

## Docker

For most users, the easiest way to get started with OVOS is to use Docker. Docker is a containerization platform that allows you to run applications in a sandboxed environment. This means that you can run OVOS on any operating system that supports Docker, including Windows, MacOS, and Linux. Podman is also supported.

The new OVOS buildroot image (under construction) uses Podman to manage the OVOS services, allowing for easy setup and upgrades.

[https://github.com/OpenVoiceOS/ovos-docker](https://github.com/OpenVoiceOS/ovos-docker)

The README at the link above explains how to set up OVOS on Docker for multiple different architectures and operating systems. New images are built nightly.

**NOTE** The Docker images are all running alpha versions of 0.0.7 until OVOS 0.0.8 is released. At that point, users will have the option to choose between alpha or stable versions.

To install Docker, [please see the official documentation](https://docs.docker.com/engine/install/).

## Manual Install

For Debian-based Linux distros, [you can install OVOS manually via a shell script](https://github.com/OpenVoiceOS/raspbian-ovos/blob/dev/manual_user_install.sh). This is not recommended for most users, but may be useful for developers and advanced users.

[OVOS also maintains an Ansible playbook for installing the assistant software](https://github.com/OpenVoiceOS/ovos-ansible). It currently supports Debian-based distros, but support for other distros is planned, and PRs are welcome.

# OVOS Quick Start Guide

So you just want to give OVOS a try? Here are the three fastest ways to get started:

- [Raspberry Pi](#raspberry-pi)
- [Docker](#docker)
- [Manual Install](#manual-install)

**NOTE** All official OVOS images are running alpha versions of 0.0.7 until OVOS 0.0.8 is released. At that point, users will have the option to choose between alpha or stable versions.

## Raspberry Pi

This quick start will help get an OVOS image installed and running on your Raspberry Pi. These images are all 64-bit operating systems.

If you want to build your own 32-bit image for OVOS, note that 32-bit operating systems on the Raspberry Pi will have limited OVOS functionality due to lack of dependency support.

**NOTE:** The OVOS GUI will not reliably run on a RPi3 and is therefore not recommended for that device.

### Download an OVOS image

OVOS provides a couple of different images specifically for the Raspberry Pi: a [headless image built on Raspberry Pi OS (RaspOVOS)](#rasberry-pi-os-latest-images) and an older/work-in-progress [full GUI image (Buildroot)](#buildroot-latest-image).

#### Raspberry Pi OS Latest Images

OVOS provides "headless" images that is similar to the original `picroft` software from `MycroftAI`. It runs without a screen, is built on top of Raspberry Pi OS, and works with a RPi3b/b+.

OVOS also provides a couple of full functioning images with a GUI.

- [raspOVOS images](https://ovosimages.ziggyai.online/raspbian/newest)
  - These are **unstable** builds, and not always working.
  - Backup images of previous builds are [located here](https://ovosimages.ziggyai.online/raspbian/development)

[Instructions on flashing the image can be found here](#flashing_an_image.md).

#### Buildroot Latest Image

The most advanced and featureful is the Buildroot image. It is specifically built for embeded hardware such as the RPi.  **New hardware is being added**

- [RPi4-64](https://drive.google.com/file/d/1PUtNXfZ5jMUlVAgyN-KXPdVdX6r51eBw/view?usp=share_link)

[Instructions on flashing the image can be found here](#flashing_an_image.md).

#### Docker on Raspberry Pi

The Docker version of OVOS works well on a Raspberry Pi with any distro. It also has a minimal GUI available. For more information, see the [Docker instructions](#docker).

## Docker

For most users, the easiest way to get started with OVOS is to use Docker. Docker is a containerization platform that allows you to run applications in a sandboxed environment. This means that you can run OVOS on any operating system that supports Docker, including Windows, MacOS, and Linux. Podman is also supported.

The new OVOS buildroot image (under construction) uses Podman to manage the OVOS services, allowing for easy setup and upgrades.

[https://github.com/OpenVoiceOS/ovos-docker](https://github.com/OpenVoiceOS/ovos-docker)

The README at the link above explains how to set up OVOS on Docker for multiple different architectures and operating systems. New images are built nightly.

To install Docker, [please see the official documentation](https://docs.docker.com/engine/install/).

## Manual Install

OVOS provides an [official installer](https://github.com/OpenVoiceOS/ovos-installer) which should allow you to easily install OVOS to a variety of OS's including Windows and MacOS.  More information on using this tool can be found on the [ovos_installer](044-ovos_installer) page in these docs.

For Debian-based Linux distros, [you can install OVOS manually via a shell script](https://github.com/OpenVoiceOS/raspbian-ovos/blob/dev/manual_user_install.sh). This is not recommended for most users, but may be useful for developers and advanced users.

[OVOS also maintains an Ansible playbook for installing the assistant software](https://github.com/OpenVoiceOS/ovos-ansible). It currently supports Debian-based distros, but support for other distros is planned, and PRs are welcome.

## Need Help?

The OVOS community is always happy to help. If you have any questions, please feel free to ask in the [OVOS Support Matrix room](https://matrix.to/#/#OpenVoiceOS-Support:matrix.org).

## Flashing an image

There are a few ways to flash your image to a drive to use in a Raspberry PI.  Both methods described below will work for either OVOS image that you would like to try.

### Raspberry PI Imager

This method can be used with a Linux or Windows host machine.

The people at raspberry pi provide a great little program made for burning an image to a device.  You can get it [here](https://www.raspberrypi.com/software/).  The team at OVOS has tried to make the setup as simple as possible, and if you follow the steps below, you should have no problems on your first boot.

- Start up the Raspberry Pi Imager.  On Linux, start Raspberry Pi Imager with `sudo raspi-imager`.
- For "Choose OS", select "Use custom" and select the OVOS image file downloaded from the step above.
- For "Choose Storage", select your removable boot media, probably something like "Internal SD Card Reader".
- Then select "Write". Do not click the cog. Do not change the username. Username is ovos and is built in. Do not enter WiFi credentials, you will add them at first boot.

### Linux dd command

**Be careful with the dd command, you can easily render your computer useless if the command is entered wrong**

- Find the location of your boot medium with the `lsblk` command.
- It should show up as something like `sdb`.  If you are unsure what drive it is, remove it, and run the command again.  The one that is missing, is the drive you want to use.
- Write the image to the disk with the `dd` command.

**WARNING: Please make sure you are writing to the correct location, as this is the step that can screw everything up**

  - `sudo dd if=<path_to_unzipped_image> of=<path_to_boot_medium> bs=4M status=progress`
  - This step will take several minutes to complete.
  - When the command is done, and the prompt apears again, finish the process with the command `sudo sync`

  With either method used, you should now have a bootable disk to use with your Raspberry PI


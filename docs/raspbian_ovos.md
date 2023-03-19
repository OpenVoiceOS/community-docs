# raspbian-ovos

Pre-built images are available at the [OpenVoiceOS Downloads Site](https://downloads.openvoiceos.com/images/picroft/github/workspace/pi-gen/deploy/)

OVOS on top of [RaspberryPiOS Lite](https://downloads.raspberrypi.org/raspios_lite_arm64/images/raspios_lite_arm64-2023-02-22/2023-02-21-raspios-bullseye-arm64-lite.img.xz)

[Build your own image](#build-your-own-image)

## Purpose of this guide

This guide will provide you with a minimal HEADLESS ovos system sutable for running on a Raspberry Pi 3.

The RPi3 does not have the processing power to reliably run [ovos-shell](https://github.com/OpenVoiceOS/ovos-shell), the GUI system for OVOS, but has pleanty to run the rest of the stack.

By the end of the guide, you should have a running OVOS stack, (messagebus, phal, skills, voice, and speech), along with a "lite" version of RaspberryPiOS.  Which means you have a package manager, (apt) available to you also.

Source files used by this guide can be found at [raspbian-ovos](https://github.com/OpenVoiceOS/raspbian-ovos).  Any issues or pull requests should be made in this repository.

## Step 1: Create the boot medium

- Download latest lite image and install to SD card or USB.
- There are lots of guides, but [this one is the official guide](https://www.raspberrypi.com/documentation/computers/getting-started.html)
- [This is the suggested download](https://www.raspberrypi.com/software/operating-systems/#raspberry-pi-os-64-bit)

## Step 2: Setup the system
Boot your newly created medium and follow the prompts to create an user.
- Create user `ovos` with password `ovos`
- The system will reboot and ask you to log in.  Log in with the above credentals

### raspi-config

RaspberryPiOS comes with a great tool `raspi-config`.  We need to access that to get started setting things up.

Run the command `sudo raspi-config` to enter the utility.

We will be running everything as a regular user, so we want to auto login.

Enter the `System Options` page

Enter the `Boot / Autologin` page
- Use the second option in the menu.  `Console Autologin`
  - This enables the ovos user to login to a console terminal on every boot

Now we will enable a few interface options.  This will allow us to access our device from a `ssh shell` and prep the PI for other devices that may be used.  Some microphone hats require SPI, or I2C (Respeaker, AIY-Voicebonnet, etc)

Go back to the main menu and enter the `Interface Options` page
- Enable SSH, SPI, I2C
  - After SSH is enabled, the rest of the guide can be done from a remote computer

Back to the main menu and enter the `Localisation Options` page
- Configure Locale, Timezone, WLAN Country

<strong>*** You will need an internet connection to complete the rest of the guide ***</strong>

### Optional: Setup WIFI
Return to the main menu and enter `System Options` again.

Enter the `Wireless LAN` section and follow the prompts

Exit out of the `raspi-config` tool.  And find your IP address.  The command is the same if you used the WiFi setup, or have a LAN connected.

Enter the command `ip addr`

In the output,if things were configured correctly, there will be one or more lines that are relavant.  Find the device that you used to connect, WiFi will start with something like `wlan` and a LAN connection should begin with `eth` or `enp` or something similar.  In the device section, there is an `inet` entry.  The number located there is your local IP address.  It should be in the format `192.168.x.xxx` or something similar.  Write this down, or remember it.  You will use it to log in with a `SSH shell`

Now the device setup is done.  Reboot

`sudo reboot now`

<strong>*** From this point on, you should be able to access your device from any SSH terminal. *** </strong>

For guide for how to do this, see [raspberrypi documentation remote-access](https://www.raspberrypi.com/documentation/computers/remote-access.html)

From a linux machine, open a terminal and enter the command `ssh ovos@<your-remembered-IP-address>`.  There will be a warning making sure you want to connect to this device.  Enter yes, and when asked, enter the password for ovos that you made earlier in the setup. `ovos`

First you need to make sure your system is up to date.  It should be close as you just installed a new image.

`sudo apt -y update && sudo apt -y upgrade`

We should be done with the basic setup now.  You should have a running RaspberryPiOS device with the user `ovos`

## Step 3: Install OVOS-CORE

There are some recommendations to use a venv for ovos. This guide DOES NOT do that.  The ovos headless stack on a RPi3 is about all it can handle.  It is assumed that this is a dedicated ovos device, therefore no venv is required.

There are a few packages required for ovos, so we will install those first

`sudo apt install build-essential python3-dev python3-pip swig libssl-dev libfann-dev portaudio19-dev libpulse-dev cmake git libncurses-dev pulseaudio-utils`

We will be using `pip` to install ovos-core and other related software.  We will also be installing everything to the user environment instead of system wide.  As ovos is the only user, this should be fine.

We will assume that everything from here will be done in the home directory of ovos.

`cd ~`

Clone this repository

`git clone https://github.com/OpenVoiceOS/raspbian-ovos.git`

`cd raspbian-ovos`

Run the install script and follow the prompts

`./manual_install.sh`

<strong>You should now have a running ovos device!!</strong>

Check with this

`systemctl --user status mycroft*`

It takes a while to load, but they should all eventually say `active (running)`, except for `mycroft.service` which should say `active (exited)`

## Step 6: Final thoughts

A generic install of ovos-core does not have any default skills shipped with it.

Check [this page](https://openvoiceos.github.io/community-docs/skills/) for more information on skills.

Audio is also not covered here.  Pulseaudio should be running, check with `systemctl --user status pulseaudio`, but each piece of hardware is different to setup.  I am sure there is a guide somewhere for your hardware.  One thing to mention, this is a full raspbian install, so installing drivers should work also.

<strong>** ================================================================================================= **</strong>


## Build your own image

This has been tested on an Ubuntu 22.04 x86_64 machine.  Others may work, but are not tested

The build system uses [pi-gen](https://github.com/RPi-Distro/pi-gen) which is a tool to create an official Raspberry Pi image.

There are a few dependencies that `pi-gen` needs.  Update and install these

`sudo apt update $$ sudo apt -y upgrade`

`apt-get install coreutils quilt parted qemu-user-static debootstrap zerofree zip dosfstools libarchive-tools libcap2-bin grep rsync xz-utils file git curl bc qemu-utils kpartx gpg pigz`

Switch to your home directory

`cd ~`

Use git to download the latest code.

`git clone https://github.com/RPi-Distro/pi-gen.git`

Use git to download this repository

`git clone https://github.com/OpenVoiceOS/raspbian-ovos.git`

Switch to the pi-gen directory

`cd pi-gen`

The [pi-gen README](https://github.com/RPi-Distro/pi-gen#readme) file has great documentation on how this all works.  Refer there for in depth information.

Run the build script using the configuration file from [raspbian-ovos](https://github.com/OpenVoiceOS/raspbian-ovos/blob/main/raspbian-ovos-config)

This must be run as `sudo` or pi-gen will ask you to do so

`sudo ./build.sh -c ~/raspbian-ovos/raspbian-ovos-config`

This build will probabally take some time, on my build server, 36 core 164G ram, it takes aprox 1.5 hours.

When the build completes, you will have a ziped image located in `~/pi-gen/deploy/`.  This can be unzipped and flashed to a SD card or USB drive just like any other RaspberryPiOS image.

Enjoy your new OVOS device

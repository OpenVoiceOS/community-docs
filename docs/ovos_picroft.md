# ovos-picroft

OVOS on top of [RaspberryPiOS Lite](https://downloads.raspberrypi.org/raspios_lite_arm64/images/raspios_lite_arm64-2023-02-22/2023-02-21-raspios-bullseye-arm64-lite.img.xz)

## Purpose of this guide

This guide will provide you with a minimal HEADLESS ovos system sutable for running on a Raspberry Pi 3.

The RPi3 does not have the processing power to reliably run [ovos-shell](https://github.com/OpenVoiceOS/ovos-shell), the GUI system for OVOS, but has pleanty to run the rest of the stack.

By the end of the guide, you should have a running OVOS stack, (messagebus, phal, skills, voice, and speech), along with a "lite" version of RaspberryPiOS.  Which means you have a package manager, (apt) available to you also.

Source files used by this guide can be found at [ovos-picroft](https://github.com/OpenVoiceOS/ovos-picroft).  Any issues or pull requests should be made in this repository.

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

For guide for how to do this, see https://www.raspberrypi.com/documentation/computers/remote-access.html.

From a linux machine, open a terminal and enter the command `ssh ovos@<your-remembered-IP-address>`.  There will be a warning making sure you want to connect to this device.  Enter yes, and when asked, enter the password for ovos that you made earlier in the setup. `ovos`

First you need to make sure your system is up to date.  It should be close as you just installed a new image.

`sudo apt -y update && sudo apt -y upgrade`

We should be done with the basic setup now.  You should have a running RaspberryPiOS device with the user `ovos`

## Step 3: Install OVOS-CORE

There are some recommendations to use a venv for ovos, this guide DOES NOT do that.  The ovos headless stack on a RPi3 is about all it can handle.  So it is assumed that this is a dedicated ovos device, therefore no venv is required.

There are a few packages required for ovos, so we will install those first

`sudo apt install build-essential python3-dev python3-pip swig libssl-dev libfann-dev portaudio19-dev libpulse-dev cmake git libncurses-dev pulseaudio-utils`

We will be using `pip` to install ovos-core and other related software.  We will also be installing everything to the user environment instead of system wide.  As ovos is the only user, this should be fine.

We will assume that everything from here will be done in the home directory of ovos.

`cd ~`

We will use `pip` to install ovos-core, but we will be using the latest version directly from github.

`git clone https://github.com/OpenVoiceOS/ovos-core`

`pip install ./ovos-core[audio,PHAL,stt,tts,skills_lgpl,skills,bus,skills-essential]`

The rest of the setup requires a few more files.

`git clone https://github.com/OpenVoiceOS/ovos-picroft.git`

## Step 4: Install the systemd files

We will be installing the systemd files as a regular user instead of system wide. The official ovos buildroot images installs these files in `/usr/lib/systemd/user/`. There are guides that say user systemd files can also be placed in `/etc/systemd/user.` or `$HOME/.config/systemd/user/`. We will be using the users home directory to avoid any permission issues.

Enter the cloned repo `ovos-picroft` assuming you cloned this to your home directory

`cd ~/ovos-picroft/systemd/`

Copy the files from there

- `cp * ~/.config/systemd/user/`

Reload the systemd daemon

- `systemctl --user daemon-reload`

Enable the system files

- `systemctl --user enable mycroft*`

## Step 5: Install the executables

These are the files that systemd uses to start ovos.  These include `hooks` for restarting and stopping the services.
- `cd ~/ovos-picroft/exec/`

Here we need to copy the files to the right location.
- `cp * ~/.local/bin/`

And make them executable
- `chmod a+x ~/.local/bin/mycroft*`

These executables require `sdnotify`

- `pip install sdnotify`

Do a reboot

- `sudo reboot now`

This takes a while, especially when you are used to a Rpi4 or x86 install.  Loading everything is about as much as a Rpi3 can handle I think.

<strong>You should now have a running ovos device!!</strong>

Check with this

- `systemctl --user status mycroft*`

It takes a while to load, but they should all say `active (running)`

## Step 6: Final thoughts

A generic install of ovos-core does not have any default skills shipped with it.

Check [this page](https://openvoiceos.github.io/community-docs/skills_service/) for more information on skills.

Audio is also not covered here.  Pulseaudio should be running, check with `systemctl --user status pulseaudio`, but each piece of hardware is different to setup.  I am sure there is a guide somewhere for your hardware.  One thing to mention, this is a full raspbian install, so installing drivers should work also.

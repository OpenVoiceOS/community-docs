# raspbian-ovos (headless)

## Purpose of this guide

This guide describes two ways to create a headless OVOS system suitable for running on a Raspberry Pi 3 or 4. You can either download and burn a prebuilt image to an installation medium like an SD card, or you can use your own installation of the Raspberry PI OS and run an OVOS install script.

The RPi3 does not have the processing power to reliably run [ovos-shell](https://github.com/OpenVoiceOS/ovos-shell), the GUI system for OVOS, but has plenty to run the rest of the stack.

By the end of the guide, you should have a running OVOS stack, (messagebus, phal, skills, listener, and audio), along with a "lite" version of RaspberryPiOS.  Which means you also have a package manager (apt) available to you.

OVOS source files used by this guide can be found at [raspbian-ovos](https://github.com/OpenVoiceOS/raspbian-ovos).  Any issues or pull requests should be made in this repository.

Raspberry Pi Imager is available [here](https://www.raspberrypi.com/software/). There have been issues when using Raspberry Pi Imager to burn pre-built images. From Linux we have had success starting the imager with the command `sudo raspi-imager`.

## Use a pre-built OVOS/PI Environment image saved to an SD card

Download a pre-built OVOS/PI image from [dead link: OpenVoiceOS Downloads Site](https://downloads.openvoiceos.com/images/raspbian/).

Here are two methods to install your OVOS/PI image file onto your SD card.

### Method 1: Write the pre-built OVOS/PI Environment image using Raspberry Pi Imager
- Start up the Raspberry Pi Imager.  On Linux, start Raspberry Pi Imager with "**sudo** raspi-imager".
- For "Choose OS", select "Use custom" and select the OVOS/PI image file downloaded from the OpenVoiceOS Downloads Site.
- For "Choose Storage", select your removable boot media, probably something like "Internal SD Card Reader".
- Then select "Write". Do not click the cog. Do not change the username. Username is ovos and is built in. Do not enter WiFi credentials, you will add them at first boot.

Upon completion, you should have a bootable SD card or USB drive.

### Method 2: Write the OVOS/PI Environment image using the Linux dd command

**Be careful with the dd command, you can easily render your computer useless** 

- If your downloaded image is zipped, unzip the image to the directory of your choice `unzip <path-to-zipped-image>`
- Check where your sd card or usb drive is located using the `lsusb` command.
  - It should be visible as `sdxx`
- Write the unzipped image to the disk `sudo dd if=<path-to-unzipped-image> of=<path-to-sd-card> bs=4M status=progress`

Upon completion, you should have a bootable SD card or USB drive.

### First Boot and Login to the pre-built OVOV/PI Environment image

Insert the SD card, hook up your audio, and turn on your OVOS Pi.

This image comes with a predefined user, `ovos` with password `ovos`.  It is recommended that you change your password on first login.

`sudo passwd ovos`

Enter your new password twice.

On first boot, you will be voice-prompted to connect to `SSID OVOS` and go to the website `start.openvoiceos.com`.  This is **not the official OVOS website** but a local hotspot that the image has created on your Raspberry Pi.

Then from a computer that supports wireless networking, connect to the SSID 'OVOS' and go to the website 'start.openvoiceos.com'. There you can enter the credentials of your WiFi network.  If your sound isn't working, no worries, you can keep scanning your computer's list of nearby SSIDs until you see OVOS, and then connect to the network without hearing the verbal prompt.

This image on a RPi3B takes several minutes to boot before you hear the audio prompt, and several more minutes to finish booting.  If you don't think it's working, please wait up to 3 minutes each time before thinking something went wrong. You can also follow progress on /var/log/syslog.

If for some reason this method does not work, `sudo raspi-config` and `nmtui` are also available.

# The section below is for advanced usage and is NOT currently recommended

## Use an OVOS/PI environment created by cloning a git repository into your own Raspberry Pi OS environment

### Step 1: Two ways to create a Raspberry Pi OS Lite (64 bit) boot SD card

There are lots of guides, but [this one is the official guide](https://www.raspberrypi.com/documentation/computers/getting-started.html)
Our experience with Linux is to invoke the raspi-imager with `sudo raspi-imager`.

- Insert your boot media into your PC.
- Start up the Raspberry Pi Imager. On Linux, start Raspberry Pi Imager with "**sudo** raspi-imager".
- For "Choose OS", select "Raspberry Pi OS Other" and then "Raspberry Pi OS Lite (64 bit)".
- For "Choose Storage", select your removable boot media, probably something like "Internal SD Card Reader" or "USB Flash Disk".

From here you must choose one of two methods:

#### Method 1: Tried, tested, and reliable, but not a headless install

Here we use the Raspberry Pi Imager to write your media **without selecting any Advanced Options**.

- Click "Write".
- After the write completes, insert your SD card in your Pi and boot your newly created medium.
- Create user `ovos` with a password of your choosing.
- The system will reboot and ask you to log in.  Log in as ovos.

Run the command `sudo raspi-config` to enter the Pi setup utility.

We will be running the OVOS environment as a regular user, and we want OVOS to start at boot time, so we want to autologin.

Enter the `System Options` page.

Enter the `Boot / Autologin` page.
- Use the second option in the menu, `Console Autologin`.
  - This enables OVOS to start up automatically at boot time.

Now we will enable a few interface options.  This will allow us to access our device from a `ssh shell` and prep the PI for other devices that may be used.  Some microphone hats require SPI, or I2C (Respeaker, AIY-Voicebonnet, etc).

Go back to the main menu and enter the `Interface Options` page.
- Enable SSH, SPI, and I2C.
  - After SSH is enabled, the rest of the guide can be done from a remote computer.

Go back to the main menu and enter the `Localisation Options` page.
- Configure Locale, Timezone, WLAN Country.

<strong>*** You will need an internet connection to complete the rest of the guide ***</strong>

** Optional: Setup WIFI **

- Return to the main menu and enter `System Options` again.
- Enter the `Wireless LAN` section and follow the prompts.
- Further down from `Wireless Lan` is `Hostname`.  Choose a name for your OVOS device and enter it there. 
- Exit out of the `raspi-config` tool. Next find your IP address.  The command is the same if you used the WiFi setup or have a LAN connected.
- Enter the command `ip addr`.

In the output, if things were configured correctly, there will be one or more lines that are relevant.  Find the device that you used to connect, WiFi will start with something like `wlan` and a LAN connection should begin with `eth` or `enp` or something similar.  In the device section, there is an `inet` entry.  The number located there is your local IP address.  It should be in the format `192.168.x.xxx` or something similar.  Write this down, or remember it.  You will be using it to log in with an `SSH shell`.

Now the device setup is done. Exit raspi-config and reboot.

`sudo reboot now`

#### Method 2: Use Raspberry Pi Imager advanced options to do a headless install of a wireless OVOS Pi

Here we use the Raspberry Pi Imager to write your media **and let the Imager handle your network and SSH setup**.

If your network cannot locate computers by their hostnames, this method will not easily work for you.  In other words, if you cannot ping a network connection with a host name, and you need to use an IP address to ping other network computers, use Method 1 described above. If you are comfortable looking up the OVOS computer's IP address using your router or other network software, Method 2 will still work.

Instead of selecting "Write", click on the cog in the lower right of the Imager panel to open Raspberry Pi Imager advanced options.

In this new panel, check the boxes for:

- "Set hostname" - hostname for your OVOS device goes here.
- "Enable SSH" - this is how you will log into your headless Raspberry Pi.  Use password authentication.
- "Enter a username and password".  For this installation we are using ovos as the username.
- "Configure wireless LAN" (if you're using a wireless connection).  Enter your SSID and wireless password.

Click "Save", then click "Write". Once writing is complete, move the SD card to your OVOS device and boot up.

After logging in as ovos, run the command `sudo raspi-config` to enter the Pi setup utility.

We will be running the OVOS environment as a regular user, and we want OVOS to start at boot time, so we want to autologin.

Enter the `System Options` page.

Enter the `Boot / Autologin` page.

- Use the second option in the menu, `Console Autologin`.
  - This enables OVOS to start up automatically at boot time.

Now we will enable a few interface options.  This will allow us to access our device from a `ssh shell` and prep the PI for other devices that may be used.  Some microphone hats require SPI, or I2C (Respeaker, AIY-Voicebonnet, etc).

Go back to the main menu and enter the `Interface Options` page.

- Enable SPI, and I2C.

Go back to the main menu and enter the `Localisation Options` page.

- Configure Locale, Timezone, WLAN Country.

Now the device setup is done.  Exit raspi-config and reboot.

`sudo reboot now`

### Step 2: ssh to your OVOS device

<strong>*** From this point on, you should be able to access your device from any SSH terminal. *** </strong>

For guide for how to do this, see [raspberrypi documentation remote-access](https://www.raspberrypi.com/documentation/computers/remote-access.html)

From a linux machine, open a terminal and enter the command `ssh ovos@<your-remembered-IP-address>` or `ssh ovos@<your-hostname>`.  There will be a warning making sure you want to connect to this device.  Enter yes, and when asked, enter the password for ovos that you made earlier in the setup.
`ovos`

As a final configuration step, make sure your system is up to date.

`sudo apt -y update && sudo apt -y upgrade`

We should be done with the basic setup now.  You should have a running RaspberryPiOS device with the user `ovos`

### Step 3: Install ovos-core

There are some recommendations to use a venv for OVOS. This guide DOES NOT do that.  The OVOS headless stack on a RPi3 is about all it can handle.  It is assumed that this is a dedicated OVOS device, therefore no venv is required.

We will be cloning code from a git repository, so before starting we need to install git.

`sudo apt install git`

We will also be installing everything to the user environment instead of system wide.  As ovos is the only user, this should be fine.

Although not strictly necessary, we assume that we're starting in the ovos home directory.

`cd ~`

Clone the repository

`git clone https://github.com/OpenVoiceOS/raspbian-ovos.git`

`cd raspbian-ovos`

Run the install script and follow the prompts. It's fine to say yes "Y" to everything.

`./manual_user_install.sh`

<strong>You should now have a running OVOS device!!</strong>

Check your installation with

`systemctl --user status ovos-*`

The full OVOS can take a few minutes to load (especially on a Pi 3), but the processes should all eventually say `active (running)`, except for `ovos.service` which should say `active (exited)`

You can also track progress by watching /var/log/syslog.  Once things slow down you can try saying "Hey Mycroft". In a few seconds (the first time is slow) you should hear a 'ding' from the system. They say "What day is it".  After a delay you should hear information about today's date.

## Final thoughts

Often the audio can take some tuning, and in general is not covered here.  Pulseaudio should be running, check with `systemctl --user status pulseaudio`. Each piece of hardware is different to set up.  I am sure there is a guide somewhere for your hardware.  One thing to mention, this is a full raspbian install, so installing drivers should work also.

Once the OVOS processes are running, if you don't hear a 'ding' after two or three times saying "Hey Mycroft", start up alsamixer and make sure your microphone is recognized and the volume is turned up.  At least one USB microphone (mine) defaults to "Auto Gain Control" which needs to be turned off and replaced by turning up the microphone volume. You may also need to turn up the speaker volume.

This installation of ovos-core only has a few default skills shipped with it.  Check [this page](https://openvoiceos.github.io/community-docs/skills/) for more information on skills.

Please enter suggestions and support requests on our [raspbian-ovos](https://github.com/OpenVoiceOS/raspbian-ovos) github page. Thank you!
# <img src='https://camo.githubusercontent.com/48b782bbddb51b97cf2971fda5817080075f7799/68747470733a2f2f7261772e6769746861636b2e636f6d2f466f7274417765736f6d652f466f6e742d417765736f6d652f6d61737465722f737667732f736f6c69642f636f67732e737667' width='50' height='50' style='vertical-align:bottom'/> Open Voice Operating System - Buildroot Edition

## Getting started.
The buildroot based OpenVoiceOS image is a minimalistic Linux OS bringing the open source voice assistant [ovos-core](https://github.com/OpenVoiceOS/ovos-core) to embbeded, low-spec headless and/or small (touch)screen devices.
This release is to be considered the reference distribution that have all the different building blocks of the OVOS software stack to be merged into one image with the focus on usability. See it as the retail version of OpenVoiceOS.

### Download and flashing


### First run

### Specific features

The OpenVoiceOS buildroot image comes with specific smartspeaker functionality that someone could expect to be present on a voice controlled smartspeaker. The following chapters will describe those specific features. What they are, how they work and how you can configure them.
Some of the features still require manual configuration although later on in time we will aim to have those configuration steps integrated within the whole ovos-core software stack.

#### Auto detection and configuration of HAT's

TODO - write docs

#### KDE Connect

KDE Connect is a multi-platform application developed by KDE, which facilitates wireless communications and data transfer between devices over local networks and is installed and configured by default on the Buildroot based image.

A couple of features of KDE Connect are:

- Shared clipboard: copy and paste between your phone, computer and/or OpenVoiceOS device.
- Share files and URLs instantly from one device to another including your OpenVoiceOS device.
- Multimedia remote control: Use your phone, tablet or computer as a remote for what is playing on your OpenVoiceOS device.
- Auto mute your OpenVoiceOS device when your mobile phone rings.
- Virtual touchpad / keyboard: Use your phone/tablet screen as your OpenVoiceOS device its mouse and keyboard.



#### Airplay

TODO - write docs

#### Spotifyd

To make your ovos device show up as a spotify player uncomment and setup the username and password variables within `~/.config/spotifyd/spotifyd.conf` and reboot

#### Bluetooth speaker

TODO - write docs

#### Snapcast Client & Server

TODO - write docs

#### Remote shared folder access (SMB - Windows)

TODO - write docs

#### Remote shared folder access (NFS - Linux) 

TODO - write docs


## Development.

At this moment development is in very early stages and focussed on the Raspberry Pi 3B & 4. As soon as an initial first workable version
is created, other hardware might be added.

Source code: https://github.com/OpenVoiceOS/ovos-buildroot

### Build Environment

Only use x86_64 based architecture/ hardware to build the image. 

The following example Build environment has been tested :

- Architecture: x86_64 
- Hardware: Intel Core i5 processor, 8GB RAM, 240GB SSD (you can build on less RAM (2GB) and slower storage but more RAM, faster storage =  quicker image building)
- OS: Ubuntu 22.04 LTS desktop

#### Installing System Build Dependencies
The following system packages are required to build the image:

- gcc
- subversion
- qttools5-dev
- qttools5-dev-tools
- python
- git
- make
- g++
- curl
- wget
- qtdeclarative5-dev

#### The following firewall ports need to be allowed to the internet.
In addition to the usual http/https ports (tcp 80, tcp 443) a couple of other ports need to be allowed to the internet :
- tcp 9418 (git).
- tcp 21 (ftp PASV) and random ports for DATA channel. This can be optional but better to have this allowed along with the corresponding random data channel ports. (knowledge of firewalls required)



### Getting the code.
First, get the code on your system! The simplest method is via git.
<br>
- cd ~/
- git clone --recurse-submodules https://github.com/OpenVoiceOS/OpenVoiceOS.git
- cd OpenVoiceOS

### Patching Buildroot.
*(ONLY at the first clean checkout/clone)* If this is the very first time you are going to build an image, you need to execute the following command once;
<br>
- ./scripts/br-patches.sh
<br>
This will patch the Buildroot packages.


## Building the image.
Building the image(s) can be done by utilizing a proper Makefile;
<br>
To see the available commands, just run: 'make help'
<br>
As example to build the rpi4 version;<br>
- make clean
- make rpi4_64-gui-config
- make rpi4_64-gui

Now grab a cup of coffee, go for a walk, sleep and repeat as the build process takes up a long time pulling everything from source and cross compiling everything for the device. Especially the qtwebengine package is taking a LONG time.
<br>
(At the moment there is an outstanding issue which prevents the build to run completely to the end. The plasma-workspace package will error out, not finding the libGLESv4 properly linked within QT5GUI. When the build stopped bacause of this error, edit the following file;
<br><br>
buildroot/output/host/aarch64-buildroot-linux-gnu/sysroot/usr/lib/cmake/Qt5Gui/Qt5GuiConfigExtras.cmake
<br><br>
at the bottom of the file replace this line;
<br><br>
_qt5gui_find_extra_libs(OPENGL "GLESv2" "" "")
<br><br>And replace it bit this line;<br><br>
_qt5gui_find_extra_libs(OPENGL "${CMAKE_SYSROOT}/usr/lib/libGLESv2.so" "" "${CMAKE_SYSROOT}/usr/include/libdrm")
<br><br>
Then you can continue the build process by re-running the "make rpi4_64-gui" command. (DO NOT, run "make clean" and/or "make rpi4_64-gui-config" again, or you will start from scratch again !!!)
<br><br>
When everything goes fine the xz compressed image will be available within the release directory.


### Booting image from sd card for the first time (setting up Wifi and backend).
1.Ensure all required peripherals (mic, speakers, HDMI, usb mouse etc) are plugged in before powering on your RPI4 for the first time.
<br>
2. Skip this step if RPI4 is using an ethernet cable. Once powered on, the screen will present the Wifi setup screen ( a Wifi HotSpot is created). Connect to the Wifi HotSpot (ssid OVOS) from another device and follow the on-screen instructions to setup Wifi.
<br>
3.Once Wifi is setup a choice of Mycroft backend and Local backend is presented. Choose the Mycroft backend for now and follow the on-screen instructions, Local backend is not ready to use yet. After the pairing process has completed and skills downloaded it's time to test/ use it.


### Accessing the CLI.

- SSH to ip address of RPI4 
- default credentials 'mycroft/mycroft'


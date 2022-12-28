# <img src='https://camo.githubusercontent.com/48b782bbddb51b97cf2971fda5817080075f7799/68747470733a2f2f7261772e6769746861636b2e636f6d2f466f7274417765736f6d652f466f6e742d417765736f6d652f6d61737465722f737667732f736f6c69642f636f67732e737667' width='50' height='50' style='vertical-align:bottom'/> Open Voice Operating System - Buildroot Edition

## Getting started.
The buildroot based OpenVoiceOS image is a minimalistic Linux OS bringing the open source voice assistant [ovos-core](https://github.com/OpenVoiceOS/ovos-core) to embbeded, low-spec headless and/or small (touch)screen devices.
This release is to be considered the reference distribution that have all the different building blocks of the OVOS software stack to be merged into one image with the focus on usability. See it as the retail version of OpenVoiceOS.

### Download and flashing

TODO - write docs

### First run

TODO - write docs


## Smartspeaker functionality and features

The OpenVoiceOS buildroot image comes with specific smartspeaker functionality that someone could expect to be present on a voice controlled smartspeaker. The following chapters will describe those specific features. What they are, how they work and how you can configure them.
Some of the features still require manual configuration although later on in time we will aim to have those configuration steps integrated within the whole ovos-core software stack.

### Auto detection and configuration of HAT's

The buildroot OpenVoiceOS editions is considered to be consumer friendly type of device, or as Mycroft A.I. would like to call, a retail version. However as we so not target a specific hardware platform and would like to support custom made systems we are implementing a smart way to detect and configure different type of Raspberry Pi HAT's.

At boot the system scan the I2C bus for known and suppiorted HAT's and if found configures the underlying linux sound system. At the moment this is still very much in development, however the below HAT's are or should soon be supported by this system;
- ReSpeaker 2-mic HAT
- ReSpeaker 4-mic Square HAT
- ReSpeaker 4-mic lineair / 6-mic HAT
- USB devices such as the PS EYE-2
- SJ-201 Dev Kits
- SJ-201 Mark2 retail device

### KDE Connect

KDE Connect is a multi-platform application developed by KDE, which facilitates wireless communications and data transfer between devices over local networks and is installed and configured by default on the Buildroot based image.

A couple of features of KDE Connect are:

- Shared clipboard: copy and paste between your phone, computer and/or OpenVoiceOS device.
- Share files and URLs instantly from one device to another including your OpenVoiceOS device.
- Multimedia remote control: Use your phone, tablet or computer as a remote for what is playing on your OpenVoiceOS device.
- Auto mute your OpenVoiceOS device when your mobile phone rings.
- Virtual touchpad / keyboard: Use your phone/tablet screen as your OpenVoiceOS device its mouse and keyboard.

For the sake of simplicity the below screen shots are made using the iPhone KDE Connect client, however as it is not yet fully feature complete and / or stable, it is recommended to use the Android and / or Linux client. Especially if you would like to have full MPRIS control of your OpenVoiceOS device.

On your mobile device, open the KDE Connect app and it will see the advertised OpenVoiceOS KDE Connect device automatically.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20KDEconnect%20devices.PNG)
Click / Tap on the "OpenVoiceOS-*" to start the pairing process.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20KDEconnect%20initiate%20pairing.PNG)
By clicking / tapping the pair button a similar pop up will appear on the screen of the OpenVoiceOS device. Also click / tap on the pair button finalises the pairing proces allowing your Mobile device to automatically connect with your OpenVoiceOS device and make use of all the extra functionality of what KDE Connect brings.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20KDEconnect%20paired.PNG)

### YouTube Music

A voiceassistant with smartspeaker functionality should be able to play music straight out of the box. For that reason the buildroot edition of OpenVoiceOS comes with the Youtube Music OCP Skill pre-installed. Just ask it to play something will start playback from Youtube assuming the asked sonmg is present on Youtube ofcourse.

Asking "Hey Mycroft, play disturbed sound of silence" should just start playing utilizing OCP as shown below. More information about the full functionality of OCP can be found at it's own chapter.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20OCP%20Playing%201.png)

### Spotifyd

Spotifyd is able to advertise itself on the network without credentials and using zeroconf authentication from Spotify Connect on your mobiles device. This is the default configuration shipped with the buildroot image. If for whatever reason zeroconf is not properly working on your network or you want spotifyd to log in itself you can configure your username and password combination within it's configuration file by uncommenting and configuring the username and password variables within `~/.config/spotifyd/spotifyd.conf` and reboot the device or run `systemctl --user restart spotifyd`.

Open spotify on you mobile device and go to the Devices menu within the Settings or tap the devices menu icon on the left bottom of the now playing screen. An OpenVoiceOS "speaker" device will be present which you can select as output device.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20Spotify%20device%20selection.PNG)

When you play something on Spotify the music will come from your OpenVoiceOS device which will be indicated by the "OPENVOICEOS" indicator on the device menu icon on the top bottom of the now playing screen on your mobile device.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20Spotify%20playing%20on%20OpenVoiceOS.PNG)

As Spotifyd has full MPRIS support including audio player controls, the the full OCP now playing screen will be shown on your OpenVoiceOS device as shown below, just like playing something from Youtube as shown above.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20OCP%20Spotify.png)

### Airplay

By default your OpenVoiceOS device is advertising itself as Airplay (v1 - currently) device on your network. This can be used from either the iOS Airplay selection screen if you play some local files, like shown below;
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20Local%20playback.PNG)
Tap / Click the bottom middle Airplay icon on your music player which opens the Airplay devices menu. It should pick up your OpenVoiceOS device automatically from the network.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20Local%20playback%20Airplay%20menu.PNG)
Select the OpenVoiceOS device to re-route your sound output to your OpenVoiceOS device.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20Local%20playback%20Airplay%20selected.PNG)

The Airplay selection menu is also available within other music clients such as the Spotify app.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20Airplay%20selection.PNG)
And if that client also supports metadata over MPRIS your OpenVoiceOS device will show it on it's screen as well.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20OCP%20Airplay.png)

### Bluetooth speaker

The buildroot edition of OpenVoiceOS by default also acts as a bluetooth speaker. You can find it from any (mobile) device as discoverable within the bluetooth pairing menu.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20Bluetooth%20menu.PNG)
You can pair with it and use your OpenVoiceOS as any other Bluetooth speaker you might own.
(NOTE: At the moment, pairing is broken but will be fixed as soon as we get to it)

### Snapcast Client & Server

TODO - write docs

### Remote shared folder access (SMB - Windows)

Your OpenVoiceOS device is accesable over the network from your Windows computer. This is still a work in process, but you can open a file explorer and navigate to you OpenVoiceOS device.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/SMB%20shares.png)
At the moment the following directories within the user's home directory are shared over the network.
- Documents
- Music
- Pictures
These folders are also used by KDE Connect file transfer plugins and for instance the Camera skill (Hey Mycroft, take a selfie) and / or Homescreen Skill (Hey Mycroft, take a screenshot)

### Remote shared folder access (NFS - Linux) 

In the near future the above Windows network shares are also made available over NFS for Linux clients. This is still a Work In Progress / To Do item.


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


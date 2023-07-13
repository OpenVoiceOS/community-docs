# Booting your OpenVoiceOS device.

Each image has it's own first boot process.

## Buildroot

When you first boot the Buildroot image, you will be greated with an OVOS splash screen as shown below.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Buildroot%20bootsplash.png)

As this is the first time you have booted your device, it might take a bit longer than normal as the system is preparing its local filesystem and extending it over the full size of the sdcard/USB device.
Eventually the progress bar will be filled up indicating the Operating System has been fully booted, after which the ovos-shell animated loading screen will be shown.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Spinner.png)

Again, since this is your first boot, this might take a bit longer as the ovos-core configuration is populated and skills are being setup.

## Raspbian

The Raspbian image is headless, and therefore you will not see these images.  You can still monitor the boot procees by attaching a screen and follow the boot process from the command line.

## Setting up your Wi-Fi network connection

The buildroot image supports setting up the network via two options.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Network%20setup.png)

- On a mobile device
- On the OpenVoiceOS device itself.

You can also skip this step to configure it later or never ask it again if you want your device to run fully offline. (Bear in mind you need to configure your device to use local STT and TTS engines and obvious asking your device things that require internet will not work.  This includes the date and time as a Raspberry Pi does not have a Real Time Clock and therefore does not know this data without being told)

### On Mobile Setup

**This is the defult option for the headless images**

Choosing this option will create a temporarily open network - hotspot called "OVOS" to which you can connect from your mobile device.  The Raspbian image will give a voice prompt to connect to the hotspot and direct you to a webpage that will allow you to connect your device to WiFi.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Connect%20hotspot.png)

On your mobile device go into Settings -> Wi-Fi Settings and the "OVOS" open network will appear in its list.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20WiFi%20network%20list.PNG)

Connect your device with the OVOS network and a webpage will open to configure the Wi-Fi network on your OpenVoiceOS device. (NOTE: On newer mobile operating systems the captive portal capture has changed and the website will not automatically be opened. If this is the case you can open a browser manually and go to http://start.OpenVoiceOS.com)
The following webpage will be shown;

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20WiFi%20setup%20startpage.PNG)

Select your Wi-Fi network from the list, insert your password and press the "Connect" button.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20WiFi%20setup%20filled-in.PNG)

If everything went fine, you will soon see the green "connected" screen, Buildroot only, on your OpenVoiceOS device.  The Raspbian image does NOT have a completed prompt

### On Device Setup

**Not avaliable on headless images**

Choosing this option allows you to set up your Wi-Fi network straight on your OpenVoiceOS device. If selected a screen with the available networks will be shown on your OpenVoiceOS device.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Select%20wifi%20on-device.png)

Select your network from the list and tap / click on it to allow you to insert your password. If you have a touch screen an on-screen keyboard will appear when you tap the password field. If not use a keyboard.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Insert%20wifi%20password.png)

When you have inserted your password, click / tap the connect button and after a short connecting animation, if all went fine you will see the green "connected" screen on your OpenVoiceOS device.

### (Re)configure your network from the drop-down menu

If you have skipped the Wi-Fi network setup before, or you just want to reconfigure your network. On the homescreen of your OpenVoiceOS device swipe down the top menu and click the "Wi-Fi" icon. This brings you to the same on-device configuration screen. 

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Network%20connections.png)

From here you can select another network or click the configuration icon on the right of connected network for details or to remove it from the configured networks.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Connection%20details.png)

## Selecting Your Backend

### What is a backend ?

## No backend - No calling home

**This is the suggested method and is default with the headless images**

**Only the Buildroot image will have these options no further action is required for the headless images**

Select A Text To Speech (TTS) Engine: A text-to-speech (TTS) system converts normal language text into speech, select an engine from the list

![TTS](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/tts.png)

Select A Speech To Text (STT) Engine: A speech-to-text (STT) system converts human speech to text, select an engine from the list

![STT](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/stt.png)

## Personal backend - Host your own

![Personal Backend](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/personal-backend.png)

Personal backend is a reverse engineered alternative to selene and requires the backend to be hosted locally.

- Install and Configure your personal backend, information available on: https://github.com/OpenVoiceOS/ovos-personal-backend
- The gui on device will display a setup page to enter the host address of your hosted backend on your device
- Pairing with your personal backend happens automatically once you hit the confirm button with the correct host address

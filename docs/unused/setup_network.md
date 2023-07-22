# Setting up your Wi-Fi network connection

Depending on which image you downloaded you will be greeted by the network configuration screen with either one or two option. The buildroot image supports setting up the network via two options.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Network%20setup.png)

- On a mobile device
- On the OpenVoiceOS device itself.

You can also skip this step to configure it later or never ask it again if you want your device to run fully offline. (Bear in mind you need to configure your device to use local STT and TTS engines and obvious asking your device things that require internet will not work.)

## On Mobile Setup

Choosing this option will create a temporarily open network - hotspot called "OVOS" to which you can connect from your mobile device.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Connect%20hotspot.png)

On your mobile device go into Settings -> Wi-Fi Settings and the "OVOS" open network will appear in its list.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20WiFi%20network%20list.PNG)

Connect your device with the OVOS network and a webpage will open to configure the Wi-Fi network on your OpenVoiceOS device. (NOTE: On newer mobile operating systems the captive portal capture has changed and the website will not automatically be opened. If this is the case you can open a browser manually and go to http://172.16.127.1 )
The following webpage will be shown;

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20WiFi%20setup%20startpage.PNG)

Select your Wi-Fi network from the list, insert your password and press the "Connect" button.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20WiFi%20setup%20filled-in.PNG)

If everything went fine, you will soon see the green "connected" screen on your OpenVoiceOS device.

## On Device Setup

Choosing this option allows you to set up your Wi-Fi network straight on your OpenVoiceOS device. If selected a screen with the available networks will be shown on your OpenVoiceOS device.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Select%20wifi%20on-device.png)

Select your network from the list and tap / click on it to allow you to insert your password. If you have a touch screen an on-screen keyboard will appear when you tap the password field. If not use a keyboard.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Insert%20wifi%20password.png)

When you have inserted your password, click / tap the connect button and after a short connecting animation, if all went fine you will see the green "connected" screen on your OpenVoiceOS device.

## (Re)configure your network from the drop-down menu

If you have skipped the Wi-Fi network setup before, or you just want to reconfigure your network. On the homescreen of your OpenVoiceOS device swipe down the top menu and click the "Wi-Fi" icon. This brings you to the same on-device configuration screen. 

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Network%20connections.png)

From here you can select another network or click the configuration icon on the right of connected network for details or to remove it from the configured networks.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Connection%20details.png)
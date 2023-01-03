# Spotifyd

Spotifyd is able to advertise itself on the network without credentials and using zeroconf authentication from Spotify Connect on your mobiles device. This is the default configuration shipped with the buildroot image. If for whatever reason zeroconf is not properly working on your network or you want spotifyd to log in itself you can configure your username and password combination within it's configuration file by uncommenting and configuring the username and password variables within `~/.config/spotifyd/spotifyd.conf` and reboot the device or run `systemctl --user restart spotifyd`.

Open spotify on you mobile device and go to the Devices menu within the Settings or tap the devices menu icon on the left bottom of the now playing screen. An OpenVoiceOS "speaker" device will be present which you can select as output device.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20Spotify%20device%20selection.PNG)

When you play something on Spotify the music will come from your OpenVoiceOS device which will be indicated by the "OPENVOICEOS" indicator on the device menu icon on the top bottom of the now playing screen on your mobile device.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/iPhone%20-%20Spotify%20playing%20on%20OpenVoiceOS.PNG)

As Spotifyd has full MPRIS support including audio player controls, the the full OCP now playing screen will be shown on your OpenVoiceOS device as shown below, just like playing something from Youtube as shown above.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20OCP%20Spotify.png)

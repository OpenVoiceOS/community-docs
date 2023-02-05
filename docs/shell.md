# OVOS Shell

[OVOS-shell](https://github.com/OpenVoiceOS/ovos-shell) is the OpenVoiceOS client implementation of the mycroft-gui library used in our embedded device images

## Plugins

OVOS-shell is tightly coupled to [PHAL](#what-is-phal), the following companion plugins should be installed if you are using ovos-shell

- [ovos-PHAL-plugin-notification-widgets](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-notification-widgets)
- [ovos-PHAL-plugin-network-manager](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-network-manager)
- [ovos-PHAL-plugin-gui-network-client](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-gui-network-client)
- [ovos-PHAL-plugin-wifi-setup](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-wifi-setup)
- [ovos-PHAL-plugin-alsa](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-alsa)
- [ovos-PHAL-plugin-system](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system)
- [ovos-PHAL-plugin-dashboard](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-dashboard)
- [ovos-PHAL-plugin-brightness-control-rpi](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-brightness-control-rpi)
- [ovos-PHAL-plugin-color-scheme-manager](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-color-scheme-manager)
- [ovos-PHAL-plugin-configuration-provider](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-configuration-provider)

## Alternative Clients

Other distributions may offer alternative implementations such as:

- [mycroft-gui](https://github.com/MycroftAI/mycroft-gui) also hosts a client for developers on the desktop.
- [plasma-bigscreen](http://invent.kde.org/plasma/plasma-bigscreen)
- [mycroft mark2](https://github.com/MycroftAI/mycroft-gui-mark-2)

## Configuration
The Shell can be configured in a few ways.

### GUI

Display settings

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/shell_settings.gif)

### Shell Options
`~/.config/OpenvoiceOS/OvosShell.conf` can be edited to change shell options that
may also be changed via UI. An example config would look like:
```
[General]
fakeBrightness=1
menuLabels=true
```

### Themes
Shell themes can be included in `/usr/share/OVOS/ColorSchemes/` or 
`~/.local/share/OVOS/ColorSchemes/` in json format. Note that colors should include
an alpha value (usually `FF`).

```json
{
  "name": "Neon Green",
  "primaryColor": "#FF072103",
  "secondaryColor": "#FF2C7909",
  "textColor": "#FFF1F1F1"
}
```
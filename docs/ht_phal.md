# OVOS PHAL
[PHAL](https://github.com/OpenVoiceOS/ovos_PHAL) is our Platform/Hardware Abstraction Layer, it completely replaces the concept of hardcoded "enclosure" from `mycroft-core`.

Any number of plugins providing functionality can be loaded and validated at runtime, plugins can
be [system integrations](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system) to handle things like reboot and shutdown, or hardware drivers such as [Mycroft Mark 2 plugin](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk2).

PHAL plugins can perform actions such as hardware detection before loading, eg, the mark2 plugin will not load if it does not detect the sj201 hat. This makes plugins safe to install and bundle by default in our base images.


## Plugins

Platform/Hardware specific integrations are loaded by PHAL, these plugins can handle all sorts of system activities.

| Plugin                                                                                                            | Description                          |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| [ovos-PHAL-plugin-alsa](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-alsa)                                     | volume control                       |
| [ovos-PHAL-plugin-system](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system)                                 | reboot / shutdown / factory reset    |
| [ovos-PHAL-plugin-mk1](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk1)                                       | mycroft mark1 integration            |
| [ovos-PHAL-plugin-mk2](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk2)                                       | mycroft mark2 integration            |
| [ovos-PHAL-plugin-respeaker-2mic](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-respeaker-2mic)                 | respeaker 2mic hat integration       |
| [ovos-PHAL-plugin-respeaker-4mic](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-respeaker-4mic)                 | respeaker 4mic hat integration       |
| [ovos-PHAL-plugin-wifi-setup](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-wifi-setup)                         | wifi setup (central plugin)          |
| [ovos-PHAL-plugin-gui-network-client](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-gui-network-client)         | wifi setup (GUI interface)           |
| [ovos-PHAL-plugin-balena-wifi](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-balena-wifi)                       | wifi setup (hotspot)                 |
| [ovos-PHAL-plugin-network-manager](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-network-manager)               | wifi setup (network manager)         |
| [ovos-PHAL-plugin-brightness-control-rpi](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-brightness-control-rpi) | brightness control                   |
| [ovos-PHAL-plugin-ipgeo](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-ipgeo)                                   | automatic geolocation  (IP address)  |
| [ovos-PHAL-plugin-gpsd](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-gpsd)                                     | automatic geolocation  (GPS)         |
| [ovos-PHAL-plugin-dashboard](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-dashboard)                           | dashboard control (ovos-shell)       |
| [ovos-PHAL-plugin-notification-widgets](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-notification-widgets)     | system notifications (ovos-shell)    |
| [ovos-PHAL-plugin-color-scheme-manager](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-color-scheme-manager)     | GUI color schemes (ovos-shell)       |
| [ovos-PHAL-plugin-configuration-provider](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-configuration-provider) | UI to edit mycroft.conf (ovos-shell) |
| [ovos-PHAL-plugin-analog-media-devices](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-analog-media-devices)     | video/audio capture devices (OCP)    |

![flow](img/phal_or_skill.png)

## Admin PHAL

AdminPHAL performs the exact same function as PHAL, but plugins it loads will have `root` privileges.

This service is intended for handling any OS-level interactions requiring escalation of privileges. Be very careful when installing Admin plugins and scrutinize them closely

NOTE: Because this service runs as root, plugins it loads are responsible for not writing configuration changes which would result in breaking config file permissions.

### Admin Plugins

AdminPlugins are just like regular PHAL plugins that run with `root` privileges.

Admin plugins will only load if their configuration contains `"enabled": true`. All admin plugins need to be explicitly enabled.

You can find plugin packaging documentation [here](https://openvoiceos.github.io/community-docs/OPM/#packaging).

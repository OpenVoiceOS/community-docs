# OCA - OVOS Config Assistant

[OCA](https://github.com/OpenVoiceOS/ovos-config-assistant) is a user facing interface to configure ovos devices


## Web UI

OCA provides a local Web UI similar to ovos-backend-manager, in here you can configure your device, view metrics, handle OAuth and more

## CLI

A command line interface is planned but not yet available to provide equivalent functionality to the Web UI

## Python utils

```python
from ovos_config_assistant.module_helpers import pprint_core_module_info
pprint_core_module_info()
"""
## Mycroft module info
     can import mycroft     : True
     is ovos-core           : True
     mycroft module location: /home/user/ovos-core/mycroft

## Downstream ovos.conf overrides
Module: neon_core
     can import neon_core     : False
     neon_core module location: None
     xdg compliance            : True
     base xdg folder           : neon
     mycroft config filename   : neon.conf
     default mycroft.conf path :
          /home/user/NeonCore/neon_core/configuration/neon.conf
Module: hivemind
     can import hivemind     : False
     hivemind module location: None
     xdg compliance            : True
     base xdg folder           : hivemind
     mycroft config filename   : hivemind.conf
     default mycroft.conf path :
          /home/user/PycharmProjects/ovos_workspace/ovos-core/.venv/lib/python3.9/site-packages/mycroft/configuration/mycroft.conf

## Downstream module overrides:
Module: neon_speech
     uses config from   : neon_core
     can import neon_speech     : False
     neon_speech module location: None
Module: neon_audio
     uses config from   : neon_core
     can import neon_audio     : False
     neon_audio module location: None
Module: neon_enclosure
     uses config from   : neon_core
     can import neon_enclosure     : False
     neon_enclosure module location: None
Module: hivemind_voice_satellite
     uses config from   : hivemind
     can import hivemind_voice_satellite     : True
     hivemind_voice_satellite module location: /home/user/HiveMind-voice-sat/hivemind_voice_satellite
"""

from ovos_config_assistant.config_helpers import pprint_ovos_conf
pprint_ovos_conf()
"""
## OVOS Configuration
 ovos.conf exists          : True
      /home/user/.config/OpenVoiceOS/ovos.conf
 xdg compliance            : True
 base xdg folder           : mycroft
 mycroft config filename   : mycroft.conf
 default mycroft.conf path :
      /home/user/ovos-core/.venv/lib/python3.9/site-packages/mycroft/configuration/mycroft.conf
"""
```

# ovos-core vs mycroft-core

## Speech Client

| Feature                   | Mycroft | OVOS | Description                                                   | 
|---------------------------|---------|------|---------------------------------------------------------------|
| Wake Word (listen)        | yes      | yes  | Only transcribe speech (STT) after a certain word is spoken   |  
| Wake Up Word (sleep mode) | yes      | yes  | When in sleep mode only listen for "wake up" (no STT)         |
| Hotword (bus event)       | no      | yes  | Emit bus events when a hotword is detected (no STT)           | 
| Multiple Wake Words       | no      | yes  | Load multiple hotword engines/models simultaneously           | 
| Fallback STT              | no      | yes  | fallback STT if the main one fails (eg, internet outage)      |
| Instant Listen            | no      | yes  | Do not pause between wake word detection and recording start  | 
| Hybrid Listen             | no      | WIP  | Do not require wake word for follow up questions              |
| Continuous Listen         | no      | WIP  | Do not require wake word, always listen using VAD             |
| Recording mode            | no      | WIP  | Save audio instead of processing speech                       |
| Wake Word Plugins         | yes      | yes  | Supports 3rd party integrations for hotword detection         |  
| STT Plugins               | yes      | yes  | Supports 3rd party integrations for STT                       | 
| VAD plugins               | no   *  | yes  | Supports 3rd party integrations for voice activiy detection   |

NOTES:

- [HiveMind Voice Satellite](https://github.com/JarbasHiveMind/HiveMind-voice-sat) uses ovos-core and supports the same
  features
- Pyaudio has a bug in python 3.10, you may need to use [this fork](https://git.skeh.site/skeh/pyaudio) (ovos-core and
  mk2 only)
- VAD is supported in mycroft mark2 branch, but is hardcoded for silero
- Sleep mode loop has been [rewritten in ovos-core](https://github.com/OpenVoiceOS/ovos-core/pull/10) and is much more
  responsive than mycroft
- [Mic handling logic](https://github.com/OpenVoiceOS/ovos-core/pull/82) has been ported from mk2 branch and is much
  more responsive than mycroft dev branch
- Instant / Hybrid / Continuous listen settings are experimental, good microphone and AEC are highly recommended (such
  as a mark2)
- in ovos-core this functionality has
  been [refactored and moved](https://github.com/OpenVoiceOS/ovos-core/tree/dev/mycroft/listener) to the
  new `mycroft.listener`module

## Audio

| Feature           | Mycroft | OVOS | Description                   | 
|-------------------|---------|------|-------------------------------|
| MPRIS integration | no      | yes   | Integrate with MPRIS protocol |

NOTES:

- [OCP](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin) can be used with mycroft-core, but not mk2
- OCP can be controlled via MPRIS, eg. KDEConnect
- OCP can control MPRIS enabled players, eg. spotify

## Skills

| Feature           | Mycroft | OVOS | Description                                                                                                            |
|-------------------|---------|------|------------------------------------------------------------------------------------------------------------------------|
| Skill Plugins     | no      | yes  | skills can be packaged like standard python projects and installed via setup.py (eg. with pip or your package manager) | 
| User Resources    | no      | yes  | Users can override resource files, eg. customize dialogs for installed skills                                          |
| Skill permissions | no      | WIP  | Users can limit converse and fallback functionality per skill and configure the order in which skills are executed     | 
| Intent Plugins    | no      | WIP  | Supports 3rd party integrations for Intent Matching                                                                    | 

## Hardware

| Feature        | Mycroft | OVOS | Description                                                                                                                                                                                                     | 
|----------------|---------|------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| System Plugins | no      | yes   | Support for 3rd party hardware (eg. [mk2-plugin](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk2)) and OS level integrations (eg. [wifi-setup](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-wifi-setup)) | 

NOTES:

- PHAL can be used with mycroft-core

## Misc

| Feature          | Mycroft | OVOS | Description                                                      | 
|------------------|---------|------|------------------------------------------------------------------|
| Offline usage    | no      | yes  | Can be configured to work without internet connectivity          | 
| MultiLingual     | no      | WIP  | Can be configured to work in multiple languages at the same time |
| HiveMind support | WIP     | WIP  | Supports HiveMind for a distributed/remote mycroft experience    | 
| XDG compliance   | WIP     | yes  | All resources respect XDG standards and support multiple users   |
| Usage as a lib   | no      | yes  | Packaged as a library, supports derivative voice assistants      |

NOTES:

- [HiveMind](https://github.com/JarbasHiveMind) is being developed against ovos-core, development under mycroft-core is
  stalled, see the [hivemind wiki](https://github.com/JarbasHiveMind/HiveMind-core/wiki/Mycroft-Messages) for details
- XDG support includes multiple skill directories, all skill data, all configuration files, and all cached files
- You can build your own assistant on top of ovos-core, multiple assistants
  can [co-exist in the same machine and use their own configuration files](https://github.com/OpenVoiceOS/ovos-config/blob/dev/ovos_config/meta.py)
  , ovos-core is packaged like a regular python package and can be handled as a requirement by package managers
    - examples projects: [neon-core](https://github.com/NeonGeckoCom/NeonCore/)
      , [hivemind-voice-sat](https://github.com/JarbasHiveMind/HiveMind-voice-sat)

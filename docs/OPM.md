# OPM

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/72edbcca11ac25b09d164afb42bf04cee23b801d/Logo/Raw/opm-logo.svg)

OPM is the [OVOS Plugin Manager](https://github.com/OpenVoiceOS/OVOS-plugin-manager), this base package provides
arbitrary plugins to the ovos ecosystem

OPM plugins import their base classes from OPM making them portable and independent from core, plugins can be used in
your standalone projects

By using OPM you can ensure a standard interface to plugins and easily make them configurable in your project, plugin
code and example configurations are mapped to a string via python entrypoints in setup.py

## Plugins

### STT

| Plugin                                                                                                             | Offline | Type       | 
|--------------------------------------------------------------------------------------------------------------------|---------|------------|
| [ovos-stt-plugin-vosk](https://github.com/OpenVoiceOS/ovos-stt-plugin-vosk)                                        | yes     | FOSS       |
| [ovos-stt-plugin-chromium](https://github.com/OpenVoiceOS/ovos-stt-plugin-chromium)                                | no      | API (free) |
| [neon-stt-plugin-google_cloud_streaming](https://github.com/NeonGeckoCom/neon-stt-plugin-google_cloud_streaming)   | no      | API (key)  |
| [neon-stt-plugin-scribosermo](https://github.com/NeonGeckoCom/neon-stt-plugin-scribosermo)                         | yes     | FOSS       |  
| [neon-stt-plugin-silero](https://github.com/NeonGeckoCom/neon-stt-plugin-silero)                                   | yes     | FOSS       | 
| [neon-stt-plugin-polyglot](https://github.com/NeonGeckoCom/neon-stt-plugin-polyglot)                               | yes     | FOSS       | 
| [neon-stt-plugin-deepspeech_stream_local](https://github.com/NeonGeckoCom/neon-stt-plugin-deepspeech_stream_local) | yes     | FOSS       | 
| [ovos-stt-plugin-pocketsphinx](https://github.com/OpenVoiceOS/ovos-stt-plugin-pocketsphinx)                        | yes     | FOSS       |

### TTS

| Plugin                                                                                            | Offline | Type              |
|---------------------------------------------------------------------------------------------------|---------|-------------------|
| [ovos-tts-plugin-mimic](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic)                     | yes     | FOSS              |
| [ovos-tts-plugin-mimic2](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic2)                   | no      | API (free)        |
| [neon-tts-plugin-larynx_server](https://github.com/NeonGeckoCom/neon-tts-plugin-larynx_server)    | no      | API (self hosted) |
| [ovos-tts-server-plugin](https://github.com/OpenVoiceOS/ovos-tts-server-plugin)                   | no      | API (self hosted) |
| [ovos-tts-plugin-pico](https://github.com/OpenVoiceOS/ovos-tts-plugin-pico)                       | yes     | FOSS              |
| [neon-tts-plugin-glados](https://github.com/NeonGeckoCom/neon-tts-plugin-glados)                  | yes     | FOSS              |
| [neon-tts-plugin-mozilla_local](https://github.com/NeonGeckoCom/neon-tts-plugin-mozilla_local)    | yes     | FOSS              |
| [ovos-tts-plugin-cotovia](https://github.com/OpenVoiceOS/ovos-tts-plugin-cotovia)                 | yes     | FOSS              |
| [neon-tts-plugin-polly](https://github.com/NeonGeckoCom/neon-tts-plugin-polly)                    | no      | API (key)         |
| [ovos-tts-plugin-voicerss](https://github.com/OpenVoiceOS/ovos-tts-plugin-voicerss)               | no      | API (key)         |
| [ovos-tts-plugin-google-TX](https://github.com/OpenVoiceOS/ovos-tts-plugin-google-TX)             | no      | API (free)        |
| [ovos-tts-plugin-responsivevoice](https://github.com/OpenVoiceOS/ovos-tts-plugin-responsivevoice) | no      | API (free)        |
| [neon-tts-plugin-mozilla_remote](https://github.com/NeonGeckoCom/neon-tts-plugin-mozilla_remote)  | no      | API (self hosted) |
| [neon-tts-plugin-tacotron2](https://github.com/NeonGeckoCom/neon-tts-plugin-tacotron2)            | yes     | FOSS              |
| [ovos-tts-plugin-espeakNG](https://github.com/OpenVoiceOS/ovos-tts-plugin-espeakNG)               | yes     | FOSS              |
| [ovos-tts-plugin-SAM](https://github.com/OpenVoiceOS/ovos-tts-plugin-SAM)                         | yes     | Abandonware       |

### WakeWord

| Plugin                                                                                        | Type         |
|-----------------------------------------------------------------------------------------------|--------------|
| [ovos-ww-plugin-pocketsphinx](https://github.com/OpenVoiceOS/ovos-ww-plugin-pocketsphinx)     | phonemes     |
| [ovos-ww-plugin-vosk](https://github.com/OpenVoiceOS/ovos-ww-plugin-vosk)                     | text samples |
| [ovos-ww-plugin-snowboy](https://github.com/OpenVoiceOS/ovos-ww-plugin-snowboy)               | model        |
| [ovos-ww-plugin-precise](https://github.com/OpenVoiceOS/ovos-ww-plugin-precise)               | model        |
| [ovos-ww-plugin-precise-lite](https://github.com/OpenVoiceOS/ovos-ww-plugin-precise-lite)     | model        |
| [ovos-ww-plugin-nyumaya](https://github.com/OpenVoiceOS/ovos-ww-plugin-nyumaya)               | model        |
| [ovos-ww-plugin-nyumaya-legacy](https://github.com/OpenVoiceOS/ovos-ww-plugin-nyumaya-legacy) | model        |
| [neon_ww_plugin_efficientwordnet](https://github.com/NeonGeckoCom/neon_ww_plugin_efnet)       | model        |
| [mycroft-porcupine-plugin](https://github.com/forslund/mycroft-porcupine-plugin)              | model        |
| [ovos-ww-plugin-hotkeys](https://github.com/OpenVoiceOS/ovos_ww_plugin_hotkeys)               | keyboard     |


### VAD

| Plugin                                                                                 | Type  |
|----------------------------------------------------------------------------------------|-------|
| [ovos-vad-plugin-silero](https://github.com/OpenVoiceOS/ovos-vad-plugin-silero)        | model |
| [ovos-vad-plugin-webrtcvad](https://github.com/OpenVoiceOS/ovos-vad-plugin-webrtcvad)  | model |


### PHAL


| Plugin                                                                                      | Description                       |
|---------------------------------------------------------------------------------------------|-----------------------------------|
| [ovos-PHAL-plugin-alsa](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-alsa)               | volume control                    |
| [ovos-PHAL-plugin-system](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system)           | reboot / shutdown / factory reset |
| [ovos-PHAL-plugin-mk1](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk1)                 | mycroft mark1 integration         |
| [ovos-PHAL-plugin-mk2](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk2)                 | mycroft mark2 integration         |
| [ovos-PHAL-plugin-balena-wifi](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-balena-wifi) | wifi setup (hotspot)              |
| [ovos-PHAL-plugin-dashboard](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-dashboard)     | dashboard control                 |


### Language Detection / Translation


| Plugin                                                                                                 | Detect | Tx  | Offline | Type              |
|--------------------------------------------------------------------------------------------------------|--------|-----|---------|-------------------|
| [neon-lang-plugin-cld2](https://github.com/NeonGeckoCom/neon-lang-plugin-cld2)                         | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-cld3](https://github.com/NeonGeckoCom/neon-lang-plugin-cld3)                         | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-langdetect](https://github.com/NeonGeckoCom/neon-lang-plugin-langdetect)             | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-fastlang](https://github.com/NeonGeckoCom/neon-lang-plugin-fastlang)                 | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-lingua_podre](https://github.com/NeonGeckoCom/neon-lang-plugin-lingua_podre)         | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-libretranslate](https://github.com/NeonGeckoCom/neon-lang-plugin-libretranslate)     | yes    | yes | no      | API (self hosted) |
| [neon-lang-plugin-apertium](https://github.com/NeonGeckoCom/neon-lang-plugin-apertium)                 | no     | yes | no      | API (self hosted) |
| [neon-lang-plugin-amazon_translate](https://github.com/NeonGeckoCom/neon-lang-plugin-amazon_translate) | yes    | yes | no      | API (key)         |
| [neon-lang-plugin-google_translate](https://github.com/NeonGeckoCom/neon-lang-plugin-google_translate) | yes    | yes | no      | API (key)         |


### Phonemes


| Plugin                                                                                        | Type |
|-----------------------------------------------------------------------------------------------|------|
| [neon-g2p-cmudict-plugin](https://github.com/NeonGeckoCom/g2p-cmudict-plugin)                 | ARPA |
| [neon-g2p-phoneme-guesser-plugin](https://github.com/NeonGeckoCom/g2p-phoneme-guesser-plugin) | ARPA |
| [neon-g2p-mimic-plugin](https://github.com/NeonJarbas/g2p-mimic-plugin)                       | ARPA |
| [neon-g2p-mimic2-plugin](https://github.com/NeonJarbas/g2p-mimic2-plugin)                     | ARPA |
| [neon-g2p-espeak-plugin](https://github.com/NeonJarbas/g2p-espeak-plugin)                     | IPA  |
| [neon-g2p-gruut-plugin](https://github.com/NeonGeckoCom/g2p-gruut-plugin)                     | IPA  |

### AudioService

| Plugin                                                                              | Description                     |
|-------------------------------------------------------------------------------------|---------------------------------|
| [ovos-ocp-audio-plugin](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin)       | framework + compatibility layer |
| [ovos-audio-plugin-simple](https://github.com/OpenVoiceOS/ovos-audio-plugin-simple) | sox / aplay / paplay / mpg123   |
| [ovos-vlc-plugin](https://github.com/OpenVoiceOS/ovos-vlc-plugin)                   | vlc audio backend               |

## Projects using OPM

OPM plugins are know to be compatible with the following projects (non-exhaustive list)

- [ovos-core](https://github.com/OpenVoiceOS/ovos-core)
- [ovos-local-backend](https://github.com/OpenVoiceOS/ovos-local-backend)
- [ovos-tts-server](https://github.com/OpenVoiceOS/ovos-tts-server)
- [ovos-stt-http-server](https://github.com/OpenVoiceOS/ovos-stt-http-server)
- [ovos-translate-server](https://github.com/OpenVoiceOS/ovos-translate-server)
- [neon-core](https://github.com/NeonGeckoCom/NeonCore)
- [HiveMind voice satellite](https://github.com/JarbasHiveMind/HiveMind-voice-sat)

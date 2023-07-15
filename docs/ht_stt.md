# How do I - STT
STT (Speech to Text) is what converts your voice into commands that OVOS recognizes and converts them to an intent that is used to activate skills.

There are several STT engines avaliable and OVOS uses [ovos-stt-plugin-server](https://github.com/OpenVoiceOS/ovos-stt-plugin-server) and a list of public servers hosted by OVOS community members by default.

## List of STT plugins

| Plugin                                                                                                             | Offline | Type              |
|--------------------------------------------------------------------------------------------------------------------|---------|-------------------|
| [ovos-stt-plugin-vosk](https://github.com/OpenVoiceOS/ovos-stt-plugin-vosk)                                        | yes     | FOSS              |
| [ovos-stt-plugin-chromium](https://github.com/OpenVoiceOS/ovos-stt-plugin-chromium)                                | no      | API (free)        |
| [neon-stt-plugin-google_cloud_streaming](https://github.com/NeonGeckoCom/neon-stt-plugin-google_cloud_streaming)   | no      | API (key)         |
| [neon-stt-plugin-scribosermo](https://github.com/NeonGeckoCom/neon-stt-plugin-scribosermo)                         | yes     | FOSS              |
| [neon-stt-plugin-silero](https://github.com/NeonGeckoCom/neon-stt-plugin-silero)                                   | yes     | FOSS              |
| [neon-stt-plugin-polyglot](https://github.com/NeonGeckoCom/neon-stt-plugin-polyglot)                               | yes     | FOSS              |
| [neon-stt-plugin-deepspeech_stream_local](https://github.com/NeonGeckoCom/neon-stt-plugin-deepspeech_stream_local) | yes     | FOSS              |
| [ovos-stt-plugin-selene](https://github.com/OpenVoiceOS/ovos-stt-plugin-selene)                                    | no      | API (free)        |
| [ovos-stt-plugin-http-server](https://github.com/OpenVoiceOS/ovos-stt-plugin-http-server)                          | no      | API (self hosted) |
| [ovos-stt-plugin-pocketsphinx](https://github.com/OpenVoiceOS/ovos-stt-plugin-pocketsphinx)                        | yes     | FOSS              |

[Advanced Usage](https://openvoiceos.github.io/ovos-technical-manual/stt_plugins/)

# TTS Configuration
TTS plugins are responsible for converting text into audio for playback.

[List of TTS Plugins](#List-of-TTS-plugins)

[Advanced TTS Plugin Documentation](https://openvoiceos.github.io/ovos-technical-manual/tts_plugins/)

Several TTS engines have different configuration settings for optimizing its use.  Several have different voices to use, or you can specify a TTS server to use.

We will cover basic configuration of the default TTS engine `ovos-tts-server-plugin`.

All changes will be made in the User configuration file, eg. `~/.config/mycroft/mycroft.conf`.

Open the file for editing.  `nano ~/.config/mycroft/mycroft.conf`.

If your file is empty, or does not have a `"tts"` section, you need to create it.  Add this to your config

```
{
    "tts": {
        "module": "ovos-tts-server-plugin",
        "fallback_module": "ovos-tts-plugin-piper",
        "ovos-tts-server-plugin": {
            "host": "https://pipertts.ziggyai.online",
            "voice": "alan-low"
        }
        "ovos-tts-plugin-piper": {}
    }
}
```

## Sections explained

`"module"` - This is where you specify what TTS plugin to use.
- [ovos-tts-server-plugin](https://github.com/OpenVoiceOS/ovos-tts-server-plugin) in this example.
  - This plugin, by default, uses a random selection of public TTS servers provided by the OVOS community.  With no `"host"` provided, one of those will be used.
  - You can still change your voice without changing the `"host"`.  The default voice is `"alan-low"`, or the Mycroft original voice `"Alan Pope".

  [Changing your assistant's voice](ht_change_voice.md)

`"fallback_module"`
- If by chance your first TTS engine fails, OVOS will try to use this one.  It is usually configured to use an `on device` engine so that you always have some output even if you are disconnected from the internet.

`"ovos-tts-server-plugin"`

`"ovos-tts-plugin-piper"`
- Specify specific plugin settings here.  Multiple entries are allowed.  If an empty dict is provided, `{}`, the plugin will use its default values.

Refer to the TTS github repository for specifications on each plugin

## List of TTS plugins

| Plugin                                                                                            | Offline | Type              |
|---------------------------------------------------------------------------------------------------|---------|-------------------|
| [ovos-tts-server-plugin](https://github.com/OpenVoiceOS/ovos-tts-server-plugin)                   | no      | API (self hosted) |
| [ovos-tts-plugin-piper](https://github.com/OpenVoiceOS/ovos-tts-plugin-piper)                     | yes     | API (self hosted) |
| [ovos-tts-plugin-mimic3](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic3)                   | yes     | FOSS              |
| [ovos-tts-plugin-mimic](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic)                     | yes     | FOSS              |
| [ovos-tts-plugin-mimic2](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic2)                   | no      | API (free)        |
| [ovos-tts-plugin-marytts](https://github.com/OpenVoiceOS/ovos-tts-plugin-marytts)                 | no      | API (self hosted) |
| [neon-tts-plugin-larynx_server](https://github.com/NeonGeckoCom/neon-tts-plugin-larynx_server)    | no      | API (self hosted) |
| [ovos-tts-plugin-pico](https://github.com/OpenVoiceOS/ovos-tts-plugin-pico)                       | yes     | FOSS              |
| [neon-tts-plugin-glados](https://github.com/NeonGeckoCom/neon-tts-plugin-glados)                  | yes     | FOSS              |
| [neon-tts-plugin-mozilla_local](https://github.com/NeonGeckoCom/neon-tts-plugin-mozilla_local)    | yes     | FOSS              |
| [neon-tts-plugin-polly](https://github.com/NeonGeckoCom/neon-tts-plugin-polly)                    | no      | API (key)         |
| [ovos-tts-plugin-voicerss](https://github.com/OpenVoiceOS/ovos-tts-plugin-voicerss)               | no      | API (key)         |
| [ovos-tts-plugin-google-TX](https://github.com/OpenVoiceOS/ovos-tts-plugin-google-TX)             | no      | API (free)        |
| [ovos-tts-plugin-responsivevoice](https://github.com/OpenVoiceOS/ovos-tts-plugin-responsivevoice) | no      | API (free)        |
| [neon-tts-plugin-mozilla_remote](https://github.com/NeonGeckoCom/neon-tts-plugin-mozilla_remote)  | no      | API (self hosted) |
| [neon-tts-plugin-tacotron2](https://github.com/NeonGeckoCom/neon-tts-plugin-tacotron2)            | yes     | FOSS              |
| [ovos-tts-plugin-espeakNG](https://github.com/OpenVoiceOS/ovos-tts-plugin-espeakNG)               | yes     | FOSS              |
| [ovos-tts-plugin-cotovia](https://github.com/OpenVoiceOS/ovos-tts-plugin-cotovia)                 | yes     | FOSS              |
| [ovos-tts-plugin-catotron](https://github.com/OpenVoiceOS/ovos-tts-plugin-catotron)               | no      | API (self hosted) |
| [ovos-tts-plugin-softcatala](https://github.com/OpenVoiceOS/ovos-tts-plugin-softcatala)           | no      | API (self hosted) |
| [ovos-tts-plugin-SAM](https://github.com/OpenVoiceOS/ovos-tts-plugin-SAM)                         | yes     | Abandonware       |
| [ovos-tts-plugin-beepspeak](https://github.com/OpenVoiceOS/ovos-tts-plugin-beepspeak)             | yes     | Fun               |

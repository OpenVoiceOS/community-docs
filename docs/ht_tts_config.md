# TTS Configuration
Several TTS engines have different configuration settings for optimizing its use.  Several have different voices to use, or you can specify a specific TTS server to use.

We will cover basic configuration of the default TTS engine `ovos-tts-server-plugin`

All changes will be made in the User configuration file, eg. `~/.config/mycroft/mycroft.conf`

Open the file for editing.  `nano ~/.config/mycroft/mycroft.conf`

If your file is empty, or does not have a `"tts"` section, you need to create it.  Add this to your config

```
{
    "tts": {
        "module": "ovos-tts-server-plugin",
        "fallback_module": "ovos-tts-plugin-piper",
        "ovos-tts-server-plugin": {
            "host": "https://mimic3.ziggyai.online",
            "voice": "en_US/vctk_low#s5"
        }
        "ovos-tts-plugin-piper": {}
    }
}
```

## Sections explained

`"module"` - This is where you specify what TTS module to use.

`"fallback_module"` - If by chance your first TTS engine fails, OVOS will try to use this one.  It is usually configured to use an `on device` engine so that you always have some output even if you are disconnected from the internet.

`"ovos-tts-server-plugin"`

`"ovos-tts-plugin-piper"` - Specify specific plugin settings here.  Multiple entries are allowed.  If an empty dict is provided, `{}`, the plugin will use its default values.

Refer to the TTS github repository for specifications on each plugin

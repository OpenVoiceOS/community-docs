# STT Configuration
Several STT engines have different configuration settings for optimizing its use.  Several have different voices to use, or you can specify a specific STT server to use.

We will cover basic configuration of the default STT engine `ovos-stt-plugin-server`

All changes will be made in the User configuration file, eg. `~/.config/mycroft/mycroft.conf`

Open the file for editing.  `nano ~/.config/mycroft/mycroft.conf`

If your file is empty, or does not have a `"stt"` section, you need to create it.  Add this to your config

```
{
    "stt": {
        "module": "ovos-stt-plugin-server",
        "fallback_module": "ovos-stt-plugin-vosk",
        "ovos-stt-plugin-server": {
            "url": "https://fasterwhisper.ziggyai.online/stt"
        }
        "ovos-stt-plugin-vosk": {}
    }
}
```

By default, the language that is configured with OVOS will be used, but should (WIP), detect the spoken language and convert it as necessary.

## Sections explained

`"module"` - This is where you specify what STT module to use.

`"fallback_module"` - If by chance your first STT engine fails, OVOS will try to use this one.  It is usually configured to use an `on device` engine so that you always have some output even if you are disconnected from the internet.

`"ovos-tts-server-plugin"`

`"ovos-tts-plugin-piper"` - Specify specific plugin settings here.  Multiple entries are allowed.  If an empty dict is provided, `{}`, the plugin will use its default values.

Refer to the STT plugin GitHub repository for specifications on each plugin

# OVOS Listener - WakeWords / HotWords
OVOS uses "wakewords" to activate the system.  This is what "hey Google" or "Alexa" is on proprietary devices.  By default, OVOS uses the WakeWord "hey Mycroft".

OVOS "hotwords" is the configuration section to specify what the WakeWord do.  Multiple "hotwords" can be used to do a variety of things from putting OVOS into active listening mode, a WakeWord like "hey Mycroft", to issuing a command such as "stop" or "wake up"

As with everything else, this too can be changed, and several plugins are available.  Some work better than others.

[Mike Grey](https://blog.graywind.org/) created a great [blog post](https://blog.graywind.org/posts/neon-change-wakeword/) about the WakeWords also.

## List of OVOS WakeWord Plugins
| Plugin                                 | Type     | Description                           |
|----------------------------------------|----------|----------------------------|
| [ovos-ww-plugin-precise-lite](https://github.com/OpenVoiceOS/ovos-ww-plugin-precise-lite) | Model | The most accurate plugin available as it uses [pretrained models](https://github.com/OpenVoiceOS/precise-lite-models) and [community models](https://github.com/OpenVoiceOS/ovos-ww-community-dataset) are available also |
| [ovos-ww-plugin-openWakeWord](https://github.com/OpenVoiceOS/ovos-ww-plugin-openWakeWord) | Model | Uses [openWakeWord](https://www.github.com/dscripka/openwakeword) for detection |
| [ovos-ww-plugin-vosk](https://github.com/OpenVoiceOS/ovos-ww-plugin-vosk) | Full Word | Uses full word detection from a loaded model. |
| [ovos-ww-plugin-pocketsphinx](https://github.com/OpenVoiceOS/ovos-ww-plugin-pocketsphinx) | Phonomes | Probably the least accurate, but can be used on almost any device |
| [ovos-ww-plugin-hotkeys](https://github.com/OpenVoiceOS/ovos-ww-plugin-hotkeys) | Model | Use an input from keyboard or button to emulate a wakeword being said.  Useful for privacy, but not so much for a smart speaker. |
| [ovos-ww-plugin-snowboy](https://github.com/OpenVoiceOS/ovos-ww-plugin-snowboy) | Model | Uses [snowboy wakeword engine](https://github.com/seasalt-ai/snowboy) |
| [ovos-ww-plugin-nyumaya](https://github.com/OpenVoiceOS/ovos-ww-plugin-nyumaya) | Model | WakeWord plugin using [Nyumaya](https://github.com/nyumaya) |

## Configuration
The configuration for wakewords are in the `"listener"` section of `mycroft.conf` and configuration of hotwords is in the `"hotwords"` section of the same file.

This example will use the vosk plugin and change the wake word to "hey Ziggy".

Add the following to your `~/.config/mycroft/mycroft.conf` file.
```
{
    "listener": {
        "wake_word": "hey_ziggy"
    },
    "hotwords": {
        "hey_ziggy": {
            "module": "ovos-ww-plugin-vosk",
            "sound": "snd/start_listening.wav",
            "debug": false,
            "rule": "fuzzy",
            "lang": "en",
            "samples": [
                "hey ziggy",
                "hay ziggy"
                ],
            "threshold": 0.80
        }
    }
}
```

### Sections explained
The most important section is `"wake_word": "hey_ziggy"` in the `"listener"` section.

This tells OVOS what the default wakeword should be.

In the `"hotwords"` section, `"active": true`, is only used if multiple wakewords are being used.  By default, what ever `wake_word` is set in the `listener` section is automatically set to `true`.

If you want to disable a wakeword, you can set this to `false`.

If enabling a wakeword, be sure to also set `"listen": true`.

Multiple hotwords can be configured at the same time, even the same word with different plugins.  This allows for more accurate ones to be used before the less accurate, but only if the plugin is installed.

[Advanced WakeWords/HotWords](https://openvoiceos.github.io/ovos-technical-manual/ww_plugins/)

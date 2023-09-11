# OVOS Listener - WakeWords / HotWords
OVOS uses "wakewords" to activate the system. This is what "hey Google" or "Alexa" is on proprietary devices. By default, OVOS uses the WakeWord "hey Mycroft".

OVOS "hotwords" is the configuration section in `mycroft.conf` config  to specify what the WakeWord do.  Multiple "hotwords" can be used to do a variety of things from putting OVOS into active listening mode, a WakeWord like "hey Mycroft", to issuing a command such as "stop" or "wake up"

Each hotword can do one or more of the following (with example configs):
* trigger listening, also called a wake_word (default option)
  * `“Listen” : “True”`

* play a sound (only or with other action), you can set a specific sound per hotword.
  * `"sound": "snd/start_listening.wav"`

* emit a utterance to open a skill directly (instead of listen), useful to open skills from others.
  * `“utterance” : “What’s the time”` 
  * `“listen” : “false”`
   
  This example will start the date & time skill with the given utterance and not listen for a command.

* emit a bus event directly to the messagebus, to for instance open a skill you developed yourself  (instead of listen / utterance), emit a message directly (microphone mute/unmute"
  *	`“bus_event” : “custom message that you use in your own skill”`
    
     or
   	
  *	`“bus_event” : “mycroft.mic.mute"`

* Use a hotkey; allows you to assign a keyboard shortcut (e.g., "ctrl+alt+h") for triggering the hotword manually. The ovos_ww_hotkeys module is         required forusing a hotkey.
  *	`“Hotkey”: “Control+shift+h”`

* assign a language for STT per wake word
  * `Example?`
    
* be a wakeup word (out of sleep mode); take ovos-core out of sleep mode, also called a wakeup_word or standup_word
  * Example:
```
  "listener": {
    // Default wake_word and stand_up_word will be automatically set to active
    // unless explicitly disabled under "hotwords" section with "active": false. This is usually not
       desired unless you are looking to completely disable wake word usage
    "wake_word": "hey mycroft",
    "stand_up_word": "wake up"
}
```
   See: [skill-ovos-naptime](https://github.com/OpenVoiceOS/skill-ovos-naptime)

    
* Take ovos-core out of recording mode, also called a `stop_word`
   * A stop word is used when using a record skill like
    [skill-audio-recordinge](https://github.com/NeonGeckoCom/skill-audio-recording)



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
    }
    "hotwords": {
        "hey_ziggy": {
            "module": "ovos-ww-plugin-vosk",
            "listen": true,
            "active": true,
            "sound": "snd/start_listening.wav",
            "debug": false
            "rule": "fuzzy",
            "lang": "en",
            "samples": [
                "hey ziggy",
                "hay ziggy"
                ]
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


### Example hotword config (keyboard wakeword)
In the following example an extra hotword is added, that uses the `ovos_ww_hotkeys` [wake word plugin](https://github.com/OpenVoiceOS/ovos-ww-plugin-hotkeys) to listen for keyboard press and start a skill based on an utterance (in this example to tell the time by just pressing space bar).  
Install the `ovos_ww_hotkeys` plug-in and add the following to your `~/.config/mycroft/mycroft.conf` file

```
 "hotwords": {
    "hotkey": {
        "module": "ovos_ww_hotkeys",
        "listen": false,
        "active": true,
        "hotkey": "space",
        "utterance": "what time is it?"
      }
  }
```



[Advanced WakeWords/HotWords](https://openvoiceos.github.io/ovos-technical-manual/ww_plugins/)

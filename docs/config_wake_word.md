# Wake Word Plugins

WakeWord plugins classify audio and report if a certain word or sound is present or not.

These plugins usually correspond to the name of the voice assistant, "hey mycroft", but can also be used for other purposes.

Unlike the original Mycroft assistant, OVOS supports multiple wakewords in any combination of engines.

![ww](https://github.com/secretsauceai/secret_sauce_ai/raw/main/SSAI_wakeword_scene_compressed.png?raw=true)

## List of Wake Word plugins

| Plugin                                                                                        | Type         |
| --------------------------------------------------------------------------------------------- | ------------ |
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

## Overview of Most Common Plugins

The default wake words for OVOS generally use one of two different plugins, Precise-lite (referred to here as Precise) or Vosk. Precise is typically the more accurate of the two because it is trained on recordings and uses an ML model. Vosk translates sounds to phonemes and will generally be more sensitive and prone to error.

## Vosk

The primary benefit of Vosk wakewords is that they require no training or downloaded models. You can simply configure the wakeword and it will work. The downside is that you will usually get many false wakes, especially with short and common phonemes. Something like "Hey Neon" will trigger almost every time the "ee" sound is pronounced in English, while "Hey Ziggy" is much less likely to trigger because the phonemes are less common.

Note that Vosk wakewords consume a large amount of memory. Configuring multiple Vosk wakewords on a device with limited memory, like the Mycroft Mark 2, can cause performance issues.

To create a Vosk wakeword on your OVOS device, open the user configuration (defaults to `~/.config/mycroft/mycroft.conf`) in your text editor of choice and add the following lines. This will enable wakewords for both "Hey Mycroft" and "Hey Ziggy."

```json
"hotwords": {
  "hey_neon": {
    "module": "ovos-ww-plugin-vosk",
    "active": true,
    "listen": true,
    "sound": "snd/start_listening.wav",
    "debug": false,
    "rule": "fuzzy",
    "lang": "en",
    "samples": ["hey neon"]
  },
  "hey_ziggy": {
    "module": "ovos-ww-plugin-vosk",
    "listen": true,
    "active": true,
    "sound": "snd/start_listening.wav",
    "debug": false,
    "rule": "fuzzy",
    "lang": "en",
    "samples": ["hey ziggy", "hay ziggy"]
  }
}
```

If you already have a `hotwords` section in your user configuration, the first and last lines are not necessary. Also, the most important section is `"active": true`, which tells the assistant to use the wakeword. If you want to disable a wakeword, you can set this to `false`. If enabling a wakeword, be sure to also set `"listen": true`.

Another important combination is `"debug": true`, which will print the phonemes to the logs when the wakeword is triggered. This can be useful for debugging issues. It can also tell you what combinations the speech-to-text engine is picking up when you try to activate it so you can add them to the `samples` array.

Those are two common default wakewords. You can also create a completely custom wakeword as follows:

```json
"hotwords": {
  "k9": {
    "module": "ovos-ww-plugin-vosk",
    "active": true,
    "listen": true,
    "sound": "snd/start_listening.wav",
    "debug": true,
    "rule": "fuzzy",
    "lang": "en",
    "samples": ["k9", "k 9", "kay nine", "k nine", "kay nein", "k nein"]
  }
}
```

OVOS community members have used Vosk for very creative wakewords. Please feel free to share [your custom wakewords in the OVOS Matrix chat!](https://matrix.to/#/#openvoiceos-show-and-tell:matrix.org)

## Precise-Lite (Precise)

**NOTE:** The original Precise engine is not actively maintained and is not recommended for new installations. Precise-Lite is a fork of Precise that is actively maintained. Please use that instead.

Precise-Lite wakewords require a pre-trained `.tflite` model to operate. [OVOS maintains several pre-trained models of commonly requested wakewords](https://github.com/OpenVoiceOS/precise-lite-models/tree/master/wakewords/en). To use them, try this configuration:

```json
"hotwords": {
  "computer": {
    "module": "ovos-ww-plugin-precise-lite",
    "model": "https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/computer.tflite",
    "active": true,
    "listen": true,
    "sound": "snd/start_listening.wav",
    "expected_duration": 3,
    "trigger_level": 3,
    "sensitivity": 0.5
   }
}
```

Your OVOS device will automatically download the model if it isn't already on the device.

OVOS maintains the following models:

- android: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/android.tflite
- computer: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/computer.tflite
- hey_chatterbox: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/hey_chatterbox.tflite
- hey_firefox: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/hey_firefox.tflite
- hey_k9: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/hey_k9.tflite
- hey_kit: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/hey_kit.tflite
- hey_moxie: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/hey_moxie.tflite
- hey_mycroft: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/hey_mycroft.tflite
- hey_scout: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/hey_scout.tflite
- marvin: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/marvin.tflite
- o_sauro: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/o_sauro.tflite
- sheila: https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/sheila.tflite

To use them, replace the `model` section with the link to the model you want to use. Then replace the key with the name of the model, e.g. instead of `computer` use `android` or `marvin` or whichever model you chose.

### Community Precise Wakeword Models

In addition to the Precise wakeword models that OVOS maintains, [the community has created many more models](https://github.com/OpenVoiceOS/ovos-ww-community-dataset), and additional model requests are welcome! If you have a model you would like to see created, please [open an issue](https://github.com/OpenVoiceOS/ovos-ww-community-dataset/issues) with the name of the wakeword. The OVOS team will generate some synthetic samples and add it to the list of models to be created.

These synthetic models perform fairly well out of the box, but always work better with community-contributed recordings. Please see the README on the repo above for instructions on how to contribute recordings, and consider contributing to as many as you can!

# Troubleshooting Wake Word

## Architecture
OpenVoiceOS uses a plugin (or plugins) to recognize the wake word.  In your mycroft.conf file you'll specify the plugin used and what the wakeword is.
## Troubleshooting Commands
### Gather Data

### Verify it's the Wake Word and not the microphone
To verify that it is the Wake Word and not the microphone causing the issue, we will get OVOS to ask us a question that we can respond to.  In the OVOS cli type in the utterance "set timer".  OVOS will then ask how long of a timer you would like.  Speaking now should result in your utterance being transcribed.

If your response is successfully transcribed, it is most likely the Wake Word engine causing the problem.

### Check your mycroft.conf file to see what plugin and wake word is configured.
Determine which configuration files are being loaded
```
ovos-config show --section hotwords
```
The output will show which hotword is configured for your wake word.


| Configuration keys (Configuration: Joined, Section: hotwords) | Value |
|---:|:---|
│ hey_mycroft │ |
│ module │ ovos-ww-plugin-precise-lite │
│ model │ https://github.com/OpenVoiceOS/precise-lite-models/raw/master/wakewords/en/hey_mycroft.tflite │
│ expected_duration │ 3 │
│ trigger_level │ 3 │
│ sensitivity │ 0.5 │
│ listen │ True │
│ fallback_ww │ hey_mycroft_precise │
│ hey_mycroft_precise │ │
│ module │ ovos-ww-plugin-precise │
│ version │ 0.3 │
│ model │ https://github.com/MycroftAI/precise-data/raw/models-dev/hey-mycroft.tar.gz │
│ expected_duration │ 3 │
│ trigger_level │ 3 │
│ sensitivity │ 0.5 │
│ listen │ False |
│ fallback_ww │ hey_mycroft_vosk │
│ hey_mycroft_vosk │ │
│ module │ ovos-ww-plugin-vosk │
│ samples │ ['hey mycroft', 'hey microsoft', 'hey mike roft', 'hey minecraft'] |
│ rule │ fuzzy │
│ listen │ False |
│ fallback_ww │ hey_mycroft_pocketsphinx │
│ hey_mycroft_pocketsphinx │ │
│ module │ ovos-ww-plugin-pocketsphinx │
│ phonemes │ HH EY . M AY K R AO F T │
│ threshold │ 1e-90 │
│ lang │ en-us │
│ listen │ False │
│ wake_up │ │
│ module │ ovos-ww-plugin-pocketsphinx │
│ phonemes │ W EY K . AH P │
│ threshold │ 1e-20 │
│ lang │ en-us │
│ wakeup │ True │
│ active │ False │

Look at your mycoft.conf file and verify how your wake word is configured.   Look for the following lines (or similar):
```
 "wake_word": "hey_mycroft"  ## this will match a hotword listed later in the config
 ...
   "hotwords": {
    "hey_mycroft": {                             ## matches the wake_word
        "module": "ovos-ww-plugin-precise",      ## what plugin is used
        "version": "0.3",
        "model": "https://github.com/MycroftAI/precise-data/raw/models-dev/hey-mycroft.tar.gz",
        "phonemes": "HH EY . M AY K R AO F T",
        "threshold": 1e-90,
        "lang": "en-us",
        "listen": true,
        "sound": "snd/start_listening.wav"
    },
```
### Verify the Wake Word plugin is loading properly
`grep wake ~/.local/state/mycroft/voice.log`
Look for lines similar to:
```
voice - ovos_plugin_manager.wakewords:load_module:85 - INFO - Loading "wake_up" wake word via ovos-ww-plugin-pocketsphinx
voice - ovos_plugin_manager.wakewords:load_module:92 - INFO - Loaded the Wake Word plugin ovos-ww-plugin-pocketsphinx
voice - ovos_plugin_manager.wakewords:load_module:85 - INFO - Loading "hey_mycroft" wake word via ovos-ww-plugin-precise
voice - ovos_plugin_manager.wakewords:load_module:92 - INFO - Loaded the Wake Word plugin ovos-ww-plugin-precise
```
If you see an error about "failed to load plugin" make sure the plugin is installed.

## Problem/Fix
Here is a [great blog](https://blog.graywind.org/posts/neon-change-wakeword/) about the wakeword and changing it.

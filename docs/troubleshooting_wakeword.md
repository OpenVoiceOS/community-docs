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
grep mycroft.conf /var/log/syslog
```
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
`grep wake /var/log/syslog`
Look for lines similar to:
```
voice - ovos_plugin_manager.wakewords:load_module:85 - INFO - Loading "wake_up" wake word via ovos-ww-plugin-pocketsphinx
voice - ovos_plugin_manager.wakewords:load_module:92 - INFO - Loaded the Wake Word plugin ovos-ww-plugin-pocketsphinx
voice - ovos_plugin_manager.wakewords:load_module:85 - INFO - Loading "hey_mycroft" wake word via ovos-ww-plugin-precise
voice - ovos_plugin_manager.wakewords:load_module:92 - INFO - Loaded the Wake Word plugin ovos-ww-plugin-precise
```
If you see an error about "failed to load plugin" make sure the plugin is installed. 

Use ovos-cli-client to see if the microphone is working and the wakeword is being triggered.
`ovos-cli-client`
Look for
``` 
 05:19:54.975 - voice - mycroft.listener.service:handle_wakeword:97 - INFO - Wakeword Detected: hey_mycroft
 05:19:55.555 - voice - mycroft.listener.service:handle_record_begin:71 - INFO - Begin Recording...
 05:19:57.052 - voice - mycroft.listener.service:handle_record_end:78 - INFO - End Recording...
```
## Problem/Fix
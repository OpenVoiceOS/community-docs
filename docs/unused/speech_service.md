# Speech Client

The speech client is responsible for loading STT, VAD and Wake Word plugins

Speech is transcribed into text and forwarded to the skills service

## Hotwords

OVOS allows you to load any number of hot words in parallel and trigger different actions when they are
detected

each hotword can do one or more of the following:

- trigger listening, also called a **wake_word**
- play a sound
- emit a bus event
- take ovos-core out of sleep mode, also called a **wakeup_word** or **standup_word**
- take ovos-core out of recording mode, also called a **stop_word**

To add a new hotword add its configuration under "hotwords" section.

By default, all hotwords are disabled unless you set `"active": true`. 
Under the `"listener"` setting a main wake word and stand up word are defined, those will be automatically enabled unless you set `"active": false`. 
This is usually not desired unless you are looking to completely disabled wake word usage

```javascript
"listener": {
    // Default wake_word and stand_up_word will be automatically set to active
    // unless explicitly disabled under "hotwords" section
    "wake_word": "hey mycroft",
    "stand_up_word": "wake up"
},

"hotwords": {
    "hey mycroft": {
        "module": "ovos-ww-plugin-precise",
        "version": "0.3",
        "model": "https://github.com/MycroftAI/precise-data/raw/models-dev/hey-mycroft.tar.gz",
        "phonemes": "HH EY . M AY K R AO F T",
        "threshold": 1e-90,
        "lang": "en-us",
        "listen": true,
        "sound": "snd/start_listening.wav"
    },
    "wake up": {
        "module": "ovos-ww-plugin-pocketsphinx",
        "phonemes": "W EY K . AH P",
        "threshold": 1e-20,
        "lang": "en-us",
        "wakeup": true
    }
},
```


## STT

Two STT plugins may be loaded at once, if the primary plugin fails for some reason the second plugin will be used. 

This allows you to have a lower accuracy offline model as fallback to account for internet outages, this ensures your device never becomes fully unusable


```javascript
"stt": {
    "module": "ovos-stt-plugin-server",
    "fallback_module": "ovos-stt-plugin-vosk",
    "ovos-stt-plugin-server": {"url": "https://stt.openvoiceos.com/stt"}
},
```

## Listener

You can modify microphone settings and enable additional features under the listener section such as wake word / utterance recording / uploading

```javascript
"listener": {
    "sample_rate": 16000,

    // if enabled the noise level is saved to a ipc file, useful for
    // debuging if microphone is working but writes a lot to disk,
    // recommended that you set "ipc_path" to a tmpfs
    "mic_meter_ipc": true,

    // Set 'save_path' to configure the location of files stored if
    // 'record_wake_words' and/or 'save_utterances' are set to 'true'.
    // WARNING: Make sure that user 'mycroft' has write-access on the
    // directory!
    // "save_path": "/tmp",
    // Set 'record_wake_words' to save a copy of wake word triggers
    // as .wav files under: /'save_path'/mycroft_wake_words
    "record_wake_words": false,
    // Set 'save_utterances' to save each sentence sent to STT -- by default
    // they are only kept briefly in-memory.  This can be useful for for
    // debugging or other custom purposes.  Recordings are saved
    // under: /'save_path'/mycroft_utterances/<TIMESTAMP>.wav
    "save_utterances": false,
    "wake_word_upload": {
      "disable": false,
      "url": "https://training.mycroft.ai/precise/upload"
    },

    // Override as SYSTEM or USER to select a specific microphone input instead of
    // the PortAudio default input.
    //   "device_name": "somename",  // can be regex pattern or substring
    //       or
    //   "device_index": 12,

    // Stop listing to the microphone during playback to prevent accidental triggering
    // This is enabled by default, but instances with good microphone noise cancellation
    // can disable this to listen all the time, allowing 'barge in' functionality.
    "mute_during_output" : true,

    // How much (if at all) to 'duck' the speaker output during listening.  A
    // setting of 0.0 will not duck at all.  A 1.0 will completely mute output
    // while in a listening state.  Values in between will lower the volume
    // partially (this is optional behavior, depending on the enclosure).
    "duck_while_listening" : 0.3,

    // In milliseconds
    "phoneme_duration": 120,
    "multiplier": 1.0,
    "energy_ratio": 1.5,

    // Settings used by microphone to set recording timeout
    "recording_timeout": 10.0,
    "recording_timeout_with_silence": 3.0,

    // instant listen is an experimental setting, it removes the need for
    // the pause between "hey mycroft" and starting to speak the utterance,
    //however it might slightly downgrade STT accuracy depending on engine used
    "instant_listen": false
},
```


## VAD

Voice Activity Detection is used by the speech client to determine when a user stopped speaking, this indicates the voice command is ready to be executed. 
Several VAD strategies are supported

```javascript
"listener": {

    // Voice Activity Detection is used to determine when speech ended
    "VAD": {
        // silence method defined the main vad strategy
        // valid values:
        //   VAD_ONLY - Only use vad
        //   RATIO_ONLY - Only use max/current energy ratio threshold
        //   CURRENT_ONLY - Only use current energy threshold
        //   VAD_AND_RATIO - Use vad and max/current energy ratio threshold
        //   VAD_AND_CURRENT - Use vad and current energy threshold
        //   ALL - Use vad, max/current energy ratio, and current energy threshold
        // NOTE: if a vad plugin is not available method will fallback to RATIO_ONLY
        "silence_method": "vad_and_ratio",
        // Seconds of speech before voice command has begun
        "speech_seconds": 0.1,
        // Seconds of silence before a voice command has finished
        "silence_seconds": 0.5,
        // Seconds of audio to keep before voice command has begun
        "before_seconds": 0.5,
        // Minimum length of voice command (seconds)
        // NOTE: max_seconds uses recording_timeout listener setting
        "min_seconds": 1,
        // Ratio of max/current energy below which audio is considered speech
        "max_current_ratio_threshold": 2,
        // Energy threshold above which audio is considered speech
        // NOTE: this is dynamic, only defining start value
        "initial_energy_threshold": 1000.0,
        // vad module can be any plugin, by default it is not used
        // recommended plugin: "ovos-vad-plugin-silero"
        "module": "",
        "ovos-vad-plugin-silero": {"threshold": 0.2},
        "ovos-vad-plugin-webrtcvad": {"vad_mode": 3}
    }
},
```


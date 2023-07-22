# Audio Service

The audio service is responsible for loading TTS and Audio plugins

All audio playback is handled by this service


## Native playback

Usually playback is triggered by some originating bus message, eg `"recognizer_loop:utterance"`, this message contains metadata that is used to determine if playback should happen.

`message.context` may contain a source and destination, playback is only triggered if a message destination is a native_source or if missing (considered a broadcast). 

This separation of native sources allows remote clients such as an android app to interact with OVOS without the actual device where ovos-core is running repeating all TTS and music playback out loud

You can learn more about message targeting [here](https://jarbashivemind.github.io/HiveMind-community-docs/mycroft/)

By default, only utterances originating from the speech client and ovos cli are considered native

for legacy reasons the names for ovos cli and speech client are `"debug_cli"` and `"audio"` respectively


## TTS

Two TTS plugins may be loaded at once, if the primary plugin fails for some reason the second plugin will be used. 

This allows you to have a lower quality offline voice as fallback to account for internet outages, this ensures your device can always give you feedback

```javascript
"tts": {
    "pulse_duck": false,
    "module": "ovos-tts-plugin-mimic2",
    "fallback_module": "ovos-tts-plugin-mimic"
},
```


## Audio

You can enable additional Audio plugins and define the native sources described above under the `"Audio"` section of `mycroft.conf`

ovos-core uses OCP natively for media playback, you can learn more about OCP [here](https://openvoiceos.github.io/community-docs/OCP)

OCP will decide when to call the Audio service and what plugin to use, the main use case is for headless setups without a GUI

NOTE: mycroft-core has a `"default-backend"` config option, in ovos-core this option has been deprecated and is always OCP.

```javascript
"Audio": {
    "native_sources": ["debug_cli", "audio"],

    "backends": {
      "OCP": {
        "type": "ovos_common_play",
        "active": true
      },
      "simple": {
        "type": "ovos_audio_simple",
        "active": true
      },
      "vlc": {
        "type": "ovos_vlc",
        "active": true
      }
    }
},
```


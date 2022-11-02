# Audio Service

The audio service is responsible for loading TTS and Audio plugins

All audio playback is handled by this service


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

You can enable additional Audio plugins, you can also define native sources

`message.context` may contain a source and destination, playback is only triggered if a message destination is a native_source or if missing (considered a broadcast). You can learn more about message targeting [here](https://jarbashivemind.github.io/HiveMind-community-docs/mycroft/)

By default only utterances originating from the speech client and ovos cli are considered native

for legacy reasons the names for ovos cli and speech client are `"debug_cli"` and `"audio"` respectively

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

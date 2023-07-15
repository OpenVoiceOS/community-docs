# OVOS Listener - Microphone
OVOS uses microphone plugins to support different setups and devices.

**NOTE** only [ovos-dinkum-listener](https://github.com/OpenVoiceOS/ovos-dinkum-listener) has this support.

The default plugin that OVOS uses is [ovos-microphone-plugin-alsa](https://github.com/OpenVoiceOS/ovos-microphone-plugin-alsa) and for most cases should work fine.

If you are running OVOS on a Mac, you need a different plugin to access the audio.  [ovos-microphone-plugin-sounddevice](https://github.com/OpenVoiceOS/ovos-microphone-plugin-sounddevice)

OVOS microphone plugins are avaliable on [PyPi](https://pypi.org/search/?q=ovos+microphone)

`pip install ovos-microphone-plugin-sounddevice`

or

`pip install --pre ovos-microphone-plugin-sounddevice`

for the latest `alpha` versions.

**NOTE** The `alpha` versions may be needed until the release of `ovos-core 0.1.0`

## List of ovos microphone plugins

| Plugin                               | Usage                        |
|--------------------------------------|------------------------------|
| [ovos-microphone-plugin-alsa](https://github.com/OpenVoiceOS/ovos-microphone-plugin-alsa) | Default plugin - should work in most cases |
| [ovos-microphone-plugin-sounddevice](https://github.com/OpenVoiceOS/ovos-microphone-plugin-sounddevice) | This plugin is needed when running OVOS on a Mac |
| [ovos-microphone-plugin-socket](https://github.com/OpenVoiceOS/ovos-microphone-plugin-socket) | Used to connect a websocket microphone for remote usage |
| [ovos-microphone-plugin-files](https://github.com/OpenVoiceOS/ovos-microphone-plugin-files) | Will use a file as the voice input instead of a microphone |
| [ovos-microphone-plugin-pyaudio](https://github.com/OpenVoiceOS/ovos-microphone-plugin-pyaudio) | Uses PyAudio for audio processing |
| [ovos-microphone-plugin-arecord](https://github.com/OpenVoiceOS/ovos-microphone-plugin-arecord) | Uses `arecord` to get input from the microphone.  In some cases this may be faster than the default `alsa` |

## Configuration
Microphone plugin configuration is located under the top level `listener` value.

```
{
    "listener": {
        "microphone": {
            "module": "ovos-microphone-plugin-alsa",
            "ovos-microphone-plugin-alsa": {
                "device": "default"
            }
        }
    }
}
```
The only required section is `"module"`.  The plugin will then use the default values.

The `"device"` section is used if you have several microphones attached, this can be used to specify which one to use.

Specific plugins may have other values that can be set.  Check the github repo of each plugin for more details.

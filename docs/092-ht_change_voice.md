# How To Change Your Assistant's Voice

## Using TTS server plugin

TTS server plugin is using services hosted by OVOS community:
https://openvoiceos.github.io/community-docs/325-members/#members-hosting-services

That reduces local resource consumption. Its recommended to use TTS server plugin for resource constraint hardware (eg. RPi 3)

Open the file for editing.  `nano ~/.config/mycroft/mycroft.conf`.

If your file is empty, or does not have a `"tts"` section, you need to create it.  Add this to your config

```json
{
    "tts": {
        "ovos-tts-plugin-server": {
            "voice": "amy-low"
        }
    }
}
```

Execute `systemctl --user restart ovos` to reload configuration.

For avaliable voices please refer to [piper-voices section](#voices-avaliable-for-piper-plugin-)

## Using local piper plugin

Local piper plugin does all Text-To-Speech translation on your local device.

Open the file for editing.  `nano ~/.config/mycroft/mycroft.conf`.

If your file is empty, or does not have a `"tts"` section, you need to create it.  Add this to your config

```json
{
    "tts": {
        "module": "ovos-tts-plugin-piper",
        "ovos-tts-plugin-piper": {
            "voice": "alba-medium"
        }
    }
}
```

Execute `systemctl --user restart ovos` to reload configuration.

For avaliable voices please refer to [piper-voices section](#voices-avaliable-for-piper-plugin-)

# Voices avaliable for [piper-plugin](https://github.com/OpenVoiceOS/ovos-tts-plugin-piper/) <a id="Voices"></a>
List of avaliable voices can be found [here](https://github.com/OpenVoiceOS/ovos-tts-plugin-piper/blob/dev/ovos_tts_plugin_piper/__init__.py#L155C8-L242C109).

You can listen for voice samples on the official piper site - https://rhasspy.github.io/piper-samples/

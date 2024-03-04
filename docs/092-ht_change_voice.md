# How To Change Your Assistant's Voice

## Using local piper plugin

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

List of avaliable voices can be found [here](https://github.com/OpenVoiceOS/ovos-tts-plugin-piper/blob/dev/ovos_tts_plugin_piper/__init__.py#L155C8-L242C109).

You can listen for voice samples on the official piper site - https://rhasspy.github.io/piper-samples/

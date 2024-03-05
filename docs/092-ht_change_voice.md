# How To Change Your Assistant's Voice

## Using TTS server plugin

### General
TTS server plugin is using services hosted by OVOS community:
https://openvoiceos.github.io/community-docs/325-members/#members-hosting-services

That reduces local resource consumption. Its recommended to use TTS server plugin for resource constraint hardware (eg. RPi 3)

> [!NOTE]
> You can host TTS server by yourself - check this [blog post for details](https://blog.graywind.org/posts/piper-tts-server-script/)  
> The post is specifically for running Piper TTS, but could also be adapted to run [other TTS plugins](https://github.com/orgs/OpenVoiceOS/repositories?language=&q=tts-plugin&sort=&type=all).

### Changes 
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

For available voices please refer to [piper-voices section](#voices-available-for-piper-plugin)

## Using local piper plugin

### General
Local piper plugin does all Text-To-Speech translation on your local device.

### Changes
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

For available voices please refer to [piper-voices section](#voices-available-for-piper-plugin)

> [!WARNING]  
> After a configuration change it's important to reload the audio service.
> (an example used with systemd services `systemctl --user restart ovos`)
>
> If your system is not using systemd - please refer to [relevant documentation](051-starting_modules.md)

# Voices available for [piper-plugin](https://github.com/OpenVoiceOS/ovos-tts-plugin-piper/)
List of available voices can be found [here](https://github.com/OpenVoiceOS/ovos-tts-plugin-piper/blob/dev/ovos_tts_plugin_piper/__init__.py#L155C8-L242C109).

You can listen to voice samples on the official piper site - https://rhasspy.github.io/piper-samples/

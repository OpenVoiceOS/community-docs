# STT Plugins

STT plugins are responsible for converting spoken audio into text

## List of STT plugins

| Plugin                                                                                                             | Offline | Type              | 
|--------------------------------------------------------------------------------------------------------------------|---------|-------------------|
| [ovos-stt-plugin-vosk](https://github.com/OpenVoiceOS/ovos-stt-plugin-vosk)                                        | yes     | FOSS              |
| [ovos-stt-plugin-chromium](https://github.com/OpenVoiceOS/ovos-stt-plugin-chromium)                                | no      | API (free)        |
| [neon-stt-plugin-google_cloud_streaming](https://github.com/NeonGeckoCom/neon-stt-plugin-google_cloud_streaming)   | no      | API (key)         |
| [neon-stt-plugin-scribosermo](https://github.com/NeonGeckoCom/neon-stt-plugin-scribosermo)                         | yes     | FOSS              |  
| [neon-stt-plugin-silero](https://github.com/NeonGeckoCom/neon-stt-plugin-silero)                                   | yes     | FOSS              | 
| [neon-stt-plugin-polyglot](https://github.com/NeonGeckoCom/neon-stt-plugin-polyglot)                               | yes     | FOSS              | 
| [neon-stt-plugin-deepspeech_stream_local](https://github.com/NeonGeckoCom/neon-stt-plugin-deepspeech_stream_local) | yes     | FOSS              | 
| [ovos-stt-plugin-selene](https://github.com/OpenVoiceOS/ovos-stt-plugin-selene)                                    | no      | API (free)        |
| [ovos-stt-plugin-http-server](https://github.com/OpenVoiceOS/ovos-stt-plugin-http-server)                          | no      | API (self hosted) |
| [ovos-stt-plugin-pocketsphinx](https://github.com/OpenVoiceOS/ovos-stt-plugin-pocketsphinx)                        | yes     | FOSS              |


## Standalone Usage

STT plugins can be used in your owm projects as follows

```python
from speech_recognition import Recognizer, AudioFile

plug = STTPlug()

# verify lang is supported
lang = "en-us"
assert lang in plug.available_languages

# read file
with AudioFile("test.wav") as source:
    audio = Recognizer().record(source)

# transcribe AudioData object
transcript = plug.execute(audio, lang)
```


## Plugin Template

```python
from ovos_plugin_manager.templates.stt import STT


# base plugin class
class MySTTPlugin(STT):
    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        # read config settings for your plugin
        lm = self.config.get("language-model")
        hmm = self.config.get("acoustic-model")

    def execute(self, audio, language=None):
        # TODO - convert audio into text and return string
        transcript = "You said this"
        return transcript
    
    @property
    def available_languages(self):
        """Return languages supported by this STT implementation in this state
        This property should be overridden by the derived class to advertise
        what languages that engine supports.
        Returns:
            set: supported languages
        """
        # TODO - what langs can this STT handle?
        return {"en-us", "es-es"}


# sample valid configurations per language
# "display_name" and "offline" provide metadata for UI
# "priority" is used to calculate position in selection dropdown 
#       0 - top, 100-bottom
# all other keys represent an example valid config for the plugin 
MySTTConfig = {
    lang: [{"lang": lang,
            "display_name": f"MySTT ({lang}",
            "priority": 70,
            "offline": True}]
    for lang in ["en-us", "es-es"]
}
```

# OPM

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/72edbcca11ac25b09d164afb42bf04cee23b801d/Logo/Raw/opm-logo.svg)

OPM is the [OVOS Plugin Manager](https://github.com/OpenVoiceOS/OVOS-plugin-manager), this base package provides
arbitrary plugins to the ovos ecosystem

OPM plugins import their base classes from OPM making them portable and independent from core, plugins can be used in
your standalone projects

By using OPM you can ensure a standard interface to plugins and easily make them configurable in your project, plugin
code and example configurations are mapped to a string via python entrypoints in setup.py

## Plugins

### STT

STT plugins are responsible for converting spoken audio into text

#### List of STT plugins

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


#### Template

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


# sample valid configurations per language
# "display_name" and "offline" provide metadata for UI
# all other keys represent an example valid config for the plugin 
MySTTConfig = {
    lang: [{"lang": lang,
            "display_name": f"MySTT ({lang}",
            "offline": True}]
    for lang in ["en-us", "es-es"]
}
```

### TTS

TTS plugins are responsible for converting text into audio for playback

#### List of TTS plugins

| Plugin                                                                                            | Offline | Type              |
|---------------------------------------------------------------------------------------------------|---------|-------------------|
| [ovos-tts-plugin-mimic](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic)                     | yes     | FOSS              |
| [ovos-tts-plugin-mimic2](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic2)                   | no      | API (free)        |
| [ovos-tts-plugin-mimic3](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic3)                   | yes     | FOSS              |
| [ovos-tts-plugin-marytts](https://github.com/OpenVoiceOS/ovos-tts-plugin-marytts)                 | no      | API (self hosted) |
| [neon-tts-plugin-larynx_server](https://github.com/NeonGeckoCom/neon-tts-plugin-larynx_server)    | no      | API (self hosted) |
| [ovos-tts-server-plugin](https://github.com/OpenVoiceOS/ovos-tts-server-plugin)                   | no      | API (self hosted) |
| [ovos-tts-plugin-pico](https://github.com/OpenVoiceOS/ovos-tts-plugin-pico)                       | yes     | FOSS              |
| [neon-tts-plugin-glados](https://github.com/NeonGeckoCom/neon-tts-plugin-glados)                  | yes     | FOSS              |
| [neon-tts-plugin-mozilla_local](https://github.com/NeonGeckoCom/neon-tts-plugin-mozilla_local)    | yes     | FOSS              |
| [neon-tts-plugin-polly](https://github.com/NeonGeckoCom/neon-tts-plugin-polly)                    | no      | API (key)         |
| [ovos-tts-plugin-voicerss](https://github.com/OpenVoiceOS/ovos-tts-plugin-voicerss)               | no      | API (key)         |
| [ovos-tts-plugin-google-TX](https://github.com/OpenVoiceOS/ovos-tts-plugin-google-TX)             | no      | API (free)        |
| [ovos-tts-plugin-responsivevoice](https://github.com/OpenVoiceOS/ovos-tts-plugin-responsivevoice) | no      | API (free)        |
| [neon-tts-plugin-mozilla_remote](https://github.com/NeonGeckoCom/neon-tts-plugin-mozilla_remote)  | no      | API (self hosted) |
| [neon-tts-plugin-tacotron2](https://github.com/NeonGeckoCom/neon-tts-plugin-tacotron2)            | yes     | FOSS              |
| [ovos-tts-plugin-espeakNG](https://github.com/OpenVoiceOS/ovos-tts-plugin-espeakNG)               | yes     | FOSS              |
| [ovos-tts-plugin-cotovia](https://github.com/OpenVoiceOS/ovos-tts-plugin-cotovia)                 | yes     | FOSS              |
| [ovos-tts-plugin-catotron](https://github.com/OpenVoiceOS/ovos-tts-plugin-catotron)               | no      | API (self hosted) |
| [ovos-tts-plugin-softcatala](https://github.com/OpenVoiceOS/ovos-tts-plugin-softcatala)           | no      | API (self hosted) |
| [ovos-tts-plugin-SAM](https://github.com/OpenVoiceOS/ovos-tts-plugin-SAM)                         | yes     | Abandonware       |
| [ovos-tts-plugin-beepspeak](https://github.com/OpenVoiceOS/ovos-tts-plugin-beepspeak)             | yes     | Fun               |

### WakeWord

WakeWord plugins classify audio and report if a certain word or sound is present or not

These plugins usually correspond to the name of the voice assistant, "hey mycroft", but can also be used for other purposes

#### List of Wake Word plugins

| Plugin                                                                                        | Type         |
|-----------------------------------------------------------------------------------------------|--------------|
| [ovos-ww-plugin-pocketsphinx](https://github.com/OpenVoiceOS/ovos-ww-plugin-pocketsphinx)     | phonemes     |
| [ovos-ww-plugin-vosk](https://github.com/OpenVoiceOS/ovos-ww-plugin-vosk)                     | text samples |
| [ovos-ww-plugin-snowboy](https://github.com/OpenVoiceOS/ovos-ww-plugin-snowboy)               | model        |
| [ovos-ww-plugin-precise](https://github.com/OpenVoiceOS/ovos-ww-plugin-precise)               | model        |
| [ovos-ww-plugin-precise-lite](https://github.com/OpenVoiceOS/ovos-ww-plugin-precise-lite)     | model        |
| [ovos-ww-plugin-nyumaya](https://github.com/OpenVoiceOS/ovos-ww-plugin-nyumaya)               | model        |
| [ovos-ww-plugin-nyumaya-legacy](https://github.com/OpenVoiceOS/ovos-ww-plugin-nyumaya-legacy) | model        |
| [neon_ww_plugin_efficientwordnet](https://github.com/NeonGeckoCom/neon_ww_plugin_efnet)       | model        |
| [mycroft-porcupine-plugin](https://github.com/forslund/mycroft-porcupine-plugin)              | model        |
| [ovos-ww-plugin-hotkeys](https://github.com/OpenVoiceOS/ovos_ww_plugin_hotkeys)               | keyboard     |

### VAD

Voice Activity Detection is the process of determining when speech starts and ends in a piece of audio

VAD plugins classify audio and report if it contains speech or not

#### List of VAD plugins

| Plugin                                                                                 | Type  |
|----------------------------------------------------------------------------------------|-------|
| [ovos-vad-plugin-silero](https://github.com/OpenVoiceOS/ovos-vad-plugin-silero)        | model |
| [ovos-vad-plugin-webrtcvad](https://github.com/OpenVoiceOS/ovos-vad-plugin-webrtcvad)  | model |

### PHAL

Platform/Hardware specific integrations are loaded by PHAL, these plugins can handle all sorts of system activities

#### List of PHAL plugins

| Plugin                                                                                                            | Description                          |
|-------------------------------------------------------------------------------------------------------------------|--------------------------------------|
| [ovos-PHAL-plugin-alsa](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-alsa)                                     | volume control                       |
| [ovos-PHAL-plugin-system](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system)                                 | reboot / shutdown / factory reset    |
| [ovos-PHAL-plugin-mk1](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk1)                                       | mycroft mark1 integration            |
| [ovos-PHAL-plugin-mk2](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk2)                                       | mycroft mark2 integration            |
| [ovos-PHAL-plugin-respeaker-2mic](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-respeaker-2mic)                 | respeaker 2mic hat integration       |
| [ovos-PHAL-plugin-respeaker-4mic](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-respeaker-4mic)                 | respeaker 4mic hat integration       |
| [ovos-PHAL-plugin-wifi-setup](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-wifi-setup)                         | wifi setup (central plugin)          |
| [ovos-PHAL-plugin-gui-network-client](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-gui-network-client)         | wifi setup (GUI interface)           |
| [ovos-PHAL-plugin-balena-wifi](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-balena-wifi)                       | wifi setup (hotspot)                 |
| [ovos-PHAL-plugin-network-manager](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-network-manager)               | wifi setup (network manager)         |
| [ovos-PHAL-plugin-brightness-control-rpi](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-brightness-control-rpi) | brightness control                   |
| [ovos-PHAL-plugin-ipgeo](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-ipgeo)                                   | automatic geolocation  (IP address)  |
| [ovos-PHAL-plugin-gpsd](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-gpsd)                                     | automatic geolocation  (GPS)         |
| [ovos-PHAL-plugin-dashboard](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-dashboard)                           | dashboard control (ovos-shell)       |
| [ovos-PHAL-plugin-notification-widgets](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-notification-widgets)     | system notifications (ovos-shell)    |
| [ovos-PHAL-plugin-color-scheme-manager](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-color-scheme-manager)     | GUI color schemes (ovos-shell)       |
| [ovos-PHAL-plugin-configuration-provider](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-configuration-provider) | UI to edit mycroft.conf (ovos-shell) |
| [ovos-PHAL-plugin-analog-media-devices](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-analog-media-devices)     | video/audio capture devices (OCP)    |


### Language Detection / Translation

These plugins can be used to detect the language of text and to translate it

They are not used internally by ovos-core but are integrated with external tools

neon-core also makes heavy use of OPM language plugins

#### List of Language plugins

| Plugin                                                                                                 | Detect | Tx  | Offline | Type              |
|--------------------------------------------------------------------------------------------------------|--------|-----|---------|-------------------|
| [neon-lang-plugin-cld2](https://github.com/NeonGeckoCom/neon-lang-plugin-cld2)                         | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-cld3](https://github.com/NeonGeckoCom/neon-lang-plugin-cld3)                         | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-langdetect](https://github.com/NeonGeckoCom/neon-lang-plugin-langdetect)             | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-fastlang](https://github.com/NeonGeckoCom/neon-lang-plugin-fastlang)                 | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-lingua_podre](https://github.com/NeonGeckoCom/neon-lang-plugin-lingua_podre)         | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-libretranslate](https://github.com/NeonGeckoCom/neon-lang-plugin-libretranslate)     | yes    | yes | no      | API (self hosted) |
| [neon-lang-plugin-apertium](https://github.com/NeonGeckoCom/neon-lang-plugin-apertium)                 | no     | yes | no      | API (self hosted) |
| [neon-lang-plugin-amazon_translate](https://github.com/NeonGeckoCom/neon-lang-plugin-amazon_translate) | yes    | yes | no      | API (key)         |
| [neon-lang-plugin-google_translate](https://github.com/NeonGeckoCom/neon-lang-plugin-google_translate) | yes    | yes | no      | API (key)         |

### Phonemes

Grapheme to Phoneme is the process of converting text into a set of "sound units" called phonemes

These plugins are used to auto generate mouth movements / visemes in the TTS stage, they can also be used to help
configuring wake words or to facilitate training of TTS systems

These plugins can provide phonemes either in ARPA or IPA alphabets, an automatic conversion will happen behind the scenes when needed

Mouth movements are generated via a mapping of ARPA to VISEMES, 

Visemes are predefined mouth positions, timing per phonemes will default to 0.4 seconds if the plugin does not report a duration

![visemes](http://www.web3.lu/wp-content/uploads/2014/09/visemes.jpg)

Mapping based on [Jeffers phoneme to viseme map, seen in table 1](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.221.6377&rep=rep1&type=pdf), partially based on the "12 mouth shapes visuals seen [here](https://wolfpaulus.com/journal/software/lipsynchronization/)

#### Public API

All G2P plugins can be used as follows

```python

utterance = "hello world"
word = "hello"
lang="en-us"

plug = G2pPlugin()

# convert a word into a list of phonemes
phones = plug.get_ipa(word, lang)
assert phones == ['h', 'ʌ', 'l', 'oʊ']

phones = plug.get_arpa(word, lang)
assert phones == ['HH', 'AH', 'L', 'OW']

# convert a utterance into a list of phonemes
phones = plug.utterance2arpa(utterance, lang)
assert phones == ['HH', 'AH', 'L', 'OW', '.', 'W', 'ER', 'L', 'D']

phones = plug.utterance2ipa(utterance, lang)
assert phones == ['h', 'ʌ', 'l', 'oʊ', '.', 'w', 'ɝ', 'l', 'd']

# convert a utterance into a list of viseme, duration pairs
visemes = plug.utterance2visemes(utterance, lang)
assert visemes == [('0', 0.0775), ('0', 0.155), ('3', 0.2325), ('2', 0.31), ('2', 0.434), ('2', 0.558), ('3', 0.682), ('3', 0.806)]
```

#### List of G2P plugins

| Plugin                                                                                        | Type |
|-----------------------------------------------------------------------------------------------|------|
| [neon-g2p-cmudict-plugin](https://github.com/NeonGeckoCom/g2p-cmudict-plugin)                 | ARPA |
| [neon-g2p-phoneme-guesser-plugin](https://github.com/NeonGeckoCom/g2p-phoneme-guesser-plugin) | ARPA |
| [neon-g2p-mimic-plugin](https://github.com/NeonJarbas/g2p-mimic-plugin)                       | ARPA |
| [neon-g2p-mimic2-plugin](https://github.com/NeonJarbas/g2p-mimic2-plugin)                     | ARPA |
| [neon-g2p-espeak-plugin](https://github.com/NeonJarbas/g2p-espeak-plugin)                     | IPA  |
| [neon-g2p-gruut-plugin](https://github.com/NeonGeckoCom/g2p-gruut-plugin)                     | IPA  |

#### ARPA Template

```python
from ovos_plugin_manager.templates.g2p import Grapheme2PhonemePlugin
from ovos_utils.lang.visimes import VISIMES

# base plugin class
class MyARPAG2PPlugin(Grapheme2PhonemePlugin):
    def __init__(self, config=None):
        self.config = config or {}

    def get_arpa(self, word, lang, ignore_oov=False):
        phones = []  # TODO implement
        return phones
    
    def get_durations(self, utterance, lang="en", default_dur=0.4):
        words = utterance.split()
        phones = [self.get_arpa(w, lang) for w in utterance.split()]
        dur = default_dur  # TODO this is plugin specific
        return [(pho, dur) for pho in phones]
    
    def utterance2visemes(self, utterance, lang="en", default_dur=0.4):
        phonemes = self.get_durations(utterance, lang, default_dur)
        return [(VISIMES.get(pho[0].lower(), '4'), float(pho[1]))
                for pho in phonemes]

```

#### IPA Template

```python
from ovos_plugin_manager.templates.g2p import Grapheme2PhonemePlugin
from ovos_utils.lang.visimes import VISIMES

# base plugin class
class MyIPAG2PPlugin(Grapheme2PhonemePlugin):
    def __init__(self, config=None):
        self.config = config or {}

    def get_ipa(self, word, lang, ignore_oov=False):
        phones = []  # TODO implement
        return phones
    
    def get_durations(self, utterance, lang="en", default_dur=0.4):
        # auto converted to arpa if ipa is implemented
        phones = [self.get_arpa(w, lang) for w in utterance.split()]
        dur = default_dur  # TODO this is plugin specific
        return [(pho, dur) for pho in phones]
    
    def utterance2visemes(self, utterance, lang="en", default_dur=0.4):
        phonemes = self.get_durations(utterance, lang, default_dur)
        return [(VISIMES.get(pho[0].lower(), '4'), float(pho[1]))
                for pho in phonemes]

```

### AudioService

Audio plugins are responsible for handling playback of media, like music and podcasts

If mycroft-gui is available these plugins will rarely be used unless ovos is explicitly configured to do so

#### List of Audio plugins

| Plugin                                                                              | Description                     |
|-------------------------------------------------------------------------------------|---------------------------------|
| [ovos-ocp-audio-plugin](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin)       | framework + compatibility layer |
| [ovos-audio-plugin-simple](https://github.com/OpenVoiceOS/ovos-audio-plugin-simple) | sox / aplay / paplay / mpg123   |
| [ovos-vlc-plugin](https://github.com/OpenVoiceOS/ovos-vlc-plugin)                   | vlc audio backend               |
| [ovos-mplayer-plugin](https://github.com/OpenVoiceOS/ovos-mplayer-plugin)           | mplayer audio backend           |

## Packaging

To package a plugin you need a `setup.py` as follows

```python
from setuptools import setup

### replace this data with your plugin specific info
PLUGIN_TYPE = "mycroft.plugin.stt"  
PLUGIN_NAME = "ovos-stt-plugin-name"
PLUGIN_PKG = PLUGIN_NAME.replace("-", "_")
PLUGIN_CLAZZ = "MyPlugin"
PLUGIN_CONFIGS = "MyPluginConfig"
###

PLUGIN_ENTRY_POINT = f'{PLUGIN_NAME} = {PLUGIN_PKG}:{PLUGIN_CLAZZ}'
CONFIG_ENTRY_POINT = f'{PLUGIN_NAME}.config = {PLUGIN_PKG}:{PLUGIN_CONFIGS}'

# add version, author, license, description....
setup(
    name=PLUGIN_NAME,
    version='0.1.0',
    packages=[PLUGIN_PKG],
    install_requires=["speechrecognition>=3.8.1",
                      "ovos-plugin-manager>=0.0.1"],
    keywords='mycroft ovos plugin',
    entry_points={PLUGIN_TYPE: PLUGIN_ENTRY_POINT,
                  f'{PLUGIN_TYPE}.config': CONFIG_ENTRY_POINT}
)
```

## Projects using OPM

OPM plugins are know to be compatible with the following projects (non-exhaustive list)

- [ovos-core](https://github.com/OpenVoiceOS/ovos-core)
- [ovos-local-backend](https://github.com/OpenVoiceOS/ovos-local-backend)
- [ovos-tts-server](https://github.com/OpenVoiceOS/ovos-tts-server)
- [ovos-stt-http-server](https://github.com/OpenVoiceOS/ovos-stt-http-server)
- [ovos-translate-server](https://github.com/OpenVoiceOS/ovos-translate-server)
- [neon-core](https://github.com/NeonGeckoCom/NeonCore)
- [HiveMind voice satellite](https://github.com/JarbasHiveMind/HiveMind-voice-sat)

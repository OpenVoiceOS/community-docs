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

#### Standalone Usage

STT plugins can be used in your projects as follows

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

![ww](https://github.com/secretsauceai/secret_sauce_ai/raw/main/SSAI_wakeword_scene_compressed.png?raw=true)

#### Standalone Usage

first lets get some boilerplate ouf of the way for the microphone handling logic

```python
import pyaudio

# helper class
class CyclicAudioBuffer:
    def __init__(self, duration=0.98, initial_data=None,
                 sample_rate=16000, sample_width=2):
        self.size = self.duration_to_bytes(duration, sample_rate, sample_width)
        initial_data = initial_data or self.get_silence(self.size)
        # Get at most size bytes from the end of the initial data
        self._buffer = initial_data[-self.size:]

    @staticmethod
    def duration_to_bytes(duration, sample_rate=16000, sample_width=2):
        return int(duration * sample_rate) * sample_width

    @staticmethod
    def get_silence(num_bytes):
        return b'\0' * num_bytes

    def append(self, data):
        """Add new data to the buffer, and slide out data if the buffer is full
        Arguments:
            data (bytes): binary data to append to the buffer. If buffer size
                          is exceeded the oldest data will be dropped.
        """
        buff = self._buffer + data
        if len(buff) > self.size:
            buff = buff[-self.size:]
        self._buffer = buff

    def get(self):
        """Get the binary data."""
        return self._buffer

# pyaudio params
FORMAT = pyaudio.paInt16
CHANNELS = 1
RATE = 16000
CHUNK = 1024
MAX_RECORD_SECONDS = 20
SAMPLE_WIDTH = pyaudio.get_sample_size(FORMAT)
audio = pyaudio.PyAudio()

# start Recording
stream = audio.open(channels=CHANNELS, format=FORMAT,
    rate=RATE, frames_per_buffer=CHUNK, input=True)


def load_plugin():
    # Wake word initialization
    config = {"model": "path/to/hey_computer.model"}
    return MyHotWord("hey computer", config=config)


def listen_for_ww(plug):
    # TODO - see examples below
    return False

plug = load_plugin()

print(f"Waiting for wake word {MAX_RECORD_SECONDS} seconds")
found = listen_for_ww(plug)
        
if found:
    print("Found wake word!")
else:
    print("No wake word found")

# stop everything
plug.stop()
stream.stop_stream()
stream.close()
audio.terminate()
```

***new style*** plugins

New style plugins expect to receive live audio, they may keep their own cyclic buffers internally

```python

def listen_for_ww(plug):
    for i in range(0, int(RATE / CHUNK * MAX_RECORD_SECONDS)):
        data = stream.read(CHUNK)
        # feed data directly to streaming prediction engines
        plug.update(data)
        # streaming engines return result here
        found = plug.found_wake_word(data)
        if found:
            return True
```

***old style*** plugins (DEPRECATED)

Old style plugins expect to receive ~3 seconds of audio data at once

```python
def listen_for_ww(plug):
    # used for old style non-streaming wakeword (deprecated)
    audio_buffer = CyclicAudioBuffer(plug.expected_duration,
                                     sample_rate=RATE, sample_width=SAMPLE_WIDTH)
    for i in range(0, int(RATE / CHUNK * MAX_RECORD_SECONDS)):
        data = stream.read(CHUNK)
        # add data to rolling buffer, used by non-streaming engines
        audio_buffer.append(data)
        # non streaming engines check the byte_data in audio_buffer
        audio_data = audio_buffer.get()
        found = plug.found_wake_word(audio_data)
        if found:
            return True
```

***new + old style*** plugins (backwards compatibility)

if you are unsure what kind of plugin you will be using you can be compatible with both approaches like ovos-core

```python
def listen_for_ww(plug):
    # used for old style non-streaming wakeword (deprecated)
    audio_buffer = CyclicAudioBuffer(plug.expected_duration,
                                     sample_rate=RATE, sample_width=SAMPLE_WIDTH)
    for i in range(0, int(RATE / CHUNK * MAX_RECORD_SECONDS)):
        data = stream.read(CHUNK)
        # old style engines will ignore the update
        plug.update(data)
        # streaming engines will ignore the byte_data
        audio_buffer.append(data)
        audio_data = audio_buffer.get()
        found = plug.found_wake_word(audio_data)
        if found:
            return True
```

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

#### Standalone Usage

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


## Developers

### Packaging

Plugins need to define one entrypoint with their plugin type and plugin class

```python
# OPM recognized plugin types
class PluginTypes(str, Enum):
    PHAL = "ovos.plugin.phal"
    SKILL = "ovos.plugin.skill"
    VAD = "ovos.plugin.VAD"
    PHONEME = "ovos.plugin.g2p"
    AUDIO = 'mycroft.plugin.audioservice'
    STT = 'mycroft.plugin.stt'
    TTS = 'mycroft.plugin.tts'
    WAKEWORD = 'mycroft.plugin.wake_word'
    TRANSLATE = "neon.plugin.lang.translate"
    LANG_DETECT = "neon.plugin.lang.detect"
    UTTERANCE_TRANSFORMER = "neon.plugin.text"
    METADATA_TRANSFORMER = "neon.plugin.metadata"
    AUDIO_TRANSFORMER = "neon.plugin.audio"
    QUESTION_SOLVER = "neon.plugin.solver"
    COREFERENCE_SOLVER = "intentbox.coreference"
    KEYWORD_EXTRACTION = "intentbox.keywords"
    UTTERANCE_SEGMENTATION = "intentbox.segmentation"
    TOKENIZATION = "intentbox.tokenization"
    POSTAG = "intentbox.postag"
```
plugins can also optionally provide metadata about language support and sample configs via the `{plugin_type}.config` entrypoint

A typical `setup.py` for a plugin looks like this
```python
from setuptools import setup

### replace this data with your plugin specific info
PLUGIN_TYPE = "mycroft.plugin.stt"  # see Enum above
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

### STT Template

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

### TTS Template


```python
from ovos_plugin_manager.templates.tts import TTS


# base plugin class
class MyTTSPlugin(TTS):
    def __init__(self, *args, **kwargs):
        # in here you should specify if your plugin return wav or mp3 files
        # you should also specify any valid ssml tags
        ssml_tags = ["speak", "s", "w", "voice", "prosody", 
                     "say-as", "break", "sub", "phoneme"]
        super().__init__(*args, **kwargs, audio_ext="wav", ssml_tags=ssml_tags)
        # read config settings for your plugin if any
        self.pitch = self.config.get("pitch", 0.5)

    def get_tts(self, sentence, wav_file):
        # TODO - create TTS audio @ wav_file (path)
        return wav_file, None

    @property
    def available_languages(self):
        """Return languages supported by this TTS implementation in this state
        This property should be overridden by the derived class to advertise
        what languages that engine supports.
        Returns:
            set: supported languages
        """
        # TODO - what langs can this TTS handle?
        return {"en-us", "es-es"}



# sample valid configurations per language
# "display_name" and "offline" provide metadata for UI
# "priority" is used to calculate position in selection dropdown 
#       0 - top, 100-bottom
# all other keys represent an example valid config for the plugin 
MyTTSConfig = {
    lang: [{"lang": lang,
            "display_name": f"MyTTS ({lang}",
            "priority": 70,
            "offline": True}]
    for lang in ["en-us", "es-es"]
}
```

### WakeWord Template

```python
from ovos_plugin_manager.templates.hotwords import HotWordEngine
from threading import Event


class MyWWPlugin(HotWordEngine):
    def __init__(self, key_phrase="hey mycroft", config=None, lang="en-us"):
        super().__init__(key_phrase, config, lang)
        self.detection = Event()
        # read config settings for your plugin
        self.sensitivity = self.config.get("sensitivity", 0.5)
        # TODO - plugin stuff
        # how does your plugin work? phonemes? text? models?
        self.engine = MyWW(key_phrase) 

    def found_wake_word(self, frame_data):
        """Check if wake word has been found.

        Checks if the wake word has been found. Should reset any internal
        tracking of the wake word state.

        Arguments:
            frame_data (binary data): Deprecated. Audio data for large chunk
                                      of audio to be processed. This should not
                                      be used to detect audio data instead
                                      use update() to incrementally update audio
        Returns:
            bool: True if a wake word was detected, else False
        """
        detected = self.detection.is_set()
        if detected:
            self.detection.clear()
        return detected

    def update(self, chunk):
        """Updates the hotword engine with new audio data.

        The engine should process the data and update internal trigger state.

        Arguments:
            chunk (bytes): Chunk of audio data to process
        """
        if self.engine.found_it(chunk): # TODO - check for wake word
            self.detection.set()

    def stop(self):
        """Perform any actions needed to shut down the wake word engine.

        This may include things such as unloading data or shutdown
        external processess.
        """
        self.engine.bye()  # TODO - plugin specific shutdown
```


### G2P Template

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

If your plugin uses IPA instead of ARPA simply replace `get_arpa` with `get_ipa`

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



## Projects using OPM

OPM plugins are know to be natively supported by the following projects (non-exhaustive list)

- [ovos-core](https://github.com/OpenVoiceOS/ovos-core)
- [ovos-local-backend](https://github.com/OpenVoiceOS/ovos-local-backend)
- [ovos-tts-server](https://github.com/OpenVoiceOS/ovos-tts-server)
- [ovos-stt-http-server](https://github.com/OpenVoiceOS/ovos-stt-http-server)
- [ovos-translate-server](https://github.com/OpenVoiceOS/ovos-translate-server)
- [neon-core](https://github.com/NeonGeckoCom/NeonCore)
- [HiveMind voice satellite](https://github.com/JarbasHiveMind/HiveMind-voice-sat)

Additionally, some plugins (AudioService, WakeWord, TTS and STT) are also backwards compatible with mycroft-core
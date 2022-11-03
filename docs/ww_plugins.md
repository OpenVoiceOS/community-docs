# Wake Word Plugins

WakeWord plugins classify audio and report if a certain word or sound is present or not

These plugins usually correspond to the name of the voice assistant, "hey mycroft", but can also be used for other purposes

![ww](https://github.com/secretsauceai/secret_sauce_ai/raw/main/SSAI_wakeword_scene_compressed.png?raw=true)

## List of Wake Word plugins

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


## Standalone Usage

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


## Plugin Template

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

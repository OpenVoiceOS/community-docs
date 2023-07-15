# OpenVoiceOS Architecture
**This section can be a bit technical, but is included for refrence**

OVOS is a collection of modular services that work together to provide a seamless, private, open source voice assistant.  Every OVOS service runs as an indivudually and interacts with one another.

The suggested way to start OVOS is with systemd service files.  Most of the supported images run these services as a normal `user` instead of system wide.  If you get and error when using the system files, try using it as a system service.

- user service
  - `systemctl --user status ovos.service`
- system service
  - `systemctl status ovos.service`

## ovos-core
https://github.com/OpenVoiceOS/ovos-core

This service provides the main instance for OVOS and handles all of the skill loading, and intent processing.

All user queries are handled by the skills service, you can think of it as OVOS's brain

typical systemd command

`systemctl --user status ovos-skills`

[Technical Docs on Skills](https://openvoiceos.github.io/ovos-technical-manual/skills_service/)

## Messagebus
https://github.com/OpenVoiceOS/ovos-messagebus

C++ version

**NOTE** This is an `alpha` version and mostly `Proof of Concept`.  It has been known to crash often

https://github.com/OpenVoiceOS/ovos-bus_service

The bus service provides a websocket where all internal events travel

You can think of the bus service as OVOS's nervous system

The mycroft-bus is considered an internal and private websocket, **external clients should not connect directly to it.**

[Technical docs for messagebus](https://openvoiceos.github.io/ovos-technical-manual/bus_service/)

typical systemd command

`systemctl --user start ovos-messagebus`

## Listener
https://github.com/OpenVoiceOS/ovos-dinkum-listener

The listener service is used to detect your voice.  It controlls the WakeWord, STT (Speech To Text), and VAD Plugins.  You can modify microphone settings and enable additional features under the listener section such as wake word / utterance recording / uploading

The [ovos-dinkum-listener](https://github.com/OpenVoiceOS/ovos-dinkum-listener) is the new OVOS listener that replaced the origional [ovos-listener](https://github.com/OpenVoiceOS/ovos-listener) and has many more options.  Others still work, but are not recommended.

[Technical Listener Docs](https://openvoiceos.github.io/ovos-technical-manual/speech_service/)

typical systemd command

`systemctl --user start ovos-dinkum-listener`

### STT Plugins

This is where speech is transcribed into text and forwarded to the skills service.

Two STT plugins may be loaded at once, if the primary plugin fails for some reason the second plugin will be used.

This allows you to have a lower accuracy offline model as fallback to account for internet outages, this ensures your device never becomes fully unusable.

Several different STT (Speech To Text) Plugins are avaliable for use.  OVOS provides a number of public servers using the [ovos-stt-plugin-server](https://github.com/OpenVoiceOS/ovos-stt-plugin-server) plugin and are hosted by OVOS contributors.  No additional configuration is required.

[OVOS Supported STT Plugins](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-stt-plugin&type=all&language=&sort=)

**TODO** Fix link to how to change stt

[Changing STT Plugin](stt-plugins.md)

### WakeWord Plugins

A WakeWord is what OVOS uses to activate the device.  By default `Hey Mycroft` is used by OVOS.  Like other things in the OVOS ecosystem, this is configurable.

[OVOS Supported WakeWord Plugins](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-ww-plugin&type=all&language=&sort=)

**TODO** Fix link to change ww

[Changing the WakeWord](change-ww.md)

#### HotWords

OVOS allows you to load any number of hot words in parallel and trigger different actions when they are detected

each hotword can do one or more of the following:

  - trigger listening, also called a **wake_word**
  - play a sound
  - emit a bus event
  - take ovos-core out of sleep mode, also called a **wakeup_word** or **standup_word**
  - take ovos-core out of recording mode, also called a **stop_word**

**TODO** fix link to adding HotWords

[Setting and adding HotWords](setting-HotWords.md)

### VAD Plugins

VAD Plugins serve to detect when you are actually speaking to the device, and when you quit talking.

[OVOS Supported VAD Plugins](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-vad-plugin&type=all&language=&sort=)

**TODO** fix link to vad stuff

[Changing VAD Plugin](Change_VAD_Plugin.md)

## Audio

https://github.com/OpenVoiceOS/ovos-audio

The audio service handles the output of of all audio. It is how you hear the voice responses, music, or any other noise from your OVOS device.

[Configuring Audio](audio_conf.md)

### TTS Plugins

TTS (Text To Speech) is the verbal response from OVOS.  There are several plugins avaliable that support different engines.  Multiple languages and voices are avaliable to use

OVOS provides a set of public TTS servers hosted by community members.  It uses the [ovos-tts-server-plugin](https://github.com/OpenVoiceOS/ovos-tts-server-plugin), and no additional configuration is needed.

[Supported TTS Plugins](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-tts-plugin&type=all&language=&sort=)

**TODO** Fix link to how to change tts

[Changing TTS Plugin](change-tts.md)

## PHAL

https://github.com/OpenVoiceOS/ovos-PHAL

PHAL stands for Plugin based Hardware Abstraction Layer and is used to allow access of different hardware devices to use the OVOS software stack.  It completely replaces the
concept of hardcoded "enclosure" from mycroft-core.

Any number of plugins providing functionality can be loaded and validated at runtime, plugins can
be [system integrations](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system) to handle things like reboot and
shutdown, or hardware drivers such as [mycroft mark1 plugin](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk1)

[Supported PHAL Plugins](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-phal-plugin&type=all&language=&sort=)

**TODO** link to phal plugin details

[PHAL Plugins](phal-plugins.md)

### Admin PHAL

Similar to regular PHAL, but is used when `sudo` or `privlidged user` is needed

[Admin PHAL](admin-phal.md)

## GUI
OVOS uses the standard mycroft-gui framework, you can find the official documentation [here](https://mycroft-ai.gitbook.io/docs/skill-development/displaying-information/mycroft-gui)

The GUI service provides a websocket for gui clients to connect to, it is responsible for implementing the gui protocol under ovos-core.

You can find indepth documentation [here](https://openvoiceos.github.io/ovos-technical-manual/gui_service/)

## Other OVOS services

OVOS provides a number of helper scripts to allow the user to control the device at the command line.

- `ovos-say-to`  This provides a way to communicate an intent to ovos.
- `ovos-say-to "what time is it"`
- `ovos-listen`  This opens the microphone for listening, just like if you would have said the WakeWord.  It is expecting a verbal command.
  - Continue by speaking to your device `"what time is it"`
- `ovos-speak`  This takes your command and runs it through the TTS (Text To Speech) engine and speaks what was provided.
- `ovos-speak "hello world"` will output `"hello world"` in the configured TTS voice
- `ovos-config` is a command line interface that allows you to view and set configuration values.

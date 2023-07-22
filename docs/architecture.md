# OpenVoiceOS Architecture
**This section can be a bit technical, but is included for reference.** It is not necessary to read this section for day-to-day usage of OVOS.

OVOS is a collection of modular services that work together to provide a seamless, private, open source voice assistant.

The suggested way to start OVOS is with systemd service files.  Most of the images run these services as a normal `user` instead of system wide.  If you get an error when using the system files, try using it as a system service.

**NOTE** The `ovos.service` is just a wrapper to control the other OVOS services.  It is used here as an example showing `--user` vs `system`.

- user service
  - `systemctl --user status ovos.service`
- system service
  - `systemctl status ovos.service`

## ovos-core
[ovos-core](https://github.com/OpenVoiceOS/ovos-core)

This service provides the main instance for OVOS and handles all of the skill loading, and intent processing.

All user queries are handled by the skills service.  You can think of it as OVOS's brain

typical systemd command

`systemctl --user status ovos-skills`

`systemctl --user restart ovos-skills`

[Technical Docs on Skills](https://openvoiceos.github.io/ovos-technical-manual/skills_service/)

## Messagebus
[ovos-messagebus](https://github.com/OpenVoiceOS/ovos-messagebus)

C++ version

**NOTE** This is an `alpha` version and mostly `Proof of Concept`.  It has been known to crash often.

[ovos-bus-service](https://github.com/OpenVoiceOS/ovos-bus_service)

You can think of the bus service as OVOS's nervous system.

The `ovos-bus` is considered an internal and private websocket, **external clients should not connect directly to it.  Please do not expose the messagebus to the outside world!**

[Technical docs for messagebus](https://openvoiceos.github.io/ovos-technical-manual/bus_service/)

typical systemd command

`systemctl --user start ovos-messagebus`

## Listener
[ovos-dinkum-listener](https://github.com/OpenVoiceOS/ovos-dinkum-listener)

The listener service is used to detect your voice.  It controls the WakeWord, STT (Speech To Text), and VAD (Voice Activity Detection) Plugins.  You can modify microphone settings and enable additional features under the listener section of your `mycroft.conf` file, such as wake word / utterance recording / uploading.

The [ovos-dinkum-listener](https://github.com/OpenVoiceOS/ovos-dinkum-listener) is the new OVOS listener that replaced the original [ovos-listener](https://github.com/OpenVoiceOS/ovos-listener) and has many more options.  Others still work, but are not recommended.

[Technical Listener Docs](https://openvoiceos.github.io/ovos-technical-manual/speech_service/)

typical systemd command

`systemctl --user start ovos-dinkum-listener`

### STT Plugins

This is where speech is transcribed into text and forwarded to the skills service.

Two STT plugins may be loaded at once.  If the primary plugin fails, the second will be used.

Having a lower accuracy offline model as fallback will account for internet outages, which ensures your device never becomes fully unusable.

Several different STT (Speech To Text) plugins are available for use.  OVOS provides a number of public services using the [ovos-stt-plugin-server](https://github.com/OpenVoiceOS/ovos-stt-plugin-server) plugin which are hosted by OVOS trusted members [(Members hosting services)](members.md#Members-hosting-services).  No additional configuration is required.

[OVOS Supported STT Plugins](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-stt-plugin&type=all&language=&sort=)

[Changing STT Plugin](ht_stt.md)

### Hotwords

OVOS uses "Hotwords" to trigger any number of actions.  You can load any number of hotwords in parallel and trigger different actions when they are detected.  Each Hotword can do one or more of the following:

  - trigger listening, also called a [Wake word](#WakeWord-plugins)
  - play a sound
  - emit a bus event
  - take ovos-core out of sleep mode, also called a **wakeup_word** or **standup_word**
  - take ovos-core out of recording mode, also called a **stop_word**

  [Setting and adding Hotwords](ht_ww.md)

#### WakeWord Plugins

A Wake word is what OVOS uses to activate the device.  By default `Hey Mycroft` is used by OVOS.  Like other things in the OVOS ecosystem, this is configurable.

[Wake word plugins](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-ww-plugin&type=all&language=&sort=)

[Changing the Wake word](ht-ww.md)


### VAD Plugins
VAD Plugins detect when you are actually speaking to the device, and when you quit talking.

Most of the time, this will not need changed.  If you are having trouble with your microphone hearing you, or stopping listening when you are done talking, you might change this and see if it helps your issue.

[Supported VAD Plugins](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-vad-plugin&type=all&language=&sort=)

[Changing VAD Plugin](ht_vad.md)

## Audio
[ovos-audio](https://github.com/OpenVoiceOS/ovos-audio)

The audio service handles the output of all audio. It is how you hear the voice responses, music, or any other sound from your OVOS device.

[Configuring Audio](audio_conf.md)

### TTS Plugins

TTS (Text To Speech) is the verbal response from OVOS.  There are several plugins available that support different engines.  Multiple languages and voices are available to use.

OVOS provides a set of public TTS servers hosted by OVOS trusted members [(Members hosting services)](members.md#Members-hosting-services).  It uses the [ovos-tts-server-plugin](https://github.com/OpenVoiceOS/ovos-tts-server-plugin), and no additional configuration is needed.

[Supported TTS Plugins](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-tts-plugin&type=all&language=&sort=)

[Changing TTS Plugin](ht_tts.md)

## PHAL
[ovos-PHAL](https://github.com/OpenVoiceOS/ovos-PHAL)

PHAL stands for **Plugin-based Hardware Abstraction Layer.**  It is used to allow access of different hardware devices access to use the OVOS software stack.  It completely replaces the concept of hardcoded "enclosure" from `mycroft-core`.

Any number of plugins providing functionality can be loaded and validated at runtime, plugins can be [system integrations](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system) to handle things like reboot and shutdown, or hardware drivers such as [mycroft mark 1 plugin](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk1)

[Supported PHAL Plugins](https://github.com/orgs/OpenVoiceOS/repositories?q=ovos-phal-plugin&type=all&language=&sort=)

[PHAL Plugins](ht_phal.md)

### Admin PHAL
Similar to regular PHAL, but is used when `sudo` or `privlidged user` is needed
**Be extremely careful when adding `admin-phal plugins`.  They give OVOS administrative privileges, or root privileges to your operating system**
[Admin PHAL](ht_phal.md#adimn-phal)

## GUI
OVOS uses the standard mycroft-gui framework, you can find the official documentation [here](https://mycroft-ai.gitbook.io/docs/skill-development/displaying-information/mycroft-gui)

The GUI service provides a websocket for GUI clients to connect to, it is responsible for implementing the GUI protocol under `ovos-core`.

You can find in depth documentation [here](https://openvoiceos.github.io/ovos-technical-manual/gui_service/)

## Other OVOS services

OVOS provides a number of helper scripts to allow the user to control the device at the command line.

- `ovos-say-to`  This provides a way to communicate an intent to ovos.
- `ovos-say-to "what time is it"`
- `ovos-listen`  This opens the microphone for listening, just like if you would have said the WakeWord.  It is expecting a verbal command.
  - Continue by speaking to your device `"what time is it"`
- `ovos-speak`  This takes your command and runs it through the TTS (Text To Speech) engine and speaks what was provided.
- `ovos-speak "hello world"` will output `"hello world"` in the configured TTS voice
- `ovos-config` is a command line interface that allows you to view and set configuration values.

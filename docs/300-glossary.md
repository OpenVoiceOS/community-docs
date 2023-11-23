# Glossary

**Editor's Note**
Some of the more detailed definitions will be moved to other pages, it's just here to keep track of the information for now.

## The Project
### The OpenVoiceOS Project (OVOS)
All the repositories under [OpenVoiceOS organization](https://github.com/OpenVoiceOS)
### The OpenVoiceOS Team
[The team](https://github.com/orgs/OpenVoiceOS/people) behind OVOS

## Terms
### Confirmations
Confirmation approaches can also be defined by Statements or Prompts , but when we talk about them in the context of confirmations we call them Implicit and Explicit.

#### Implicit Confirmation

This type of confirmation is also a statement. The idea is to parrot the information back to the user to confirm that it
was correct, but not require additional input from the user. The implicit confirmation can be used in a majority of
situations.
#### Explicit Confirmation

This type of confirmation requires an input from the user to verify everything is correct.
### Conversations

Any time the user needs to input a lot of information or the user needs to sort through a variety of options a conversation will be needed.
Users may be used to systems that require them to separate input into different chunks.

### Context
Allows for natural conversation by having skills set a "context" that can be used by subsequent handlers.  Context could be anything from person to location.  Context can also create "bubbles" of available intent handlers, to make sure certain **Intents** can't be triggered unless some previous stage in a conversation has occurred.

You can find an example [Tea Skill using conversational context on Github](https://github.com/krisgesling/tea-skill).

As you can see, Conversational Context lends itself well to implementing a [dialog tree or conversation tree](https://en.wikipedia.org/wiki/Dialog_tree).

### Grapheme
All of the letters and letter combinations that represent a phoneme.

### Home Screen
The OpenVoiceOS home screen is the central place for all your tasks. It is the first thing you will see after completing the onboarding process. It supports a variety of pre-defined widgets which provide you with a quick overview of information you need to know like the current date, time and weather. The home screen contains various features and integrations which you can learn more about in the following sections.

### Intent
When an utterance is classified for its action and entities (e.g. 'turn on the kitchen lights' -> skill: home assistant, action: turn on/off, entity: kitchen lights)

### MPRIS
 (Media Player Remote Interfacing Specification) is a standard D-Bus interface which aims to provide a common programmatic API for controlling media players.
[More Inforamtion](https://wiki.archlinux.org/title/MPRIS)

### mycroft.conf
Primary configuration file for the voice assistant. Possible locations:
- /home/ovos/.local/lib/python3.9/site-packages/mycroft/configuration/mycroft.conf
- /etc/mycroft/mycroft.conf
- /home/ovos/.config/mycroft/mycroft.conf
- /etc/xdg/mycroft/mycroft.conf
- /home/ovos/.mycroft/mycroft.conf
[More Information](061-config_ovos_config.md)

### OCP

[OCP](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin) stands for OpenVoiceOS Common Play, it is a full fledged
media player

OCP is a [OVOSAbstractApplication](https://github.com/OpenVoiceOS/OVOS-workshop/blob/dev/ovos_workshop/app.py#L47), this
means it is a standalone but native OVOS application with full voice integration

OCP differs from mycroft-core in several aspects:

- Can run standalone, only needs a bus connection
- OCP provides its own intents as if it was a skill
- OCP provides its own GUI as if it was a skill
- mycroft-core CommonPlay skill framework is disabled when OCP loads
- OCP skills have a dedicated MycroftSkill class and decorators in ovos-workshop
- OCP skills act as media providers, they do not (usually) handle playback
- mycroft-core CommonPlay skills have an imperfect compatibility layer and are given lower priority over OCP skills
- OCP handles several kinds of playback, including video
- OCP has a sub-intent parser for matching requested media types
- AudioService becomes a subsystem for OCP
- OCP also has AudioService plugin component introducing a compatibility layer for skills using "old style audioservice
  api"
- OCP integrates with MPRIS, it can be controlled from external apps, e.g. KdeConnect in your phone
- OCP manages external MPRIS enabled players, you can voice control 3rd party apps without writing a skill for it via
  OCP
### ovos-core
The central [repository](https://github.com/OpenVoiceOS/ovos-core) where the voice assistant "brain" is developed
### OPM
OPM is the [OVOS Plugin Manager](https://github.com/OpenVoiceOS/OVOS-plugin-manager), this base package provides arbitrary plugins to the ovos ecosystem

OPM plugins import their base classes from OPM making them portable and independent from core, plugins can be used in your standalone projects

By using OPM you can ensure a standard interface to plugins and easily make them configurable in your project, plugin code and example configurations are mapped to a string via python entrypoints in setup.py

Some projects using OPM are [ovos-core](https://github.com/OpenVoiceOS/ovos-core)
, [hivemind-voice-sat](https://github.com/JarbasHiveMind/HiveMind-voice-sat)
, [ovos-personal-backend](https://github.com/OpenVoiceOS/OVOS-local-backend)
, [ovos-stt-server](https://github.com/OpenVoiceOS/ovos-stt-http-server)
and [ovos-tts-server](https://github.com/OpenVoiceOS/ovos-tts-server)
### OVOS-shell
The [gui service](https://github.com/OpenVoiceOS/ovos-core/tree/dev/mycroft/gui) in ovos-core will expose a websocket to
the GUI client following the protocol
outlined [here](https://github.com/MycroftAI/mycroft-gui/blob/master/transportProtocol.md)

The GUI library which implements the protocol lives in the [mycroft-gui](https://github.com/MycroftAI/mycroft-gui)
repository, The repository also hosts a development client for skill developers wanting to develop on the desktop.

[OVOS-shell](https://github.com/OpenVoiceOS/ovos-shell) is the OpenVoiceOS client implementation of the mycroft-gui
library used in our embedded device images, other distributions may offer alternative implementations such
as [plasma-bigscreen](http://invent.kde.org/plasma/plasma-bigscreen)*
or [mycroft mark2](https://github.com/MycroftAI/mycroft-gui-mark-2)

OVOS-shell is tightly coupled to [PHAL](#what-is-phal), the following companion plugins should be installed if you are
using ovos-shell

- [ovos-PHAL-plugin-notification-widgets](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-notification-widgets)
- [ovos-PHAL-plugin-network-manager](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-network-manager)
- [ovos-PHAL-plugin-gui-network-client](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-gui-network-client)
- [ovos-PHAL-plugin-wifi-setup](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-wifi-setup)
- [ovos-PHAL-plugin-alsa](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-alsa)
- [ovos-PHAL-plugin-system](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system)
- [ovos-PHAL-plugin-dashboard](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-dashboard)
- [ovos-PHAL-plugin-brightness-control-rpi](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-brightness-control-rpi)
- [ovos-PHAL-plugin-color-scheme-manager](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-color-scheme-manager)
- [ovos-PHAL-plugin-configuration-provider](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-configuration-provider)

### PHAL
Physical Hardware Abstraction Layer
[PHAL](https://github.com/OpenVoiceOS/ovos_PHAL) is our Platform/Hardware Abstraction Layer, it completely replaces the
concept of hardcoded "enclosure" from mycroft-core

Any number of plugins providing functionality can be loaded and validated at runtime, plugins can
be [system integrations](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system) to handle things like reboot and
shutdown, or hardware drivers such as [mycroft mark2 plugin](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk2)

PHAL plugins can perform actions such as hardware detection before loading, eg, the mark2 plugin will not load if it
does not detect the sj201 hat. This makes plugins safe to install and bundle by default in our base images
### Phoneme
The smallest phonetic unit in a language that is capable of conveying a distinction in meaning, as the m of mat and the b of bat in English.

### Service

### Snapcast
Snapcast is a multiroom client-server audio player, where all clients are time synchronized with the server to play perfectly synced audio. It's not a standalone player, but an extension that turns your existing audio player into a Sonos-like multiroom solution.
[More Information](https://github.com/badaix/snapcast)
### Prompts and Statements
You can think of **Prompts** as questions and **Statements** as providing information to the user that does not need a follow-up response.
### QML
Qt Markup Language, the language for Qt Quick UIs. [More Information](https://doc.qt.io/qt-5/qml-tutorial.html)

The [Mycroft GUI Framework](https://mycroft-ai.gitbook.io/docs/skill-development/displaying-information/mycroft-gui) uses QML.
### STT
Speech To Text
Also known as ASR, automated speech recognition, the process of converting audio into words
### TTS
Text To Speech
The process of generating the audio with the responses
### Utterance
Command, question, or query from a user (eg 'turn on the kitchen lights')
### Wake Word
A specific word or phrase trained used to activate the STT (eg 'hey mycroft')
### XDG
XDG stands for "Cross-Desktop Group", and it's a way to help with compatibility between systems. [More Information](https://www.freedesktop.org/wiki/)


# Frequently Asked Questions

+ [What is OVOS?](#what-is-ovos)
+ [How did OVOS start?](#how-did-ovos-start)
+ [Who is behind OVOS?](#who-is-behind-ovos)
+ [What is the relationship between OVOS and Mycroft?](#what-is-the-relationship-between-ovos-and-mycroft)
+ [How does OVOS make money?](#how-does-ovos-make-money)
+ [Where is your website?](#where-is-your-website)
+ [Does OVOS have any default skills?](#does-ovos-have-any-default-skills)
+ [Does OVOS work offline?](#does-ovos-work-offline)
+ [Does OVOS depend on any servers?](#does-ovos-depend-on-any-servers)
+ [How many voices does OVOS support?](#how-many-voices-does-ovos-support)
+ [Can I change the wake word?](#can-i-change-the-wake-word)
+ [Can OVOS run without a wake word?](#can-ovos-run-without-a-wake-word)
+ [What is OPM?](#what-is-opm)
+ [What is PHAL?](#what-is-phal)
+ [What is OCP?](#what-is-ocp)
+ [What is OVOS-shell?](#what-is-ovos-shell)

### What is OVOS?

OVOS aims to be a full operating system that is free and open source. The Open Voice Operating System consists of OVOS
packages (programs specifically released by the OVOS Project) as well as free software released by third parties such as
skills and plugins. OVOS makes it possible to voice enable technology without software that would trample your freedom.

Historically OVOS has been used to refer to several things, the team, the github organization and the reference
buildroot implementation

### How did OVOS start?

OVOS started as MycroftOS, you can find the original mycroft forums
thread [here](https://community.mycroft.ai/t/openvoiceos-a-bare-minimal-production-type-of-os-based-on-buildroot/4708).

Over time more mycroft community members joined the project and it was renamed to OpenVoiceOS to avoid trademark issues.

Initially OVOS was focused on bundling mycroft-core and on creating only companion software, but due to contributions
not being accepted upstream we now maintain an enhanced reference fork of mycroft-core with extra functionality, while
keeping all companion software mycroft-core (dev branch) compatible

You can think of OVOS as the unsanctioned "Mycroft Community Edition"

### Who is behind OVOS?

Everyone in the OVOS team is a long term mycroft community member and has experience working with the mycroft code base

Meet the team:

- [Peter Steenbergen](https://github.com/j1nx) - mycroft community developer since 2018, founder of MycroftOS project
- [Casimiro Ferreira](https://github.com/JarbasAl) - mycroft community developer since 2017, co-founder
  of [HelloChatterbox](https://hellochatterbox.com/)
- [Aditya Mehra](https://github.com/AIIX) - mycroft community developer since
  2016, [mycroft-gui](https://github.com/MycroftAI/mycroft-gui) lead developer
- [Daniel McKnight](https://github.com/NeonDaniel) - community developer since
  2017, [NeonGecko](https://github.com/NeonGeckoCom) lead developer
- [Parker Seaman](https://github.com/5trongthany) - mycroft enthusiast since 2018
- [Chance](https://github.com/ChanceNCounter) - mycroft community developer since 2019, ex-maintainer
  of [lingua_franca](https://github.com/MycroftAI/lingua-franca)
    - currently taking a break, he will be back!

### What is the relationship between OVOS and Mycroft?

Both projects are fully independent, initially OVOS was focused on wrapping mycroft-core with a minimal OS, but as both
projects matured, ovos-core was created to include extra functionality and make OVOS development faster and more
efficient. OVOS has been committed to keeping our components compatible with Mycroft and many of our changes are
submitted to Mycroft to include in their projects at their discretion.

### How does OVOS make money?

We don't, OVOS is a volunteer project with no source of income or business model

However we want to acknowledge [Blue Systems](https://blue-systems.com) and [NeonGeckoCom](https://neon.ai), a lot of
the work in OVOS is done on paid company time from these projects

### Where is your website?

- website - [openvoiceos.com](https://openvoiceos.com)
- chat - [matrix](https://matrix.to/#/!XFpdtmgyCoPDxOMPpH:matrix.org?via=matrix.org)
- forums - [github discussions](https://github.com/OpenVoiceOS/OpenVoiceOS/discussions)

### Does OVOS have any default skills?

We provide essential skills and those are bundled in all our reference images.

ovos-core does not manage your skills, unlike mycroft it won't install or update anything by itself. if you installed
ovos-core manually you also need to install skills manually

### Does OVOS work offline?

yes! by default ovos-core does not require internet.

That said individual skills and plugins may require internet and most of the time you will want to use those

### Does OVOS depend on any servers?

no! you can integrate ovos-core with [selene](https://github.com/MycroftAI/selene-backend)
or [personal backend](https://github.com/OpenVoiceOS/OVOS-local-backend) but that is **fully optional**

we provide some microservices for some of our skills, but you can also use your own api keys

### How many voices does OVOS support?

hundreds! nearly everything in OVOS is modular and configurable, that includes Text To Speech.

Voices depend on language and the plugins you have installed, you can find a non-exhaustive list of plugins
in [the ovos plugins awesome list](https://github.com/OpenVoiceOS/awesome-ovos-plugins#tts)

### Can I change the wake word?

yes, ovos-core supports several [wake word plugins](https://github.com/OpenVoiceOS/awesome-ovos-plugins#wakeword).

Additionally OVOS allows you to load any number of hot words in paralel and trigger different actions when they are
detected

each hotword can do one or more of the following:

- trigger listening, also called a **wake_word**
- play a sound
- emit a bus event
- take ovos-core out of sleep mode, also called a **wakeup_word** or **standup_word**
- take ovos-core out of recording mode, also called a **stop_word**

### Can OVOS run without a wake word?

mostly yes, depending on exactly what you mean by this question

OVOS can run without any wake word configured, in this case you will only be able to interact via CLI or button press,
best for privacy, not so great for a smart speaker

ovos-core also provides a couple experimental settings, if you enable continuous listening then VAD will be used to
detect speech and no wake word is needed, just speak to mycroft and it should answer! However this setting is
experimental for a reason, you may find that mycroft answers your TV or even tries to answer itself if your hardware
does not have AEC

Another experimental setting is hybrid mode, with hybrid mode you can ask follow up questions up to 45 seconds after the
last mycroft interaction, if you do not interact with mycroft it will go back to waiting for a wake word

### What is OPM?

OPM is the [OVOS Plugin Manager](https://github.com/OpenVoiceOS/OVOS-plugin-manager), this base package provides
arbitrary plugins to the ovos ecosystem

OPM plugins import their base classes from OPM making them portable and independent from core, plugins can be used in
your standalone projects

By using OPM you can ensure a standard interface to plugins and easily make them configurable in your project, plugin
code and example configurations are mapped to a string via python entrypoints in setup.py

Some projects using OPM are [ovos-core](https://github.com/OpenVoiceOS/ovos-core)
, [hivemind-voice-sat](https://github.com/JarbasHiveMind/HiveMind-voice-sat)
, [ovos-personal-backend](https://github.com/OpenVoiceOS/OVOS-local-backend)
, [ovos-stt-server](https://github.com/OpenVoiceOS/ovos-stt-http-server)
and [ovos-tts-server](https://github.com/OpenVoiceOS/ovos-tts-server)

### What is PHAL?

[PHAL](https://github.com/OpenVoiceOS/ovos_PHAL) is our Platform/Hardware Abstraction Layer, it completely replaces the
concept of hardcoded "enclosure" from mycroft-core

Any number of plugins providing functionality can be loaded and validated at runtime, plugins can
be [system integrations](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-system) to handle things like reboot and
shutdown, or hardware drivers such as [mycroft mark2 plugin](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk2)

PHAL plugins can perform actions such as hardware detection before loading, eg, the mark2 plugin will not load if it
does not detect the sj201 hat. This makes plugins safe to install and bundle by default in our base images

### What is OCP?

[OCP](https://github.com/OpenVoiceOS/ovos-ocp-audio-plugin) stands for OpenVoiceOS Common Play, it is a full fledged
media player

OCP is a [OVOSAbstractApplication](https://github.com/OpenVoiceOS/OVOS-workshop/blob/dev/ovos_workshop/app.py#L47), this
means it is a standalome but native OVOS applicatiom with full voice integration

OCP differs from mycroft-core in several aspects:

- Can run standalone, only needs a bus connection
- OCP provides it's own intents as if it was a skill
- OCP provides it's own GUI as if it was a skill
- mycroft-core CommonPlay skill framework is disabled when OCP loads
- OCP skills have a dedicated MycroftSkill class and decorators in ovos-workshop
- OCP skills act as media providers, they do not (usually) handle playback
- mycroft-core CommonPlay skills have an imperfect compatibility layer and are given lower priority over OCP skills
- OCP handles several kinds of playback, including video
- OCP has a sub-intent parser for matching requested media types
- AudioService becomes a subsystem for OCP
- OCP also has AudioService plugin component introducing a compatibility layer for skills using "old style audioservice
  api"
- OCP integrates with MPRIS, it can be controlled from external apps, eg KdeConnect in your phone
- OCP manages external MPRIS enabled players, you can voice control 3rd party apps without writing a skill for it via
  OCP

### What is OVOS-shell?

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

Further reading:

* [plasma-bigscreen GUI clients](#plasma-bigscreen-gui-clients)

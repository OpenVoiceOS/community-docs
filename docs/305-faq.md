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
+ [How fast can OVOS respond?](#how-fast-can-ovos-respond)
+ [How do I run OVOS behind a proxy?](#how-do-i-run-ovos-behind-a-proxy)

### What is OVOS?

OVOS aims to be a full operating system that is free and open source. The Open Voice Operating System consists of OVOS
packages (programs specifically released by the OVOS Project) as well as free software released by third parties such as
skills and plugins. OVOS makes it possible to voice enable technology without software that would trample your freedom.

Historically OVOS has been used to refer to several things, the team, the github organization and the reference
buildroot implementation

### How did OVOS start?

OVOS started as MycroftOS, you can find the original mycroft forums
thread [here](https://community.mycroft.ai/t/openvoiceos-a-bare-minimal-production-type-of-os-based-on-buildroot/4708).

Over time more mycroft community members joined the project, and it was renamed to OpenVoiceOS to avoid trademark issues.

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

However, we want to acknowledge [Blue Systems](https://blue-systems.com) and [NeonGeckoCom](https://neon.ai), a lot of
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

By default ovos-core does not require a backend internet server to operate. Some skills can be accessed (via command line) entirely offline. The default speech-to-text (STT) engine currently requires an internet connection, though some self-hosted, offline options are available. Individual skills and plugins may require internet, and most of the time you will want to use those.

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

Additionally, OVOS allows you to load any number of hot words in parallel and trigger different actions when they are
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
detect speech and no wake word is needed, just speak to mycroft and it should answer! However, this setting is
experimental for a reason, you may find that mycroft answers your TV or even tries to answer itself if your hardware
does not have AEC

Another experimental setting is hybrid mode, with hybrid mode you can ask follow-up questions, up to 45 seconds after the
last mycroft interaction, if you do not interact with mycroft it will go back to waiting for a wake word

### How fast can OVOS respond?

By default, to answer a request:

1. Detects the wake word 
2. Records 3 - 10 seconds of audio 
3. Transcribes the audio and returns the text transcription , either locally or remotely, depending on the speech-to-text \(STT\) engine in use 
4. Parses the text to understand the intent 
5. Sends the text to the intent handler with the highest confidence 
6. Allows the Skill to perform some action and provide the text to be spoken 
7. Synthesizes audio from the given text, either locally or remotely, depending on the text-to-speech \(TTS\) engine in use 
8. Plays the synthesized spoken audio.

Through this process there are a number of factors that can affect the perceived speed of responses:

* System resources - more processing power and memory never hurts!
* Network latency - depending on configured plugins, network latency and connection speed can play a significant role in slowing down response times.
* Streaming STT - we have been experimenting with the use of streaming services. This transcribes audio as it's received rather than waiting for the entire utterance to be finished and sending the resulting audio file to a server to be processed in its entirety. It is possible to switch to a streaming STT service. See [STT Plugins](../OPM/#list-of-stt-plugins) for a list of options available.
* Dialog structure - a long sentence will always take more time to synthesize than a short one. Skill developers can help provide quicker response times by considering the structure of their dialog and breaking that dialog up.
* TTS Caching - synthesized audio is cached meaning common recently generated phrases don't need to be generated, they can be returned immediately.


### How do I run OVOS behind a proxy?

Many schools, universities and workplaces run a `proxy` on their network. If you need to type in a username and password to access the external internet, then you are likely behind a `proxy`.

If you plan to use OVOS behind a proxy, then you will need to do an additional configuration step.

_NOTE: In order to complete this step, you will need to know the `hostname` and `port` for the proxy server. Your network administrator will be able to provide these details. Your network administrator may want information on what type of traffic OVOS will be using. We use `https` traffic on port `443`, primarily for accessing ReST-based APIs._

#### Using OVOS behind a proxy without authentication

If you are using OVOS behind a proxy without authentication, add the following environment variables, changing the `proxy_hostname.com` and `proxy_port` for the values for your network. These commands are executed from the Linux command line interface (CLI).

```bash
$ export http_proxy=http://proxy_hostname.com:proxy_port
$ export https_port=http://proxy_hostname.com:proxy_port
$ export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com,0.0.0.0,::1"
```

#### Using OVOS behind an authenticated proxy

If you are behind a proxy which requires authentication, add the following environment variables, changing the `proxy_hostname.com` and `proxy_port` for the values for your network. These commands are executed from the Linux command line interface (CLI).

```bash
$ export http_proxy=http://user:password@proxy_hostname.com:proxy_port
$ export https_port=http://user:password@proxy_hostname.com:proxy_port
$ export no_proxy="localhost,127.0.0.1,localaddress,.localdomain.com,0.0.0.0,::1"
```

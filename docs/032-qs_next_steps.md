# OpenVoiceOS Quickstart - Next Steps

## Woo Woo!! You Have A Running OVOS Device!! Now what?

Prebuilt images come with a default set of skills installed, including, but not limited to the date/time, and weather.  Give them a shot.

Speak these commands and enjoy the spoils:

`Hey Mycroft, what time is it?`

`Hey Mycroft, what is today's date?`

`Hey Mycroft, what is the weather today?`

`Hey Mycroft, will it rain today?`

While there are several default skills installed, there are many more available to be used.  The link below will show you how to find and install more skills.

[Installing Skills](080-ht_skills.md)

But wait, there's more!!

OVOS is highly configurable, and uses a file in either `JSON` or `YAML` format to provide these options.  While in most cases, OVOS should just work, sometimes you either need to, or want to change some options.

[OVOS Configuration](060-config.md)

OVOS ships with a default TTS (Text to Speech) engine which speaks in the original `Alan-Pope` voice that Mycroft used.  There are MANY more to choose from.  The following link will help you choose and configure a different voice for your assistant.

[Configuring TTS](090-ht_tts.md)

Your device does not understand your voice when you speak?  There are options for different STT (Speech To Text) engines also.  Some work better than others, but can provide less privacy.

[Changing STT](102-ht_stt.md)

Your OVOS assistant uses a "wake word" which lets it know it is time to start listening to your commands.  By default, the phrase to wake OVOS is `Hey Mycroft`.  This, like most things in OVOS, is totally configurable.  Follow the link to learn more.

[Changing the Wake Word](104-ht_ww.md)

PHAL plugins allow OVOS to interact with the underlying hardware and operating system.  Several are available, and may be installed and run together.

[Configuring PHAL](110-ht_phal.md)

OVOS ships with default services available to the public to use.  These include public TTS and STT servers, a weather API provided by [OpenMeteo](https://openmeteo.com/), access to Wolfram, and more.  Since OVOS is an open and private system, you can also change these to your own preferences.

[Install your own Services](999-not-implemented) **WIP**

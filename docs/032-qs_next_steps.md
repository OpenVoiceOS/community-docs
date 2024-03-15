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

## Interacting by command line

While OVOS is primarily a voice-driven platform, sometimes it makes sense to interact by CLI for troubleshooting, testing, or development. OVOS ships several tools with [ovos-bus-client](https://github.com/OpenVoiceOS/ovos-bus-client) in most distros.

### ovos-listen

Typing the command `ovos-listen` will make the listener service start listening for voice commands. If you haven't set up a wakeword or you're having issues with your wakeword, this can be a good way to check if the entire listener is not working.

### ovos-speak

The `ovos-speak` command will tell the assistant to speak whatever you type after it. This command can be useful for demonstrations or to play pranks on nearby family members or roommates. For example:

```bash
$ ovos-speak "Look ma, no data shared with big companies!"
```

Note the quotes - you must include the quotes, otherwise the assistant would only say "look."

### ovos-say-to

The `ovos-say-to` command will send an utterance to the assistant, to be processed normally by the assistant. It effectively skips the speech-to-text portion of the interaction. This command is useful in situations where you can't or don't want to speak to the assistant - for example, when roommates or family members are sleeping, or you're already typing to test new skill code.

Example:

```bash
$ ovos-say-to "What time is it?"
```

Again, note the quotes. Without quotes only the first word will be sent to the assistant, which will typically result in an error.


# OpenVoiceOS Architecture
**Editors Note**
Most of the text in the entire architecture section will not remain, it's my notes so I can create some architecture drawings and simplified information.

## Bus Service

The bus service provides a websocket where all internal events travel

You can think of the bus service as OVOS's nervous system

The mycroft-bus is considered an internal and private websocket, external clients should not connect directly to it.  **Please do not expose the messagebus to the outside world!**

### Message
A Message consists of a json payload, it contains a `type` , some `data` and a `context`. 

The `context` is considered to be metadata and might be changed at any time in transit, the `context` can contain anything depending on where the message came from, and often is completely empty. 

You can think of the message `context` as a sort of session data for a individual interaction, in general messages down the chain keep the `context` from the original message, most listeners (eg, skills) will only care about `type` and `data`. 

ovos-core uses the message `context` to add metadata about the messages themselves, where do they come from and what are they intended for.

#### Sources

ovos-core injects the context when it emits an utterance, this can be either typed in the `ovos-cli-client` or spoken via STT service

STT will identify itself as `audio`

ovos-cli-client will identify itself as `debug_cli`

`mycroft.conf` contains a `native_sources` section you can configure to change how the audio service processes external requests

#### Destinations

Output capable services are the cli and the TTS

The command line is a debug tool, it will ignore the `destination`

TTS checks the message context if it's the intended target for the message and will only speak in the following conditions:

- Explicitly targeted i.e. the `destination` is `"audio"`
- `destination` is set to `None`
- `destination` is missing completely

The idea is that for example when the android app is used to access OpenVoiceOS the device at home shouldn't start to speak.

TTS will be executed when `"audio"` or `"debug_cli"` are the `destination`

A missing `destination` or if the `destination` is set to `None` is interpreted as a multicast and should trigger all output capable processes (be it the audio service, a web-interface, the KDE plasmoid or maybe the android app)


# Converse

Each Skill may define a `converse()` method. This method will be called anytime the Skill has been recently active and a new utterance is processed.&#x20;

The converse method expects a single argument which is a standard Mycroft Message object. This is the same object an intent handler receives.

Converse methods must return a Boolean value. True if an utterance was handled, otherwise False.

### Active Skill List

A Skill is considered active if it has been called in the last 5 minutes.

Skills are called in order of when they were last active. For example, if a user spoke the following commands:

> Hey Mycroft, set a timer for 10 minutes
>
> Hey Mycroft, what's the weather

Then the utterance "what's the weather" would first be sent to the Timer Skill's `converse()` method, then to the intent service for normal handling where the Weather Skill would be called.

As the Weather Skill was called it has now been added to the front of the Active Skills List. Hence, the next utterance received will be directed to:

1. `WeatherSkill.converse()`
2. `TimerSkill.converse()`
3. Normal intent parsing service

### Making a Skill Active

There are occasions where a Skill has not been triggered by the User, but it should still be considered "Active".

In the case of our Ice Cream Skill - we might have a function that will execute when the customers order is ready. At this point, we also want to be responsive to the customers thanks, so we call `self.make_active()` to manually add our Skill to the front of the Active Skills List.

## GUI Protocol

T[he [gui service](https://github.com/OpenVoiceOS/ovos-core/tree/dev/mycroft/gui) in ovos-core will expose a websocket to
the GUI clients following the protocol outlined [here](https://github.com/MycroftAI/mycroft-gui/blob/master/transportProtocol.md)

The transport protocol works between gui service and the gui clients, mycroft does not directly use the protocol but instead communicates with the gui service via the standard mycroft bus]()

OVOS images are powered by [ovos-shell](https://openvoiceos.github.io/community-docs/shell/), the client side
implementation of the gui protocol

The GUI library which implements the protocol lives in the [mycroft-gui](https://github.com/MycroftAI/mycroft-gui) repository.

# GUI Service

OVOS uses the standard mycroft-gui framework, you can find the official
documentation [here](https://mycroft-ai.gitbook.io/docs/skill-development/displaying-information/mycroft-gui)

The GUI service provides a websocket for gui clients to connect to, it is responsible for implementing the gui protocol
under ovos-core.

You can find indepth documentation in the dedicated GUI section of these docs
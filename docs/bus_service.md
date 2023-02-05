# Bus Service

The bus service provides a websocket where all internal events travel

You can think of the bus service as OVOS's nervous system

The mycroft-bus is considered an internal and private websocket, external clients should not connect directly to it.

## Exposing the bus

Please do not expose the messagebus to the outside world!

Anything connected to the bus can fully control OVOS, and OVOS usually has full control over the whole system!

You can read more about the security issues over at [Nhoya/MycroftAI-RCE](https://github.com/Nhoya/MycroftAI-RCE)

If you need to connect to the bus from the outside world please check the companion project [HiveMind](https://openvoiceos.github.io/community-docs/friends/#hivemind)

Lots of guides for mycroft tell you to expose the websocket, please (re)read the info and links above, think 10 times before following steps blindly

## Message

A Message consists of a json payload, it contains a `type` , some `data` and a `context`. 

The `context` is considered to be metadata and might be changed at any time in transit, the `context` can contain anything depending on where the message came from, and often is completely empty. 

You can think of the message `context` as a sort of session data for a individual interaction, in general messages down the chain keep the `context` from the original message, most listeners (eg, skills) will only care about `type` and `data`. 

### Targeting Theory

ovos-core uses the message `context` to add metadata about the messages themselves, where do they come from and what are they intended for.

the `Message` object provides the following methods:

- `message.forward` method, keeps previous context.
	- message continues going to same `destination`
- `message.reply` method swaps `"source"` with `"destination"`
	- message goes back to `source`

The context `destination` parameter in the original message can be set to a list with any number of intended targets:

```python
bus.emit(Message('recognizer_loop:utterance', data, 
				 context={'destination': ['audio', 'kde'],
						  'source': "remote_service"))
```

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

#### Internal routing

- intent service will `.reply` to the original utterance message
- all skill/intent service messages are `.forward` (from previous intent service `.reply`)
- skills sending their own messages might not respect this **warning**
- `converse`/`get_response` support is limited, the context may be lost **warning**
- in the context of the multiple users skills might keep a shared state between clients, eg. a client may enable [parrot mode](https://github.com/JarbasSkills/skill-parrot) for everyone  **warning**
- scheduled events support is limited, the context is lost **warning**

## Configuration

The messagebus has a dedicated section in `mycroft.conf`

```javascript
"websocket": {
    "host": "0.0.0.0",
    "port": 8181,
    "route": "/core",
    "shared_connection": true
}
```

## Security

in mycroft-core all skills share a bus connection, this allows malicious skills to manipulate it and affect other skills

you can see a demonstration of this problem with [BusBrickerSkill](https://github.com/EvilJarbas/BusBrickerSkill)

`"shared_connection": false` ensures each skill gets it's own websocket connection and avoids this problem

Additionally, it is recommended you change `"host": "127.0.0.1"`, this will ensure no outside world connections are allowed


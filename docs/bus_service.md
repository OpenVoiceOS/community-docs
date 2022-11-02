# Bus Service

The bus service provides a websocket where all internal events travel

You can think of the bus service as OVOS's nervous system

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

## Exposing the bus

Please do not expose the messagebus to the outside world!

Anything connected to the bus can fully control OVOS, and OVOS usually has full control over the whole system!

You can read more about the security issues over at [Nhoya/MycroftAI-RCE](https://github.com/Nhoya/MycroftAI-RCE)

If you need to connect to the bus from the outside world please check the companion project [HiveMind](https://openvoiceos.github.io/community-docs/friends/#hivemind)

Lots of guides for mycroft tell you to expose the websocket, please (re)read the info and links above, think 10 times before following steps blindly

## Security

in mycroft-core all skills share a bus connection, this allows malicious skills to manipulate it and affect other skills

you can see a demonstration of this problem with [BusBrickerSkill](https://github.com/EvilJarbas/BusBrickerSkill)

`"shared_connection": false` ensures each skill gets it's own websocket connection and avoids this problem

Additionally, it is recommended you change `"host": "127.0.0.1"`, this will ensure no outside world connections are allowed

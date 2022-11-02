# GUI Service

OVOS uses the standard mycroft-gui framework, you can find the official
documentation [here](https://mycroft-ai.gitbook.io/docs/skill-development/displaying-information/mycroft-gui)

The GUI service provides a websocket for gui clients to connect to, it is responsible for implementing the gui protocol
under ovos-core.

## Protocol

The [gui service](https://github.com/OpenVoiceOS/ovos-core/tree/dev/mycroft/gui) in ovos-core will expose a websocket to
the GUI clients following the protocol
outlined [here](https://github.com/MycroftAI/mycroft-gui/blob/master/transportProtocol.md)

The GUI library which implements the protocol lives in the [mycroft-gui](https://github.com/MycroftAI/mycroft-gui)
repository.

OVOS images are powered by [ovos-shell](https://openvoiceos.github.io/community-docs/shell/), the client side
implementation of the gui protocol

## Configuration

The gui service has a few sections in `mycroft.conf`

```javascript
"gui": {
    "idle_display_skill": "skill-ovos-homescreen.openvoiceos",
    "extension": "generic",
    "generic": {
        "homescreen_supported": false
    }
},
  
"gui_websocket": {
    "host": "0.0.0.0",
    "base_port": 18181,
    "route": "/gui",
    "ssl": false
},
```

## GUI Extensions

OVOS Core supports a GUI Extension framework which allows the GUI service to incorporate additional behaviour for a
specific platform. GUI Extensions currently supported:

### Smartspeaker Extension:

This extension is responsible for managing the smartspeaker GUI interface behaviour, it supports homescreens and
homescreen management. Enabling the smartspeaker GUI extension:

```javascript
"gui": {
    "extension": "smartspeaker",
    "idle_display_skill": "skill-ovos-homescreen.openvoiceos"
}
```

### Bigscreen Extension:

This extension is responsible for managing the plasma bigscreen GUI interface behaviour, it supports window management
and window behaviour control on specific window managers like Kwin. Enabling the Bigscreen GUI extension:

```javascript
"gui": {
    "extension": "bigscreen"
}
```

### Mobile Extension:

This extension is responsible for managing the mobile GUI interface behaviour, it supports homescreens and additionally
adds support for global page back navigation. Enabling the Mobile GUI extension:

```javascript
"gui": {
    "extension": "smartspeaker",
    "idle_display_skill": "skill-android-homescreen.openvoiceos",
}
```

### Generic Extension:

This extension provides a generic GUI interface and does not add any additional behaviour,
it optionally supports homescreens if the platform or user manually enables it.
This extension is enabled by default when no other extension is specified.

```javascript
"gui": {
    "idle_display_skill": "skill-ovos-homescreen.openvoiceos",
    "extension": "generic",
    "generic": {
        "homescreen_supported": false
    }
}
```

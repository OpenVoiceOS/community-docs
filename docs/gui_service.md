# GUI Service

OVOS uses the standard mycroft-gui framework, you can find the official
documentation [here](https://mycroft-ai.gitbook.io/docs/skill-development/displaying-information/mycroft-gui)

The GUI service provides a websocket for gui clients to connect to, it is responsible for implementing the gui protocol
under ovos-core.

You can find indepth documentation in the dedicated GUI section of these docs

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

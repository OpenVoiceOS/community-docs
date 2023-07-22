## Protocol

The [gui service](https://github.com/OpenVoiceOS/ovos-core/tree/dev/mycroft/gui) in ovos-core will expose a websocket to
the GUI clients following the protocol outlined [here](https://github.com/MycroftAI/mycroft-gui/blob/master/transportProtocol.md)

The transport protocol works between gui service and the gui clients, mycroft does not directly use the protocol but instead communicates with the gui service via the standard mycroft bus

OVOS images are powered by [ovos-shell](https://openvoiceos.github.io/community-docs/shell/), the client side
implementation of the gui protocol

The GUI library which implements the protocol lives in the [mycroft-gui](https://github.com/MycroftAI/mycroft-gui) repository.

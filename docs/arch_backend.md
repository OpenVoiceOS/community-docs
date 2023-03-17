# OpenVoiceOS Backends

A backend is a service that provides your device with additional tools to function, these could range from managing your skill settings to configuring certain aspects of your device. The backend is optional in OVOS, especially if you're running a single device. 

A backend can provide:

- A nice web ui to configure device, this allows for you to configure once and push it to all your devices.
- Free API services for weather and wolfram alpha
- Collecting data, e.g. upload ww and utterance audio samples from all your devices

Available backends:

- Offline: no backend all configuration local
- Personal: Self hosted minimal backend
- OpenvoiceOS API Service: Not a true backend, provides a proxy for APIs for privacy
- Selene: Provided by Mycroft.ai, can be [self hosted](https://github.com/MycroftAI/selene-backend).  The official Mycroft.ai hosting will likely be going away and is deprecated.
- Neon: Coming soon

## Selecting a backend
**Editors Note** coming soon, placeholder information

You can go without a backend and go offline and use our free proxy for API services with no accounts.

Install the skill-ovos-setup to get the prompt to setup a backend.  Without this installed, you will NOT hear the prompt to pick a backend.

You can manually change mycroft.conf to enable a different backend if needed, but you will have to install setup skill and add "setup" to "ready_settings" in mycroft.conf


More Information is available in the [backend client repo](https://github.com/OpenVoiceOS/ovos-backend-client)



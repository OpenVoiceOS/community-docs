# OpenVoiceOS Backends

A backend is a service that provides your device with additional tools to function, these could range from managing your skill settings to configuring certain aspects of your device. The backend is optional and concidered to be advanced usage in OVOS.  By default, OVOS does not use a backend, and is totally unnecessasary for basic usage.  A local backend becomes usefull if you have several devices around the house and would like a central place to configure them.

A backend can provide:

- A nice web ui to configure device, this allows for you to configure once and push it to all your devices.
- Free API services for weather and wolfram alpha
- Collecting data, e.g. upload ww and utterance audio samples from all your devices

Available backends:

- Offline: no backend all configuration local. This is the DEFAULT
- Personal: [Self hosted minimal backend](https://github.com/OpenVoiceOS/ovos-personal-backend)

**TODO** fix link to personal backend

[Setting Up a Personal Backend](setup-backend.md)

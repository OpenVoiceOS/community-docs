# The OpenVoiceOS Project Documentation

![](https://github.com/OpenVoiceOS/ovos_assets/blob/master/Logo/ovos-logo-512.png?raw=true)

the OVOS project documentation is written and maintained by users just like you! 

Think of these docs both as your starting point and also forever changing and incomplete

Please [open Issues and Pull Requests](https://github.com/OpenVoiceOS/community-docs)!

## Table of Contents

* [Glossary](#glossary)
* [FAQ](#faq)
  + [What is OVOS?](#what-is-ovos-)
  + [Where is your website](#where-is-your-website)
  + [Does OVOS have any default skills?](#does-ovos-have-any-default-skills-)
  + [Does OVOS work offline?](#does-ovos-work-offline-)
  + [Does OVOS depend on any servers?](#does-ovos-depend-on-any-servers-)
  + [How many voices does OVOS support?](#how-many-voices-does-ovos-support-)


## Glossary

- The OpenVoiceOS Project - All the repositories under [OpenVoiceOS organization](https://github.com/OpenVoiceOS)
- The OpenVoiceOS Team - [The team](https://github.com/orgs/OpenVoiceOS/people) behind OVOS
- ovos-core - the central [repository](https://github.com/OpenVoiceOS/ovos-core) where the voice assistant "brain" is developed
- OVOS - all of the above!

## FAQ

### What is OVOS?

OVOS aims to be a full operating system that is free and open source. The Open Voice Operating System consists of OVOS packages (programs specifically released by the OVOS Project) as well as free software released by third parties such as skills and plugins. The development of OVOS makes it possible to voice enable technology without software that would trample your freedom.

Historically OVOS has been used to refer to several things, the team, the github organization and the reference buildroot implementation

### Where is your website

- website - [openvoiceos.com](https://openvoiceos.com)
- chat - [matrix](https://matrix.to/#/!XFpdtmgyCoPDxOMPpH:matrix.org?via=matrix.org)
- forums - [github discussions](https://github.com/OpenVoiceOS/OpenVoiceOS/discussions)

### Does OVOS have any default skills?

We provide essential skills and those are bundled in all our reference images.

ovos-core does not manage your skills, unlike mycroft it won't install or update anything by itself. if you installed ovos-core manually you also need to install skills manually

### Does OVOS work offline?

yes! by default ovos-core does not require internet.

That said individual skills and plugins may require internet and most of the time you will want to use those

### Does OVOS depend on any servers?

no! you can integrate ovos-core with [selene](https://github.com/MycroftAI/selene-backend) or [personal backend](https://github.com/OpenVoiceOS/OVOS-local-backend) but that is **fully optional**

we provide some microservices for some of our skills, but you can also use your own api keys

### How many voices does OVOS support?

hundreds! nearly everything in OVOS is modular and configurable, that includes Text To Speech.

Voices depend on language and the plugins you have installed, you can find a non-exhaustive list of plugins in [the ovos plugins awesome list](https://github.com/OpenVoiceOS/awesome-ovos-plugins#tts)


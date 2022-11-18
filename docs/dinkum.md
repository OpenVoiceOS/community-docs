# Dinkum

## What is Dinkum

Mycroft Mark2 shipped with a new version of mycroft called "dinkum", this is a total overhaul of mycroft-core and
incompatible

mycroft-core is now referred to as "Classic Core" by MycroftAI

MycroftAI now provides what they call sandbox images, to add to the confusing those only work in the mark 2 and "Classic
Core" means the mark2/latest branch of mycroft-core, this is the branch that was used in the dev kits and is also
backwards incompatible, the majority of changes in this branch were not done via PRs and had no review or community input

- mark 2 docs - https://mycroft-ai.gitbook.io/mark-ii/
- dinkum source code - https://github.com/MycroftAI/mycroft-dinkum
- sandbox images - https://mycroft-ai.gitbook.io/mark-ii/advanced/sandbox-images
- mark2/latest - https://github.com/MycroftAI/mycroft-core/tree/mark-ii/latest

## Dinkum vs ovos-core

you can find mycroft's guide to porting skills to dinkum here https://mycroft-ai.gitbook.io/mark-ii/differences-to-classic-core/porting-classic-core-skills

mark2/latest brought some changes to mycroft-core, not all of them backwards compatible and some that were contentious
within the community.

- skill states - converse method introduced skill states, this changed some core assumptions behind converse method and
  active skills, OVOS did not adopt skill states, see community discussion
  here [mycroft-core/pull/2901](https://github.com/MycroftAI/mycroft-core/pull/2901) + [mycroft-core/pull/2906](https://github.com/MycroftAI/mycroft-core/pull/2906)
- self.resource - resource file loading was overhauled, this feature has been
  improved ([ovos-core/pull/130](https://github.com/OpenVoiceOS/ovos-core/pull/130) + [ovos-core/pull/131](https://github.com/OpenVoiceOS/ovos-core/pull/131) + [ovos-core/pull/135](https://github.com/OpenVoiceOS/ovos-core/pull/135) + [ovos-core/pull/170](https://github.com/OpenVoiceOS/ovos-core/pull/170))
  and ported to OVOS and is also available in OVOSkill class ([OVOS-workshop/pull/30](https://github.com/OpenVoiceOS/OVOS-workshop/pull/30)) for usage in classic core
- audio hal - audio playback was rewritten from scratch, audio plugin support has been removed, OVOS will not adopt this new approach but keep improving the previous one
- activities - an activity is just a set of bus messages to indicate something started and ended, it is a reimplementation of an already existing feature, in ovos this is a native part of the self.add_event methods, we did not adopt the new api, a compatibility layer may be added later

dinkum contains all changes above and also brought further changes to the table

- session - in dinkum session handling is done by skills, it completely ignores the message.context mechanism and existing session_id, in ovos we believe session should come in the message and handled by the clients (eg, a chat user or a hivemind client....), in ovos we are expanding the original session concept  [ovos-core/pull/160](https://github.com/OpenVoiceOS/ovos-core/pull/160)
- hal - a dbus service specific to the mk2 has been introduced, in ovos we have a generic PHAL service and companion plugins to interface with mk2 hardware instead, this component is mark2 specific and should be ignored in the ovos ecosystem

## FAQ

### Do OVOS skills run in dinkum?

No, not even classic core skills run in dinkum. We have no plans to support this

### Do Dinkum skills run in ovos?

No, dinkum is designed in a very incompatible way, the `mycroft` module is not always mycroft-core and the `MycroftSkill` class is not always a MycroftSkill, we have no intention of transparently loading dinkum skills in ovos-core

We have a small proof of concept tool to convert a dinkum skill into a ovos/classic core compatible skill, see https://github.com/OpenVoiceOS/undinkumfier

### Does OCP work in dinkum?

No, Audio plugin support has been removed, you can run OCP standalone but will be missing the compatibility layers and can't load OCP skills anyway

It could be made to work but this is not in the roadmap, PRs will be accepted and reviewed

### Does PHAL work in dinkum?

It should! We don't explicitly target or test it with dinkum, but it is a fairly standalone component

### Does OPM work in dinkum?

STT , TTS and WW plugins should work, We don't explicitly target or test compatibility, PRs will be accepted and reviewed
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

## Changes

you can see mycroft guide to porting skills to dinkum here https://mycroft-ai.gitbook.io/mark-ii/differences-to-classic-core/porting-classic-core-skills

mark2/latest brought some changes to mycroft-core, not all of them backwards compatible and some that were contentious
within the community.

- skill states - converse method introduced skill states, this changed some core assumptions behind converse method and
  active skills, see community discussion
  here [mycroft-core/pull/2901](https://github.com/MycroftAI/mycroft-core/pull/2901) + [mycroft-core/pull/2906](https://github.com/MycroftAI/mycroft-core/pull/2906)
- self.resource - resource file loading was overhauled, this feature has been
  improved ([ovos-core/pull/130](https://github.com/OpenVoiceOS/ovos-core/pull/130) + [ovos-core/pull/131](https://github.com/OpenVoiceOS/ovos-core/pull/131) + [ovos-core/pull/135](https://github.com/OpenVoiceOS/ovos-core/pull/135) + [ovos-core/pull/170](https://github.com/OpenVoiceOS/ovos-core/pull/170))
  and ported to ovos and is also available in OVOSkill class ([OVOS-workshop/pull/30](https://github.com/OpenVoiceOS/OVOS-workshop/pull/30))
- audio hal - audio playback was rewritten from scratch, audio plugin support has been removed
- activities - an activity is just a set of bus messages to indicate something started and ended, it is a reimplementation of an already existing feature baked into self.add_event methos

dinkum contains all changes above and also brought further changes to the table

- session - in dinkum session handling is done by skills, it completely ignores the message.context mechanism and existing session_id, in ovos we believe session should come in the message and handled by the clients (eg, a chat user or a hivemind client....), in ovos we are expanding the original session concept  [ovos-core/pull/160](https://github.com/OpenVoiceOS/ovos-core/pull/160)
- hal - a dbus service specific to the mk2 has been introduced, in ovos we have a generic PHAL service and companion plugins to interface with mk2 hardware instead, this component is mark2 specific and should be ignored in the ovos ecosystem
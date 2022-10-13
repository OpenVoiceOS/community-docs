## Compatibility FAQ

+ [Do OVOS images run on the mark2?](#do-ovos-images-run-on-the-mark2)
+ [Do OVOS skills work in mycroft-core?](#do-ovos-skills-work-in-mycroft-core)
+ [Do OPM plugins work in mycroft-core?](#do-opm-plugins-work-in-mycroft-core)
+ [Does PHAL work with mycroft-core?](#does-phal-work-with-mycroft-core)
+ [Known Incompatibilities](#known-incompatibilities)

### Do OVOS images run on the mark2?

The [mark2 developer kit](https://www.instructables.com/Mycroft-Mark-II-Developer-Kit-Assembly) is one of the reference
platforms we test and develop against, the [ovos-buildroot](https://github.com/OpenVoiceOS/ovos-buildroot) images can be
used in a mark 2 device

### Do OVOS skills work in mycroft-core?

If you are a developer please subclass your skills
from [OVOSSkill](https://github.com/OpenVoiceOS/OVOS-workshop/blob/dev/ovos_workshop/skills/ovos.py) provided in
ovos-workshop package

We implement all skill development tools under the ovos-workshop library, this allows most OVOS functionality to be used
in mycroft-core without problems. This
includes [intent_layers](https://github.com/OpenVoiceOS/OVOS-workshop/blob/dev/ovos_workshop/skills/layers.py)
, [decorators](https://github.com/OpenVoiceOS/OVOS-workshop/tree/dev/ovos_workshop/decorators)
and [killable_events](https://github.com/OpenVoiceOS/skill-abort-test)

However some skills may decide to depend on features exclusive to ovos-core, or be missing bug fixes in mycroft-core,
therefore we can not ensure 100% compatibility. eg, if a skill depends on
the [converse deactivated](https://github.com/OpenVoiceOS/ovos-core/blob/V0.0.5a8/mycroft/skills/mycroft_skill/mycroft_skill.py#L613)
event it may misbehave under mycroft-core because that event is only sent in ovos-core

When we introduce new functionality in ovos-core that if used in a skill would cause incompatibilities with mycroft we
always make the methods private, as long as a skill does not access any property that starts with an underscore,
eg. `self._resources`, it should work in mycroft-core

See the table of [Known Incompatibilities](#known-incompatibilities)

### Do OPM plugins work in mycroft-core?

yes! OPM provides new kinds of plugins not supported by mycroft-core, but STT, TTS, WakeWord and AudioService plugins
will work in regular mycroft

OPM base classes may contain improvements and new features, such as better caching and automatic viseme generation in
TTS plugins, but we try very hard to ensure they remain compatible with mycroft-core dev branch

### Does PHAL work with mycroft-core?

yes! PHAL is a standalone component, it only needs to connect to the mycroft messagebus. You can connect PHAL to vanilla
mycroft-core and load any plugin.

Depending on the plugin this may make sense or not

### Known Incompatibilities

Here we present a list of know incompatibilites between ovos-core and mycroft-core

| feature                              | consequence                                | reason                                            | workarounds                                |
|--------------------------------------|--------------------------------------------|---------------------------------------------------|--------------------------------------------|
| [converse deactivated](https://github.com/OpenVoiceOS/ovos-core/blob/V0.0.5a8/mycroft/skills/mycroft_skill/mycroft_skill.py#L613) event           | skill won't know when its no longer active | mycroft-core does not emit bus event              |                                            |
| access private skill property/method | skill will not load                        | syntax error                                      | port the feature to ovos_workshop          |
| using "mycroft.gui.list.move"        | GUI may be messed up                       | mycroft-core does not implement full [GUI protocol](https://github.com/MycroftAI/mycroft-gui/blob/master/transportProtocol.md) | run ovos-gui, do not run mycroft enclosure |

# License

we have a universal donor policy, our code should be able to be used anywhere by anyone, no ifs or conditions attached.

We go to great lengths to avoid GPL code for this reason, all our code is either Apache2 or BSD licensed

Individual plugins or skills may have their own license, for example mimic3 is AGPL so we can not change the license of
our plugin.

We are committed to maintain all core components fully free, any GPL code will live in an optional plugin and be flagged
as such.

This includes avoiding LGPL code for reasons
explained [here](https://softwareengineering.stackexchange.com/questions/119436/what-does-gpl-with-classpath-exception-mean-in-practice/326325#326325)
.

### Notable licensing exceptions

The following repositories do not respect our [universal donor policy](#how-is-ovos-licensed), please ensure their
licenses are compatible before you use them

| Repository                                                                                  | License   | Reason                                                                                                     |
|---------------------------------------------------------------------------------------------|-----------|------------------------------------------------------------------------------------------------------------|
| [ovos-intent-plugin-padatious](https://github.com/OpenVoiceOS/ovos-intent-plugin-padatious) | Apache2.0 | [padatious](https://github.com/MycroftAI/padatious) license might not be valid, depends on libfann2 (LGPL) |
| [ovos-tts-plugin-mimic3](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic3)             | AGPL      | depends on mimic3 (AGPL)                                                                                   |
| [ovos-tts-plugin-SAM](https://github.com/OpenVoiceOS/ovos-tts-plugin-SAM)                   | ?         | reverse engineered abandonware                                                                             |

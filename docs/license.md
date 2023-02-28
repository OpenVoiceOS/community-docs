# License

We have a universal donor policy, our code should be able to be used anywhere by anyone, no ifs or conditions attached.

OVOS is predominately Apache2 or BSD licensed. There are only a few exceptions to this, which are all licensed under other compatible open source licenses.

Individual plugins or skills may have their own license, for example mimic3 is AGPL, so we can not change the license of our plugin.

We are committed to maintain all core components fully free, any code that we have no control over the license will live in an optional plugin and be flagged as such.

This includes avoiding LGPL code for reasons explained [here](https://softwareengineering.stackexchange.com/questions/119436/what-does-gpl-with-classpath-exception-mean-in-practice/326325#326325).

Our license policy has the following properties:

-  It gives you, the user of the software, complete and unrestrained access to the software, such that you may inspect, modify, and redistribute your changes
    - Inspection - Anyone may inspect the software for security vulnerabilities
    - Modification - Anyone may modify the software to fix issues or add features
    - Redistribution - Anyone may redistribute the software on their terms
- It is compatible with GPL licenses - Projects licensed as GPL can be distributed with OVOS
- It allows for the incorporation of GPL-incompatible free software, such as software that is CDDL licensed

The license does not restrict the software that may run on OVOS, however -- and thanks to the plugin architecture, even traditionally tightly-coupled components such as drivers can be distributed separately, so maintainers are free to choose whatever license they like for their projects.


### Notable licensing exceptions

The following repositories do not respect our universal donor policy, please ensure their licenses are compatible before you use them

| Repository                                                                                  | License   | Reason                                                                                                     |
|---------------------------------------------------------------------------------------------|-----------|------------------------------------------------------------------------------------------------------------|
| [ovos-intent-plugin-padatious](https://github.com/OpenVoiceOS/ovos-intent-plugin-padatious) | Apache2.0 | [padatious](https://github.com/MycroftAI/padatious) license might not be valid, depends on libfann2 (LGPL) |
| [ovos-tts-plugin-mimic3](https://github.com/OpenVoiceOS/ovos-tts-plugin-mimic3)             | AGPL      | depends on mimic3 (AGPL)                                                                                   |
| [ovos-tts-plugin-SAM](https://github.com/OpenVoiceOS/ovos-tts-plugin-SAM)                   | ?         | reverse engineered abandonware                                                                             |

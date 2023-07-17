# OpenVoiceOS Services
**Editors Note** Major revisions coming here, mostly placeholder information

## Skills Service

The skills service is responsible for loading skills and intent parsers

All user queries are handled by the skills service, you can think of it as OVOS's brain
[More Information](https://openvoiceos.github.io/ovos-technical-manual/skills_service/)
## Speech Service
### Speech Client

The speech client is responsible for loading STT, VAD and Wake Word plugins

Speech is transcribed into text and forwarded to the skills service

### Hotwords

OVOS allows you to load any number of hot words in parallel and trigger different actions when they are detected

each hotword can do one or more of the following:

- trigger listening, also called a **wake_word**
- play a sound
- emit a bus event
- take ovos-core out of sleep mode, also called a **wakeup_word** or **standup_word**
- take ovos-core out of recording mode, also called a **stop_word**

To add a new hotword add its configuration under "hotwords" section.

By default, all hotwords are disabled unless you set `"listen": true`. 
Under the `"listener"` setting a main wake word and stand up word are defined, those will be automatically enabled unless you set `"active": false`. 
This is usually not desired unless you are looking to completely disabled wake word usage

### STT

Two STT plugins may be loaded at once, if the primary plugin fails for some reason the second plugin will be used. 

This allows you to have a lower accuracy offline model as fallback to account for internet outages, this ensures your device never becomes fully unusable

### Listener

You can modify microphone settings and enable additional features under the listener section such as wake word / utterance recording / uploading


### VAD

Voice Activity Detection is used by the speech client to determine when a user stopped speaking, this indicates the voice command is ready to be executed. 
Several VAD strategies are supported



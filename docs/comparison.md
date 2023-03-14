# Images compared

OpenVoiceOS ready to use images come in several flavours; The buildroot version, being the minimal consumer type of
image and the Manjaro version, being the full distribution easy / easier for developing. a headless raspbian image is also maintained by the community

Some friend projects also publish images that include OpenVoiceOS in some form, those are also listed here

Mycroft images are largely unmaintained and are also listed for comparison purposes, usage is not recommended


- [Operating System](#operating-system)
      * [OpenVoiceOS](#openvoiceos)
      * [Friends](#friends)
      * [Mycroft](#mycroft)
- [Plugins](#plugins)
      * [OpenVoiceOS](#openvoiceos-1)
      * [Friends](#friends-1)
      * [Mycroft](#mycroft-1)
- [Functionality](#functionality)
      * [OpenVoiceOS](#openvoiceos-2)
      * [Friends](#friends-2)
      * [Mycroft](#mycroft-2)
- [Configuration](#configuration)
      * [OpenVoiceOS](#openvoiceos-3)
      * [Friends](#friends-3)
      * [Mycroft](#mycroft-3)
- [Hardware](#hardware)
      * [OpenVoiceOS](#openvoiceos-4)
      * [Friends](#friends-4)
      * [Mycroft](#mycroft-4)
    

## Operating System


### OpenVoiceOS

|                                                | ovos-buildroot                     | ovos-arch                 | ovos-raspbian                   |
|------------------------------------------------|------------------------------------|---------------------------|---------------------------------|
| **Operating System**                           |                                    |                           |                                 |
| Base OS                                        | buildroot                          | manjaro                   | raspbian                        |
| Last Updated - YYYY/MM/DD                      | 2023-0?-??                         | 2023-0?-??                | 2023-0?-??                      |
| **Customization**                              |                                    |                           |                                 |
| Open Build System                              | Yes                                | Yes                       | Yes<br>(pi-gen github workflow) |
| Package manager                                | N/A<br>(*No buildtools available*) | pacman                    | apt                             |
| **Software - Architecture**                    |                                    |                           |                                 |
| Core                                           | ovos-core                          | ovos-core                 | ovos-core                       |
| GUI                                            | ovos-shell                         | ovos-shell                | N/A                             |
| Launcher                                       | systemd<br>user session            | systemd<br>system session | systemd<br>user session         |
| **Updating**                                   |                                    |                           |                                 |
| Update mechanism                               | pip<br>(bash scripts)              | pip<br>(bash scripts)     | pip<br>(bash scripts)           |
| **Screen - GUI**                               |                                    |                           |                                 |
| GUI supported<br>*Show GUI if screen attached* | eglfs                              | eglfs                     | N/A                             |

### Friends

|                                                | NeonAI                    | Bigscreen                              |
|------------------------------------------------|---------------------------|----------------------------------------|
| **Operating System**                           |                           |                                        |
| Base OS                                        | debian                    | manjaro                                |
| Last Updated - YYYY/MM/DD                      | 2023-03 (regular updates) | [Rolling Release](https://github.com/manjaro-arm/bigscreen/releases)          |
| **Customization**                              |                           |                                        |
| Open Build System                              | Yes                       | [Manjaro ARM Tools](https://gitlab.manjaro.org/manjaro-arm/applications/manjaro-arm-tools)                               |
| Package manager                                | apt                       | pacman                                 |
| **Software - Architecture**                    |                           |                                        |
| Core                                           | neon-core                 | ovos-core                              |
| GUI                                            | ovos-shell                | Plasma Shell                           |
| Launcher                                       | systemd<br>system session | systemd<br>user session                |
| **Updating**                                   |                           |                                        |
| Update mechanism                               | PHAL plugin<br>(pip/git)  | package manager<br>(mycroft-bigscreen) |
| **Screen - GUI**                               |                           |                                        |
| GUI supported<br>*Show GUI if screen attached* | eglfs                     | X11/Wayland                            |

### Mycroft

|                                                | Mark 1<br>(Classic Core) | Mark 2<br>(Dinkum)                         | Picroft<br>(Classic Core) |
|------------------------------------------------|--------------------------|--------------------------------------------|---------------------------|
| **Operating System**                           |                          |                                            |                           |
| Base OS                                        | raspbian                 | Pantacor                                   | raspbian                  |
| Last Updated - YYYY/MM/DD                      | 20??-??-??               | 2023-??-??                                 | 20??-??-??                |
| **Customization**                              |                          |                                            |                           |
| Open Build System                              | github readme            | No (?)<br>*build tools are not public*     | github readme             |
| Package manager                                | apt                      | apt<br>(*limited by read-only filesystem*) | apt                       |
| **Software - Architecture**                    |                          |                                            |                           |
| Core                                           | mycroft-core             | dinkum                                     | mycroft-core              |
| GUI                                            | N/A                      | plasma-nano                                | N/A                       |
| Launcher                                       | systemd (?)              | Pantacor                                   | bash script               |
| **Updating**                                   |                          |                                            |                           |
| Update mechanism                               | package manager (?)      | OTA<br>*controlled by Mycroft*             | git pull                  |
| **Screen - GUI**                               |                          |                                            |                           |
| GUI supported<br>*Show GUI if screen attached* | N/A                      | X11                                        | N/A                       |

## Plugins

### OpenVoiceOS

|                         | ovos-buildroot                                    | ovos-arch                                         | ovos-raspbian                                     |
|-------------------------|---------------------------------------------------|---------------------------------------------------|---------------------------------------------------|
| **Default Plugins**     |                                                   |                                                   |                                                   |
| VAD                     | ovos-vad-plugin-webrtcvad                         | ovos-vad-plugin-webrtcvad                         | ovos-vad-plugin-webrtcvad                         |
| stt                     | ovos-stt-plugin-server<br>(ovos proxy)            | ovos-stt-plugin-server<br>(ovos proxy)            | ovos-stt-plugin-server<br>(ovos proxy)            |
| fallback_stt            | N/A                                               | N/A                                               | N/A                                               |
| tts                     | ovos-tts-plugin-mimic3-server<br>(public servers) | ovos-tts-plugin-mimic3-server<br>(public servers) | ovos-tts-plugin-mimic3-server<br>(public servers) |
| fallback_tts            | ovos-tts-plugin-mimic                             | ovos-tts-plugin-mimic                             | ovos-tts-plugin-mimic                             |
| **Recommended Plugins** |                                                   |                                                   |                                                   |
| STT - On device         | ovos-stt-plugin-vosk                              | ovos-stt-plugin-vosk                              | ovos-stt-plugin-vosk                              |
| STT - On premises       | ovos-stt-plugin-server<br>(any plugin)            | ovos-stt-plugin-server<br>(any plugin)            | ovos-stt-plugin-server<br>(any plugin)            |
| STT - Cloud             | ovos-stt-plugin-server<br>(ovos proxy)            | ovos-stt-plugin-server<br>(ovos proxy)            | ovos-stt-plugin-server<br>(ovos proxy)            |
| TTS - On device         | ovos-tts-plugin-mimic3                            | ovos-tts-plugin-mimic3                            | ovos-tts-plugin-mimic3                            |
| TTS - On premises       | ovos-tts-plugin-server<br>(any plugin)            | ovos-tts-plugin-server<br>(any plugin)            | ovos-tts-plugin-server<br>(any plugin)            |
| TTS - Cloud             | ovos-tts-plugin-mimic3-server<br>(public servers) | ovos-tts-plugin-mimic3-server<br>(public servers) | ovos-tts-plugin-mimic3-server<br>(public servers) |
| VAD                     | ovos-vad-plugin-webrtcvad                         | ovos-vad-plugin-silero                            | ovos-vad-plugin-silero                            |


### Friends

|                         | NeonAI                                         | Bigscreen                                         |
|-------------------------|------------------------------------------------|---------------------------------------------------|
| **Default Plugins**     |                           	                   |                                                   |
| VAD                     | ovos-vad-plugin-webrtcvad                      | ovos-vad-plugin-webrtcvad                      | 
| stt                     | neon-stt-plugin-google-cloud-streaming         | ovos-stt-plugin-server<br>(ovos proxy)            |
| fallback_stt            | ovos-stt-plugin-vosk                           | N/A                                               |
| tts                     | neon-tts-plugin-coqui-remote                   | ovos-tts-plugin-mimic2                            |
| fallback_tts            | neon-tts-plugin-coqui                          | ovos-tts-plugin-mimic                             |
| **Recommended Plugins** |                           	                   |                                                   |
| STT - On device         | ovos-stt-plugin-vosk                           | ovos-stt-plugin-vosk                              |
| STT - On premises       | neon-stt-plugin-nemo                           | ovos-stt-plugin-server<br>(any plugin)            |
| STT - Cloud             | neon-stt-plugin-google-cloud-streaming         | ovos-stt-plugin-server<br>(ovos proxy)            |
| TTS - On device         | neon-tts-plugin-coqui                          | ovos-tts-plugin-mimic3                            |
| TTS - On premises       | ovos-stt-plugin-server + neon-tts-plugin-coqui | ovos-tts-plugin-server<br>(any plugin)            |
| TTS - Cloud             | neon-tts-plugin-coqui-remote                   | ovos-tts-plugin-mimic3-server<br>(public servers) |
| VAD                     | ovos-vad-plugin-webrtcvad                      | ovos-vad-plugin-webrtcvad                         |

### Mycroft

|                         | Mark 1<br>(Classic Core)              | Mark 2<br>(Dinkum)                    | Picroft<br>(Classic Core)             |
|-------------------------|---------------------------------------|---------------------------------------|---------------------------------------|
| **Default Plugins**     |                                       |                                       |                                       |
| VAD                     | N/A<br>(missing feature)              | silero (hardcoded)                    | N/A<br>(missing feature)              |
| stt                     | mycroft (selene)<br>(internal plugin) | mycroft (selene)<br>(internal plugin) | mycroft (selene)<br>(internal plugin) |
| fallback_stt            | N/A<br>(missing feature)              | N/A<br>(missing feature)              | N/A<br>(missing feature)              |
| tts                     | mimic2<br>(internal plugin)           | mimic 3<br>(internal plugin)          | mimic2<br>(internal plugin)           |
| fallback_tts            | mimic<br>(internal plugin)            | mimic<br>(internal plugin)            | mimic<br>(internal plugin)            |
| **Recommended Plugins** |                                       |                                       |                                       |
| STT - On device         | N/A                                   | grokotron<br>(internal plugin)        | N/A                                   |
| STT - On premises       | N/A (?)                               | N/A                                   | N/A (?)                               |
| STT - Cloud             | mycroft (selene)<br>(internal plugin) | mycroft (selene)<br>(internal plugin) | mycroft (selene)<br>(internal plugin) |
| TTS - On device         | mimic<br>(internal plugin)            | mimic 3<br>(internal plugin)          | mimic<br>(internal plugin)            |
| TTS - On premises       | N/A (?)                               | N/A (?)                               | N/A (?)                               |
| TTS - Cloud             | mimic2<br>(internal plugin)           | N/A (?)                               | mimic2<br>(internal plugin)           |
| VAD                     | N/A<br>(missing feature)              | silero (hardcoded)                    | N/A<br>(missing feature)              |


## Functionality

MNOs - Mycroft/Neon/OVOS

### OpenVoiceOS

|                                    | ovos-buildroot                      | ovos-arch                           | ovos-raspbian                       |
|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| **Skill Frameworks**               |                                     |                                     |                                     |
| Mycroft Audio Service<br>(bus api) | Yes                                 | Yes                                 | Yes                                 |
| Adapt Intents                      | Yes                                 | Yes                                 | Yes                                 |
| Padatious Intents                  | Yes                                 | Yes                                 | Yes                                 |
| OCP Skills                         | Yes                                 | Yes                                 | Partial<br>(audio only)             |
| MNOS Common Query Skills           | Yes                                 | Yes                                 | Yes                                 |
| MNOs Fallback Skills               | Yes                                 | Yes                                 | Yes                                 |
| MNOs Skills                        | Yes                                 | Yes                                 | Yes                                 |
| Mycroft Common Play Skills         | Partial<br>(imperfect compat layer) | Partial<br>(imperfect compat layer) | Partial<br>(imperfect compat layer) |
| **Media Frameworks**               |                                     |                                     |                                     |
| OCP                                | Yes                                 | Yes                                 | Yes                                 |
| MPRIS                              | Yes                                 | Yes                                 | Yes (?)                             |
| KDEConnect                         | Yes                                 | Yes (?)                             | No                                  |
| Spotify Daemon                     | Yes                                 | No (?)                              | No                                  |
| Airplay                            | Yes                                 | No (?)                              | No                                  |
| Bluetooth Speaker                  | WIP                                 | No (?)                              | No                                  |
| **IOT Frameworks**                 |                                           |                    |                           |     
| HomeAssistant integration          | **WIP**<br>*HomeAssistant<br>PHAL Plugin* | **WIP**<br>*HomeAssistant<br>PHAL Plugin* | **WIP**<br>*HomeAssistant<br>PHAL Plugin*<br>(manual install) |    

### Friends

|                                 	 | NeonAI                              | Bigscreen                           |
|------------------------------------|-------------------------------------|-------------------------------------| 
| **Skill Frameworks**               |                                     |                                     |  
| Mycroft Audio Service<br>(bus api) | Yes                                 | Yes                                 |
| Adapt Intents                      | Yes                                 | Yes                                 | 
| Padatious Intents                  | Yes                                 | Yes                                 | 
| OCP Skills                         | Yes                                 | Yes                                 | 
| MNOS Common Query Skills           | Yes                                 | Yes                                 |
| MNOs Fallback Skills               | Yes                                 | Yes                                 | 
| MNOs Skills                        | Yes                                 | Yes                                 | 
| Mycroft Common Play Skills         | Partial<br>(imperfect compat layer) | Partial<br>(imperfect compat layer) |
| **Media Frameworks**               |                                     |                                     |
| OCP                                | Yes                                 | Yes                                 | 
| MPRIS                              | Yes (?)                             | Yes                                 | 
| KDEConnect                         | No (?)                              | Yes (?)                             |
| Spotify Daemon                     | No                                  | No (?)                              | 
| Airplay                            | No                                  | No (?)                              | 
| Bluetooth Speaker                  | No                                  | No (?)                              | 
| **IOT Frameworks**                 |                                           |                                           |                            
| HomeAssistant integration          | **WIP**<br>*HomeAssistant<br>PHAL Plugin* | **WIP**<br>*HomeAssistant<br>PHAL Plugin* |


### Mycroft

|                                    | Mark 1<br>(Classic Core) | Mark 2<br>(Dinkum)  | Picroft<br>(Classic Core) |
|------------------------------------|--------------------------|---------------------|---------------------------|
| **Skill Frameworks**               |                          |                     |                           |
| Mycroft Audio Service<br>(bus api) | Yes                      | ?                   | Yes                       |
| Adapt Intents                      | Yes                      | Yes                 | Yes                       |
| Padatious Intents                  | Yes                      | Yes                 | Yes                       |
| OCP Skills                         | No                       | No                  | No                        |
| MNOS Common Query Skills           | Yes                      | No                  | Yes                       |
| MNOs Fallback Skills               | Yes                      | No                  | Yes                       |
| MNOs Skills                        | Yes                      | No                  | Yes                       |
| Mycroft Common Play Skills         | Yes                      | No                  | Yes                       |
| **Media Frameworks**               |                          |                     |                           |                                     
| OCP                                | No                       | No                  | No                        |
| MPRIS                              | No                       | No                  | No                        |
| KDEConnect                         | No                       | No                  | No                        |
| Spotify Daemon                     | Partial (?)              | No                  | Partial (?)               |
| Airplay                            | No                       | No                  | No                        |
| Bluetooth Speaker                  | No                       | No                  | No                        |
| **IOT Frameworks**                 |                          |                     |                           |     
| HomeAssistant integration          | Yes (?)<br>Mycroft Skill | Yes<br>Dinkum Skill | Yes (?)<br>Mycroft Skill |    


## Configuration

### OpenVoiceOS

|           | ovos-buildroot | ovos-arch | ovos-raspbian |
|-----------|----------------|-----------|---------------|
| **Configuration - Option**                                                      |
| Data privacy                                                                    |                                   Yes                                   |                        Yes                        |                       Yes                         |                       
| Offline mode                                                                    |                                   Yes  <br> (setup skill)               |                        Yes  <br> (setup skill)    |                       yes  <br> (need to change default plugins)                       |                      
| Color theming                                                                   |                                   Yes                                   |                        Yes                        |                       No                          |                      
| Non-Pairing mode                                                                |                                   Yes  <br> (setup skill)                                 |                        Yes   <br> (setup skill)                     |                 Yes<br> (preconfigured default)                  |                      
| API Access w/o pairing                                                          |                                   Yes                                   |                        Yes                        |                       Yes                         |                      
| On-Screen configuration                                                         |                                   Yes                                   |                        Yes                        |                       No                          |                     
| Online configuration                                                            |                           personal-backend + dashboard<br>**wip**                            |                personal-backend + dashboard<br>**wip**                 |               personal-backend + dashboard<br>(manual install)                 |                     
| **Network Setup - Options**                                                     |
| Mobile WiFi Setup<br>*Easy device "hotspot"<br>to connect from phone*           |                                   Yes                                   |                        No                         |                   No                    |                       
| On device WiFi Setup<br>*Configure the connection<br>directly on screen*        |                                   Yes                                   |                        Yes                        |                   No                     |                     
| On screen keyboard                                                              |                                   Yes                                   |                        Yes                        |                       No                          |                     
| Reconfigure network<br>*Easy way to change the<br>network settings*             |                                   Yes <br> (on screen)                                  |                        Yes  <br> (on screen)                       |                  Yes  <br> (raspi-config)                     |                      



### Friends

|         	| NeonAI | Bigscreen |
|-----------|--------|-----------| 
| **Network Setup - Options**                                                                                |
| Mobile WiFi Setup<br>*Easy device "hotspot"<br>to connect from phone*                                      |                        No                        |                       No                       |
| On device WiFi Setup<br>*Configure the connection<br>directly on device*                                |                                                                     Yes                        |                      Yes                       |
| On screen keyboard                                                                                         |                                                                               Yes                        |                       Yes                       |
| Reconfigure network<br>*Easy way to change the<br>network settings*                                            |                                                                            Yes                        |                      Yes                       |
| **Configuration - Option**                                                                                  |
| Data privacy                                                                                               |                                                                           Yes                        |                     Yes                     |
| Offline mode                                                                                               |                                                                       Yes                        |                       Yes                        | 
| Color theming                                                                                              |                                                                           Yes                        |                       No                        | 
| Non-Pairing mode                                                                                           |                                                                     Yes                        |                       Yes                        |
| API Access w/o pairing                                                                                     |                                                                              Yes                        |                       Yes                        |
| On-Device configuration                                                                                     |                                                                             Yes                        |                       ?                        | 
| Online configuration                                                                                        |                                                   *WIP*                       |                       ?                       | 


### Mycroft

|           | Mark 1<br>(Classic Core) | Mark 2<br>(Dinkum) | Picroft<br>(Classic Core) |
|-----------|--------------------------|--------------------|---------------------------|
| **Network Setup - Options**                                                                                |
| Mobile WiFi Setup<br>*Easy device "hotspot"<br>to connect from phone*                                      |                        Yes                        |                       Yes                       | No |
| On device WiFi Setup<br>*Configure the connection<br>directly on device*                                |                            No                        |                       No                        | No |
| On screen keyboard                                                                                         |                         No                        |                       Yes                       | No |
| Reconfigure network<br>*Easy way to change the<br>network settings*                                            |                                                                            Yes  <br> (mk1 menu)                      |                       No                        | No |
| **Configuration - Option**                                                                                  |
| Data privacy                                                                                               |                                                                           Partial                        |                     Partial                     | Partial |
| Offline mode                                                                                               |                                                                      No                 |                       No                        | No |
| Color theming                                                                                              |                                                                  No                        |                       No                        | No |
| Non-Pairing mode                                                                                           |                                                                 No                        |                       No                        | No |
| API Access w/o pairing                                                                                     |                                                                         No                       |                       No                        | No |
| On-Device configuration                                                                                     |                                                                         No                       |                       No                        | No |
| Online configuration                                                                                        |                                                   Yes                      |                       Yes                       | Yes |


## Hardware

### OpenVoiceOS

|                              | ovos-buildroot                | ovos-arch            | ovos-raspbian                        |
|------------------------------|-------------------------------|----------------------|--------------------------------------|
| **Hardware - Compatibility** |
| Raspberry Pi 3B              | **WIP**                           | No                   | Yes                                  |   
| Raspberry Pi 3B+             | **WIP**                           | No                   | Yes                                  | 
| Raspberry Pi 3A+             | **WIP**                           | No                   | Yes                                  |   
| Raspberry Pi 4               | Yes                           | Yes                  | Yes                                  | 
| X86_64                       | *planned*                     | No                   | No                                   |                     
| Mark-1                       | **WIP**                       | No                   | No<br>*possibly in future*           |                        
| Mark-2                       | **WIP**<br>(no leds)          | **WIP**<br>(no leds) | partial<br>(no gui + manual install) |           
| Mark-2  (dev kit)            | Yes                           | Yes                  | partial<br>(no gui + manual install) |           
| **Hardware - Peripherals**   |
| ReSpeaker  2-mic             | Yes (?)                       | Yes (?)              | manual install (?)                   |        
| ReSpeaker  4-mic squared     | Yes (?)                       | No (?)               | manual install (?)                   |        
| ReSpeaker  4-mic linear      | Yes (?)                       | No (?)               | manual install (?)                   |  
| ReSpeaker  6-mic             | Yes (?)                       | No (?)               | manual install (?)                   |                
| USB                          | Yes                           | Yes                  | Yes                                  |                    
| SJ-201                       | Yes                           | Yes                  | manual install (?)                   |                   
| Google AIY v1                | manual install (?)            | manual install       | manual install (?)                   |                     
| Google AIY v2                | No<br>*perhaps in the future* | manual install       | manual install (?)                   |                   


### Friends

|         	| NeonAI | Bigscreen |
|-----------|--------|-----------|
| **Hardware - Compatibility** |
| Raspberry Pi 3B              | No                 | No                   | 
| Raspberry Pi 3B+             | No                 | No                   | 
| Raspberry Pi 3A+             | No                 | No                   | 
| Raspberry Pi 4               | Yes                | Yes                  | 
| X86_64                       | No                 | No                   |                   
| Mark-1                       | No                 | No                   |                      
| Mark-2                       | Yes                | No                   |         
| Mark-2  (dev kit)            | Yes                | No                   | 
| **Hardware - Peripherals**   |
| ReSpeaker  2-mic             | manual install (?) | manual install (?)   | 
| ReSpeaker  4-mic squared     | manual install (?) | manual install (?)   |   
| ReSpeaker  4-mic linear      | manual install (?) | manual install (?)   |
| ReSpeaker  6-mic             | manual install (?) | manual install (?)   |          
| USB                          | Yes                | Yes                  |                 
| SJ-201                       | Yes                | No                   |              
| Google AIY v1                | manual install (?) | manual install (?)   |                 
| Google AIY v2                | manual install (?) | manual install (?)   |              


### Mycroft

|                              | Mark 1<br>(Classic Core) | Mark 2<br>(Dinkum)     | Picroft<br>(Classic Core)            |
|------------------------------|--------------------------|------------------------|--------------------------------------|
| **Hardware - Compatibility** |
| Raspberry Pi 3B              | No                       | No                     | Yes                                  |   
| Raspberry Pi 3B+             | No                       | No                     | Yes                                  | 
| Raspberry Pi 3A+             | No                       | No                     | No (?)                               |   
| Raspberry Pi 4               | No                       | Yes<br>(sandbox image) | Yes (?)                              | 
| X86_64                       | No                       | No                     | No                                   |                      
| Mark-1                       | Yes                      | No                     | No                                   |                        
| Mark-2                       | No                       | Yes                    | No                                   |           
| Mark-2  (dev kit)            | No                       | Yes                    | No                                   |           
| **Hardware - Peripherals**   |
| ReSpeaker  2-mic             | No                       | No                 | manual install (?)                   |        
| ReSpeaker  4-mic squared     | No                       | No                 | manual install (?)                   |        
| ReSpeaker  4-mic linear      | No                       | No                 | manual install (?)                   |  
| ReSpeaker  6-mic             | No                       | No                 | manual install (?)                   |                
| USB                          | Yes (?)                  | No (?)             | Yes                                  |                    
| SJ-201                       | No                       | Yes                | manual install (?)                   |                   
| Google AIY v1                | No                       | No                 | Yes (?)                              |                     
| Google AIY v2                | No                       | No                 | manual install (?)                   |                   

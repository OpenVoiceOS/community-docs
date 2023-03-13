# OpenVoiceOS vs Neon A.I. vs Mycroft A.I.

## OpenVoiceOS images

OpenVoiceOS ready to use images come in several flavours;
The buildroot version, being the minimal consumer type of image and the Manjaro version, being the full distribution easy / easier for developing.

a headless raspbian image is also maintained by the community

|                                                                                 |                     **OpenVoiceOS<br>(Buildroot)**                      |           **OpenVoiceOS<br>(Manjaro)**            |           **OpenVoiceOS<br>(Raspbian)**           | 
|:--------------------------------------------------------------------------------|:-----------------------------------------------------------------------:|:-------------------------------------------------:|:-------------------------------------------------:|
| **Operating System**                                                            |
| Base OS                                                                         |                    buildroot                     |                     manjaro                     | raspbian |
| Last updated - YYYY/MM/DD                                                       |                    2023-0?-??                      |                     2023-0?-??                      | 2023-03-?? |
| **Software - Architecture**                                                     |
| Core                                                                            |                                ovos-core                                |                     ovos-core                     |                     ovos-core                     |  
| GUI                                                                             |                   ovos-shell<br>*(mycroft-gui based)*                   |        ovos-shell<br>*(mycroft-gui based)*        |                       N/A                        |   
| Launcher                                                                        |                         systemd<br>user session                         |             systemd<br>system session             |              systemd<br>user session              |    
| **Hardware - Compatibility**                                                    |
| Raspberry Pi                                                                    |                                3/3b/3b+/4                                |                         4                         |                    3/3b/3b+/4                     |   
| X86_64                                                                          |                                *planned*                                |                        No                         |               No               |                    
| Virtual Appliance                                                               |                                *planned*                                |                        No                         |                     ?                       |                    
| Docker                                                                          |                       No<br>*possibly in future*                        |                        Yes                        |                     ?                       |                      
| Mark-1                                                                          |                              **WIP**                               |                        No                         |   No<br>*possibly in future*  |                        
| Mark-2                                                                          |                    **WIP**<br>(no leds)                                 |            **WIP**<br>(no leds)                   |            partial<br>(no gui + manual install)           |           
| Mark-2  (dev kit)                                                               |                    Yes                                                  |            Yes                                    |            partial<br>(no gui + manual install)           |           
| **Hardware - Peripherals**                                                      |
| ReSpeaker                                                                       |             **WIP**<br>2-mic<br>4-mic squared<br>4-mic linear<br>6-mic             |  **WIP**<br>2-mic<br>4-mic squared<br>4-mic linear<br>6-mic  |                       manual install                         |                  
| USB                                                                             |                                   Yes                                   |                        Yes                        |                       Yes                         |                    
| SJ-201                                                                          |                                   Yes                                   |                        Yes                        |                       manual install                         |                   
| Google AIY v1                                                                   |                      manual install                      |           manual install            |      manual install      |                     
| Google AIY v2                                                                   |                      No<br>*perhaps in the future*                      |           manual install            |      manual install      |                   
| **Screen - GUI**                                                                |
| GUI supported<br>*Showing a GUI if a screen is attached*                        |                      Yes<br>*ovos-shell on eglfs*                       |           Yes<br>*ovos-shell on eglfs*            |                       No                          |        
| **Network Setup - Options**                                                     |
| Mobile WiFi Setup<br>*Easy device "hotspot"<br>to connect from phone*           |                                   Yes                                   |                        No                         |                   No                    |                       
| On device WiFi Setup<br>*Configure the connection<br>directly on screen*        |                                   Yes                                   |                        Yes                        |                   No                     |                     
| On screen keyboard                                                              |                                   Yes                                   |                        Yes                        |                       No                          |                     
| Reconfigure network<br>*Easy way to change the<br>network settings*             |                                   Yes <br> (on screen)                                  |                        Yes  <br> (on screen)                       |                  Yes  <br> (raspi-config)                     |                      
| **Configuration - Option**                                                      |
| Data privacy                                                                    |                                   Yes                                   |                        Yes                        |                       Yes                         |                       
| Offline mode                                                                    |                                   Yes  <br> (setup skill)               |                        Yes  <br> (setup skill)    |                       yes  <br> (need to change default plugins)                       |                      
| Color theming                                                                   |                                   Yes                                   |                        Yes                        |                       No                          |                      
| Non-Pairing mode                                                                |                                   Yes  <br> (setup skill)                                 |                        Yes   <br> (setup skill)                     |                 Yes<br> (preconfigured default)                  |                      
| API Access w/o pairing                                                          |                                   Yes                                   |                        Yes                        |                       Yes                         |                      
| On-Screen configuration                                                         |                                   Yes                                   |                        Yes                        |                       No                          |                     
| Online configuration                                                            |                           personal-backend + dashboard<br>**wip**                            |                personal-backend + dashboard<br>**wip**                 |               personal-backend + dashboard<br>(manual install)                 |                     
| **Customization**                                                               |
| Open Build System                                                               |                                   Yes                                   |                        Yes                        |                       Yes                         |                      
| Package manager                                                                 |     No<br>*No buildtools available.<br>Perhaps opkg in the future*      |                 Yes<br>*(pacman)*                 |                  Yes<br>*(apt)*                   |                      
| **Updating**                                                                    |
| Update mechanism(s)                                                             | pip <br>(bash scripts)<br>*planned:Firmware updates.<br>On-device and Over The Air* |              pip <br>(bash scripts)               |    pip <br>(bash scripts)  | 
| **Voice Assistant - Functionality**                                             |
| STT - On device                                                                 |   Yes<br>*Kaldi/Vosk-API<br>WhisperCPP (WIP)<br>Whisper TFlite (WIP)*   |              Yes<br>*Kaldi/Vosk-API*              |              No                          |         
| STT - On premises                                                               |              Ovos STT Server<br>(any plugin)               |   Ovos STT Server<br>(any plugin)     |   Ovos STT Server<br>(any plugin)    |      
| STT - Cloud                                                                     |            Ovos Server Proxy<br>(google chromium)            |     Ovos Server Proxy<br>(google chromium)      |    Ovos Server Proxy<br>(google chromium)     |                 
| TTS - On device                                                                 |                      default: **Mimic 1**                       |           default: **Mimic 1**            |              default: **Mimic 1**                     |     
| TTS - On premises                                                               |         Ovos TTS Server<br>(any plugin)                  |  Ovos TTS Server<br>(any plugin)     |   Ovos TTS Server<br>(any plugin)    |     
| TTS - Cloud                                                                     |            default: **Mimic 3**               | default: **Mimic 3** | default: **Mimic 3** |              
| **Smart Speaker - Functionality**                                               |
| Music player connectivity<br>*use of external applications<br>on other devices* |  Yes<br>*Airplay<br>Spotifyd<br>Bluetooth<br>Snapcast<br>KDE Connect*   |                      ?                      |           ?                       |                     
| Music player sync                                                               |                          Yes<br>*OCP<br>MPRIS*                          |               Yes<br>*OCP<br>MPRIS*               |                   No<br>*wip*                     |              
| HomeAssistant integration                                                       |                                 **WIP**<br>*HomeAssistant<br>PHAL Plugin*                                 |       **WIP**<br>*HomeAssistant<br>PHAL Plugin*       |                    **WIP**<br>*HomeAssistant<br>PHAL Plugin*<br>(manual install)                     |    
| Camera support                                                                  |                                   Yes                                   |                       *wip*                       |                      *wip*                        |                    


## Friend Images

Some other projects also provide images shipping OpenVoiceOS, such as Bigscreen, or some derivative voice assistant, such as NeonAI

|                                                                                                            |                   **Neon AI**                    |             Bigscreen |
|:----------------------------------------------------------------------------------------------------------:|:------------------------------------------------:|:------------------------------------------------:|
| **Operating System**                                                            |
| Base OS                                                                         |                    debian                     |                     manjaro                   | 
| Last updated - YYYY/MM/DD                                                       |                    2023-0?-??                      |                     [Rolling Release](https://github.com/manjaro-arm/bigscreen/releases)                      | 
| **Software - Architecture**                                                                                |
| Core                                                                                                       |                    neon-core                     |                     ovos-core                      | 
| GUI                                                                                                        |       ovos-shell<br>*(mycroft-gui based)*        |      Plasma Shell<br>*(mycroft-gui embedded)*       | 
| Launcher                                                                                                   |            systemd<br>system session             |            systemd<br>user            | 
| **Hardware - Compatibility**                                                                               |
| Raspberry Pi                                                                                               |                        4                         |                4                | 
| X86_64                                                                                                     |                          No                      |                      Manual Install                        | 
| Virtual Appliance                                                                                          |                     ?                      |                       No                        | 
| Docker                                                                                                     |                       Yes                        |                       No                        | 
| Mark-1                                                                                                     |                        No                        |                       No                        | 
| Mark-2                                                                                                     |            Yes            |              No               | 
| Mark-2  (dev kit)                                                               |                    Yes                                                  |            No                                   |          
| **Hardware - Peripherals**                                                                                 |
| ReSpeaker                                                                                                  |                     ?                      |                       Yes (Manual Install)                        | 
| USB                                                                                                        |                     ?                      |                       Yes                        |
| SJ-201                                                                                                     |                                                         Yes                        |                       No                       | 
| Google AIY v1                                                                                              |                                        ?                      |                       Yes (Manual Install)                        |
| Google AIY v2                                                                                              |                                       ?                      |                       Yes (Manual Install)                        |
| **Screen - GUI**                                                                                           |
| GUI supported<br>*Showing a GUI if a screen is attached*                                                   |                                                  Yes<br>*ovos-shell on eglfs*           |           Yes<br>*plasma-bigscreen <br>X11 or Wayland*           |
| **Network Setup - Options**                                                                                |
| Mobile WiFi Setup<br>*Easy device "hotspot"<br>to connect from phone*                                      |                        No                        |                       No                       |
| On device WiFi Setup<br>*Configure the connection<br>directly on device*                                |                                                                     Yes                        |                      Yes                       |
| On screen keyboard                                                                                         |                                                                               Yes                        |                       Yes                       |
| Reconfigure network<br>*Easy way to change the<br>network settings*                                            |                                                                            Yes                        |                      Yes                       |
| **Configuration - Option**                                                                                  |
| Data privacy                                                                                               |                                                                           Yes                        |                     Yes                     |
| Offline mode                                                                                               |                                                                       Yes                        |                       Yes                        | 
| Color theming                                                                                              |                                                                           Yes                        |                       System                        | 
| Non-Pairing mode                                                                                           |                                                                     Yes                        |                       Yes                        |
| API Access w/o pairing                                                                                     |                                                                              Yes                        |                       Yes                        |
| On-Device configuration                                                                                     |                                                                             Yes                        |                       ?                        | 
| Online configuration                                                                                        |                                                   *WIP*                       |                       ?                       | 
| **Customization**                                                                                          |
| Open Build System                                                                                          |                                                              Yes                        |     Yes    | 
| Package manager                                                                                            |                                     Yes                        | Yes |
| **Updating**                                                                                               |
| Update mechanism(s)                                                                                        |       Plugin-based mechanism</br>OS Updates **WIP** |         package manager          |
| **Voice Assistant - Functionality**                                                                        |
| STT - On device                                                                                                                   |           default: **Deepspeech**            |            Yes<br>*Vosk*         | 
| STT - On premises                                                                                           |      Ovos STT Server<br>(any plugin)       |                        Ovos STT Server<br>(any plugin)                        | 
| STT - Cloud                                                                                                    |                 Ovos Server Proxy
(google chromium)                  |     Yes<br>*Google*     |
| TTS - On device                                                                                                                 |       default: **Coqui**       |                default: **Mimic**                 | 
| TTS - On premises                                                                                                              |      Ovos TTS Server<br>(any plugin)       |                        Ovos TTS Server<br>(any plugin)                        |
| TTS - Cloud                                                                                                |                         default: **Amazon Polly**               |                       default: **Mimic 2**                        |
| **Smart Speaker - Functionality**                                                                          |
| Music player connectivity<br>*use of external applications<br>on other devices*                            |                     ?                      |           Yes<br>*MPRIS (KDEKonnect)*           | 
| Music player sync                                                                                          |                                                      Yes<br>*OCP<br>MPRIS*               |                       Yes<br>*OCP<br>MPRIS*                        | 
| HomeAssistant integration                                                                                  |                                                            **WIP**<br>*HomeAssistant<br>PHAL Plugin*     |                     Yes (Manual Install)<br>*HomeAssistant<br>PHAL Plugin*                     | 
| Camera support                                                                                             |                                                                             Yes                        |                     No                     | 

## Mycroft Images

MycroftAI also provides some images, we do not recommend using any of these but provide a table for comparison

|                                                                                                            |                   **Mark I<br>(Classic Core)**                    |             **Mark II<br>(Dinkum)**             | **Picroft<br>(Classic Core)**  |
|:----------------------------------------------------------------------------------------------------------:|:------------------------------------------------:|:------------------------------------------------:|:-----------------------------------------------:|
| **Operating System**                                                            |
| Base OS                                                                         |                    raspbian                     |                     pantacor containers                    | raspbian |
| Last updated - YYYY/MM/DD                                                       |                    20??-0?-??                      |                     2023-0?-??                      | 20??-??-?? |
| **Software - Architecture**                                                                                |
| Core                                                                                                       |                    mycroft-core                     |                     Dinkum                      | mycroft-core |
| GUI                                                                                                        |       N/A        |      plasma-nano<br>*(mycroft-gui based)*       | N/A |
| Launcher                                                                                                   |            ?             |            Pantacor            | bash script |
| **Hardware - Compatibility**                                                                               |
| Raspberry Pi                                                                                               |                        Mark I <br> (only)                         |                Mark II<br>(only)                | 3/3b/3b/4 |
| X86_64                                                                                                     |                          No                      |                       No                        | No |
| Virtual Appliance                                                                                          |                     ?                      |                       No                        | No |
| Docker                                                                                                     |                       ?                        |                       No                        | No |
| Mark-1                                                                                                     |                        Yes                        |                       No                        | No |
| Mark-2                                                                                                     |            No            |              Yes               | No |
| Mark-2  (dev kit)                                                               |                    No                                                 |            No                                   |            No           |
| **Hardware - Peripherals**                                                                                 |
| ReSpeaker                                                                                                  |                     No                      |                       No                        | Yes<br>*manual installation?* |
| USB                                                                                                        |                     No                      |                       No                        | Yes<br>*manual installation* |
| SJ-201                                                                                                     |                    No                        |                       Yes                       | No<br>*sandbox image maybe* |
| Google AIY v1                                                                                              |                    No                      |                       No                        | No<br>*manual installation?* |
| Google AIY v2                                                                                              |                    No                     |                       No                        | No<br>*manual installation?* |
| **Screen - GUI**                                                                                           |
| GUI supported<br>*Showing a GUI if a screen is attached*                                                   |                                                  No         |           Yes<br>*plasma-nano on X11*           | No |
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
| **Customization**                                                                                          |
| Open Build System                                                                                          |                                                              Yes                        |     Partial<br>*build tools are not public*     | Yes |
| Package manager                                                                                            |                                     Yes                        | Yes<br>*limited becuase of read-only filesystem | Yes |
| **Updating**                                                                                               |
| Update mechanism(s)                                                                                        |       ? |         OTA<br>*controlled by Mycroft*          | git pull |
| **Voice Assistant - Functionality**                                                                        |
| STT - On device                                                                                                                   |      No           |            Yes<br>*Vosk*<br>*Coqui*             | No |
| STT - On premises                                                                                           |      No     |                       No                        | No |
| STT - Cloud                                                                                                    |                 default: **Selene**<br>(Google Chromium Proxy)                |     default: **Selene**<br>(Google Cloud Proxy)     |   default: **Selene**<br>(Google Chromium Proxy) |
| TTS - On device                                                                                                                 |       default: **Mimic 1**       |                default: **Mimic 3**                 | default: **Mimic 1** |
| TTS - On premises                                                                                                              |       ?         |                       No                        | No |
| TTS - Cloud                                                                                                |                         default: **Mimic 2**            |                       default: **Mimic 2**                        | default: **Mimic 2** |
| **Smart Speaker - Functionality**                                                                          |
| Music player connectivity<br>*use of external applications<br>on other devices*                            |                     No                   |           Yes<br>*MPD<br>Local Files*           | No<br>*manual installation?* |
| Music player sync                                                                                          |                                                     No             |                       No                        | No |
| HomeAssistant integration                                                                                  |                                                            ?   |                     Yes<br>Mycroft Skill                     | ? |
| Camera support                                                                                             |                                                                          No                      |                     ?                     | ? |

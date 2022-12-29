# OpenVoiceOS vs Neon A.I. vs Mycroft A.I.

## Ready to go images compared
OpenVoiceOS ready to use images come in two flavours; The buildroot version, being the minimal consumer type of image and the Manjaro version, being the full distribution easy / easier for developing.

|  | **OpenVoiceOS<br>(Buildroot)** | **OpenVoiceOS<br>(Manjaro)** | **Neon AI** | **Mark II<br>(Dinkum)** | **Mycroft A.I.<br>(PiCroft)**  |
|:---|:---:|:---:|:---:|:---:|:---:|
| **Software - Architecture** |
| Core | ovos-core | ovos-core | neon-core | Dinkum | mycroft-core |
| GUI | ovos-shell<br>*(mycroft-gui based)* | ovos-shell<br>*(mycroft-gui based)* | ovos-shell<br>*(mycroft-gui based)* | plasma-nano<br>*(mycroft-gui based)* | N/A |
| Services | systemd<br>user session | systemd<br>system session | systemd<br>system session | systemd<br>system session | N/A |
| **Hardware - Compatibility** |
| Raspberry Pi | 3/3b/3b/4| 4 | 4 | Mark II<br>(only) | 3/3b/3b/4 |
| X86_64 | *planned* | No | Unknown | No | No |
| Virtual Appliance | *planned* | No | Unknown | No | No |
| Docker | No<br>*possibly in future* | Yes | Yes | No | No |
| Mark-1 | Yes<br>*WIP* | No | No | No | No |
| Mark-2 | Yes<br>*Dev-Kit<br>Retail (WIP)* | Yes<br>*Dev-Kit<br>Retail* | Yes<br>*Dev-Kit<br>Retail* | Yes<br>*Retail ONLY* | No |
| **Hardware - Peripherals** |
| ReSpeaker | 2-mic<br>4-mic squared<br>4-mic lineair<br>6-mic | 2-mic<br>4-mic squared<br>4-mic lineair<br>6-mic | Unknown | No | Yes<br>*manual installation?* |
| USB | Yes | Yes | Unknown | No | Yes<br>*manual installation* |
| SJ-201 | Yes | Yes | Yes | Yes | No<br>*sandbox image maybe* |
| Google AIY v1 | Yes<br>*manual configuration* | Yes<br>*manual installation* | Unknown | No | No<br>*manual installation?* |
| Google AIY v2 | No<br>*perhaps in the future* | Yes<br>*manual installation*  | Unknown | No | No<br>*manual installation?* |
| **Screen - GUI** |
| GUI supported<br>*Showing a GUI if a screen is attached* | Yes<br>*ovos-shell on eglfs* | Yes<br>*ovos-shell on eglfs* | Yes<br>*ovos-shell on eglfs* | Yes<br>*plasma-nano on X11* | No |
| **Network Setup - Options** |
| Mobile WiFi Setup<br>*Easy device "hotspot" to connect to preset network from phone or pad.*  | Yes | No | No | Yes | No |
| On device WiFi Setup<br>*Configure the WiFi connection on the device itself* | Yes | Yes | WIP | No | No |
| On screen keyboard | Yes | Yes | No | Yes | No |
| Reconfigure network<br>*Easy way to change the network settings* | Yes | Yes | Yes | No | No |
| **Configuration - Option** |
| Data privacy | Yes | Yes | Yes | Partial | Partial |
| Offline mode | Yes | Yes | Yes | No | No |
| Color theming | Yes | Yes | Yes | No | No |
| Non-Pairing mode | Yes | Yes | Yes | No | No |
| API Acces w/o pairing | Yes | Yes | Yes | No | No |
| On-Device configuration | Yes | Yes | WIP | No | No |
| Online configuration | Dashboard<br>*wip*  | Dashboard<br>*wip* | No | Yes | Yes |
| **Custimization** |
| Open Build System | Yes | Yes | Yes | Partial<br>*build tools are not public* | Yes |
| Package manager | No<br>*No buildtools available.<br>Perhaps opkg in the future* | Yes<br>*(pacman)* | Yes | Yes<br>*limited bacuase of read-only filesystem | Yes |
| **Updating** |
| Update mechanism(s) | pip<br>*In the future:<br>Firmware updates. On-device and Over The Air* | pip<br>package manager | pip<br>package manager | OTA<br>*controlled by Mycroft* | pip<br>package manager |
| **Voice Assistant - Functionality** |
| STT - On device | Yes<br>*Kaldi/Vosk-API<br>WhisperCPP (WIP)<br>Whisper TFlite (WIP)* | Yes<br>*Kaldi/Vosk-API* | Yes<br>*?* | No | No |
| STT - On premises | Yes<br>*Ovos Server Proxy<br>More...?* | Yes<br>*Ovos Server Proxy<br>* | Yes<br>*?* | No | No |
| STT - Cloud | Yes<br>*Ovos Server Proxy<br>Google<br>More...?* | Yes<br>*Ovos Server Proxy<br>Google<br>* | Yes<br>*?* | No | No |
| TTS - On device | Yes<br>*Mimic 1<br>More...?* | Yes<br>*Mimic 1<br>More...?* | Yes<br>*Mimic 1<br>Mimic 3<br>More...?* | Yes<br>*Mimic 3* | Yes<br>*Mimic 1* |
| TTS - On premises | Yes<br>*?* | Yes<br>*?* | Yes<br>*?* | No | No |
| TTS - Cloud | Yes<br>*Google<br>Mimic 2<br>Mimic 3<br>More...?* | Yes<br>*Google<br>Mimic 2<br>Mimic 3<br>More...?*  | Yes<br>*?* | No | No |
| **Smart Speaker - Functionality** |
| Music player connectivity<br>*The use of external application on other devices to connect to your device.* | Yes<br>*Airplay<br>Spotifyd<br>Bluetooth<br>Snapcast<br>KDE Connect* | Unknown | Unknown | Yes<br>*MPD<br>Local Files* | No<br>*manual installation?* |
| Music player sync | Yes<br>*OCP<br>MPRIS* | Yes<br>*OCP<br>MPRIS* | Yes<br>*OCP<br>MPRIS* | No | No |
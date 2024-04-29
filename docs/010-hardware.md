# Supported Hardware

OVOS has been confirmed to run on several devices, and more to come.

- RPI3b / RPI3b+  (Headless only)
  - [Headless Image](https://ovosimages.ziggyai.online/raspbian/development/)
  - [Mark 1 image](https://ovosimages.ziggyai.online/mark1)
    - [Mycroft Mark 1 device.](https://github.com/MycroftAI/hardware-mycroft-mark-1)  ([ovos-PHAL-plugin-mk1 plugin required](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk1))
- RPI4  (GUI and Headless)
  - [Buildroot GUI image](https://drive.google.com/file/d/1PUtNXfZ5jMUlVAgyN-KXPdVdX6r51eBw/view?usp=share_link)
    - Will run native on a Mark 2 device.
  - [Mycroft Mark 2 device.](https://github.com/MycroftAI/hardware-mycroft-mark-II)  (Multiple plugins required)
    - [neon-phal-plugin-linear_led](https://github.com/NeonGeckoCom/neon-phal-plugin-linear_led)
    - [neon-phal-plugin-switches](https://github.com/NeonGeckoCom/neon-phal-plugin-switches)
    - [neon-phal-plugin-fan](https://github.com/NeonGeckoCom/neon-phal-plugin-fan)
- x86-64
  - Linux OS (Python packages or Docker)
  - Windows (Docker)
  - MacOS  (Docker)
  - [Docker GitHub](https://github.com/OpenVoiceOS/ovos-docker)
- OrangePi (Possible, but not yet tested)
- More to come

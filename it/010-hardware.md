# Hardware supportato

È stato confermato che OVOS funziona su vari dispositivi e molti altri saranno aggiunti.

- RPI3b e RPI3b+ (solo headless)
    - [Immagine headless](https://ovosimages/ziggyai.online/raspbian/development/)
    - [Immagine per Mark 1](https://ovosimages/ziggyai/online/mark1)
        - [Mark 1 di Mycroft](https://github.com/MycroftAI/hardware-mycroft-mark-1) (è richiesto il plugin [ovos-PHAL-plugin-mk1](https://github.com/OpenVoiceOS/ovos-PHAL-plugin-mk1))
- RPI4 (con interfaccia grafica e headless)
    - [Immagine Buildroot con interfaccia grafica](https://drive.google.com/file/d/1PUtNXfZ5jMUlVAgyN-KXPdVdX6r51eBw/view?usp=share_link)
        - Funziona nativamente con Mark 2.
    - [Mark 2 di Mycroft](https://github.com/MycroftAI/hardware-mycroft-mark-II) (sono richiesti vari plugin)
        - [neon-phal-plugin-linear_led](https://github.com/NeonGeckoCom/neon-phal-plugin-linear_led)
        - [neon-phal-plugin-switches](https://github.com/NeonGeckoCom/neon-phal-plugin-switches)
        - [neon-phal-plugin-fan](https://github.com/NeonGeckoCom/neon-phal-plugin-fan)
- x86-64
    - Linux (pacchetti Python o Docker)
    - Windows (Docker)
    - MacOS  (Docker)
    - [GitHub per Docker](https://github.com/OpenVoiceOS/ovos-docker)
- OrangePi (possibile ma non ancora testato)
- Altri a venire

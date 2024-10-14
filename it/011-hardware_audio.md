# Hardware audio

Raccomandazioni e note sugli altoparlanti e sui microfoni

La maggior parte dei dispositivi audio può essere utilizzata tramite plugin e nella maggior parte dei casi dovrebbe funzionare senza problemi.

If your device does not work, pop in to our [Matrix support channel](https://app.element.io/#/room/#openvoiceos-support:matrix.org), please create an [issue](https://github.com/OpenVoiceOS/ovos-dinkum-listener/issues) or start a [discussion](https://github.com/orgs/OpenVoiceOS/discussions) about your device.

## USB

Most USB devices should work without any issues.  But, not all devices are created equally.

#### Dispositivi USB testati

- Microfoni
    - BlueSnowball (funziona bene senza problemi)
    - Webcam generica con microfono (funziona ma la qualità del suono può essere carente. Rende meno accurati il rilevamento della parola d'attivazione e l'elaborazione STT)
    - PS3 Eye (funziona senza problemi)
    - Kinect V1 (funziona ma potrebbe essere necessario un aggiornamento del firmware)
- Altoparlanti
    - Altoparlanti USB generici (funzionano senza problemi ma la qualità del suono varia)
- Videocamere
    - Webcam generica (funziona ma non è garantito che funzioni con alcune funzioni della fotocamera)
    - PS3 Eye (uguale alla webcam generica)
    - Kinect V1 (uguale alla webcam generica)
    - [Andrea Electronics C1-1028100-3](https://mycroft-ai.gitbook.io/docs/using-mycroft-ai/get-mycroft/picroft#tested-hardware)

[Risoluzione dei problemi audio - USB](145-troubleshooting_audio.md#USB)

## HDMI

L'audio HDMI dovrebbe funzionare senza problemi se il tuo dispositivo lo supporta.

[Risoluzione dei problemi audio - HDMI](145-troubleshooting_audio.md#HDMI)

## Analogico

Dovrebbe funzionare anche l'uscita analogica per cuffie o altoparlanti esterni ma potrebbe essere necessaria una configurazione su alcuni dispositivi.

[Risoluzione dei problemi audio - Analogico](145-troubleshooting_audio.md#analog)

## HAT di Raspberry Pi

Ci sono diversi HAT disponibili, alcuni con solo un microfono e altri che riproducono anche l'audio. Molti sono supportati e testati, altri dovrebbero funzionare con la configurazione corretta.

### HAT di RPi testati

- Respeaker
    - Schede microfoniche 2/4/6/8 (funzionano in modo nativo con l'immagine Buildroot. Altre necessitano di una relativa configurazione)
- AIY VoiceHat V1 (funziona con la modifica di `/boot/config.txt`)
- AIY VoiceBonnet V2 (funziona con l'aggiornamento del driver personalizzato e con la modifica di `/boot/config.txt`)
- [Risoluzione dei problemi audio - HAT](145-troubleshooting_audio.md#hats)

## Hardware specializzato

Sono supportate anche alcune schede audio speciali.

- Scheda audio SJ201 (scheda audio di Mark 2)

    - Supporto nativo Buildroot
    - Supportata su altri dispositivi con installazione manuale dei driver
    - [Risoluzione dei problemi audio - SJ201](145-troubleshooting_audio.md#sj201)

- Scheda audio personalizzata di Mark 1

    - (Supporto nativo - immagine raspbian-ovos mark1)
    - Supporto di altri dispositivi con la modifica di `/boot.config.txt`
    - [Risoluzione dei problemi audio - Mark 1](145-troubleshooting_audio.md#mk1)

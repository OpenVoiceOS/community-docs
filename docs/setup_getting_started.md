# Welcome To OpenVoice OS Getting Started Guide

### Some information to get you started
We will take you through a series of setup steps to get your device going, Before we get started we would like to help you understand some of the key terms you will see during setup

![Welcome Scree](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/welcome-screen.png)

### Selecting Your Backend

#### What is a backend ?
A backend is a service that provides your device with additional tools to function, these could range from managing your skill settings to configuring certain aspects of your device OpenVoiceOS is all about choice,  We currently supports 3 backend types

![Select Backend](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/select-backend.png)

#### Selene Backend
The mycroft backend connects your device to mycroft servers and allows you to use their web interface to manage your device, this requires paring and all your Speech to text queiries are processed via this backend

#### Personal Backend
The personal backend is a choice for users who would like to self host their own backend on the device or in their personal home network, this backend requires additional setup but also provides a cool web interface to configure your device and manage your settings

#### No Backend
Open Voice OS by default comes with no backend, we do not really believe you need a backend to do anything, this is the best choice for
your device if you wish to run completely locally, we provide you with a whole list of Speech to text and Text to speech online and offline options to choose from, All communication to the outside world happens from your own device without data sharing

## SELENE BACKEND SELECTED ##

The Pairing Process

![Selene](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/selene.png)

The GUI will now show you a Pairing Code, This pairing code needs to be entered on the mycroft backend which you can find online at https://account.mycroft.ai

- Create an account using your email id on https://account.mycroft.ai
- Head over to https://account.mycroft.ai/devices/add
- Enter the pairing code, a unique device name, and location settings
- Click next on the web interface, your device should now be paired

## NO BACKEND SELECTED ##

Select A Text To Speech (TTS) Engine: A text-to-speech (TTS) system converts normal language text into speech, select an engine from the list

![TTS](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/tts.png)

Select A Speech To Text (STT) Engine: A speech-to-text (STT) sustem converts human speech to text, select an engine from the list

![STT](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/stt.png)

## PERSONAL BACKEND SELECTED ##

![Personal Backend](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/personal-backend.png)

Personal backend is a reverse engineered alternative to selene and requires the backend to be hosted locally.

- Install and Configure your personal backend, information available on: https://github.com/OpenVoiceOS/ovos-personal-backend
- The gui on device will display a setup page to enter the host address of your hosted backend on your device
- Pairing with your personal backend happens automatically once you hit the confirm button with the correct host address

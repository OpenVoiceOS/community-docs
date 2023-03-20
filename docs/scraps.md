## from downloading image
  - Buildroot SSH Details: Username: mycroft | password: mycroft
  - Manjaro SSH Details for Respeaker Image: Username: mycroft | password: 12345
  - Manjaro SSH Details for Mark-2/DevKit Image: Username: ovos | password: ovos

- [buildroot](https://drive.google.com/drive/folders/113-zmx6ncoeLNsayseNxoaTlaAk1AfU2)
- [manjaro](http://downloads.openvoiceos.com/images/)


From Backend

## Admin Api (personal backend only!)
Since local backend does not provide a web ui a [admin api](https://github.com/OpenVoiceOS/OVOS-local-backend#admin-api)
can be used to manage your devices

A backend is a service that provides your device with additional tools to function, these could range from managing your skill settings to configuring certain aspects of your device OpenVoiceOS is all about choice,  We currently support 3 backend types

![Select Backend](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/select-backend.png)

### Selene Backend
The mycroft backend connects your device to mycroft servers and allows you to use their web interface to manage your device, this requires paring and all your Speech to text queries are processed via this backend

### Personal Backend
The personal backend is a choice for users who would like to self-host their own backend on the device or in their personal home network, this backend requires additional setup but also provides a cool web interface to configure your device and manage your settings

### No Backend
Open Voice OS by default comes with no backend, we do not really believe you need a backend to do anything, this is the best choice for
your device if you wish to run completely locally, we provide you with a whole list of Speech to text and Text to speech online and offline options to choose from, All communication to the outside world happens from your own device without data sharing

## From First Run

# Setting up your device at first run.

At first run of your OpenVoiceOS device a first run setup wizard is started that guides you through the process of setting up your device.

![Welcome Screen](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/welcome-screen.png)

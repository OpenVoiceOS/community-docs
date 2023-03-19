# Welcome To OpenVoice OS Getting Started User Guide

You can find a pdf version of a getting started guide [here](https://github.com/OpenVoiceOS/ovos_assets/raw/master/printables/device-getting-started-guide.pdf)

### Where to get OVOS?

OVOS is in early stages, we publish our raspberry pi images for download but expect new bugs and new fixes on every release, we are not yet stable!

These images are development images in alpha stage, bugs and incomplete features are guaranteed

Download Images:

- [buildroot](https://drive.google.com/drive/folders/113-zmx6ncoeLNsayseNxoaTlaAk1AfU2)
  - SSH Details: Username: mycroft | password: mycroft
- [manjaro](http://downloads.openvoiceos.com/images/)
  - SSH Details for Respeaker Image: Username: mycroft | password: 12345
  - SSH Details for Mark-2/DevKit Image: Username: ovos | password: ovos
- [raspbian](https://downloads.openvoiceos.com/images/raspbian/)
  - SSH Details: Username: ovos | password: ovos
  - systemd services are `ovos-<service-name>.service`

Build images from scratch:

- [buildroot](https://openvoiceos.github.io/community-docs/buildroot/)
- [manjaro](https://openvoiceos.github.io/community-docs/manjaro/)
- [raspbian](https://openvoiceos.github.io/community-docs/raspbian_ovos/)

### Flashing your image

Flashing your image to your sdcard or USB drive is not different from flashing any other image. For the non-technical users we advise to use the flashing utility from the Raspberry Pi Foundation which you can find [here](https://www.raspberrypi.com/software/).
Under "CHOOSE OS" select custom at the very bottom of the list and browse to the downloaded image file. It is not required to unzip / unpack the image as the Raspberry Pi imager software can do that for you on the fly.
Under "CHOOSE STORAGE" select your sdcard or USB device.

If you have a Raspberry Pi 4 we recommend to use a good USB3.1 device. If you have a Raspberry Pi 3, use a proper sdcard. (From fast to slow: USB3.1 - sdcard - USB2)

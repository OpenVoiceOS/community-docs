# Welcome To OpenVoice OS Getting Started User Guide
# Installing an Image

[Which Image should I choose?] #todo

## Downloading an Image

###Buildroot Latest Images

- [RPi3-64](https://drive.google.com/file/d/1gTrQxMZEOV0J4ZrICyxfjA5cpNIjwDJP/view?usp=share_link)
- [RPi4-64](https://drive.google.com/file/d/1PUtNXfZ5jMUlVAgyN-KXPdVdX6r51eBw/view?usp=share_link)
### Manjaro Latest Images

- [devkit](https://downloads.openvoiceos.com/images/manjaro/ovos-dev-edition-devkit-190822.img.gz) Aug 2022
- [Generic](https://downloads.openvoiceos.com/images/manjaro/ovos-dev-edition-generic-090323-221429.img.xz) Mar 2023
- [Mark 2](https://downloads.openvoiceos.com/images/manjaro/ovos-dev-edition-mark2-170223-091407.img.xz) Feb 2023
- [Respeaker](https://downloads.openvoiceos.com/images/manjaro/ovos-dev-edition-respeaker-090223-172552.img.xz) Feb 2023
### Raspbian Latest Images

- [rpi3-headless](https://downloads.openvoiceos.com/images/raspbian/)

## Default users
- **BuildRoot:** Username: mycroft | password: mycroft
- **Manjaro:** Username: ovos | password: ovos
- **Raspbian:** Username: ovos | password: ovos
### Build images from scratch:

- [buildroot](https://openvoiceos.github.io/community-docs/buildroot/)
- [manjaro](https://openvoiceos.github.io/community-docs/manjaro/)

## Flashing your image

Flashing your image to your sdcard or USB drive is not different from flashing any other image. For the non-technical users we advise to use the flashing utility from the Raspberry Pi Foundation which you can find [here](https://www.raspberrypi.com/software/).
Under "CHOOSE OS" select custom at the very bottom of the list and browse to the downloaded image file. It is not required to unzip / unpack the image as the Raspberry Pi imager software can do that for you on the fly.
Under "CHOOSE STORAGE" select your sdcard or USB device.

If you have a Raspberry Pi 4 we recommend to use a good USB3.1 device. If you have a Raspberry Pi 3, use a proper sdcard. (From fast to slow: USB3.1 - sdcard - USB2)
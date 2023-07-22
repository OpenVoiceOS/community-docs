# OVOS Quick Start Guide - Get an image

So you just want to give OVOS a try?  This quick start will help get an OVOS image installed and running on your Raspberry Pi.

**NOTE** The GUI will not reliably run on a RPi3 and is therefore not recommended for that device.

## Download an OVOS image
OVOS provides a couple of different images specifically for the Raspberry Pi.

### Buildroot Latest Image

The most advanced and featureful is the Buildroot image.  If you want a GUI, this is currently your only choice.

- [RPi4-64](https://drive.google.com/file/d/1PUtNXfZ5jMUlVAgyN-KXPdVdX6r51eBw/view?usp=share_link)

### Raspbian Latest Images

OVOS also provides a "Headless" image that is similar to the origional `picroft` software from `MycroftAI`.  It runs without a screen and works with a RPi3b/b+

- [headless images](https://ovosimages.ziggyai.online/raspbian/development)

## Flashing your image

Once you have an image downloaded, it needs to be flashed to a boot device.

**NOTE** If you have a Raspberry Pi 4 we recommend to use a good USB3.1 device or better, a USB3 SSD. If you have a Raspberry Pi 3, use a proper SD card. (From fast to slow: SSD - USB3.1 - SD card - USB2)

### Decompress the image
Some image writing methods, `dd`, may require your file be decompressed.  Others, BalenaEtcher for example, can use a compressed image.
The Buildroot image is compressed in `.xz` format and the raspbian image is in `.zip` format.

**Windows**

Use `winzip` or `7-zip` to decompress the image.

**Linux**

Use `gunzip` to decompress `.xz` compressed images and `unzip` to decompress `.zip` images.

The resulting file should end in `.img` and is now ready to flash to a device.

### Flashing Software

Flashing your image to your SD card or USB drive is not different from flashing any other image. For the non-technical users we advise to use the flashing utility, [Raspberry Pi Imager](https://www.raspberrypi.com/software/) from the Raspberry Pi Foundation.  It is available for Windows, Mac OS, and Linux.

- Start up the Raspberry Pi Imager.  On Linux, start Raspberry Pi Imager with "**sudo** raspi-imager".
- For "Choose OS", select "Use custom" and select the OVOS/PI image file downloaded from the OpenVoiceOS Downloads Site.
- For "Choose Storage", select your removable boot media, probably something like "Internal SD Card Reader".
- Then select "Write". Do not click the cog. Do not change the username. Username is ovos and is built in. Do not enter WiFi credentials, you will add them at first boot.

Upon completion, you should have a bootable SD card or USB drive.

## Warning EXTREME CARE needs to be taken while using this method

**Be careful with the dd command, you can easily render your computer useless**

- Check where your sd card or usb drive is located using the `lsusb` command.
- It should be visible as `sdxx`
- Write the unzipped image to the disk `sudo dd if=<path-to-unzipped-image> of=<path-to-sd-card> bs=4M status=progress`

No matter what method you used, upon completion, you should have a bootable SD card or USB drive.

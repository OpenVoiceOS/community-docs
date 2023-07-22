# Installing OVOS using a prebuilt image

## Prebuilt images
OVOS provides a couple of prebuilt images to use with a Raspberry Pi

### Buildroot
This is the most advanced image that OVOS provides and is intended to be used as a complete system with a GUI.  This image has auto-detection of a large amount of hardware, including but not limited to respeaker microphones, and the sj201 sound board that is used by the Mark2.

Buildroot images are avaliable for download [here](https://drive.google.com/drive/folders/113-zmx6ncoeLNsayseNxoaTlaAk1AfU2).  Decompress this file and continue to the next section [Burning the image to a SD card or USB drive](#burning_an_image)

### Raspbian-ovos
This is a new image created as a headless device.  This is supposed to be optimized to run on less powerful devices such as a RPi3 which does not have the power to run a GUI.  This image is still in heavy development and expect some bugs while using.

Raspbian-ovos images are avaliable for download [here](https://ovosimages.ziggyai.online/raspbian/).  Unzip this file and continue to the next section [Burning the image to a SD card or USB drive](#burning_an_image)

## Burning an image

There are a few ways to burn your image to a drive to use in a Raspberry PI.  Both methods described below will work for either OVOS image that you would like to try.

### Raspberry PI Imager

This method can be used with a Linux or Windows host machine.

The people at raspberry pi provide a great little program made for burning an image to a device.  You can get it [here](https://www.raspberrypi.com/software/).  The team at OVOS has tried to make the setup as simple as possible, and if you follow the steps below, you should have no problems on your first boot.

- Start up the Raspberry Pi Imager.  On Linux, start Raspberry Pi Imager with `sudo raspi-imager`.
- For "Choose OS", select "Use custom" and select the OVOS image file downloaded from the step above.
- For "Choose Storage", select your removable boot media, probably something like "Internal SD Card Reader".
- Then select "Write". Do not click the cog. Do not change the username. Username is ovos and is built in. Do not enter WiFi credentials, you will add them at first boot.

### Linux dd command

**Be careful with the dd command, you can easily render your computer useless if the command is entered wrong**

- Find the location of your boot medium with the `lsblk` command.
  - It should show up as something like `sdb`.  If you are unsure what drive it is, remove it, and run the command again.  The one that is missing, is the drive you want to use.
- Write the image to the disk with the `dd` command.

**WARNING: Please make sure you are writing to the correct location, as this is the step that can screw everything up**

  - `sudo dd if=<path_to_unzipped_image> of=<path_to_boot_medium> bs=4M status=progress`
  - This step will take several minutes to complete.
- When the command is done, and the prompt apears again, finish the process with the command `sudo sync`

With either method used, you should now have a bootable disk to use with your Raspberry PI


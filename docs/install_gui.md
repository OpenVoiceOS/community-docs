# Installing OVOS-GUI
The GUI is a totaly optional component of OVOS, but adds a ton more functionality to the device.  Some skills will not work without one.

## About the GUI
The OVOS GUI is an independent component of OVOS which uses QT5/6 to display information on your devices screen.  It is touchscreen compliant [1](#Footnotes#1), and has an on-screen keyboard for entering data.  On a Raspberry Pi, the GUI runs in a framebuffer, therefore not needing a full window manager.  This saves resources on underpowered devices.

[mycroft-gui-qt5](https://github.com/OpenVoiceOS/mycroft-gui-qt5) is a fork of the original [mycroft-gui](https://github.com/MycroftAI/mycroft-gui)

[mycroft-gui-qt6](https://github.com/OpenVoiceOS/mycroft-gui-qt6) is in the works, but not all skills support it yet.

## Installing the GUI

The GUI software comes with a nice script which will install the needed packages for you.

To get the software we will use `git` and the `dev_setup.sh` script that is provided.

```
cd ~
git clone https://github.com/OpenVoiceOS/mycroft-gui-qt5
cd mycroft-gui-qt5
bash dev_setup.sh
```

**NOTE** The mycroft-gui is NOT a python script, therefore will not run in the venv created for the rest of the software stack.

## That's it !!
That is all it takes to install the GUI for OVOS.  Invoke the GUI with the command:

`ovos-gui-app`

You can refer to the [README](https://github.com/OpenVoiceOS/mycroft-gui-qt5/blob/dev/README.md) in the mycroft-gui-qt5 repository for more information

[Starting the GUI](starting_modules.md#gui)

### Footnotes

#### 1
It has been my experience that while the touchscreen will work with OVOS, some have the touch matrix opposite of what the screen is displayed.  With one of these screens, it is still possible to use it, but you will need a full window manager installed instead of the GUI running in a framebuffer.

# Troubleshooting OpenVoiceOS Installation
**coming soon**

## Architecture

## Troubleshooting Commands

### Gather Data

## Problem/Fix
### Install fails to create OVOS wifi hotspot 
There is a known issue with balena (the wifi access point app) when it detects a WPA3 network of any sort, it fails.
[More Information](https://github.com/balena-os/wifi-connect/issues/416)

### Raspbian OVOS stuck on "Generating SSH keys..."
Not sure what is causing this, but if you reboot the pi (ctrl-alt-del) it will come up fine on the second boot.
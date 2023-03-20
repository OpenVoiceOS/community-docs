# Troubleshooting operating system audio
If audio isn't working for OpenVoiceOS, it's useful to verify that the operating system audio is working.

## Architecture
### ALSA
ALSA is the kernel level sound mixer, it manages your sound card directly. ALSA is crap (seriously) and it can handle a few (sometimes just one) channel. We don't generally have to deal with ALSA directly.

ALSA can be configured to use PulseAudio as it's default device, that way ALSA applications that are not PulseAudio aware will still use PulseAudio via an indirection layer.

### Pulse Audio
PulseAudio is a software mixer, running in user space. When it runs, it uses Alsa's channel and manages everything. mixing, devices, network devices, etc.

PulseAudio always uses ALSA as backend, and on startup opens all ALSA devices. Since most ALSA devices can't be opened multiple times, this will cause all ALSA applications that try to use an ALSA device directly when PulseAudio is running to fail.  If you have a legacy application that for some reason doesn't work, you can use `pasuspender` to temporary suspend PulseAudio to run this particular application.

[Pulse Audio Modules](https://www.freedesktop.org/wiki/Software/PulseAudio/Documentation/User/Modules/)
## Troubleshooting Commands
List hardware cards `cat /proc/asound/cards`
List Playback and capture devices visible to ALSA (note the Card Number)
```
aplay -l
arecord -l
```
This will list the cards, which can then be referenced in arecord using -D hw:<card number>,0:
```
arecord -f dat -r 16000 -D hw:4,0 -c 4 -d 10 test2.wav
```
You can then play the file back to test your speakers
``` 
aplay -D hw:2,0 test2.wav
```
** If PulseAudio is installed, Alsa should be configured to use PulseAudio as it's default, and we don't change anything in Alsa, we configure our default sources and sinks in Pulse Audio**

Verify that pulseaudio is installed
```
apt list pulseaudio
```
Verify that Alsa is using Pulse Audio as the default
``` 
$ aplay -L | head -n9
null
    Discard all samples (playback) or generate zero samples (capture)
default
    Playback/recording through the PulseAudio sound server
```
### PulseAudio
List sinks (speakers) and sources (microphones) visible to PulseAudio
```
pactl list sinks
pactl list sources
```
This will list the sources that can be used to set the default source for pulseaudio below.
```
pacmd set-default-source
```
e.g.
```
pacmd set-default-source alsa_input.usb-OmniVision_Technologies__Inc._USB_Camera-B4.09.24.1-01.multichannel-input
```
### Test if OVOS is receiving mic input
You can test if OVOS is recieving mic input using the `ovos-cli-client`

Install the ovos-cli-client from github to ensure you have the latest version
```
cd ~
git clone https://github.com/openvoiceos/ovos-cli-client
pip install ./ovos-cli-client
```
Run the ovos-cli-client
``` 
ovos-cli-client
```
In the lower left you can observe the microphone levels, when you talk, the levels should increase.  If they don't ovos is probably using the wrong microphone.
### Gather Data
Before submitting an issue or asking a question on Element, please gather the following data.

For Microphone issues:
``` 
arecord -l
arecord -L | head -n9
pactl list sources
pacmd dump
```
For Speaker issues:
``` 
aplay -l
aplay -L | head -n9
pactl list sinks
pacmd dump
```
## Additional Resources
- [PulseAudio Troubleshooting](https://wiki.archlinux.org/title/PulseAudio/Troubleshooting)

## Problem/fix
##### ERROR: pulseaudio sink always suspended
Try disabling suspend-on-idle in /etc/pulse/default.pa

Change this:
```
### Automatically suspend sinks/sources that become idle for too long
load-module module-suspend-on-idle
```
to this:
```
### Automatically suspend sinks/sources that become idle for too long
#load-module module-suspend-on-idle
```
and then restart PulseAudio. There is quite a lot of variation in how people do this but killall pulseaudio is one option (it gets automatically started again).  If you want to be sure, you can restart the system.
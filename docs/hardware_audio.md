# Audio Hardware

Recommendations and notes on speakers and microphones

Most audio devices are avaliable to use with the help of Plugins and should for the most part work by default.

If your device does not work, pop in to our [matrix support channel](https://app.element.io/#/room/#openvoiceos-support:matrix.org), please create an [issue](https://github.com/OpenVoiceOS/ovos-dinkum-listener/issues) or start a [discussion](https://github.com/orgs/OpenVoiceOS/discussions) about your device.

## USB
Most USB devices should work without any issues.  But, not all devices are created equally.

#### Tested USB devices
- Microphones
  - BlueSnowball (Works well without issues)
  - Generic webcam with mic (Works, but sound quality can be lacking.  Makes wakeword detection and STT processing less accurate)
  - PS3 Eye (Works without issue)
  - Kinect V1 (Works, but may need a firmware upgrade)
- Speakers
  - Generic USB Speakers (Works without issue, but sound quality varies)
- Cameras
  - Generic webcam (Works, but is not guarenteed to work with some camera skills)
  - PS3 Eye (Same as Generic webcam)
  - Kinect V1 (Same as Generic webcam)

[Audio Troubleshooting - USB](troubleshooting_audio.md#USB)

## HDMI
HDMI audio should work without issues if your device supports it.

[Audio Troubleshooting - HDMI](troubleshooting_audio.md#HDMI)

## Analog
Analog output to headphones, or external speakers should work also.  There may be some configuration needed on some devices.

[Audio Troubleshooting - Analog](troubleshooting_audio.md#analog)

## Raspberry Pi HAT's
There are several HAT's that are avaliable, some with just a microphone, others that play audio out also.  Several are supported and tested, others should work with the proper configuration.

### Tested RPi HAT's
- Respeaker
  - 2/4/6/8 mic boards (Works native with Buildroot image.  Others needs configuration)
- AIY VoiceHat V1 (Works with `/boot/config.txt` modification)
- AIY VoiceBonnet V2 (Works with custom driver update and `/boot/config.txt` modification)

[Audio Troubleshooting - HATs](troubleshooting_audio.md#hats)

## Specialty Hardware
Some special sound boards are also supported.

- SJ201 sound board (Mark 2 sound board)
  - Buildroot Native support
  - Supported on other devices with manual install of drivers

[Audio Troubleshooting - SJ201](troubleshooting_audio.md#sj201)

- Mark 1 custom sound board
  - (Native support - raspbian-ovos mark1 image)
  - Other device support with `/boot.config.txt` modification

[Audio Troubleshooting - Mark 1](troubleshooting_audio.md#mk1)

## Introduction:
OpenVoiceOS GUI supports various Skills and PHAL plugins that share a voice application interface with Plasma Bigscreen. In order to enable key navigation on Plasma Bigscreen and Media Centers, the user needs to export an environment variable.

## Exporting the Environment Variable:
In order to enable key navigation on Plasma Bigscreen and Media Centers, the user needs to export the environment variable `QT_FILE_SELECTORS=mediacenter`. This can be done by executing the following command in the terminal:

```
export QT_FILE_SELECTORS=mediacenter
```

This environment variable by default is enabled and added to the Plasma Bigscreen environment. To create your own media center environment store the variable in /etc/environment or /etc/profile.d/99-ovos-media-center.sh

Exporting the environment variable `QT_FILE_SELECTORS=mediacenter` is a necessary step to enable key navigation on Plasma Bigscreen and Media Centers for the Open Voice OS project GUI. With this in place, the user can enjoy seamless key navigation while using the Skills and PHAL plugins on their Plasma Bigscreen and Media Centers.

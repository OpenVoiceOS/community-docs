# Backend Services

ovos-core supports multiple backends under a single unified interface

- Personal backend - [self hosted](https://github.com/OpenVoiceOS/OVOS-local-backend)
- Selene - https://api.mycroft.ai
- OpenVoiceOS API Service - https://api.openvoiceos.com
- Offline - support for setting your own api keys and query services directly

Developers do not need to worry about backend details in their applications and skills

* [Overview](#backend-overview)
* [STT](#stt)
* [Admin Api (personal backend only!)](#admin-api--personal-backend-only--)


## Overview

| API       | Offline | Personal | Selene | OVOS    | 
|-----------|---------|----------|--------|---------|
| Admin     | yes [1] | yes      | no     | no      | 
| Device    | yes [2] | yes      | yes    | yes [4] | 
| Metrics   | yes [2] | yes      | yes    | yes [4] | 
| Dataset   | yes [2] | yes      | yes    | yes [4] | 
| OAuth     | yes [2] | yes      | yes    | yes [4] |
| Wolfram   | yes [3] | yes      | yes    | yes     | 
| Geolocate | yes     | yes      | yes    | yes     |
| STT       | yes [3] | yes      | yes    | yes     | 
| Weather   | yes [3] | yes      | yes    | yes     | 
| Email     | yes [3] | yes      | yes    | yes     |

    [1] will update user level mycroft.conf
    [2] shared json database with ovos-config-assistant and ovos-backend-manager
    [3] needs additional configuration (eg. credentials)
    [4] uses offline_backend functionality

## Backend Manager

A web UI is provided to manage a personal backend instance

![](https://github.com/OpenVoiceOS/ovos-backend-manager/raw/dev/screenshots/demo.gif)

source code: https://github.com/OpenVoiceOS/ovos-backend-manager

## STT

a companion stt plugin is available - [ovos-stt-plugin-selene](https://github.com/OpenVoiceOS/ovos-stt-plugin-selene)

## Admin Api (personal backend only!)

personal backend provides a [admin api](https://github.com/OpenVoiceOS/OVOS-local-backend#admin-api) that can be used to manage your devices

```python
from ovos_backend_client.api import AdminApi

admin = AdminApi("secret_admin_key")
uuid = "..."  # check identity2.json in the device you want to manage

# manually pair a device
identity_json = admin.pair(uuid)

# set device info
info = {"opt_in": True,
        "name": "my_device",
        "device_location": "kitchen",
        "email": "notifications@me.com",
        "isolated_skills": False,
        "lang": "en-us"}
admin.set_device_info(uuid, info)

# set device preferences
prefs = {"time_format": "full",
         "date_format": "DMY",
         "system_unit": "metric",
         "lang": "en-us",
         "wake_word": "hey_mycroft",
         "ww_config": {"phonemes": "HH EY . M AY K R AO F T",
                       "module": "ovos-ww-plugin-pocketsphinx",
                       "threshold": 1e-90},
         "tts_module": "ovos-tts-plugin-mimic",
         "tts_config": {"voice": "ap"}}
admin.set_device_prefs(uuid, prefs)

# set location data
loc = {
    "city": {
        "code": "Lawrence",
        "name": "Lawrence",
        "state": {
            "code": "KS",
            "name": "Kansas",
            "country": {
                "code": "US",
                "name": "United States"
            }
        }
    },
    "coordinate": {
        "latitude": 38.971669,
        "longitude": -95.23525
    },
    "timezone": {
        "code": "America/Chicago",
        "name": "Central Standard Time",
        "dstOffset": 3600000,
        "offset": -21600000
    }
}
admin.set_device_location(uuid, loc)
```


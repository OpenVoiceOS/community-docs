# Backend Services

* [Supported Backends](#supported-backends)
* [STT Plugin](#stt-plugin)
* [Selene](#selene)
* [Offline](#offline)
* [Personal Backend](#personal-backend)
    + [Backend Manager](#backend-manager)
    + [Admin Api](#admin-api)
* [OVOS API Service](#ovos-api-service)

## Supported Backends

ovos-core supports multiple backends under a single unified interface

- Personal backend - [self hosted](https://github.com/OpenVoiceOS/OVOS-local-backend)
- Selene - https://api.mycroft.ai
- OpenVoiceOS API Service - https://api.openvoiceos.com
- Offline - support for setting your own api keys and query services directly

Developers do not need to worry about backend details in their applications and skills

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

## STT Plugin

a companion stt plugin is available to use a backend as remote STT provider

`pip install ovos-stt-plugin-selene`

edit your configuration to use it

```json
  "stt": {
"module": "ovos-stt-plugin-selene"
}

```

[source code](https://github.com/OpenVoiceOS/ovos-stt-plugin-selene)

## Selene

The official mycroft home backend is called selene, users need to create an account and pair devices with the mycroft
servers. 

This backend is not considered optional by MycroftAI but is not used by OVOS unless explicitly enabled

Selene is AGPL licensed:
- [backend source code](https://github.com/MycroftAI/selene-backend)
- [frontend source code](https://github.com/MycroftAI/selene-ui)

## Offline

OVOS by default runs without a backend, in this case you will need to configure api keys manually

This can be done with [OCA](https://github.com/OpenVoiceOS/ovos-config-assistant) or by editing mycroft.conf

## Personal Backend

Personal backend is a reverse engineered alternative to selene that predates it

It provides the same functionality for devices and packs some extra options

It is not intended to serve different users or thousands of devices, there are no user accounts!

This is currently the only way to run a vanilla mycroft-core device offline

[source code](https://github.com/OpenVoiceOS/ovos-personal-backend)

### Backend Manager

A web UI is provided to manage a personal backend instance

![](https://github.com/OpenVoiceOS/ovos-backend-manager/raw/dev/screenshots/demo.gif)

[source code](https://github.com/OpenVoiceOS/ovos-backend-manager)

### Admin Api

personal backend provides a [admin api](https://github.com/OpenVoiceOS/OVOS-local-backend#admin-api) that can be used to
manage your devices

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

## OVOS API Service

OVOS Api Service is not a full backend, it is a set of free proxy services hosted by the OVOS Team for usage in default
skills

device management functionality and user accounts do not exist, offline mode will be used for these apis

[source code](https://github.com/OpenVoiceOS/ovos_api_service)

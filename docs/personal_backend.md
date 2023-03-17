# OVOS Personal Backend

Personal mycroft backend alternative to mycroft.home, written in flask

This repo is an alternative to the backend meant for personal usage, this allows you to run without mycroft servers

:warning: there are no user accounts :warning:

This is NOT meant to provision third party devices, but rather to run on the mycroft devices directly or on a private network

For a full backend experience, the official mycroft backend has been open sourced, read the [blog post](https://mycroft.ai/blog/open-sourcing-the-mycroft-backend/)

NOTE: There is no pairing, devices will just activate themselves and work

## Install

from pip

```bash
pip install ovos-local-backend
```

### Mycroft Setup

There are 2 main intended ways to run local backend with mycroft

- on same device as mycroft-core, tricking it to run without mycroft servers
- on a private network, to manage all your devices locally

NOTE: you can not fully run mycroft-core offline, it refuses to launch without internet connection, you can only replace the calls to use this backend instead of mycroft.home

We recommend you use [ovos-core](https://github.com/OpenVoiceOS/ovos-core) instead

update your mycroft config to use this backend, delete `identity2.json` and restart mycroft

```json
{
  "server": {
    "url": "http://0.0.0.0:6712",
    "version": "v1",
    "update": true,
    "metrics": true
  },
  "listener": {
    "wake_word_upload": {
      "url": "http://0.0.0.0:6712/precise/upload"
    }
  }
}
```


## Companion projects

- [ovos-backend-client](https://github.com/OpenVoiceOS/ovos-backend-client) - reference python library to interact with selene/local backend
- [ovos-backend-manager](https://github.com/OpenVoiceOS/ovos-backend-manager) - graphical interface to manage all things backend
- [ovos-stt-plugin-selene](https://github.com/OpenVoiceOS/ovos-stt-plugin-selene) - stt plugin for selene/local backend

## Usage

start backend

```bash
$ ovos-local-backend -h
usage: ovos-local-backend [-h] [--flask-port FLASK_PORT] [--flask-host FLASK_HOST]

optional arguments:
  -h, --help            show this help message and exit
  --flask-port FLASK_PORT
                        Mock backend port number
  --flask-host FLASK_HOST
                        Mock backend host

```


## Docker

There is also a docker container you can use

```bash
docker run -p 8086:6712 -d --restart always --name local_backend ghcr.io/openvoiceos/local-backend:dev
```

a `docker-compose.yml` could look like this
```yaml
version: '3.6'
services:
    # ...
    ovosbackend:
        container_name: ovos_backend
        image: ghcr.io/openvoiceos/local-backend:dev
        # or build from local source (relative to docker-compose.yml)
        # build: ../ovos/ovos-personal-backend/.
        restart: unless-stopped
        ports:
          - "6712:6712"                                              # default port backend API
          - "36535:36535"                                            # default port backend-manager
        volumes:                                                     # <host>:<guest>:<SELinux flag>
          - ./ovos/backend/config:/root/.config/json_database:z      # shared config directory
          - ./ovos/backend/data:/root/.local/share/ovos_backend:Z    # shared data directory
                                                                     # set `data_path` to `/root/.local/share/ovos_backend`
```
about [selinux flags](https://docs.docker.com/storage/bind-mounts/#configure-the-selinux-label) (omit if you don't deal with selinux)

## How it works

### Configuration

configure backend by editing/creating ```~/.config/json_database/ovos_backend.json```

see default values [here](https://github.com/OpenVoiceOS/ovos-personal-backend/blob/dev/ovos_local_backend/configuration.py)

```json
{
  "stt": {
    "module": "ovos-stt-plugin-server",
    "ovos-stt-plugin-server": {"url": "https://stt.openvoiceos.com/stt"}
  },
  "backend_port": 6712,
  "geolocate": true,
  "override_location": false,
  "api_version": "v1",
  "data_path": "~",
  "record_utterances": false,
  "record_wakewords": false,
  "wolfram_key": "$KEY",
  "owm_key": "$KEY",
  "lang": "en-us",
  "date_format": "DMY",
  "system_unit": "metric",
  "time_format": "full",
  "default_location": {
    "city": {"...": "..."},
    "coordinate": {"...": "..."},
    "timezone": {"...": "..."}
  }
}
```

- stt config follows the same format of mycroft.conf and
  uses [ovos-plugin-manager](https://github.com/OpenVoiceOS/OVOS-plugin-manager)
- set wolfram alpha key for wolfram alpha proxy expected by official mycroft skill
- set open weather map key for weather proxy expected by official mycroft skill
- if record_wakewords is set, recordings can be found at `DATA_PATH/wakewords`
- if record_utterances is set, recordings can be found at `DATA_PATH/utterances`

### Databases

Since the local backend is not meant to provision hundreds of devices or manage user accounts it works only with [json databases](https://github.com/OpenJarbas/json_database)

- metadata about uploaded wakewords can be found at `~/.local/share/json_database/ovos_wakewords.jsondb`
- metadata about uploaded utterances can be found at `~/.local/share/json_database/ovos_utterances.jsondb`
- database of uploaded metrics can be found at `~/.local/share/json_database/ovos_metrics.jsondb`
- paired devices database can be found at `~/.local/share/json_database/ovos_devices.json`
- per device skill settings database can be found at `~/.local/share/json_database/ovos_skill_settings.json`
- shared skill settings database can be found at `~/.local/share/json_database/ovos_shared_skill_settings.json`

metrics, wake words and utterances respect the individual devices `opt_in` flag, nothing will be saved unless devices opt_in (default True)

### Device Settings

Each paired device has a few settings that control behaviour backend side

- `name` - default `"Device-{uuid}"`, friendly device name for display
- `opt_in` - default `True`, flag to control if metrics and speech from this device will be saved
- `device_location` - default `"unknown"`, friendly name for indoor location
- `email` - default from backend config, email to send notifications to
- `isolated_skills` - default `False`, flag to control if skill settings are shared across devices (ovos only)

In selene this info would be populated during pairing process, in local backend it needs to be updated manually

- you can change these settings per device via the admin api (./ovos_local_backend/backend/admin.py)
- you can also change these settings per device by manually editing paired devices database

### Location

Device location can be updated via the backend, mycroft-core will request this info on its own from time to time

default values comes from the local backend config file
```json
{
  "geolocate": true,
  "override_location": false,
  "default_location": {
    "city": {"...": "..."},
    "coordinate": {"...": "..."},
    "timezone": {"...": "..."}
  }
}
```

- if override location is True, then location will be set to configured default value
- if geolocate is True then location will be set from your ip address
- you can set a default location per device via the admin api
- you can also set a default location per device by manually editing paired devices database

### Device Preferences

Some settings can be updated via the backend, mycroft-core will request this info on its own from time to time

default values comes from the local backend config file
```json
{
  "lang": "en-us",
  "date_format": "DMY",
  "system_unit": "metric",
  "time_format": "full"
}
```

- these settings are also used for wolfram alpha / weather default values
- you can set these values per device via the admin api (./ovos_local_backend/backend/admin.py)
- you can also set these values per device by manually editing paired devices database

### Skill settings

in selene all device share skill settings, with local backend you can control this per device via `isolated_skills` flag

"old selene" supported a single endpoint for both skill settings and settings meta, this allowed devices both to download and upload settings

"new selene" split this into two endpoints, settingsMeta (upload only) and settings (download only), this disabled two-way sync across devices

- you can set `isolated_skills` per device via the admin api (./ovos_local_backend/backend/admin.py)
- you can also set `isolated_skills` per device by manually editing paired devices database
- both endpoints are available, but mycroft-core by default will use the new endpoints and does not support two-way sync
- you can edit settings by using the "old selene" endpoint
- you can also edit settings by manually editing settings database

### Email

Mycroft skills can request the backend to send an email to the account used for pairing the device

- Email will be sent to a pre-defined recipient email since there are no user accounts
- you can set a recipient email per device via the admin api (./ovos_local_backend/backend/admin.py)
- you can set a recipient email per device by manually editing paired devices database

with the local backend you need to configure your own SMTP server and recipient email, add the following section to your .conf

```json
{
  "email": {
    "smtp": {
      "username": "sender@gmail.com",
      "password": "123456",
      "host": "",
      "port": 465
    },
    "recipient": "receiver@gmail.com"
  }
}
```

If using gmail you will need to [enable less secure apps](https://hotter.io/docs/email-accounts/secure-app-gmail/)

### Selene Proxy

You can integrate local backend with selene, the backend will show up as a device you can manage in mycroft.home

wait... what? isn't the point of local backend to disable selene?

- Open Dataset, You do not want to use selene, but you want to opt_in to the open dataset (share recordings with mycroft)
- Privacy, you want to use selene, but you do not want to give away your personal data (email, location, ip address...)
- Control, you want to use only a subset of selene features
- Convenience, pair once, manage all your devices
- Functionality, extra features such as isolated skill settings and forced 2 way sync
- Esoteric Setups, isolated mycroft services that can not share an identity file, such as [ovos-qubes](https://github.com/OpenVoiceOS/ovos-qubes)

#### Pairing

To pair the local backend with selene you have 2 options

1 - pair a mycroft-core instance, then copy the identity file

2 - enable proxy_pairing, whenever a device pairs with local backend the code it speaks is also valid for selene, use that code to pair local backend with selene

If a device tries to use a selene enabled endpoint without the backend being paired a 401 authentication error will be returned, if the endpoint does not use selene (e.g. disabled in config) this check is skipped
#### Selene Config

In your backend config add the following section

```python
    "selene": {
        "enabled": False,  # needs to be explicitly enabled by user
        "url": "https://api.mycroft.ai",  # change if you are self-hosting selene
        "version": "v1",
        # pairing settings
        # NOTE: the file should be used exclusively by backend, do not share with a mycroft-core instance
        "identity_file": BACKEND_IDENTITY,  # path to identity2.json file
        # send the pairing from selene to any device that attempts to pair with local backend
        # this will provide voice/gui prompts to the user and avoid the need to copy an identity file
        # only happens if backend is not paired with selene (hopefully exactly once)
        # if False you need to pair an existing mycroft-core as usual and move the file for backend usage
        "proxy_pairing": False,
        
        # micro service settings
        # NOTE: STT is handled at plugin level, configure ovos-stt-plugin-selene
        "proxy_weather": True,  # use selene for weather api calls
        "proxy_wolfram": True,  # use selene for wolfram alpha api calls
        "proxy_geolocation": True,  # use selene for geolocation api calls
        "proxy_email": False,  # use selene for sending email (only for email registered in selene)
        
        # device settings - if you want to spoof data in selene set these to False
        "download_location": True,  # set default location from selene
        "download_prefs": True,  # set default device preferences from selene
        "download_settings": True,  # download shared skill settings from selene
        "upload_settings": True,  # upload shared skill settings to selene
        "force2way": False,  # this forcefully re-enables 2way settings sync with selene
        # this functionality was removed from core, we hijack the settingsmeta endpoint to upload settings
        # upload will happen when mycroft-core boots and overwrite any values in selene (no checks for settings changed)
        # the assumption is that selene changes are downloaded instantaneously
        # if a device is offline when selene changes those changes will be discarded on next device boot
        
        # opt-in settings - what data to share with selene
        # NOTE: these also depend on opt_in being set in selene
        "opt_in": False,  # share data from all devices with selene (as if from a single device)
        "opt_in_blacklist": [],  # list of uuids that should ignore opt_in flag (never share data)
        "upload_metrics": True,  # upload device metrics to selene
        "upload_wakewords": True,  # upload wake word samples to selene
        "upload_utterances": True  # upload utterance samples to selene
    }
```

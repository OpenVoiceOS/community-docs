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
**WIP Coming Soon**

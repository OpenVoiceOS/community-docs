## Audio Service

The audio service is responsible for loading TTS and Audio plugins

All audio playback is handled by this service


### Native playback

Usually playback is triggered by some originating bus message, eg `"recognizer_loop:utterance"`, this message contains metadata that is used to determine if playback should happen.

`message.context` may contain a source and destination, playback is only triggered if a message destination is a native_source or if missing (considered a broadcast). 

This separation of native sources allows remote clients such as an android app to interact with OVOS without the actual device where ovos-core is running repeating all TTS and music playback out loud

You can learn more about message targeting [here](https://jarbashivemind.github.io/HiveMind-community-docs/mycroft/)

By default, only utterances originating from the speech client and ovos cli are considered native

for legacy reasons the names for ovos cli and speech client are `"debug_cli"` and `"audio"` respectively


### TTS

Two TTS plugins may be loaded at once, if the primary plugin fails for some reason the second plugin will be used. 

This allows you to have a lower quality offline voice as fallback to account for internet outages, this ensures your device can always give you feedback

```javascript
"tts": {
    "pulse_duck": false,
    "module": "ovos-tts-plugin-mimic2",
    "fallback_module": "ovos-tts-plugin-mimic"
},
```


### Audio

You can enable additional Audio plugins and define the native sources described above under the `"Audio"` section of `mycroft.conf`

ovos-core uses OCP natively for media playback, you can learn more about OCP [here](https://openvoiceos.github.io/community-docs/OCP)

OCP will decide when to call the Audio service and what plugin to use, the main use case is for headless setups without a GUI

NOTE: mycroft-core has a `"default-backend"` config option, in ovos-core this option has been deprecated and is always OCP.

```javascript
"Audio": {
    "native_sources": ["debug_cli", "audio"],

    "backends": {
      "OCP": {
        "type": "ovos_common_play",
        "active": true
      },
      "simple": {
        "type": "ovos_audio_simple",
        "active": true
      },
      "vlc": {
        "type": "ovos_vlc",
        "active": true
      }
    }
},
```

# Configuration

- [Reading Configuration](#reading-configuration)
- [Configuring Configuration](#configuring-configuration)
    * [protected_keys](#protected-keys)
    * [disable_user_config](#disable-user-config)
    * [disable_remote_config](#disable-remote-config)
- [Meta Configuration](#meta-configuration)
    * [ovos.conf](#ovosconf)

## Reading Configuration

`ovos_config.config.Configuration` is a singleton that loads a single config
object. The configuration files loaded are determined by `ovos.conf` as described below and can be in either json or
yaml format.

if `Configuration()` is called the following configs would be loaded in this
order:

- `{core-path}`/configuration/mycroft.conf
- `os.environ.get('MYCROFT_SYSTEM_CONFIG')` or /etc/mycroft/mycroft.conf
- `os.environ.get('MYCROFT_WEB_CACHE')` or `XDG_CONFIG_PATH`/neon/web_cache.json
- ~/.mycroft/mycroft.conf (Deprecated)
- `XDG_CONFIG_DIRS` + /mycroft/mycroft.conf
- /etc/xdg/mycroft/mycroft.conf
- `XDG_CONFIG_HOME` (default ~/.config) + /mycroft/mycroft.conf

When the configuration loader starts, it looks in these locations in this order, and loads ALL configurations. Keys that
exist in multiple configuration files will be overridden by the last file to contain the value. This process results in
a minimal amount being written for a specific device and user, without modifying default distribution files.

## Configuring Configuration

There are a couple of special configuration keys that change the way the configuration stack loads.

* `Default` config refers to the config specified at `default_config_path` in
  `ovos.conf` (#1 `{core-path}/configuration/mycroft.conf` in the stack above).
* `System` config refers to the config at `/etc/{base_folder}/{config_filename}` (#2 `/etc/mycroft/mycroft.conf` in the stack
  above).

### protected_keys

A `"protected_keys"` configuration section may be added to a `Default` or `System` Config file
(default `/etc/mycroft/mycroft.conf`). This configuration section specifies
other configuration keys that may not be specified in `remote` or `user` configurations.
Keys may specify nested parameters with `.` to exclude specific keys within nested dictionaries.
An example config could be:

```json
{
  "protected_keys": {
    "remote": [
      "gui_websocket.host",
      "websocket.host"
    ],
    "user": [
      "gui_websocket.host"
    ]
  }
}
```

This example specifies that `config['gui_websocket']['host']` may be specified in user configuration, but not remote.
`config['websocket']['host']` may not be specified in user or remote config, so it will only consider default
and system configurations.

### disable_user_config

If this config parameter is set to True in `Default` or `System` configuration,
no user configurations will be loaded (no XDG configuration paths).

### disable_remote_config

If this config parameter is set to True in `Default` or `System` configuration,
the remote configuration (`web_cache.json`) will not be loaded.


## Meta Configuration

while `mycroft.conf` configures the voice assistant, `ovos.conf` configures the library

what this means is that `ovos.conf` decides what files are loaded by the `Configuration` class described above, as an end user or skill developer you should never have to worry about this

all XDG paths across OpenVoiceOS packages build their paths taking `ovos.conf` into consideration

this feature is what allows downstream voice assistants such as neon-core to change their config files to `neon.yaml`

Using the above example, if `Configuration()` is called from `neon-core`, the following configs would be loaded in this
order:

- `{core-path}`/configuration/neon.yaml
- `os.environ.get('MYCROFT_SYSTEM_CONFIG')` or /etc/neon/neon.yaml
- `os.environ.get('MYCROFT_WEB_CACHE')` or `XDG_CONFIG_PATH`/neon/web_cache.json
- ~/.neon/neon.yaml (Deprecated)
- `XDG_CONFIG_DIRS` + /neon/neon.yaml
- /etc/xdg/neon/neon.yaml
- `XDG_CONFIG_HOME` (default ~/.config) + /neon/neon.yaml


### ovos.conf

The `ovos_config` package determines which config files to load based on `ovos.conf`.
`get_ovos_config` will return default values that load `mycroft.conf` unless otherwise configured.

`ovos.conf` files are loaded in the following order, with later files taking priority over earlier ones in the list:

- /etc/OpenVoiceOS/ovos.conf
- /etc/mycroft/ovos.conf (Deprecated)
- `XDG_CONFIG_DIRS` + /OpenVoiceOS/ovos.conf
- /etc/xdg/OpenVoiceOS/ovos.conf
- `XDG_CONFIG_HOME` (default ~/.config) + /OpenVoiceOS/ovos.conf

A simple `ovos_config` should have a structure like:

```json
{
  "base_folder": "mycroft",
  "config_filename": "mycroft.conf",
  "default_config_path": "<Absolute Path to Installed Core>/configuration/mycroft.conf",
  "module_overrides": {},
  "submodule_mappings": {}
}
```

> *Note*: `default_config_path` should always be an absolute path. This is generally
> detected automatically, but any manual override must specify an absolute path to a json or yaml config file.

Non-Mycroft modules may specify alternate config paths. A call to `get_ovos_config` from
`neon_core` or `neon_messagebus` will return a configuration like:

```json
{
  "base_folder": "neon",
  "config_filename": "neon.yaml",
  "default_config_path": "/etc/example/config/neon.yaml",
  "module_overrides": {
    "neon_core": {
      "base_folder": "neon",
      "config_filename": "neon.yaml",
      "default_config_path": "/etc/example/config/neon.yaml"
    }
  },
  "submodule_mappings": {
    "neon_messagebus": "neon_core",
    "neon_speech": "neon_core",
    "neon_audio": "neon_core",
    "neon_gui": "neon_core"
  }
}
```

If `get_ovos_config` was called from `mycroft` with the same configuration file as the last example,
the returned configuration would be:

```json
{
  "base_folder": "mycroft",
  "config_filename": "mycroft.conf",
  "default_config_path": "<Path to Installed Core>/configuration/mycroft.conf",
  "module_overrides": {
    "neon_core": {
      "base_folder": "neon",
      "config_filename": "neon.yaml",
      "default_config_path": "/etc/example/config/neon.yaml"
    }
  },
  "submodule_mappings": {
    "neon_messagebus": "neon_core",
    "neon_speech": "neon_core",
    "neon_audio": "neon_core",
    "neon_gui": "neon_core"
  }
}
```

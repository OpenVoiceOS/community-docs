# OVOS Configuration
When you first start OVOS, there should not be any configuration needed to have a working device.

**NOTE** To continue with the examples, you will need access to a shell on your device.  This can be achevied with SSH.  Connect to your device with the command `ssh ovos@<device_ip_address>` and enter the password `ovos`.

This password is **EXTREAMLY** insecure and should be changed or use ssh keys for logging in.

This section will explain how the configuration works, and how to do basic configuration changes.

The rest of this section will assume you have shell access to your device.

## How it works

OVOS will load configuration files from several locations and combine them into a single `json` file that is used throughout the software.

- `{ovos-config-path}/mycroft.conf`
  - usually in `<python_install_path>/site-packages/ovos_config/mycroft.conf`
  - This is the default configuration file distrubuted with `ovos-core`
- `os.environ.get('MYCROFT_SYSTEM_CONFIG')` or /etc/mycroft/mycroft.conf
  - This is the default configuration file used by images, and may change specific values to corispond with how the image works.
- `os.environ.get('MYCROFT_WEB_CACHE')` or `XDG_CONFIG_PATH`/mycroft/web_cache.json
- `~/.mycroft/mycroft.conf` (Deprecated)
- `XDG_CONFIG_DIRS` + /mycroft/mycroft.conf
- `/etc/xdg/mycroft/mycroft.conf`
- `XDG_CONFIG_HOME` (default ~/.config) + /mycroft/mycroft.conf
  - This is the file that you should use to modify the configuration.

When the configuration loader starts, it looks in these locations in this order, and loads ALL configurations. Keys that exist in multiple configuration files will be overridden by the last file to contain the value. This process results in a minimal amount being written for a specific device and user, without modifying default distribution files.

[Advanced Configuration Docs](https://openvoiceos.github.io/ovos-technical-manual/config/)

## Included Tools
OVOS provides a command line tool `ovos-config` for viewing and changing configuration values.

Values can also be set manually in config files instead of using the CLI tool

These methods will be used later in the [How To](how_to.md) section of these Docs.

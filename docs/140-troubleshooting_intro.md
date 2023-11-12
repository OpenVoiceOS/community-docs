# Introduction to Troubleshooting OpenVoiceOS
** Coming soon **
## Architecture

## Troubleshooting Commands

## Problem/Fix
### locale.Error: unsupported locale setting
This error could from the ovos-cli-client, or other sources.

To resolve, ensure that your locale is set correctly, try running raspi-config to set it if your on Raspberry Pi OS (Raspbian).  

Manually update `/etc/default/locale`

use `locale` to verify your current locale, and `locale -a` to verify the local you've set is actually available.
[Source](https://stackoverflow.com/questions/14547631/python-locale-error-unsupported-locale-setting)


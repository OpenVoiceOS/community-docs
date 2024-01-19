# OVOS Installer

[OVOS-Installer](https://github.com/OpenVoiceOS/ovos-installer) is the newest way to install OVOS and is probably the easiest way to install on an existing system.

You do need a few packages installed on your host system before starting.
- `curl`
- `git`
- `sudo` and sudo access for your user
After installing those packages, simply run a command and follow the on screen instructions.

`sh -c "curl -s https://raw.githubusercontent.com/OpenVoiceOS/ovos-installer/main/installer.sh -o installer.sh && chmod +x installer.sh && sudo ./installer.sh && rm installer.sh"`

More information on the OVOS Installer can be found on the [README](https://github.com/OpenVoiceOS/ovos-installer/blob/main/README.md) page in the Github repository.

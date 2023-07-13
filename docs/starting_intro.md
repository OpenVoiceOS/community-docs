# Starting OVOS
Being a modular system has the advantage of being able to start with several different methods.

If you installed an image, your device is already pre-configured to start all of the services automatically.

At the time of this writing, both images use systemd service files to start, restart, and stop each OVOS module.

Typical command to restart the OVOS stack

`systemctl --user restart ovos.service`

`ovos.service` is a special systemd service file that instructs the rest of the stack to follow what it is doing.  If you stop `ovos.service` all of the services will stop.  Same with `start` and `restart`.  This makes it handy to restart the complete stack in one command after changes have been made.

The rest of this section will describe this method, and others in detail.

[Starting as stand alone modules](starting_modules.md)

[Starting with systemd service files](starting_systemd.md)

[Starting Docker](starting_docker.md)

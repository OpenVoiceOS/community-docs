# Starting OVOS - modules
OVOS in its simplest form is just a python module, and can be invoked as one.  In fact, the [systemd service](starting_systemd.md) method of starting uses a glorified version of this.

## ovos-core
ovos-core is the brains of the device.  Without it, you would have some cool software that does not work together.  It controlls the `skills` service and directs `intents` to the right skill.

### Invoking the skills module
Open a command shell and type the following

`ovos-core`

You will see a bunch of lines from the logs, and at the end, it will say `WARNING - Message Bus Client will reconnect in 5.0 seconds.`  This is because we have not started the messagebus service and that is the `nervous system`.  You cannot communicate to the other parts without it.

## ovos-messagebus
ovos-messagebus is the nervous system of OVOS.  This is what makes everything work together.

**NOTE**  The messagebus is an unsecured bus to your system and should **NOT** be exposed to the outside world.

### Invoking the messagebus
With ovos-core running in one terminal shell, open another and type the command

`ovos-messagebus`

Once again, a whole bunch of log lines will scroll by, and at the end, it will say `INFO - Message bus service started!`

If you look back at the terminal with ovos-core, you will notice that there are new logs that ovos-core has connected to the messagebus.

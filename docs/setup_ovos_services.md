# Running & Setting Up OVOS Services

OpenVoiceOS is a software stack that includes six important services, with some being optional, depending on the platform or environment. If you are a developer or would like to quickly test OpenVoiceOS for debugging purposes, you can run each service separately in a terminal. However, for users, distributions, and packagers, it is recommended to use systemd or any other init service that their userland supports for launching and managing OpenVoiceOS services.

### Here are the commands for launching each of the services from the CLI:

 - Launching the Messagebus service: python3 -m mycroft.messagebus.service
 - Launching the Skills service: python3 -m mycroft.skills
 - Launching the PHAL service: python3 -m ovos_PHAL
 - Launching the Audio service: python3 -m mycroft.audio
 - Launching the Voice service: python3 -m mycroft.client.speech
 - Launching the GUI service: python3 -m mycroft.gui

OpenVoiceOS services can be set up as SYSTEM or USER systemd services. The choice of which type to use and how to set them up is left up to the user, packager, and distributions. Keep in mind that these service scripts are just examples and may require changes based on your requirements.

### Setup the OpenVoiceOS service on Manjaro:
- Create a service file called "ovos.service" under "/usr/lib/systemd/user/" with the following contents:

```
[Unit]
Description=OpenVoiceOS Software stack.
Requires=ovos-messagebus.service
Requires=ovos-skills.service
Requires=ovos-audio.service
Requires=ovos-voice.service
Requires=ovos-gui.service
Requires=ovos-phal.service

[Service]
Type=simple
ExecStart=/bin/true
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

Here are the service files required for each of the individual services:

### Setting up Messagebus service as a user service:
- Create a service file called "ovos-messagebus.service" under "/usr/lib/systemd/user/" with the following contents:

```
[Unit]
Description=OpenVoiceOS Messagebus
Requires=ovos.service
PartOf=ovos.service

[Service]
Type=simple
ExecStart=/usr/bin/python -m mycroft.messagebus.service
TimeoutStartSec=1m
TimeoutStopSec=1m
Restart=on-failure
StartLimitInterval=5min
StartLimitBurst=4

[Install]
WantedBy=ovos.service
```

### Setting up Skills service:
- Create a service file called "ovos-skills.service" under "/usr/lib/systemd/user/" with the following contents:

```
[Unit]
Description=OpenVoiceOS Skills
PartOf=ovos.service
Requires=ovos-messagebus.service

[Service]
Type=simple
ExecStart=/usr/bin/python -m mycroft.skills
TimeoutStartSec=1m
TimeoutStopSec=1m
Restart=on-failure
StartLimitInterval=5min
StartLimitBurst=4

[Install]
WantedBy=ovos.service
```

### Setting up PHAL service:
- Create a service file called "ovos-phal.service" under "/usr/lib/systemd/user/" with the following contents:

```
[Unit]
Description=OVOS PHAL
PartOf=ovos.service
Requires=ovos-messagebus.service


[Service]
Type=simple
ExecStart=/usr/bin/python -m ovos_PHAL
TimeoutStartSec=1m
TimeoutStopSec=1m
Restart=on-failure
StartLimitInterval=5min
StartLimitBurst=4

[Install]
WantedBy=ovos.service
```

### Setting up Audio service:
- Create a service file called "ovos-audio.service" under "/usr/lib/systemd/user/" with the following contents:

```
[Unit]
Description=OVOS Audio
PartOf=ovos.service
Requires=ovos-messagebus.service


[Service]
Type=simple
ExecStart=/usr/bin/python -m mycroft.audio
TimeoutStartSec=1m
TimeoutStopSec=1m
Restart=on-failure
StartLimitInterval=5min
StartLimitBurst=4

[Install]
WantedBy=ovos.service
```

### Setting up Voice service:
- Create a service file called "ovos-voice.service" under "/usr/lib/systemd/user/" with the following contents:

```
[Unit]
Description=OVOS Voice
PartOf=ovos.service
Requires=ovos-messagebus.service


[Service]
Type=simple
ExecStart=/usr/bin/python -m mycroft.client.speech
TimeoutStartSec=1m
TimeoutStopSec=1m
Restart=on-failure
StartLimitInterval=5min
StartLimitBurst=4

[Install]
WantedBy=ovos.service
```

### Setting up GUI service:
- Create a service file called "ovos-gui.service" under "/usr/lib/systemd/user/" with the following contents:

```
[Unit]
Description=OVOS Gui
PartOf=ovos.service
Requires=ovos-messagebus.service


[Service]
Type=simple
ExecStart=/usr/bin/python -m mycroft.gui
TimeoutStartSec=1m
TimeoutStopSec=1m
Restart=on-failure
StartLimitInterval=5min
StartLimitBurst=4

[Install]
WantedBy=ovos.service
```

### Setup the OpenVoiceOS service on Raspbian
- Check [Services in Rasbian](./docs/setup_ovos_services.raspian.md)

### Using helper scripts

You can find helper scripts such as **start-mycroft.sh** and **stop-mycroft.sh** on this website: https://github.com/OpenVoiceOS/scripts. These scripts are designed to mimic a daemon and manage multiple OVOS services. However, please note that they are optional and should be used with care. They are not the most recommended method for running OVOS services.

# Running & Setting Up OVOS Services

## Setup the OpenVoiceOS service in Raspbian:

Note that we assume you are running with the user **pi**, if not, change your working directories.

- Create a folder for your systemd 
  ```
  mkdir -p ~/.config/systemd/user/
  ```

- Create a service file `~/.config/systemd/user/ovos.service` with the following contents:
  ```sh
  [Unit]
  Description=OpenVoiceOS Software stack.
  Requires=ovos-messagebus.service
  Requires=ovos-skills.service
  Requires=ovos-audio.service
  Requires=ovos-voice.service
  #Requires=ovos-gui.service
  Requires=ovos-phal.service
  
  [Service]
  Type=simple
  WorkingDirectory=/home/pi/ovos-core/
  ExecStart=/bin/true
  RemainAfterExit=yes
  
  [Install]
  WantedBy=multi-user.target
  ```

  Please note that the ovos-gui.service is commented out as these scripts have been tested on a Raspian Bullseye running on a headless RPi3-B

  Here are the service files required for each of the individual services:

- Create a service file `~/.config/systemd/user/ovos-messagebus.service` with the following contents:

  ```sh
  [Unit]
  Description=OpenVoiceOS Messagebus
  Requires=ovos.service
  PartOf=ovos.service
  
  [Service]
  Type=simple
  WorkingDirectory=/home/pi/ovos-core
  ExecStart=/home/pi/ovos-core/bin/python -m mycroft.messagebus.service
  TimeoutStartSec=1m
  TimeoutStopSec=1m
  Restart=on-failure
  StartLimitInterval=5min
  StartLimitBurst=4
  
  [Install]
  WantedBy=ovos.service
  ```

- Create a service file `~/.config/systemd/user/ovos-skills.service` with the following contents:

  ```sh
  [Unit]
  Description=OpenVoiceOS Skills
  Requires=ovos-messagebus.service
  PartOf=ovos.service

  [Service]
  Type=simple
  WorkingDirectory=/home/pi/ovos-core
  ExecStart=/home/pi/ovos-core/bin/python -m mycroft.skills
  TimeoutStartSec=1m
  TimeoutStopSec=1m
  Restart=on-failure
  StartLimitInterval=5min
  StartLimitBurst=4

  [Install]
  WantedBy=ovos.service
  ```

- Create a service file `~/.config/systemd/user/ovos-phal.service` with the following contents:

  ```sh
  [Unit]
  Description=OpenVoiceOS PHAL
  Requires=ovos-messagebus.service
  PartOf=ovos.service

  [Service]
  Type=simple
  WorkingDirectory=/home/pi/ovos-core
  ExecStart=/home/pi/ovos-core/bin/python -m ovos_PHAL
  TimeoutStartSec=1m
  TimeoutStopSec=1m
  Restart=on-failure
  StartLimitInterval=5min
  StartLimitBurst=4

  [Install]
  WantedBy=ovos.service
  ```

- Create a service file `~/.config/systemd/user/ovos-audio.service` with the following contents:

  ```sh
  [Unit]
  Description=OpenVoiceOS Audio
  Requires=ovos-messagebus.service
  PartOf=ovos.service

  [Service]
  Type=simple
  WorkingDirectory=/home/pi/ovos-core
  ExecStart=/home/pi/ovos-core/bin/python -m mycroft.audio
  TimeoutStartSec=1m
  TimeoutStopSec=1m
  Restart=on-failure
  StartLimitInterval=5min
  StartLimitBurst=4

  [Install]
  WantedBy=ovos.service
  ```

- Create a service file `~/.config/systemd/user/ovos-voice.service` with the following contents:

  ```sh
  [Unit]
  Description=OpenVoiceOS Voice
  Requires=ovos-messagebus.service
  PartOf=ovos.service

  [Service]
  Type=simple
  WorkingDirectory=/home/pi/ovos-core
  ExecStart=/home/pi/ovos-core/bin/python -m mycroft.client.speech
  TimeoutStartSec=1m
  TimeoutStopSec=1m
  Restart=on-failure
  StartLimitInterval=5min
  StartLimitBurst=4

  [Install]
  WantedBy=ovos.service
  ```

- Create a service file `~/.config/systemd/user/ovos-gui.service` with the following contents:

  ```sh
  [Unit]
  Description=OVOS Gui
  PartOf=ovos.service
  Requires=ovos-messagebus.service

  [Service]
  Type=simple
  WorkingDirectory=/home/pi/ovos-core
  ExecStart=/home/pi/ovos-core/bin/python -m mycroft.gui
  TimeoutStartSec=1m
  TimeoutStopSec=1m
  Restart=on-failure
  StartLimitInterval=5min
  StartLimitBurst=4

  [Install]
  WantedBy=ovos.service
  ```
  
- Start your OVOS with `systemctl --user start ovos.service`
- Monitor the status of your services with `systemctl --user status`

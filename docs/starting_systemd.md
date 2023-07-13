# Starting OVOS - systemd
OVOS being a modular system has several pieces that can start individually.

user systemd service files are the recomended way to start each module, but may be started in other ways also.

This is the prefered method to start the OVOS modules.  If you have not used `systemd` before, there is a lot of refrence on the web with more information.  It is out of scope of this document.  The following is assuming the user `ovos` is being used.

A `systemd service` file and a `systemd hook` file is required for this to work.  We will create both files for the `ovos-messagebus` service because this is used by all other modules.  The provided `system hook` files need another python package `sdnotify` to work as written.

`pip install sdnotify`

### ovos.service
This is the main service file that is used to start the stack as a unit.  This is not necessasary, but helpful if more than one module should start together.

Create the service file

`nano .config/systemd/user/ovos.service`

This file should contain
```
[Unit]
Description=OVOS A.I. Software stack.

[Service]
Type=oneshot
ExecStart=/bin/true
RemainAfterExit=yes

[Install]
WantedBy=default.target
```

There is no `hook` file needed for this service.

### ovos-messagebus.service
The messagebus is the main nervous system for OVOS and is needed by all other modules to enable communication between them.

Create the service file

`nano ~/.config/systemd/user/ovos-messagebus.service`

And make it contain the following

```
[Unit]
Description=OVOS Messagebus
PartOf=ovos.service
After=ovos.service

[Service]
Type=notify
ExecStart=/home/ovos/.local/bin/ovos-systemd-messagebus
TimeoutStartSec=1m
TimeoutStopSec=1m
Restart=on-failure
StartLimitInterval=5min
StartLimitBurst=4
#StartLimitAction=reboot-force
#WatchdogSec=30s

[Install]
WantedBy=ovos.service
```

Create the hook file

`nano ~/.local/bin/ovos-systemd-messagebus`

This file should contain
```
#!/usr/bin/env python
##########################################################################
# ovos-systemd_messagebus.py
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
##########################################################################
import sdnotify
from mycroft.messagebus.service.__main__ import main

n = sdnotify.SystemdNotifier()

def notify_ready():
    n.notify('READY=1')
    print('Startup of Mycroft Messagebus service complete')

    def notify_stopping():
        n.notify('STOPPING=1')
        print('Stopping the Mycroft Messagebus service')

        main(ready_hook=notify_ready, stopping_hook=notify_stopping)
```

Reload the systemd daemon

`systemctl --user daemon-reload`

The service can now be started

`systemctl --user start ovos-messagebus.service`

To start the stack on boot, enable both of the services

`systemctl --user enable ovos.service`

`systemctl --user enable ovos-messagebus.service`

Now on every reboot, the OVOS system should start automatically.

**NOTE** the systemd service and hook files are examples used in the [raspbian-ovos](https://github.com/OpenVoiceOS/raspbian-ovos) repository.

For each module that needs to be started, they should have similar `service` and `hook` files.

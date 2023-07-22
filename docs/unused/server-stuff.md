
## Using a Personal Backend

This is concidered an advanced function and is unnecessasary for normal usage

The default for ovos-core is no backend.

You can go without a backend and go offline and use our free proxy for API services with no accounts.

This setup requires there to be a running personal-backend.  Refer to [this Github page](https://github.com/OpenVoiceOS/ovos-personal-backend) for details.

### Gui Configuration

If your instalation has the [skill-ovos-setup](https://github.com/OpenVoiceOS/skill-ovos-setup) installed, you will have a gui available to perform the setup of your device to use the personal backend that you setup.

**NOTE** it is NOT advised to install this skill manually, as it can cause issues if OVOS was not configured to use it.  Skip to the [Manual Configuration](#Manual Configuration) section for headless devices or if this skill was not pre-installed.

On first boot, you will be presented with a screen to choose a backend option.

**NOTE** The Selene backend shown in the image is no longer available as an option

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/select-backend.png)

Select `Personal Backend` from the options.  The next screen will allow you to enter the IP address of your personal backend server.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/personal-backend.png)

Enter the IP address and Port number of your personal backend

eg. `192.168.1.xxx:6712`

If everything is entered correctly, and you backend is running, you should see a screen showing that your connection was successful.  You should now be able to configure your device with your backend.

### Manual Configuration

This section requires shell access to the device, either with direct connection, or [SSH](#Connect with ssh).

The local file `~/.config/mycroft/mycroft.conf` contains local settings that the user has specified.  This file may not exist, and will have to be created to continue.

Open the file to edit it

`nano ~/.config/mycroft/mycroft.conf`

Add this section to your file.  This file must be in valid json or yaml format.

```
{
    "server": {
        "url": "http://<your_server_IP_address:port_number>",
        "version": "v1",
        "update": true,
        "metrics": true
        }
}
```

You will also have to make sure there is not an `identity file` already configured

`rm ~/.config/mycroft/identity/identity2.json`

Restart your device, and you should be connected to your backend.

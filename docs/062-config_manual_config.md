# Configuration - Manually Change Files
User configuration should be set in the `XDG_CONFIG_HOME` file.  Usually located at `~/.config/mycroft/mycroft.conf`.  This file may or may not exist by default.  If it does NOT exist, create it.

`mkdir -p ~/.config/mycroft`

`touch ~/.config/mycroft/mycroft.conf`

Now you can edit that file.  To continue with the previous example, we will change the host of the TTS server, then add the value manually to the user's `mycroft.conf` file.

Open the file for editing.  It is not uncommon for this file to exist, but be empty.

`nano ~/.config/mycroft/mycroft.conf`

Enter the following into the file.  **NOTE** this file must be valid json or yaml format.  OVOS knows how to read both


```
{
  "tts": {
    "module": "ovos-tts-plugin-server",
    "ovos-tts-plugin-server": {
      "host": "https://pipertts.ziggyai.online"
    }
  }
}
```

You can check the formatting of your file with the `jq` command.

`cat ~/.config/mycroft/mycroft.conf | jq`
If your distribution does not include `jq` it can be installed with the command `sudo apt install jq` or the equivalent for your distro.

If there are no errors, it will output the complete file.  On error, it will output the line where the error is.  You can use an online JSON checker if you want also.

[online json checker](https://jsonlint.com/)
[online yaml checker](https://www.yamllint.com/)

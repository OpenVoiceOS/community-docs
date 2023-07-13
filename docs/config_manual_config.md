# Configuration - Manually Change Files
User configuration should be set in the `XDG_CONFIG_HOME` file.  Usually located at `~/.config/mycroft/mycroft.conf`.  This file may or may not exist by default.  If it does NOT exist, create it.

`mkdir -p ~/.config/mycroft`

`touch ~/.config/mycroft/mycroft.conf`

Now you can edit that file.  To continue with the previous example, we will change the host of the TTS server, we will add the value manually to the Users `mycroft.conf` file.

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

You can check the formating of your file with the `jq` command.

`cat ~/.config/mycroft/mycroft.conf | jq`

If there are no errors, it will output the complete file.  On error, it will output the line where the error is.  You can use an online json checker if you want also.

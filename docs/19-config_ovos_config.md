# Configuration - ovos-config
OVOS provides a small command line tool, [ovos-config](https://github.com/OpenVoiceOS/ovos-config), for viewing and setting configuration values in the OVOS ecosystem.

**NOTE** The CLI of this script is new, and may contain some bugs.  [Please report issues](https://github.com/OpenVoiceOS/ovos-config/issues) to the `ovos-config` github page.

## Viewing Configuration Settings
`ovos-config --help` will show a list of commands to use with this tool.

`ovos-config show` will display a table representing all of the current configuration values.

To get the values of a specific section:

`ovos-config show --section tts` will show just the "tts" section of the configuration

```
ovos-config show --section tts
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Configuration keys (Configuration: Joined, Section: tts)       ┃ Value                  ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━┩
│ pulse_duck                                                   │ False                  │
│ module                                                       │ ovos-tts-plugin-server │
│ fallback_module                                              │ ovos-tts-plugin-mimic  │
├──────────────────────────────────────────────────────────────┼────────────────────────┤
│ ovos-tts-plugin-server                                       │                        │
│     host                                                     │                        │
└──────────────────────────────────────────────────────────────┴────────────────────────┘
```

## Changing Configuration Values
We will continue with the example above, TTS.

Change the host of the TTS server:

`ovos-config set -k tts` will show a table of values that can be edited

```
set -k tts
┏━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━┓
┃ # ┃ Path                            ┃ Value ┃
┡━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━┩
│ 0 │ tts/pulse_duck                  │ False │
│ 1 │ tts/ovos-tts-plugin-server/host │       │
└───┴─────────────────────────────────┴───────┘
Which value should be changed? (2='Exit') [0/1/2]:
```
Enter `1` to change the value of `tts/ovos-tts-plugin-server/host`

`Please enter the value to be stored (type: str) :`

Enter the value for the tts server that you want ovos to use.

`https://pipertts.ziggyai.online`

Use `ovos-config show --section tts` to check your results

```
ovos-config show --section tts
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ Configuration keys (Configuration: Joined, Section: tts)       ┃ Value                           ┃
┡━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━╇━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┩
│ pulse_duck                                                   │ False                           │
│ module                                                       │ ovos-tts-plugin-server          │
│ fallback_module                                              │ ovos-tts-plugin-mimic           │
├──────────────────────────────────────────────────────────────┼─────────────────────────────────┤
│ ovos-tts-plugin-server                                       │                                 │
│     host                                                     │ https://pipertts.ziggyai.online │
└──────────────────────────────────────────────────────────────┴─────────────────────────────────┘
```

This can be done for any of the values in the configuration stack.

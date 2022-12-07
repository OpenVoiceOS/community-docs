# GUI Extensions

OVOS Core supports a GUI Extension framework which allows the GUI service to incorporate additional behaviour for a
specific platform. GUI Extensions currently supported:

## Smartspeaker Extension

This extension is responsible for managing the smartspeaker GUI interface behaviour, it supports homescreens and
homescreen management. Enabling the smartspeaker GUI extension:

```javascript
"gui": {
    "extension": "smartspeaker",
    "idle_display_skill": "skill-ovos-homescreen.openvoiceos"
}
```

## Bigscreen Extension

This extension is responsible for managing the plasma bigscreen GUI interface behaviour, it supports window management
and window behaviour control on specific window managers like Kwin. Enabling the Bigscreen GUI extension:

```javascript
"gui": {
    "extension": "bigscreen"
}
```

## Mobile Extension

This extension is responsible for managing the mobile GUI interface behaviour, it supports homescreens and additionally
adds support for global page back navigation. Enabling the Mobile GUI extension:

```javascript
"gui": {
    "extension": "smartspeaker",
    "idle_display_skill": "skill-android-homescreen.openvoiceos",
}
```

## Generic Extension

This extension provides a generic GUI interface and does not add any additional behaviour,
it optionally supports homescreens if the platform or user manually enables it.
This extension is enabled by default when no other extension is specified.

```javascript
"gui": {
    "idle_display_skill": "skill-ovos-homescreen.openvoiceos",
    "extension": "generic",
    "generic": {
        "homescreen_supported": false
    }
}
```

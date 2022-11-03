# Skills Service

The skills service is responsible for loading skills and intent parsers

All user queries are handled by the skills service, you can think of it as OVOS's brain

## Configuration

```javascript
"skills": {

    // don't start loading skills until internet is detected
    // this config value is not present in mycroft-core (internet is required)
    // ovos-core expects that some instances will be running fully offline
    "wait_for_internet": false,

    // folder name, relative to "data_dir"
    "directory": "skills",

    // used by selene marketplace integration
    "upload_skill_manifest": true,

    // blacklisted skills to not load
    // NB: This is the skill_id, usually the basename() of the directory where the skill lives, so if
     // the skill you want to blacklist is in /usr/share/mycroft/skills/mycroft-alarm.mycroftai/
    // then you should write `["mycroft-alarm.mycroftai"]` below.
    "blacklisted_skills": [],

    // DEPRECATED: priority skills to be loaded first
    // setup.py installed skills take precedence over this
    // this option is an artifact from the past when internet and pairing blocked skill loading
    "priority_skills": [],

    // fallback skill configuration (see below)
    "fallbacks": {...},

    // converse stage configuration (see below)
    "converse": {...}

},
```


## Converse

A malicious or badly designed skill using the converse method can potentially hijack the whole conversation loop and render the skills service unusable

Some settings are exposed to add some limitations to which skills can be activated and under what circumstances

The concept of "converse priority" is under active development, work on a "converse session" mechanism is also underway [@ovos-core/pull/160](https://github.com/OpenVoiceOS/ovos-core/pull/160)

```javascript
"skills": {
    // converse stage configuration
    "converse": {
        // the default number of seconds a skill remains active,
        // if the user does not interact with the skill in this timespan it
        // will be deactivated, default 5 minutes (same as mycroft)
        "timeout": 300,
        
        // override of "skill_timeouts" per skill_id
        // you can configure specific skills to remain active longer
        "skill_timeouts": {},

        // conversational mode has 3 modes of operations:
        // - "accept_all"  # default mycroft-core behavior
        // - "whitelist"  # only call converse for skills in "converse_whitelist"
        // - "blacklist"  # only call converse for skills NOT in "converse_blacklist"
        "converse_mode": "accept_all",
        "converse_whitelist": [],
        "converse_blacklist": [],

        // converse activation has 4 modes of operations:
        // - "accept_all"  # default mycroft-core behavior, any skill can
        //                 # activate itself unconditionally
        // - "priority"  # skills can only activate themselves if no skill with
        //               # higher priority is active
        // - "whitelist"  # only skills in "converse_whitelist" can activate themselves
        // - "blacklist"  # only skills NOT in converse "converse_blacklist" can activate themselves
        // NOTE: this does not apply for regular skill activation, only to skill
        //       initiated activation requests, eg, self.make_active()
        "converse_activation": "accept_all",

        // number of consecutive times a skill is allowed to activate itself
        // per minute, -1 for no limit (default), 0 to disable self-activation
        "max_activations": -1,
        
        // override of "max_activations" per skill_id
        // you can configure specific skills to activate more/less often
        "skill_activations": {},

        // if false only skills can activate themselves
        // if true any skill can activate any other skill
        "cross_activation": true,

        // if false only skills can deactivate themselves
        // if true any skill can deactivate any other skill
        // NOTE: skill deactivation is not yet implemented
        "cross_deactivation": true,

        
        // you can add skill_id: priority to override the developer defined
        // priority of those skills, 
        
        // converse priority is work in progress and not yet exposed to skills
        // priority is assumed to be 50
        // the only current source for converse priorities is this setting
        "converse_priorities": {
           // "skill_id": 10
        }
    }

},
```

## Fallback Skills

Just like with converse a badly designed or malicious skill can hijack the fallback skill loop, while this is not as serious as with converse some protections are also provided

You can configure what skills are allowed to use the fallback mechanism, you can also modify the fallback priority to ensure skills behave well together. 

Since priority is defined by developers sometimes the default value is not appropriate and does not fit well with the installed skills collection

```javascript
"skills": {
    // fallback skill configuration
    "fallbacks": {
        // you can add skill_id: priority to override the developer defined
        // priority of those skills, this allows customization
        // of unknown intent handling for default_skills + user preferences
        "fallback_priorities": {
           // "skill_id": 10
        },
        // fallback skill handling has 3 modes of operations:
        // - "accept_all"  # default mycroft-core behavior
        // - "whitelist"  # only call fallback for skills in "fallback_whitelist"
        // - "blacklist"  # only call fallback for skills NOT in "fallback_blacklist"
        "fallback_mode": "accept_all",
        "fallback_whitelist": [],
        "fallback_blacklist": []
    }
},
```

## Intent Engines

ovos-core currently supports the same intent parsers as mycroft, a plugin solution is being actively developed [@ovos-plugin-manager/pull/47](https://github.com/OpenVoiceOS/ovos-plugin-manager/pull/47)

While plugin support is not implemented we provide a drop in replacement alternative to padatious that is lightweight and performs similarly.

This was done to avoid the non-python dependency on libfann2 which made core hard to package in some systems

NOTE: fann2 is LGPL licensed, it is one of the exceptions to our [licensing policy](../license)

[Padacioso](https://github.com/OpenJarbas/padacioso) will be used if padatious is not installed or if explicitly enabled in `mycroft.conf`

```javascript
"padatious": {
    "intent_cache": "~/.local/share/mycroft/intent_cache",
    "train_delay": 4,
    "single_thread": false,
    // fallback settings for padacioso (pure regex)
    "regex_only": false,
    "fuzz": true
},
```
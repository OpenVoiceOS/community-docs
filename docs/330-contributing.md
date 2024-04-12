# Contributing to OVOS
Welcome to OVOS! First off, thanks for taking the time to contribute! ❤️

If you're not familiar with us, OVOS is a voice assistant project that is open source and privacy-focused. We're building a platform that can run on a variety of devices, from a Raspberry Pi to a desktop computer, and we're always looking for help to make it better.

If you want to know more about us, you can check out about [About OVOS](https://openvoiceos.github.io/community-docs/001-about/) section in our community docs.


We're a very friendly and open community and most responsive on [Matrix](https://matrix.to/#/#OpenVoiceOS-Support:matrix.org). Please come say hi and feel free to ask any questions.

## How can you help?

In short, OVOS has found ourselves in the position of having to take a large amount of R&D code and polish it up for a broader user base. We welcome PRs at the best of times, but we especially need help with things that may not be marked as issues:

1. Adding docstrings to methods, especially on skills (starts with `skill-ovos-`) and plugins (has `plugin` in the name somewhere).
2. Localization. We strive to be an international private and open source voice assistant, and it's a huge contribution to translate our skills to your language! No, really! #goodfirstissue
3. Writing tests. Nobody loves it, everybody needs it, and we love if you do it!
4. Documentation. Both our [technical manual](https://openvoiceos.github.io/ovos-technical-manual/) and our [community docs](https://openvoiceos.github.io/community-docs/) are community-managed and could use PRs ranging from grammatical fixes, fixing broken links, and clarifying/expanding on existing information. #goodfirstissue
5. Testing out skills and looking for flaws/ways to improve. Many of our skills have been released and in the wild for years, but could use some loving attention. You can find actively supported skills in the `OpenVoiceOS` org, or skills in need of some care in the `OVOSHatchery` org.

## How do you get started?

First of all, if you're just starting out and want to contribute documentation or localization PRs, don't sweat it if you don't have OVOS running. We're happy to help with testing those. If you'd like to run it yourself and confirm things work as you expect, read on.

The easiest way to get OVOS running on any given Linux or Windows with WSL2 system. is to use [ovos-installer.](https://github.com/openvoiceos/ovos-installer)

OVOS also has a [reference setup for Docker](https://github.com/OpenVoiceOS/ovos-docker) that will run on any platform and architecture that uses Docker - Linux, Mac OS, and Windows with WSL2. (and yes it works with Podman too!)

If you have a spare Raspberry Pi with a microphone/speaker available, OVOS maintains [a ready-to-use image](https://openvoiceos.github.io/community-docs/qs_intro/#rasberry-pi-os-latest-images) for that platform. It is currently not fully tested on the Pi 5.

Raspberry Pi also supports GUI skills (that means if you have a screen attached to your Pi, you can run skills that have a graphical interface), which are written in Qt. If you're a Qt developer, we'd love to have your help!

The most up-to-date information on running OVOS can be found [in our community docs](https://openvoiceos.github.io/community-docs/qs_intro/).

## Skills and plugins

The docs above are meant for a broad set of users. For the details you're looking for on how all these different pieces of OVOS interact, [please check out our technical manual](https://openvoiceos.github.io/ovos-technical-manual/). 

For more details about the skills and plugins, you can check the technical documentation here [OVOS Technical Manual](hhttps://openvoiceos.github.io/ovos-technical-manual/) It is inspired by [Neon.AI](https://neon.ai) and Mycroft documentation and covers diverse topics such as design philosophy, available helper methods, writing GUIs (Qt devs wanted!), how to get a skill to converse back and forth with a user, and more.

If you're stuck or have any questions, please come chat with us on [Matrix](https://matrix.to/#/#OpenVoiceOS-Support:matrix.org). We're grateful for your assistance and will do everything we can to help you.

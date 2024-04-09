Welcome to OVOS! First off, thanks for taking the time to contribute! ❤️

If you're not familiar with us, [our GoFundMe page has a brief history of what we do and how we got here](https://www.gofundme.com/f/openvoiceos). (Please don't feel obligated to contribute to the GoFundMe unless you really want to though - we're okay right now and you're here to help code!)

We're a very friendly and open community and most responsive on [Matrix](https://matrix.to/#/#OpenVoiceOS-Support:matrix.org). Please come say hi and feel free to ask any questions.

## How can you help?

In short, OVOS has found ourselves in the position of having to take a large amount of R&D code and polish it up for a broader user base. We welcome PRs at the best of times, but we especially need help with things that may not be marked as issues:

1. Adding docstrings to methods, especially on skills (starts with `skill-ovos-`) and plugins (has `plugin` in the name somewhere).
2. Localization. We strive to be an international private and open source voice assistant, and it's a huge contribution to translate our skills to your language! No, really! #goodfirstissue
3. Writing tests. Nobody loves it, everybody needs it, and we love if you do it!
4. Documentation. Both our [technical manual](https://openvoiceos.github.io/ovos-technical-manual/) and our [community docs](https://openvoiceos.github.io/community-docs/) are community-managed and could use PRs ranging from grammatical fixes, fixing broken links, and clarifying/expanding on existing information. #goodfirstissue
5. Testing out skills and looking for flaws/ways to improve. Many of our skills have been released and in the wild for years, but could use some loving attention.

## How do you get started?

First of all, if you're just starting out and want to contribute documentation or localization PRs, don't sweat it if you don't have OVOS running. We're happy to help with testing those. If you'd like to run it yourself and confirm things work as you expect, read on.

OVOS has a [reference setup for Docker](https://github.com/OpenVoiceOS/ovos-docker) that will run on any platform and architecture that uses Docker - Linux, Mac OS, and Windows with WSL2. If you're comfortable with Docker, this is the fastest and easiest way to get OVOS running locally to contribute back. (Yes, it also works with Podman!)

If you have a spare Raspberry Pi with a microphone/speaker available, OVOS maintains [a ready-to-use image](https://openvoiceos.github.io/community-docs/qs_intro/#rasberry-pi-os-latest-images) for that platform. It doesn't run the GUI, but it does everything else.

It's not quite ready for Hacktoberfest 2023, but there's also a [full Buildroot image](https://openvoiceos.github.io/community-docs/qs_intro/#buildroot-latest-image) that will be available for any architecture.

The most up-to-date information on running OVOS can be found [in our community docs](https://openvoiceos.github.io/community-docs/qs_intro/).

## Skills and plugins

The docs above are meant for a broad set of users. For the details you're looking for on how all these different pieces of OVOS interact, [please check out our technical manual](https://openvoiceos.github.io/ovos-technical-manual/). 

A friend-of-OVOS, [Neon.AI](https://neon.ai), has a comprehensive set of [documentation for skill development](https://neongeckocom.github.io/neon-docs/skill_development/voice-user-interface-design-guidelines/what-can-a-skill-do/) specifically. Much of this was forked from the (excellent) Mycroft skill documentation and covers diverse topics such as design philosophy, available helper methods, writing GUIs (Qt devs wanted!), how to get a skill to converse back and forth with a user, and more.

If you're stuck or have any questions, please come chat with us on [Matrix](https://matrix.to/#/#OpenVoiceOS-Support:matrix.org). We're grateful for your assistance and will do everything we can to help you.

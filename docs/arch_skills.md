# Skills Architecture
# OVOS Skills

## What can a Skill do?

Skills give OVOS the ability to perform a variety of functions. They can be installed or removed by the user, and can be easily updated to expand functionality. To get a good idea of what skills to build, let’s talk about the best use cases for a voice assistant, and what types of things OVOS can do.

OVOS can run on a variety of platforms from the Linux Desktop to SBCs like the raspberry pi.
Different devices will have slightly different use cases. Devices in the home are generally located in the living room or kitchen and are ideal for listening to the news, playing music, general information, using timers while cooking, checking the weather, and other similar activities that are easily accomplished hands free.

### Basic functions

We cover a lot of the basics with our Default Skills, things like Timers, Alarms, Weather, Time and Date, and more.

### Information

We also call this General Question and Answer, and it covers all of those factual questions someone might think to ask a
voice assistant. Questions like “who was the 32nd President of the United States?”, or “how tall is Eiffel Tower?”
Although the Default Skills cover a great deal of questions there is room for more. There are many topics that could use a specific skill such as Science, Academics, Movie Info, TV info, and Music info, etc..

### Media

One of the biggest use cases for Smart Speakers is playing media. The reason media playback is so popular is that it makes playing a song so easy, all you have to do is say “Hey Mycroft play the Beatles,” and you can be enjoying music without having to reach for a phone or remote. In addition to listening to music, there are
skills that handle videos as well.

### News

Much like listening to music, getting the latest news with a simple voice interaction is extremely convenient. OVOS
supports multiple news feeds, and has the ability to support multiple news skills.

### Smart Home

Another popular use case for Voice Assistants is to control Smart Home and IoT products. Within the mycroft ecosystem
there are skills for Home Assistant, Wink IoT, Lifx and more, but there are many products that we do not have skill for yet.
The open source community has been enthusiastically expanding OVOS's ability to voice control all kinds of smart home
products.

### Games

Voice games are becoming more and more popular, especially those that allow multiple users to play together. Trivia games are some of the most popular types of games to develop for voice assistants. There are several games already available for OVOS. There are native voice adventure games, ports of the popular text adventure games from infocom, a Crystal Ball game, a Number Guessing game and much more!

# OpenVoiceOS Standard Skills

# Standard Skills Usage

Your OpenVoiceOS device comes with certain skills pre-installed for basic functionality out of the box. You can also install new skills however more about that at a later stage.

## Date / Time skill

You can ask your device what time or date it is just in case you lost your watch.

> Hey Mycroft, what time is it?

![Time](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Time.png)

> Hey Mycroft, what is the date?

![Date](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Date.png)

## Setting an alarm

Having your OpenVoiceOS device knowing and showing the time is great, but it is even better to be woken up in the morning by your device.

> Hey Mycroft, set an alarm for 8 AM.

![Alarm](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Alarm.png)

## Setting of timers

Sometimes you are just busy but want to be alerted after a certain time. For that you can use timers.

> Hey Mycroft, set a timer for 5 minutes.

![Timer](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%205%20minutes%20timer.png)

You can always set more timers and even name them, so you know which timers is for what.

> Hey, Mycroft, set another timer called rice cooking for 7 minutes.

![Timers](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Two%20timers.png)

## Asking the weather

You can ask your device what the weather is or would be at any given time or place.

> Hey Mycroft, what is the weather like today?

![Weather 1](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Weather%201.png)

The weather skill actually uses multiple pages indicated by the small dots at the bottom of the screen.

![Weather 2](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20Weather%202.png)

## File Browser

The file browser allows you to browse the filesystem in your device and any connected media, you can view images and play music and videos.

KDEConnect integration allows you to share files with your mobile devices

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/ocp/file_browser.gif)


## GUI Framework

Mycroft-GUI is an open source visual and display framework for Mycroft running on top of KDE Plasma Technology and built using Kirigami a lightweight user interface framework for convergent applications which are empowered by Qt.

OVOS uses the standard mycroft-gui framework, you can find the official documentation [here](https://mycroft-ai.gitbook.io/docs/skill-development/displaying-information/mycroft-gui)
# OpenVoiceOS Home Screen

The home screen is the central place for all your tasks. It is the first thing you will see after completing the onboarding process. It supports a variety of pre-defined widgets which provide you with a quick overview of information you need to know like the current date, time and weather. The home screen contains various features and integrations which you can learn more about in the following sections.

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/homescreen.png)

## Features

### Night Mode Feature

The Night Mode feature let's you quickly switch your home screen into a dark standby clock, reducing the amount of light emitted by your device. This is especially useful if you are using your device in a dark room or at night. You can enable the night mode feature by tapping on the left edge pill button on the home screen.

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/homescreen-nightmode.gif)

### Quick Actions Dashboard

The Quick Actions Dashboard provides you with a card-based interface to quickly access and add your most used action. The Quick Actions dashboard comes with a variety of pre-defined actions like the ability to quickly add a new alarm, start a new timer or add a new note. You can also add your own custom actions to the dashboard by tapping on the plus button in the top right corner of the dashboard. The Quick Actions dashboard is accessible by tapping on the right edge pill button on the home screen.

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/homescreen-dashboard.gif)

### Application Launcher

OpenVoiceOS comes with support for dedicated voice applications. Voice Applications can be dedicated skills or PHAL plugins, providing their own dedicated user interface. The application launcher will show you a list of all available voice applications. You can access the application launcher by tapping on the center pill button on the bottom of the home screen.

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/homescreen-app-drawer.png)


### Wallpapers

The home screen supports custom wallpapers and comes with a bunch of wallpapers to choose from. You can easily change your custom wallpaper by swiping from right to left on the home screen.

## Widgets

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/homescreen-widgets.png)

### Notifications Widget

The notifications widget provides you with a quick overview of all your notifications. The notifications bell icon will be displayed in the top left corner of the home screen. You can access the notifications overview by tapping on the bell icon when it is displayed.

### Timer Widget

The timer widget is displayed in top left corner after the notifications bell icon. It will show up when you have an active timer running. Clicking on the timer widget will open the timers overview.

### Alarm Widget

The alarm widget is displayed in top left corner after the timer widget. It will show up when you have an active alarm set. Clicking on the alarm widget will open the alarms overview.

### Media Player Widget

The media player widget is displayed in the bottom of the home screen, It replaces the examples widget when a media player is active. The media player widget will show you the currently playing media and provide you with a quick way to pause, resume or skip the current media. You can also quickly access the media player by tapping the quick display media player button on the right side of the media player widget.

![](https://github.com/OpenVoiceOS/ovos_assets/raw/master/Images/homescreen-mediawidget.gif)

## Configuration

### Settings

The homescreen has several customizations available.  This is sample `settings.conf` file with all of the options explained

```
{
    "__mycroft_skill_firstrun": false,  # This is set on first load of the skill
    "weather_skill": "skill-weather.openvoiceos",  # DEPRECIATED has no effect - PR pending
    "datetime_skill": "skill-date-time.mycroftai",  # Allows you to use a custom
                    skill to display the date and time.  When NOT set defaults
                    to "skill-ovos-date-time.openvoiceos"
    "examples_skill": "ovos-skills-info.openvoiceos",  # Allows use of a custom
                    skill for the examples.  When NOT set, defaults to use
                    "ovos_skills_manager.utils.get_skills_example()" function
    "wallpaper": "default.jpg",  # Allows a custom wallpaper url. Use complete url
                    without any tilde `~`
    "persistent_menu_hint": false,  # When true displays a hint of the pull-down
                    menu at the top of the page
    "examples_enabled": true,  # When false, the examples at the bottom of the screen
                    will Not be visible
    "randomize_examples": true,  # When false, the rotation of the examples will
                    follow the way they are loaded in the list instead of a random example
    "examples_prefix": true  # When false, the prefix 'Ask Me' will NOT be displayed
                    with the examples
}
```

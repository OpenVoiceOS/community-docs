# GUI Architecture
## Introduction

OVOS devices with displays provide skill developers the opportunity to create skills that can be empowered by both voice and screen interaction. 

The display interaction technology is based on the QML user interface markup language that gives you complete freedom to create in-depth innovative interactions without boundaries or provide you with simple templates within the Mycroft GUI framework that allow minimalistic display of text and images based on your skill development specifics and preferences.

## Framework

Mycroft-GUI is an open source visual and display framework for Mycroft running on top of KDE Plasma Technology and built using Kirigami a lightweight user interface framework for convergent applications which are empowered by Qt.

## Introduction to QML

QML user interface markup language is a declarative language built on top of Qt's existing strengths designed to describe the user interface of a program: both what it looks like, and how it behaves. QML provides modules that consist of sophisticated set of graphical and behavioral building elements.

A collection of resources to familiarize you with QML and Kirigami Framework.

* [Introduction to QML ](http://doc.qt.io/qt-5/qml-tutorial.html)
* [Introduction to Kirigami](https://www.kde.org/products/kirigami/)
## GUI Extensions

OVOS Core supports a GUI Extension framework which allows the GUI service to incorporate additional behaviour for a
specific platform. GUI Extensions currently supported:
### Smartspeaker Extension

This extension is responsible for managing the smartspeaker GUI interface behaviour, it supports homescreens and
homescreen management. Enabling the smartspeaker GUI extension:

### Bigscreen Extension

This extension is responsible for managing the plasma bigscreen GUI interface behaviour, it supports window management
and window behaviour control on specific window managers like Kwin. Enabling the Bigscreen GUI extension:

### Mobile Extension

This extension is responsible for managing the mobile GUI interface behaviour, it supports homescreens and additionally
adds support for global page back navigation. Enabling the Mobile GUI extension:

### Generic Extension

This extension provides a generic GUI interface and does not add any additional behaviour,
it optionally supports homescreens if the platform or user manually enables it.
This extension is enabled by default when no other extension is specified.

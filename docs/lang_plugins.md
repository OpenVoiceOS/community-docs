# Language Detection/Translation Plugins

These plugins can be used to detect the language of text and to translate it

They are not used internally by ovos-core but are integrated with external tools

neon-core also makes heavy use of OPM language plugins

## List of Language plugins

| Plugin                                                                                                 | Detect | Tx  | Offline | Type              |
|--------------------------------------------------------------------------------------------------------|--------|-----|---------|-------------------|
| [neon-lang-plugin-cld2](https://github.com/NeonGeckoCom/neon-lang-plugin-cld2)                         | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-cld3](https://github.com/NeonGeckoCom/neon-lang-plugin-cld3)                         | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-langdetect](https://github.com/NeonGeckoCom/neon-lang-plugin-langdetect)             | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-fastlang](https://github.com/NeonGeckoCom/neon-lang-plugin-fastlang)                 | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-lingua_podre](https://github.com/NeonGeckoCom/neon-lang-plugin-lingua_podre)         | yes    | no  | yes     | FOSS              |
| [neon-lang-plugin-libretranslate](https://github.com/NeonGeckoCom/neon-lang-plugin-libretranslate)     | yes    | yes | no      | API (self hosted) |
| [neon-lang-plugin-apertium](https://github.com/NeonGeckoCom/neon-lang-plugin-apertium)                 | no     | yes | no      | API (self hosted) |
| [neon-lang-plugin-amazon_translate](https://github.com/NeonGeckoCom/neon-lang-plugin-amazon_translate) | yes    | yes | no      | API (key)         |
| [neon-lang-plugin-google_translate](https://github.com/NeonGeckoCom/neon-lang-plugin-google_translate) | yes    | yes | no      | API (key)         |

# Open Linguistika
[Open Linguistika](https://github.com/OpenVoiceOS/Open-Linguistika) is a tool to allow Mycroft Skill developers working on GUI’s to easily translate their GUI’s to other languages.

For Mycroft’s GUI, the UI interface used currently by Mycroft for which you can find QML files under the UI directory of skills, is based on Qt. Mycroft GUI uses Qt’s translation mechanism to translate GUI’s to other languages.

To get your skills GUI translated and ready for other languages involves several manual steps from running Qt tools like lupdate against each QML UI file for each translatable language to running Qt’s tool lrelease for specific language targets to compile a language for the QT environment to understand. To make your developer experience smarter and easier the OpenVoiceOS team is introducing an all-in-one toolkit for GUI language translations.

The Open Linguistika toolkit allows developers to use auto-translate from various supported translator providers, and additionally support more languages, with the possibility for manual translations without having to go through the different Qt tools and command chain required to manually support a skill GUI for a different language.

As a GUI skill Developer, the only know-how you need is to add the translation calls to your skill QML files, Developers can get more information about how to add them here Internationalization and Localization with Qt Quick | Qt 6.3.

The “TLDR” version is that for every hard-coded string in your QML UI skill file you need to decorate your strings with the qsTr() decorator and your model list elements with the QT_TR_NOOP() decorator.

Open Linguistika when installed by default on your distribution by choice, currently supports 6 European languages and 2 auto-translation providers.

The tool provides extensibility through its JSON configuration interface to add more language support, where using a simple JSON language addition mechanism you can extend the tool to support a number of additional languages you would like to support for your skills UI. You can read more about adding additional languages on the tool’s GitHub repository.

How-To-Use Demo:
[![Watch the video](https://img.youtube.com/vi/s2EZyBHRXeA/maxresdefault.jpg)](https://www.youtube.com/watch?v=s2EZyBHRXeA)

# Playing music

For playing music (and video as discussed within the next chapter), OpenVoiceOS uses OCP (OpenVoiceOS Common Play) and is basically a full fledge multimedia player on its own designed around open standards like MPRIS and with the vision of being fully integrated within the OpenVoiceOS software stack.

Skills designed for OCP provide search results for OCP (think about them as media providers/catalogs/scrapers), OCP will play the best search result for you.
OpenVoiceOS comes with a few OCP skills pre-installed, however more can be installed just like any other OVOS skill. 

You can find more OCP skills in the [awesome-ocp-skills](https://github.com/OpenVoiceOS/awesome-ocp-skills) list 

## Youtube Music

A voiceassistant with smartspeaker functionality should be able to play music straight out of the box. For that reason the buildroot edition of OpenVoiceOS comes with the Youtube Music OCP Skill pre-installed. 
Just ask it to play something will start playback from Youtube assuming the asked sonmg is present on Youtube ofcourse.

> Hey Mycroft, play disturbed sound of silence

This should just start playing utilizing OCP as shown below. More information about the full functionality of OCP can be found at its own chapter.
![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20OCP%20Playing%201.png)

## Play the news

Nothing more relaxing after you woke up, cancelling your alarm set on you OpenVoiceOS device than listening to your favorite news station while drinking some coffee (No OpenVoiceOS can not make you that coffee yet).

> Hey Mycroft, play the BBC news

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20News%20skill%20BBC.png)

## Some more features that come out of the box

The whole OCP framework has some benefits and features that are not skill specific, such as "Playlists" and a view of the search results. You can access those by swiping to the right when something is playing.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/Screenshot%20-%20OCP%202nd%20screen%20results.png)

## Homescreen widget

The homescreen skill that comes pre-installed with OpenVoiceOS also comes with a widget for the OCP framework.

![](https://raw.githubusercontent.com/OpenVoiceOS/ovos_assets/master/Images/homescreen-mediawidget.gif)

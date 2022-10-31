# Developer FAQ

* [How do I know what is currently happening in the GUI?](#how-do-i-know-what-is-currently-happening-in-the-gui)
* [How do I stop an intent mid execution?](#how-do-i-stop-an-intent-mid-execution)
* [How do I send files over the bus?](#how-do-i-send-files-over-the-bus)
* [How do I use OAuth in a skill?](#how-do-i-use-oauth-in-a-skill)
* [How do I manage remote skill settings?](#how-do-i-manage-remote-skill-settings-)
* [How do I share data between devices?](#how-do-i-share-data-between-devices-)
* [How do I use Geolocation backend services?](#how-do-i-use-geolocation-backend-services-)
* [How do I use Weather backend services?](#how-do-i-use-weather-backend-services-)
* [How do I use WolframAlpha backend services?](#how-do-i-use-wolframalpha-backend-services-)


## How do I know what is currently happening in the GUI?

```python
from ovos_utils.gui import GUITracker
from ovos_workshop.skills import OVOSSkill
from mycroft import intent_handler


class MyGUIEventTracker(GUITracker):
    # GUI event handlers
    # skill can/should subclass this
    
    def on_idle(self, namespace):
        print("IDLE", namespace)
        timestamp = self.idle_ts

    def on_active(self, namespace):
        # NOTE: page has not been loaded yet
        # event will fire right after this one
        print("ACTIVE", namespace)
        # check namespace values, they should all be set before this event
        values = self.gui_values[namespace]

    def on_new_page(self, page, namespace, index):
        print("NEW PAGE", namespace, index, namespace)
        # check all loaded pages
        for n in self.gui_pages:  # list of named tuples
            nspace = n.name  # namespace / skill_id
            pages = n.pages  # ordered list of page uris

    def on_gui_value(self, namespace, key, value):
        # WARNING this will pollute logs quite a lot, and you will get
        # duplicates, better to check values on a different event,
        # demonstrated in on_active
        print("VALUE", namespace, key, value)


class MySkill(OVOSSkill): 
    def initialize(self):
        self.tracker = MyGUIEventTracker(bus=self.bus)
    
    @intent_handler("gui.status.intent")
    def handle_status_intent(self, message):
        print("device has screen:", self.tracker.can_display())
        print("mycroft-gui installed:", self.tracker.is_gui_installed())
        print("gui connected:", self.tracker.is_gui_connected())
        # TODO - speak or something
            
    @intent_handler("list.idle.screens.intent")
    def handle_idle_screens_intent(self, message):
        # check registered idle screens
        print("Registered idle screens:")
        for name in self.tracker.idle_screens:
            skill_id = self.tracker.idle_screens[name]
            print("   - ", name, ":", skill_id)
            # TODO - speak or something
```

## How do I stop an intent mid execution?

Sometimes you want to abort a running intent immediately, the stop method may not be enough in some circumstances
we provide a `killable_intent` decorator in `ovos_workshop` that can be used to abort a running intent immediately

a common use case is for GUI interfaces where the same action may be done by voice or clicking buttons, in this case you may need to abort a running `get_response` loop

```python
from ovos_workshop.skills import OVOSSkill
from ovos_workshop.decorators import killable_intent
from mycroft import intent_handler
from time import sleep


class Test(OVOSSkill):
    """
    send "mycroft.skills.abort_question" and confirm only get_response is aborted
    send "mycroft.skills.abort_execution" and confirm the full intent is aborted, except intent3
    send "my.own.abort.msg" and confirm intent3 is aborted
    say "stop" and confirm all intents are aborted
    """
    def __init__(self):
        super(Test, self).__init__("KillableSkill")
        self.my_special_var = "default"

    def handle_intent_aborted(self):
        self.speak("I am dead")
        # handle any cleanup the skill might need, since intent was killed
        # at an arbitrary place of code execution some variables etc. might
        # end up in unexpected states
        self.my_special_var = "default"

    @killable_intent(callback=handle_intent_aborted)
    @intent_handler("test.intent")
    def handle_test_abort_intent(self, message):
        self.my_special_var = "changed"
        while True:
            sleep(1)
            self.speak("still here")

    @intent_handler("test2.intent")
    @killable_intent(callback=handle_intent_aborted)
    def handle_test_get_response_intent(self, message):
        self.my_special_var = "CHANGED"
        ans = self.get_response("question", num_retries=99999)
        self.log.debug("get_response returned: " + str(ans))
        if ans is None:
            self.speak("question aborted")

    @killable_intent(msg="my.own.abort.msg", callback=handle_intent_aborted)
    @intent_handler("test3.intent")
    def handle_test_msg_intent(self, message):
        if self.my_special_var != "default":
            self.speak("someone forgot to cleanup")
        while True:
            sleep(1)
            self.speak("you can't abort me")
```

## How do I send files over the bus?

Sometimes you may want to send files or binary data over the messagebus, `ovos_utils` provides some tools to make this easy

Sending a file
```python
from ovos_utils.messagebus import send_binary_file_message, decode_binary_message
from ovos_workshop.skills import OVOSSkill


class MySkill(OVOSSkill): 
    def initialize(self):
        self.add_event("mycroft.binary.file", self.receive_file)
    
    def receive_file(self, message):
        print("Receiving file")
        path = message.data["path"]  # file path, extract filename if needed
        binary_data = decode_binary_message(message)
        # TODO process data somehow
        
    def send_file(self, my_file_path):
        send_binary_file_message(my_file_path)
```

Sending binary data directly
```python
from ovos_utils.messagebus import send_binary_data_message, decode_binary_message
from ovos_workshop.skills import OVOSSkill


class MySkill(OVOSSkill):
    def initialize(self):
        self.add_event("mycroft.binary.data", self.receive_binary)
    
    def send_data(self, binary_data):
        send_binary_data_message(binary_data)

    def receive_binary(self, message):
        print("Receiving binary data")
        binary_data = decode_binary_message(message)
         # TODO process data somehow
```


## How do I use OAuth in a skill?

Retrieving the tokens in a skill does not depend on the selected backend, the mechanism to register a token is backend
specific

First you need to authorize the application, this can be done
with [ovos-config-assistant](https://github.com/OpenVoiceOS/ovos-config-assistant) if running offline
or [ovos-backend-manager](https://github.com/OpenVoiceOS/ovos-backend-manager) if using personal backend

If using selene there is no automated process to add a
token, [you need to contact](https://chat.mycroft.ai/community/pl/ynftpfuwo3gubxmta5qqronpch) support@mycroft.ai

```python
from ovos_backend_client.api import OAuthApi, BackendType

# api = OAuthApi()  # determine oauth backend from mycroft.conf
api = OAuthApi(backend_type=BackendType.OFFLINE)  # explicitly use ovos-backend-manager oauth
token_json = api.get_oauth_token("spotify")
```

## How do I manage remote skill settings?

To interact with skill settings via DeviceApi

```python
from ovos_backend_client.settings import RemoteSkillSettings

# in ovos-core skill_id is deterministic and safe
s = RemoteSkillSettings("skill.author")
# in mycroft-core please ensure a valid remote_id
# in MycroftSkill class you can use
# remote_id = self.settings_meta.skill_gid
# s = RemoteSkillSettings("skill.author", remote_id="@|whatever_msm_decided")
s.download()

s.settings["existing_value"] = True
s.settings["new_value"] = "will NOT show up in UI"
s.upload()

# auto generate new settings meta for all new values before uploading
s.settings["new_value"] = "will show up in UI"
s.generate_meta()  # now "new_value" is in meta
s.upload()


```

## How do I share data between devices?

by hijacking skill settings we allow storing arbitrary data via DeviceApi and use it across devices and skills

```python
from ovos_backend_client.cloud import SeleneCloud

cloud = SeleneCloud()
cloud.add_entry("test", {"secret": "NOT ENCRYPTED MAN"})
data = cloud.get_entry("test")
```

an encrypted version is also supported if you don't trust the backend!

```python
from ovos_backend_client.cloud import SecretSeleneCloud

k = "D8fmXEP5VqzVw2HE"  # you need this to read back the data
cloud = SecretSeleneCloud(k)
cloud.add_entry("test", {"secret": "secret data, selene cant read this"})
data = cloud.get_entry("test")
```

![](https://matrix-client.matrix.org/_matrix/media/r0/download/matrix.org/SrqxZnxzRNSqJaydKGRQCFKo)

## How do I use Geolocation backend services?

```python
from ovos_backend_client.api import GeolocationApi

geo = GeolocationApi()
data = geo.get_geolocation("Lisbon Portugal")
```

## How do I use Weather backend services?

```python
from ovos_backend_client.api import OpenWeatherMapApi

owm = OpenWeatherMapApi()
data = owm.get_weather()
# dict - see api docs from owm onecall api
```

## How do I use WolframAlpha backend services?

```python
from ovos_backend_client.api import WolframAlphaApi

wolf = WolframAlphaApi()
answer = wolf.spoken("what is the speed of light")
# The speed of light has a value of about 300 million meters per second

data = wolf.full_results("2+2")
# dict - see api docs from wolfram
```

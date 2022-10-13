# Developer FAQ

* [How do I use OAuth in a skill?](#how-do-i-use-oauth-in-a-skill)
* [How do I manage remote skill settings?](#how-do-i-manage-remote-skill-settings-)
* [How do I share data between devices?](#how-do-i-share-data-between-devices-)
* [How do I use Geolocation backend services?](#how-do-i-use-geolocation-backend-services-)
* [How do I use Weather backend services?](#how-do-i-use-weather-backend-services-)
* [How do I use WolframAlpha backend services?](#how-do-i-use-wolframalpha-backend-services-)


## How do I use OAuth in a skill?

Retrieving the tokens in a skill does not depend on the selected backend, the mechanism to register a token is backend specific

First you need to authorize the application, this can be done with [ovos-backend-manager](https://github.com/OpenVoiceOS/ovos-backend-manager) if running offline or using personal backend

If using selene there is no automated process to add a token, [you need to contact](https://chat.mycroft.ai/community/pl/ynftpfuwo3gubxmta5qqronpch) support@mycroft.ai

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

## Developer FAQ

+ [How do I use OAuth in a skill?](#how-do-i-use-oauth-in-a-skill)

### How do I use OAuth in a skill?

Retrieving the tokens in a skill does not depend on the selected backend, the mechanism to register a token is backend specific

First you need to authorize the application, this can be done with [ovos-backend-manager](https://github.com/OpenVoiceOS/ovos-backend-manager) if running offline or using personal backend

If using selene there is no automated process to add a token, [you need to contact](https://chat.mycroft.ai/community/pl/ynftpfuwo3gubxmta5qqronpch) support@mycroft.ai

```python
from ovos_backend_client.api import OAuthApi, BackendType

# api = OAuthApi()  # determine oauth backend from mycroft.conf
api = OAuthApi(backend_type=BackendType.OFFLINE)  # explicitly use ovos-backend-manager oauth
token_json = api.get_oauth_token("spotify")
```

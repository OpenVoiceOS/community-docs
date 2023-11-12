# OpenVoiceOS Security

## Securing SSH
Most of our guides have you create a user called ovos with a password of ovos, while this makes install easy, it's VERY insecure.  As soon as possible, you should secure ssh using a key and disable password authentication.

### When connecting from a Linux or MacOS client
Create a keyfile (you can change ovos to whatever you want)
```
ssh-keygen -t ed25519 -f ~/.ssh/ovos
```

Copy to host (use the same filename as above, specify the user and hostname you are using)
```
ssh-copy-id -i ~/.ssh/ovos  ovos@mycroft
```
On your dekstop, edit ~/.ssh/config and add the following lines
``` 
Host rp2
  user ovos
  IdentityFile ~/.ssh/ovos
```
On your ovos system, edit /etc/ssh/sshd_config and add or uncomment the following line:
``` 
PasswordAuthentication no
```
restart sshd or reboot
``` 
sudo systemctl restart sshd
```

### Message Bus Security
Anything connected to the bus can fully control OVOS, and OVOS usually has full control over the whole system!

You can read more about the security issues over at [Nhoya/MycroftAI-RCE](https://github.com/Nhoya/MycroftAI-RCE)

in mycroft-core all skills share a bus connection, this allows malicious skills to manipulate it and affect other skills

you can see a demonstration of this problem with [BusBrickerSkill](https://github.com/EvilJarbas/BusBrickerSkill)

`"shared_connection": false` ensures each skill gets its own websocket connection and avoids this problem

Additionally, it is recommended you change `"host": "127.0.0.1"`, this will ensure no outside world connections are allowed


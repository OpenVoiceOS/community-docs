# How to Secure SSH
Most of our guides have you create a user called ovos with a password of ovos, while this makes install easy, it's VERY insecure.  As soon as possible, you should secure ssh using a key and disable password authentication.

## When connecting from a Linux or MacOS client
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
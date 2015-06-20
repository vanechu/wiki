---
title: "Use SSH Keys with Server"
layout: page
date: 2015-06-20 00:00
---

## Step One — Create the RSA Key Pair


```
ssh-keygen -t rsa
```

## Step Two — Copy the SSH Keys

You can usually get this key by copying the results of:

```
cat ~/.ssh/id_rsa.pub
```

Copy it into your control panel.(Github or DigitalOcean)

## Step Three — Spin Up a New Server
In order to add additional keys to pre-existing droplets, you can paste in the keys using SSH:

```
cat ~/.ssh/id_rsa.pub | ssh root@[your.ip.address.here] "cat >> ~/.ssh/authorized_keys"
```


## Step Four — Connect to Server


```
ssh root@[your.ip.address.here]
```


## Step Five - Lockdown Root SSH Access to Keys Only

After you have confirmed that you can now login as root to the server without being prompted for a password you can disable password logins for root. This makes your server more secure since no one can brute force your SSH password.

It's necessary to edit the server's SSHd configuration /etc/ssh/sshd_config and update the following line to now read:

```
PermitRootLogin without-password
```

Now it's necessary to restart or rehup the sshd process to have it re-read the new configuration. This can be done via the following:

```
# ps auxw | grep ssh
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root       681  0.0  0.1  49948  2332 ?        Ss    2012   3:23 /usr/sbin/sshd -D
```

```
# kill -HUP 681
```

Now your server's root login is protected and you can test this by trying to SSH directly as root to this server from a system that doesn't have its keys shared and you will be automatically kicked out without being prompted for a root password.



## Remote Deployment

### rsync

- -r recursive - recurse into directories
- -u update - skip files that are newer on the receiver
- -i itemize - output a change summary

```
rsync -rui ./* xxx@laxxx.org:/path/wiki.laxxx.org/public_html/
```


# Reference #

[SHow To Use SSH Keys with DigitalOcean Droplets](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-keys-with-digitalocean-droplets)
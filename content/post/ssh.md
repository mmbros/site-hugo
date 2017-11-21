---
title: "SSH"
date: 2017-11-21T18:45:47+01:00
subtitle: ""
tags: [ssh]
---

##  Key authentication
* [How To Configure SSH Key-Based Authentication on a Linux Server](https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server)
* [How To Set Up SSH Keys ](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2)


## Configuration file

* [Simplify Your Life With an SSH Config File](http://nerderati.com/2011/03/17/simplify-your-life-with-an-ssh-config-file/)
* [ssh returns “Bad owner or permissions on ~/.ssh/config”](https://serverfault.com/questions/253313/ssh-returns-bad-owner-or-permissions-on-ssh-config) 


### Example

Enter the SSH config file:

    # contents of $HOME/.ssh/config
    Host rpi
        HostName 192.168.1.2
	    Port 22
		User fooey

This means that I can simply `$ ssh rpi`, and the options will be read from the configuration file.


### Permissions and ownership

In case of `Bad owner or permissions on ~/.ssh/config` error,
set proper permissions and ownership to fix it.

1. config file must have rw for user only permissions,

        chmod 600 ~/.ssh/config

2. the user must be the file owner.

        chown $USER ~/.ssh/config



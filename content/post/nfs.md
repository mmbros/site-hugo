+++
date = "2015-11-01T23:12:31+01:00"
draft = true
title = "NFS - Network File System"
tags = ["linux", "nfs"]

+++


[Network File System](https://en.wikipedia.org/wiki/Network_File_System), a distributed file system protocol

## Client

### fstab

#### Delaying a NFS mount in `/etc/fstab` on system boot.

Mounts as `noauto,users` makes it possible for a user to mount it whenever its ready.

    192.168.1.2:/export/share /media/SHARED nfs noauto,users,defaults 0 0


## Server

---
title: "Crypt"
author: ""
type: ""
date: 2019-03-09T21:31:14+01:00
subtitle: ""
image: ""
tags: ["crypt"]
---

## Linux Hard Disk Encryption With LUKS [ cryptsetup Command  ]

[Credits](https://www.cyberciti.biz/hardware/howto-linux-hard-disk-encryption-with-luks-cryptsetup-command/)

I will explain how to encrypt your partitions using Linux Unified Key Setup-on-disk-format (LUKS) on your Linux based computer or laptop.


### Step #1: Install cryptsetup utility

You need to install the following package. It contains cryptsetup, a utility for setting up encrypted filesystems using Device Mapper and the dm-criypt target. Debian / Ubuntu Linux user type the following apt-get command or apt command:

	# apt install cryptsetup


### Step #2: Configure LUKS partition

In this example, I’m going to encrpt `/dev/sdc1`. Type the following command:

	# cryptsetup -y -v luksFormat /dev/sdc1

Sample outputs:

	WARNING!
	========
	This will overwrite data on /dev/sdc1 irrevocably.

	Are you sure? (Type uppercase yes): YES
	Enter LUKS passphrase:
	Verify passphrase:
	Command successful.

This command initializes the volume, and sets an initial key or passphrase. Please note that the passphrase is not recoverable so do not forget it.

Type the following command create a mapping:

	# cryptsetup luksOpen /dev/sdc1 backup2

You can see a mapping name `/dev/mapper/backup2` after successful verification of the supplied key material which was created with luksFormat command extension:

	# ls -l /dev/mapper/backup2

Sample outputs:

	lrwxrwxrwx 1 root root 7 mar  9 21:51 /dev/mapper/backup2 -> ../dm-0

You can use the following command to see the status for the mapping:

	# cryptsetup -v status backup2

Sample outputs:

	/dev/mapper/backup2 is active.
	  type:    LUKS1
	  cipher:  aes-xts-plain64
	  keysize: 256 bits
	  key location: dm-crypt
	  device:  /dev/sdc1
	  sector size:  512
	  offset:  4096 sectors
	  size:    15970240 sectors
	  mode:    read/write
	Command successful.

You can dump LUKS headers using the following command:

	# cryptsetup luksDump /dev/sdc1

Sample outputs:

	LUKS header information for /dev/sdc1

	Version:       	1
	Cipher name:   	aes
	Cipher mode:   	xts-plain64
	Hash spec:     	sha256
	Payload offset:	4096
	MK bits:       	256
	MK digest:     	2b 22 92 4a 28 ad 98 b1 72 b4 8a 31 9b 48 ca a3 d4 09 df e6 
	MK salt:       	70 d8 f3 7b c9 a4 e0 ca 18 d5 b7 3c 34 51 98 fe 
	               	43 85 50 f9 22 fd a0 cf f1 63 3a f0 27 40 6f 93 
	MK iterations: 	158490
	UUID:          	4fe7b1af-07a0-4b7b-8617-5a2d84f58a9d

	Key Slot 0: ENABLED
		Iterations:         	2535854
		Salt:               	0c 56 4a 83 3a 68 7a fc eb ab da b9 e8 32 46 06 
		                      	f3 a5 e5 b8 4d a9 66 d3 6f 44 52 b9 1a 5f 46 80 
		Key material offset:	8
		AF stripes:            	4000
	Key Slot 1: DISABLED
	Key Slot 2: DISABLED
	Key Slot 3: DISABLED
	Key Slot 4: DISABLED
	Key Slot 5: DISABLED
	Key Slot 6: DISABLED
	Key Slot 7: DISABLED


### Step #3: Format LUKS partition

First, you need to write zeros to `/dev/mapper/backup2` encrypted device. This will allocate block data with zeros. This ensures that outside world will see this as random data i.e. it protect against disclosure of usage patterns:

	# dd if=/dev/zero of=/dev/mapper/backup2 status=progress

Sample outputs:

	8053063680 bytes (8,1 GB, 7,5 GiB) copied, 959 s, 8,4 MB/s
	dd: error writing '/dev/mapper/backup2': No space left on device
	61+0 records in
	60+0 records out
	8176762880 bytes (8,2 GB, 7,6 GiB) copied, 1024,17 s, 8,0 MB/s

Next, create a filesystem i.e. format filesystem, enter:

	# mkfs.ext4 /dev/mapper/backup2

Sample outputs:

	mke2fs 1.44.1 (24-Mar-2018)
	Creating filesystem with 1996280 4k blocks and 499712 inodes
	Filesystem UUID: 7e6ec344-5591-4b73-8ab9-61984ba95899
	Superblock backups stored on blocks:
		32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

	Allocating group tables: done
	Writing inode tables: done
	Creating journal (16384 blocks): done
	Writing superblocks and filesystem accounting information: done

To mount the new filesystem at `/media/crypt`, enter:

	# mkdir /media/crypt
	# mount /dev/mapper/backup2 /media/crypt
	# df -H
	# cd /media/crypt
	# ls -l

### How do I unmount and secure data?

Type the following commands:

	# umount /media/crypt
	# cryptsetup luksClose backup2


### How do I mount or remount encrypted partition?

Type the following command:

	# cryptsetup luksOpen /dev/sdc1 backup2
	# mount /dev/mapper/backup2 /media/crypt
	# df -H
	# mount


### How do I change LUKS passphrase (password) for encrypted partition?

Type the following command

	### see key slots, max -8 i.e. max 8 passwords can be setup for each device ####
	# cryptsetup luksDump /dev/sdc1
	# cryptsetup luksAddKey /dev/sdc1

	Enter any passphrase:
	Enter new passphrase for key slot:
	Verify passphrase:

Remove or delete the old password:

	# cryptsetup luksRemoveKey /dev/sdc1

Please note that you need to enter the old password / passphrase.

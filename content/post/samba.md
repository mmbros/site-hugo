---
title: "Samba"
date: 2017-11-15T20:28:15+01:00
subtitle: ""
tags: ["samba"]
---


### Installazione

1. Installazione dei pacchetti necessari:

        # apt-get install samba

2. Ferma il servizio:

        # service smbd stop

    Attenzione a non usare "samba" come servizio:
	nelle distribuzioni Debian e derivate il nome del servizio è stato cambiato da "samba" a "smbd".

3. Salva il file di configurazione originale:

        # cp /etc/samba/smb.conf /etc/samba/smb.conf.old

4. Edita il file di configurazione ``/etc/samba/smb.conf``:

        [globals]

        ### authentication ###
        security = user
        encrypt password = true

        [shared]
		comment = File multimediali
		path = /media/disk/
		browsable = yes
		writeble = yes
		guest ok = no
		validusers = @sambashare


### Creazione di un utente per Samba

Crea l'utente ``sambauser`` senza home directory e senza shell
e lo assegna al gruppo ``sambashare`` che è stato creato con
l'installazione di samba:

    # useradd sambauser --no-create-home --shell /bin/false -g sambashare

Imposta la SMB password dell'utente ``sambauser``:

    # smbpasswd -a sambauser
	****


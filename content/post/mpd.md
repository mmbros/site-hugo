---
title: "MPD"
author: ""
type: ""
date: 2019-09-09T22:30:04+02:00
subtitle: ""
image: ""
tags: ["mpd"]
---


### Clients

Given the following `mpd.conf` server configuration

    ...
	audio_outputi {
		type  "shout"
		name  "MPD stream on Raspberry Pi"
		host  "localhost"  # -> 192.168.1.2
		port  "8000"
		mount "/mpd"
	}
	...


the client will read the stream from URL:

    http://192.168.1.2:8000/mpd


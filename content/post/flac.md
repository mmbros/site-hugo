---
title: "Flac"
date: 2019-02-24T18:00:56+01:00
draft: true
tags: ["music"]
---


## How do I split a flac with a cue?

- https://unix.stackexchange.com/questions/10251/how-do-i-split-a-flac-with-a-cue



I only know a CLI way. You will need `cuetools` and `shntool`.

```
cuebreakpoints file.cue | shnsplit -o flac file.flac
cuetag.sh file.cue "split-*".flac
```





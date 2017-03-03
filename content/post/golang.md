+++
date = "2015-10-31T23:12:13+01:00"
draft = true
title = "The Go Programming Language"
tags = ["golang", "programming-language"]
+++

Go is an open source programming language that makes it easy to build simple,
reliable, and efficient software

* [golang.org](https://golang.org/)
* [wikipedia.en](https://en.wikipedia.org/wiki/Go_%28programming_language%29)

## Installation

Install to a custom location and workspace setup:

* [GOROOT](https://golang.org/doc/install#tarball): `$HOME/local/go`
* [GOPATH](https://golang.org/doc/code.html#GOPATH): `$HOME/Code/go`

For full install instruction see [Getting Started](https://golang.org/doc/install).

[Download the archive](https://golang.org/dl/) and extract the archive into the destination folder.
For example extract the archive into `$HOME/local`, creating a Go tree in `$HOME/local/go`:

    tar -C $HOME/local -xzf go$VERSION.$OS-$ARCH.tar.gz

Assuming that `$HOME/local/bin` is in `$PATH`,
create in the `$HOME/local/bin` folder the symlinks to the `$HOME/local/go/bin` files:

    for i in $HOME/local/go/bin/\*; do ln -s "$i" $(basename "$i"); done

Add the following commands to $HOME/.profile:

    export GOROOT=$HOME/local/go
    export GOPATH=$HOME/Code/go

Note: `GOROOT` must be set only when installing to a custom location.


# NOTES

## train
[train](https://github.com/shaoshing/train) Asset Management for web app using Golang

## wellington

[Building from Source (any OS)](http://getwt.io/docs/install/)

Prerequisites `go`, `gcc`

    go get github.com/wellington/wellington

If `go get` fails, try the makefile preqrequisites `autotools`, `libtool`

    cd $(GOPATH)/src/github.com/wellington/wellington
    make
    wt -v

Ensure that `$GOPATH/bin` in in `$PATH`.

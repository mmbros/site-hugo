---
title: "Rust"
author: ""
type: ""
date: 2019-06-25T23:16:11+02:00
subtitle: ""
image: ""
tags: ["rust"]
---

## VIM configuration

* [Rust IDE + REPL In Vim](https://startupsventurecapital.com/rust-ide-repl-in-vim-11daa921a2c4)
* [rust-lang/rust.vim](https://github.com/rust-lang/rust.vim)

Edit `.vimrc`


    Plug 'rust-lang/rust.vim'

    let g:rustfmt_autosave = 1

If `:RustFmt` doesn't work, install `rustfmt` and then reload VIM:

    rustup component add rustfmt


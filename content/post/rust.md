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

* [rust-lang/rust.vim][rust.vim]
* [Rust IDE + REPL In Vim](https://startupsventurecapital.com/rust-ide-repl-in-vim-11daa921a2c4)

### Basic support for Rust

The Rust team makes this easy with [rust-lang/rust.vim][rust.vim]
The rust.vim plugin adds the usual: file detection, syntax highlighting,
formatting, etc...

Edit `.vimrc`

    Plug 'rust-lang/rust.vim'

    let g:rustfmt_autosave = 1

If `:RustFmt` doesn't work, install `rustfmt` and then reload VIM:

    rustup component add rustfmt


### Language Server Protocol

After establishing basic support, the next step is getting access to the RLS.
In order to do this you’ll need a plugin to communicate with the language
server. In Vim there is Vim-Lsp and for [Neovim LanguageClient-Neovim](https://github.com/autozimu/LanguageClient-neovim) — also
works with Vim.

    " a basic set up for LanguageClient-Neovim

    " << LSP >> {{{

    let g:LanguageClient_autoStart = 0
    nnoremap <leader>lcs :LanguageClientStart<CR>

    " if you want it to turn on automatically
    " let g:LanguageClient_autoStart = 1

    let g:LanguageClient_serverCommands = {
        \ 'python': ['pyls'],
        \ 'rust': ['rustup', 'run', 'nightly', 'rls'],
        \ 'javascript': ['javascript-typescript-stdio'],
        \ 'go': ['go-langserver'] }

    noremap <silent> H :call LanguageClient_textDocument_hover()<CR>
    noremap <silent> Z :call LanguageClient_textDocument_definition()<CR>
    noremap <silent> R :call LanguageClient_textDocument_rename()<CR>
    noremap <silent> S :call LanugageClient_textDocument_documentSymbol()<CR>
    " }}}

[rust.vim]: https://github.com/rust-lang/rust.vim "rust.vim"

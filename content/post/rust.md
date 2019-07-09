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

{{< highlight vim >}}
Plug 'rust-lang/rust.vim'

let g:rustfmt_autosave = 1
{{< /highlight >}}

If `:RustFmt` doesn't work, install `rustfmt` and then reload VIM:

{{< highlight bash >}}
rustup component add rustfmt
{{< /highlight >}}


### Language Server Protocol

After establishing basic support, the next step is getting access to the RLS.
In order to do this you’ll need a plugin to communicate with the language
server. In Vim there is Vim-Lsp and for [Neovim LanguageClient-Neovim](https://github.com/autozimu/LanguageClient-neovim) — also
works with Vim.

{{< highlight vim >}}
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
{{< /highlight >}}

### RLS

Now we are starting to get to the meaty part — the RLS, or [Rust Language Server][rls]. A brief description from the repo is below.

> The RLS provides a server that runs in the background, providing IDEs, editors, and other tools with information about Rust programs. It supports functionality such as ‘goto definition’, symbol search, reformatting, and code completion, and enables renaming and refactorings.

> The RLS gets its source data from the compiler and from Racer. Where possible it uses data from the compiler which is precise and complete. Where its not possible, (for example for code completion and where building is too slow), it uses Racer.

The installation process is easy enough.

{{< highlight bash >}}
# get rustup
# don't use hombrew
curl https://sh.rustup.rs -sSf | sh

rustup self update

# get nightly compiler
rustup update nightly

# after nightly installed
rustup component add rls-preview --toolchain nightly
rustup component add rust-analysis --toolchain nightly
rustup component add rust-src --toolchain nightly
{{< /highlight >}}

After that, you’ll pass in the commands to your LSP plugin of choice. An example config for LanguageClient-Neovim is provided below.

{{< highlight vim >}}
let g:LanguageClient_serverCommands = {
    \ 'rust': ['rustup', 'run', 'nightly', 'rls']
}
{{< /highlight >}}




[rust.vim]: https://github.com/rust-lang/rust.vim "rust.vim"
[rls]: https://github.com/rust-lang-nursery/rls "RLS"

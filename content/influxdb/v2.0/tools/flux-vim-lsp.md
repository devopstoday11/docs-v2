---
title: Use the Flux Vim LSP plugin
description: >
  Use the Flux Vim LSP plugin.
menu:
  influxdb_2_0:
    parent: Tools & integrations
weight: 102
---

Vim provides support for the [Language Server Protocol](https://microsoft.github.io/language-server-protocol/).
Flux

## Requirements

- Vim 8+
- [npm](https://www.npmjs.com/get-npm)

## Installation

There are two methods:

- [Install with vim-lsp](#install-with-vim-lsp)
- [Install with vim-coc](#install-with-vim-coc)

Both methods require that you add the following to your `.vimrc` so that Vim can recognize the `.flux` file type:

```
" Flux file type
au BufRead,BufNewFile *.flux		set filetype=flux
```

### Install with vim-lsp

1. **Install `flux-lsp-cli` with npm**

    ```
    npm i -g @influxdata/flux-lsp-cli
    ```

2. **Install [vim-lsp](https://github.com/prabirshrestha/vim-lsp)**

    If it doesn't exist yet, create a directory called `pack/<user>/start/` in your `.vim/` and clone `vim-lsp` into it:

    ```sh
    cd ~
    mkdir -p .vim/pack/<user>/start/
    cd .vim/pack/<user>/start/
    git clone https://github.com/prabirshrestha/vim-lsp
    ```

3. **Edit your `.vimrc`**

    Next, edit your `.vimrc` configuration file to include the following:

    ```
    let g:lsp_diagnostics_enabled = 1

    if executable('flux-lsp')
        au User lsp_setup call lsp#register_server({
            \ 'name': 'flux lsp',
            \ 'cmd': {server_info->[&shell, &shellcmdflag, 'flux-lsp']},
            \ 'whitelist': ['flux'],
            \ })
    endif

    autocmd FileType flux nmap gd <plug>(lsp-definition)
    ```

### Install with vim-coc

1. **Install `flux-lsp-cli` from npm**

    ```
    npm i -g @influxdata/flux-lsp-cli
    ```
2. **Install plug-vim**

    Follow the instructions here: https://github.com/junegunn/vim-plug#installation.

    Requires_vim-coc.

vim-coc uses a coc-settings.json file and it is located in your ~/.vim directory.
In order to run the flux-lsp you need to add the flux section in the languageserver.

```json
{
  "languageserver": {
      "flux": {
        "command": "flux-lsp",
        "filetypes": ["flux"]
      }
  }
}
```

If you need to debug what flux-lsp is doing, you can configure it to log to `/tmp/fluxlsp`:

```json
{
  "languageserver": {
      "flux": {
        "command": "flux-lsp",
        "args": ["-l", "/tmp/fluxlsp"],
        "filetypes": ["flux"]
      }
  }
}
```

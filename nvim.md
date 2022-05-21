# Neovim



## Global Keymaps

- `<leader>ec` to edit configuration init.vim

- <leader> = `;`

- <C-z> will supsend neovim and return to bash. when done with shell commands return to neovim by pressing `fg` command on bash

  

## Vim-plug

### List of plugins installed
Vim-plug  https://github.com/junegunn/vim-plug

Vim-aritline  https://github.com/vim-airline/vim-airline

NerdTree https://github.com/preservim/nerdtree 

Vim surround https://github.com/tpope/vim-surround

Vim-Fugitive https://github.com/tpope/vim-fugitive

### Fzf

- https://www.youtube.com/watch?v=qgG5Jhi_Els
- https://dev.to/iggredible/how-to-search-faster-in-vim-with-fzf-vim-36k
- Go to parent dir https://github.com/junegunn/fzf.vim/issues/624
- How to quickly go to `init.vim` using fzf ?
- 

### Vim Fugitive

- `:Gstatus`or `:G` shows the current 'git status'  in a window buffer
  - `-`  on a file will stage `s` or unstage `u`
  - `=` on a file will show the diff or patch for that file
- `-` while in the Gstatus view, the `-` will add the file to be committed
- `D` while in the Gstatus view, `D` will show the diff for the file
- `cc` while in the Gstatus view, cc will transition the pane into a commit message view
- `:Gblame` will show all of the commits for a file along with which developer made the change
- Resolving conflict -http://vimcasts.org/episodes/fugitive-vim-resolving-merge-conflicts-with-vimdiff/
  - In a three way diff view 
    - Be on middle file and `:diffget 2` to apply changes from left
    - Be on middle  buffer and `:diffget 3` to apply changes from right.
    - Avengers_Assemble@Ship2



### Coc-Vim

- Install extensions `:CocInstall coc-json coc-tsserver`
- Or configure language server in coc-settings.json opened by :CocConfig, like:
    ```
    {
      "languageserver": {
        "go": {
          "command": "gopls",
          "rootPatterns": ["go.mod"],
          "trace.server": "verbose",
          "filetypes": ["go"]
        }
      }
    }
    ```



#### [Coc-vim extensions](https://github.com/neoclide/coc.nvim/wiki/Using-coc-extensions)

- `:CocList commands` to open the command list and choose one you need
- `:CocInstall coc-json` to install extensions
- or `let g:coc_global_extensions = ['coc-json', 'coc-git']` in init.vim 
- or `Plug 'neoclide/coc-tsserver', {'do': 'yarn install --frozen-lockfile'}` using vim plugin manager
- Use the command `:CocUpdate` or `:CocUpdateSync` to update all extensions to the latest version.
- Uninstall extension  ex: `:CocUninstall coc-css`
- List extension `:CocList extensions` 
  - Supported actions (hit `<Tab>` to activate action menu):
    - `toggle` default action. activate/deactivate selected extension(s).
    - `enable`: enable selected extension(s).
    - `disable`: disable selected extension(s).
    - `reload`: reload selected extension(s).
    - `uninstall`: remove selected extension(s).
    - `lock`: toggle lock of extension, locked extension won't be updated by `:CocUpdate`



### vim-startify

- reopen the screen via `:Startify`
- https://www.youtube.com/watch?v=9IcXJvoPHCY
- https://github.com/mhinz/vim-startify/wiki/Plugin-features-in-detail



## Git gutters using signify

- https://www.youtube.com/watch?v=F7JZdAwGmpU
- https://github.com/airblade/vim-gitgutter



### Ripgrep - rg

- https://mariusschulz.com/blog/fast-searching-with-ripgrep
- TODO: Group all the matches in a file togethe





## Colors and Apperance

- `:colorscheme <SPACE> <TAB>` to view schemes available and `:colorscheme NAME` to enable.

### Themes

https://www.nordtheme.com/ports/vim





## Configuration Resources:

- https://medium.com/geekculture/neovim-configuration-for-beginners-b2116dbbde84
- https://gist.github.com/subfuzion/7d00a6c919eeffaf6d3dbf9a4eb11d64
- https://github.com/Optixal/neovim-init.vim
- https://dev.to/reobin/reload-init-vim-without-restarting-neovim-1h82
- 
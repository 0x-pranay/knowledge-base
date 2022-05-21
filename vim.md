## Moving around

### using marks

- : `7G` Goto line number 7

- :h :marks
- `:h navigation`
-  `ma` to mark a position in a file as `a`
- `'a`'  to jump to the mark named a 
- `:marks` list all marks
- `delm[arks] {marks}` Delete the specified marks.
- 

## Registers

 https://www.brianstorti.com/vim-registers/

## Buffers:

 https://www.oreilly.com/library/view/learning-the-vi/9780596529833/ch04s03.html

### Working with buffers

- `:new` command creates a new window displaying the contents of a new (empty) buffer.

- `:ls` to list all buffers. `:help :ls` to know more

- `Ctrl-W` + `hjkl` to  move between windows in a same tab.

- `:vsp` Split window veritically

- `:bdelete fileName` to delete a buffer

- `:%bdelete` Delete all buffers except current one

  

## Find and Replace:

 https://linuxize.com/post/vim-find-replace/



## Terminal

- `:vnew term://zsh` Open a terminal in a vertical new window.

- `:help terminal-emulator` for mapping suggestions

  - `:tnoremap <Esc> <C-\><C-n>`  maps escape button to exit terminal mode

  - ```
    To use `ALT+{h,j,k,l}` to navigate windows from any mode: >
        :tnoremap <A-h> <C-\><C-N><C-w>h
        :tnoremap <A-j> <C-\><C-N><C-w>j
        :tnoremap <A-k> <C-\><C-N><C-w>k
        :tnoremap <A-l> <C-\><C-N><C-w>l
        :inoremap <A-h> <C-\><C-N><C-w>h
        :inoremap <A-j> <C-\><C-N><C-w>j
        :inoremap <A-k> <C-\><C-N><C-w>k
        :inoremap <A-l> <C-\><C-N><C-w>l
        :nnoremap <A-h> <C-w>h
        :nnoremap <A-j> <C-w>j
        :nnoremap <A-k> <C-w>k
        :nnoremap <A-l> <C-w>l
    
    ```

- Terminal emuilator : https://thoughtbot.com/upcase/videos/neovims-terminal-emulator#:~:text=In%20NeoVim%2C%20we%20can%20launch,in%20the%20shell%20as%20usual.&text=When%20we%20exit%20the%20shell,back%20to%20a%20regular%20buffer.

- `:tab new` open a termnial in a new tab

- `:tab term` Opens a terminal in a new tab.



## Windows

- `:h window` 
- `CTRL-W` for window . `s` split , `v` vertical split, `n` New window, :jk





## External commands and Retrieving

- `:!`execute an external command ex: `:!ls`
- `:r` Retriieves the disk file and puts it below the cursor position. reads any stream and puts it below cursor
- ex: `:r !ls` reads the output of ls and put it below the cursor position



# Screen Movement

```
+-------------------------------+
^                               |
|c-e (keep cursor)              |
|H(igh)             zt (top)    |
|                   ^           |
|           ze      |      zs   |
|M(iddle)  zh/zH <--zz--> zl/zL |
|                   |           |
|                   v           |
|L(ow)              zb (bottom) |
|c-y (keep cursor)              |
v                               |
+-------------------------------+
```

adding to other answers also pay attention to `ze` and `zs`, meaning: move screen to the left/right of the cursor

below I paste my mnemonic for scrolling also look at the position of `h` and `l` (and `t` and `b`) on the keyboard to remember where the screen is moving 

[slackoverflow](https://stackoverflow.com/questions/5989739/horizontal-navigation-in-long-lines#:~:text=You%20just%20press%20z%20once,you%20press%20any%20other%20key.)




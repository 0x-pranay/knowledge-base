`:lua print('hello world')`  Run lua commands in command mode

Inside the init.vim we can run lua code using

```
lua <<EOF
print('hello from lua')
EOF
```



```
lua print('this also works')

-- gets imports config from lua/basic.lua any where in the `runtimepath` of neovim.
lua require('basic')

-- require('usermod.settings')  # dot notation subfolder


```

## Scopes

- general settings

  `vim.o.background = 'light'`

- window-scoped 

  `vim.wo.colorcolumn = '80'`

- Buffer-scoped options

  `vim.bo.filetype = 'lua'`

- Global scope

  `vim.g.mapleader = ' '`

- get or set environment variable

  `vim.env.NAME=  `

- With `vim.opt` we can set global, window and buffer settings.

  ```
  -- buffer-scoped
  vim.opt.autoindent = true
  
  -- window-scoped
  vim.opt.cursorline = true
  
  -- global scope
  vim.opt.autowrite = true
  ```

  

 
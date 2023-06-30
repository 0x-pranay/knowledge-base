More about patterns here: https://neovim.io/doc/user/pattern.html



 Here is the regex to match all req.* but exclude `req.params` and `req._lmClient`  in nvim 

```
/req\.\(params\|_lmclient\)\@!\w\+
```



Ignore case  using `\c` option

```
/fetch\c
```


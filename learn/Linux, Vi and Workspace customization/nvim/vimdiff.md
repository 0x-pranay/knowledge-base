Using vim diff tool to compare two files or two buffers. 

### To compare two buffers which are not saved yet in files. 

Step 1:  `nvim`

step2: open one buffer: `:new` and paste the content in it

step3: open another buffer with vertical split `:vertical new` and paste the other content in it. 

step4: `:windo diffthis` will show the diff.



Sources: 

- http://vimcasts.org/episodes/comparing-buffers-with-vimdiff/
- https://www.freecodecamp.org/news/compare-two-files-in-linux-using-vim/
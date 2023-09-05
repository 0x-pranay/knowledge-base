```bash
$ brightnessctl set 5%-
$ brightnessctl set +5%
```

```bash
$ xev -event keyboard
```

```bash
$ xrandr
```

To watch the network strength of the wifi and other network adapters. 
Updates every sec

```bash
$ watch -n1 iwconfig
```





## rename files using xargs

```
ls -t | head -n 6  |  sed 'p;;s/\.png/\.jpg/' | xargs -n2 mv
```





### 2>&1

Grep docker logs both from error stream and stroutput
```
docker logs nginx 2>&1 | grep "127." 
```



https://en.wikipedia.org/wiki/File_descriptor

| Integer value | Name                                                    | <[unistd.h](https://en.wikipedia.org/wiki/Unistd.h)> symbolic constant[[1\]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-1) | <[stdio.h](https://en.wikipedia.org/wiki/Stdio.h)> file stream[[2\]](https://en.wikipedia.org/wiki/File_descriptor#cite_note-2) |
| ------------- | ------------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 0             | [Standard input](https://en.wikipedia.org/wiki/Stdin)   | STDIN_FILENO                                                 | stdin                                                        |
| 1             | [Standard output](https://en.wikipedia.org/wiki/Stdout) | STDOUT_FILENO                                                | stdout                                                       |
| 2             | [Standard error](https://en.wikipedia.org/wiki/Stderr)  | STDERR_FILENO                                                | stderr                                                       |





https://gist.github.com/roylee0704/b5c8090e6cbfe1a9ae6c63062623a7cd



https://stackoverflow.com/questions/818255/what-does-21-mean

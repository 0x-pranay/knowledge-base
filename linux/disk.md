DIsk is full and need to find big files and folders including hidden files

```
du -sch .[!.]* * |sort -h
```

https://askubuntu.com/questions/413358/disk-is-full-but-cannot-find-big-files-or-folders



April 10th 2022 file-roller filled my disk while interuppting the process.

```
ls -alS --time-style=+%D | grep 'date +%D'
```

```
find . -maxdepth 1 -newermt "2016-12-06"
```

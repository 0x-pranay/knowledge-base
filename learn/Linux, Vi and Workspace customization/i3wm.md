Weird issue when opening a save as dialog box, when trying to name it jumps to seach. 

```
Uninstall xdg-desktop-portal-gnome, ensure xdg-desktop-portal-gtk is installed, reboot.

Log in and open a terminal and run pgrep -fa portal and make sure you see xdg-desktop-portal-gtk running and not xdg-desktop-portal-gnome.
```


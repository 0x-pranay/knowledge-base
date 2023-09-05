#Keychron, #bluetooth,  #bluetoothctl



Install `bluetoothctl` if it is not already installed. In Ubuntu 20.04 it comes with the default install.

In terminal, run the command `bluetoothctl`:

```
$ bluetoothctl
Agent registered
[MX Vertical]# agent on
Agent is already registered
```

Start the scan:

```
[MX Vertical]# scan on
Discovery started
[CHG] Controller DC:53:60:0E:0A:C8 Discovering: yes
[CHG] Device 34:88:5D:EF:19:51 RSSI: -49
[CHG] Device 34:88:5D:EF:19:51 Class: 0x00002540
[CHG] Device 34:88:5D:EF:19:51 Icon: input-keyboard
[CHG] Device 88:0F:10:87:00:F1 RSSI: -87
```

In this output, the MAC address of the keyboard is this one: 34:88:5D:EF:19:51. Copy it! Then stop the scan:

```
[MX Vertical]# scan off
[CHG] Device 88:0F:10:87:00:F1 RSSI is nil
[CHG] Device 34:88:5D:EF:19:51 RSSI is nil
[CHG] Controller DC:53:60:0E:0A:C8 Discovering: no
Discovery stopped
```

Trust the device with:

```
[MX Vertical]# trust 34:88:5D:EF:19:51
[CHG] Device 34:88:5D:EF:19:51 Trusted: yes
Changing 34:88:5D:EF:19:51 trust succeeded
```

And pair it. Now the passkey shown in terminal (300892 in this case) must be typed in keyboard, and after that an Enter should be pressed. It'll looks like this:

```
[MX Vertical]# pair 34:88:5D:EF:19:51
Attempting to pair with 34:88:5D:EF:19:51
[CHG] Device 34:88:5D:EF:19:51 Connected: yes
[agent] Passkey: 300892
[agent] Passkey:  00892
[agent] Passkey:   0892
[agent] Passkey:    892
[agent] Passkey:     92
[agent] Passkey:      2
[agent] Passkey:         
```

Hit Enter now.

```
[CHG] Device 34:88:5D:EF:19:51 Modalias: usb:v046DpB342d4201
[CHG] Device 34:88:5D:EF:19:51 UUIDs: 00001000-0000-1000-8000-00805f9b34fb
[CHG] Device 34:88:5D:EF:19:51 UUIDs: 00001124-0000-1000-8000-00805f9b34fb
[CHG] Device 34:88:5D:EF:19:51 UUIDs: 00001200-0000-1000-8000-00805f9b34fb
[CHG] Device 34:88:5D:EF:19:51 ServicesResolved: yes
[CHG] Device 34:88:5D:EF:19:51 Paired: yes
Pairing successful
[CHG] Device 34:88:5D:EF:19:51 ServicesResolved: no
[CHG] Device 34:88:5D:EF:19:51 Connected: no
[MX Vertical]# connect 34:88:5D:EF:19:51
Attempting to connect to 34:88:5D:EF:19:51
[CHG] Device 34:88:5D:EF:19:51 Connected: yes
Connection successful
[CHG] Device 34:88:5D:EF:19:51 ServicesResolved: yes
```

And finally it's working!
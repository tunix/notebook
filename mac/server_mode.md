# Server Mode
## Prevent sleep when lid is closed
You can accomplish this in terminal. No additional software is needed. Display global power settings with: `pmset-g`

```
System-wide power settings:
Currently in use:
 lidwake              1
 autopoweroff         1
 standbydelayhigh     86400
 autopoweroffdelay    28800
 proximitywake        1
 standby              1
 standbydelaylow      10800
 ttyskeepawake        1
 hibernatemode        3
 powernap             1
 gpuswitch            2
 hibernatefile        /var/vm/sleepimage
 highstandbythreshold 50
 womp                 0
 displaysleep         10
 networkoversleep     0
 sleep                1 (sleep prevented by sharingd)
 tcpkeepalive         1
 halfdim              1
 acwake               0
 disksleep            10
```

To stop sleep entirely: `sudo pmset -a disablesleep 1`
To revert: `sudo pmset -a disablesleep 0`

## Enabling SSH
```
sudo systemsetup -getremotelogin
sudo systemsetup -setremotelogin on
```

Above commands may fail due to full disk inaccessibility. In that case, SSH service shall be enabled with the following commands:

```
sudo /bin/launchctl load -w /System/Library/LaunchDaemons/ssh.plist
sudo /bin/launchctl unload -w /System/Library/LaunchDaemons/ssh.plist
```

After this, you should be able to login:

```
ssh alper.kanat@192.168.1.199
```

Placing your SSH public key on the host beforehand is recommended.

## Enabling VNC
```
sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart \
  -configure \
  -allowAccessFor \
  -allUsers \
  -privs \
  -all
```

You may need a restart before trying to connect.

#### References
https://prodisup.com/posts/2021/05/fix-vnc-black-screen-on-big-sur/
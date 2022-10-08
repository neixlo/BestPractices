# BestPractices
Code Snippets for every day..

## create a directory tree for github readmes
-L arg is for depth level of main dir
```
tree dir_name/ -L 3 >> tree.txt
```
Copy output into readme inside code quotations
```
dir_name/
├── sub_dir#1
│   └── subsub_dir
│       ├── sample_file#1.txt
│       └── sample_file#2.txt
└── sub_dir#2
    └── subsub_dir
        ├── sample_file#1.txt
        ├── sample_file#2.txt
        └── sample_file#3.txt
```


## freeze pip packages into requirements.txt
```
pip freeze > requirements.txt
```

## erase disk completely and overwrite
```
sudo shred -n 6 -vz /dev/sda1
```
```-n``` 6: Overwrite 6 times instead of the default (25 times). \
```-v``` : Show progress. \
```-z``` : Add a final overwrite with zeros to hide shredding. \

## if you're unable to access the shared folder in VBox
see: https://unix.stackexchange.com/questions/52667/file-permission-issues-with-shared-folders-under-virtual-box-ubuntu-guest-wind

add your user to vboxsf group then reboot
```
usermod -aG vboxsf <youruser>
sudo reboot
```

## set github identity

### set the identity only in this repository
```
git config user.email <you@example.com>
git config user.name <Your Name>
```

### set the identity globaly
```
git config --global user.email <you@example.com>
git config --global user.name <Your Name>
```

### python file header

```
#!/usr/bin/env python3
#-*- coding: utf-8 -*-

'''
description of this script

usage: how to use.. python3 main.py -arg1 <argument>
'''

```

### if chrome remote desktop isn't working on Ubuntu

<img src="./chrome-remote-desktop-setup.png">
Simply create the config dir..
`$ mkdir ~/.config/chrome-remote-desktop`


### install ubuntu on external disk (with seperate bootloader)
Based on [this](https://unix.stackexchange.com/questions/305345/where-is-grub-installed-and-do-i-need-a-new-one-for-a-separate-linux-installatio) post.
**Do not reboot during this process**
1. Boot Live Image (in test mode)
2. Set Flags (on windows drive) according to this:![changed_flags_efi_part](https://user-images.githubusercontent.com/34251323/139534953-bd86aaca-421c-4804-aeb5-d1729fc73a8c.png)
3. Install Ubuntu, use custom partition layout like this: ![new_partition_layout](https://user-images.githubusercontent.com/34251323/139534956-0062a5c6-2ddb-4c7d-89a7-9bd22392ac46.png)
4. DO NOT REBOOT
5. Set the flags back (on windows drive) ![org_flags_efi_part](https://user-images.githubusercontent.com/34251323/139534958-7da265c1-b782-4061-a3f8-bb27f915a12a.png)
6. reboot




### if there is "no space left on device" while installing pip / pip-compile packages
https://askubuntu.com/questions/1326304/cannot-install-pip-module-because-there-is-no-space-left-on-device

- `/` is too small to store downloaded files
- TMPDIR=/home/user/cachedir python3 -m piptools compile --verbose
- TMPDIR=/home/user/cachedir python3 -m pip install -r requirements.txt

### if there is "no space left on device" for tmp files
check `sudo du -h --max-depth=1 /var/log/journal` and check how big it is, then follow:
https://ubuntuhandbook.org/index.php/2020/12/clear-systemd-journal-logs-ubuntu/


### mount harddrive in ubuntu cli
1. `lsblk -f` -> get UUID of wanted harddrive
2. `mkdir /media/MOUNT/PATH`
3. `sudo mount --uuid YOUR-UUID /media/MOUNT/PATH`
4. or `sudo mount -o umask=000,dmask=000 --uuid YOUR-UUID /media/MOUNT/PATH` if permission issue
5. 


### install x11vnc
`sudo apt-get update` \
`sudo apt-get install x11vnc`

### configure x11vnc:
`sudo x11vnc -storepasswd /etc/x11vnc.pass` \
`sudo chown USERNAME: /etc/x11vnc.pass`

### change login screen to light dm
See also [this post](https://c-nergy.be/blog/?p=11767) \
`sudo apt-get -y install slick-greeter` \
-> then choose lightdm

### setup an x11vnc service
See also [this post](https://askubuntu.com/questions/229989/how-to-setup-x11vnc-to-access-with-graphical-login-screen) \
`sudo nano /etc/systemd/system/x11vnc.service` \
-> paste and save the following snippet:
```
[Unit]
Description="x11vnc"
Requires=display-manager.service
After=display-manager.service

[Service]
ExecStart=/usr/bin/x11vnc -xkb -noxrecord -noxfixes -noxdamage -display :0 -auth /var/run/lightdm/root/:0
ExecStop=/usr/bin/killall x11vnc
Restart=on-failure
Restart-sec=2

[Install]
WantedBy=multi-user.target
```
-> then run:

`sudo systemctl daemon-reload` \
`sudo systemctl enable x11vnc` \
`sudo systemctl start x11vnc` 

And check the status with: \
`sudo systemctl status x11vnc`



### install ubuntu on machine with nvidia gpu

At boot enter bios with `F2`, `DEL` or alike:
- disable fastboot
- disable secure boot
- disable secure chip tpm

At restart, boot from LiveUSB stick.
- Hit `Shift`
- Hit `e` on the selected Ubuntu line
- append `quiet splash` to `quiet splash nomodeset`

Install ubuntu as usual.

After installation boot with nomodeset (see above) and set nomodeset by default. See: https://askubuntu.com/questions/38780/how-do-i-set-nomodeset-after-ive-already-installed-ubuntu


### clone an entire harddrive
`dd if=/dev/sda of=/dev/sdb bs=32M status=progress`



## install nvidia driver for new ubunto installation (resolutuion will work again)

′sudo apt purge nvidia*′
′ubuntu-drivers devices′
′ubuntu-drivers devices | grep recommended′
′sudo apt install nvidia-driver-470′









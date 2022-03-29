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

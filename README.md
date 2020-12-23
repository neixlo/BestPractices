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

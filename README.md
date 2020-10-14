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
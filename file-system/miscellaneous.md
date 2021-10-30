# File System: Miscellaneous


### Count the Lines of all Files under A Directory

```sh
# Count the lines of all .txt files under the current directory.
find . -name '*.txt' | xargs wc -l
```


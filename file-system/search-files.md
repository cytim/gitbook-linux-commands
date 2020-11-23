# File System: Search Files


### Search By Metadata

```sh
find <PATH> [-name <PATTERN>] [-type <FILE_TYPE>] [-delete]
```

> `<FILE_TYPE>`: regular file (`f`), directory (`d`), symlink (`l`), etc.


**Execute Command After "find"**

```sh
# Run the CMD on each result
# Example CMD: `dirname {}`

find ... -exec <CMD> \;
# OR
find ... -print0 | xargs -0 -n1 -I {} <CMD>

# Run the CMD on the whole result

find ... -exec <CMD> \+
# OR
find ... -print0 | xargs -0 -I {} <CMD>
```

> [Differences between `find -exec` and `find | xargs`](https://www.everythingcli.org/find-exec-vs-find-xargs/)


### Search By Content

```sh
grep -inr '<SEARCH_PATTERN>' <FILENAME_PATTERN>
```

> `-i`: Case-insenstive  
> `-n`: Display line number  
> `-r`: Search the files recursively


### Replace the Content in Multiple Files

```sh
sed -i 's/foo/bar/g' *

# or for BSD systems like MacOS
sed -i '.bak' 's/foo/bar/g' *
```

> Reference: https://stackoverflow.com/a/11392505


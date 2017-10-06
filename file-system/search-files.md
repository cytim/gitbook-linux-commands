# File System: Search Files


### Search By Metadata

```sh
find <PATH> [-name <PATTERN>] [-type <FILE_TYPE>] [-delete]
```

> `<FILE_TYPE>`: regular file (`f`), directory (`d`), symlink (`l`), etc.


### Search By Content

```sh
grep -inr '<SEARCH_PATTERN>' <FILENAME_PATTERN>
```

> `-i`: Case-insenstive  
> `-n`: Display line number  
> `-r`: Search the files recursively


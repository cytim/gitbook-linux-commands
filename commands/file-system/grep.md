# File System: Grep

`grep` is a handy utility to search lines by patterns.

There are some variations.

`egrep` can read the patterns as extended regex.

`fgrep` is the most performant, but it does not understand regex.

To grep compressed file, there are `zgrep`, `zegrep`, and `zfgrep` accordingly.

### Useful Command Options

**Turn `grep` into `egrep`**

```sh
grep -E <PATTERN> <FILE>
```

**Print Only The Matching Parts**

```sh
grep -o <PATTERN> <FILE>

# [EXAMPLE]
# Command: echo 'INFO 2020-01-01 Hello World' | grep -Eo '^[A-Z]+'
# Output:  INFO
```

**Print The N Lines Around Each Match**

```sh
# Print the matching line, and the N lines AFTER.
grep -A <N> <PATTERN> <FILE>

# Print the matching line, and the N lines BEFORE.
grep -B <N> <PATTERN> <FILE>

# Print the matching line, and the N lines AROUND.
grep -C <N> <PATTERN> <FILE>
```

**Print The Mismatching Lines**

```sh
grep -v <PATTERN> <FILE>
```

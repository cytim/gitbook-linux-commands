# YUM: List Packages

```sh
# List the packages under ALL repository.
yum list available

# List the packages under SPECIFIC repostory.
yum --disablerepo="*" --enablerepo="docker-ce" list available

# List a specific package.
yum list docker-ce

# List a specific package with all versions.
yum list docker-ce --showduplicates | sort -r
```


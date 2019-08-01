# Docker: Manage Images


### Remove All Dangling Image

```sh
docker images -qf dangling=true | xargs docker rmi
```

### Remove All `<none>` Image

```sh
docker images --digests | grep '<none>' | awk '{print $1 "@" $3}' | xargs docker rmi
```


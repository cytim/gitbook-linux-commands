# Docker: Manage Images


### Remove All Dangling Image

```sh
docker images -qf dangling=true | xargs docker rmi
```


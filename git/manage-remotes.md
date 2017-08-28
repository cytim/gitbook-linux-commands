# Manage Remotes


### List All Remote

```sh
git remote -v
```


### Update Remote Endpoint

> This allows you to switch the remote endpoint between SSH and HTTPS, or to a new endpoint.

```sh
git remote set-url <name> <endpoint>
```

Example:

```
git remote set-url origin git@github.com:cytim/gitbook-linux-commands.git
```


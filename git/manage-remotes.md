# Git: Manage Remotes


### List All Remote

```sh
git remote -v
```


### Add Remote

> This is usually used after `git init`.

```sh
git remote add <name> <endpoint>
```

**Example**

```sh
git remote add origin git@github.com:cytim/gitbook-linux-commands.git
```


### Update Remote Endpoint

> This allows you to switch the remote endpoint between SSH and HTTPS, or to a new endpoint.

```sh
git remote set-url <name> <endpoint>
```

Example:

```sh
git remote set-url origin git@github.com:cytim/gitbook-linux-commands.git
```


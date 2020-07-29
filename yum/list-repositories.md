# YUM: List Repositories

```sh
yum [-v] repolist [enabled|disabled|all]
```

> *Flags*
> - `-v`: Verbose mode
>
> *Output Columns*
> - repo id
> - repo name
> - status: Number of packages in the format of `X+Y`.
>   - X = Number of available packages
>   - Y = Number of excluded packages


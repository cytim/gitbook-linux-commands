# Elixir - IEx

The Interactive Elixir shell. It supports most of the elixir arguments.

**Execute Script**

```bash
iex [--sname <SHORT_NAME>] [--cookie <SECRET>] -S <SCRIPT>
```

- `--sname`: Provide a short name to be identified by other nodes in the network.
- `--cookie`: Provide a shared secret that only nodes with the same secret can communicate with each other.
- `-S`: Provide the script or command to run before starting the shell.

**Open A Remote Shell**

```bash
iex --sname node2 [--cookie foo] --remsh node1
```

- `--sname node2`: Start the local shell with the short name `node2`
- `--cookie foo`: Start the local shell with the shared secret `foo`
- `--remsh node1`: Connect to the remote node `node1` and starts the shell on it

**Require File**

```bash
iex -r <FILE>
```

**Recompile and Reload the Module**

```
iex> r <MODULE>
```

**IEx Helpers**

[https://hexdocs.pm/iex/IEx.Helpers.html](https://hexdocs.pm/iex/IEx.Helpers.html)

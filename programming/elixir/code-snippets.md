# Elixir - Code Snippets

## Time the Function Call

Reference: [:timer](https://www.erlang.org/doc/man/timer.html#tc-1)

```elixir
{time, value} = :timer.tc(func, arguments)

# e.g.
# {time, value} = :timer.tc(&foo/2, [arg1, arg2])
```

`time`: the elapsed real time in microseconds (μs)  
`value`: the return value of the function `func`

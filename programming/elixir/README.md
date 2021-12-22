# Elixir

## Erlang/OTP

Erlang was proprietary software within Ericsson, which is a telecom company. The software was maintained by the **O**pen **T**elecom **P**latform (OTP) product unit, who released Erlang/OTP as open-source in the late 1990s.

The release comes with many handy tools and libraries for development…

- Erlang compiler;
- Test framework;
- Profiler;
- (etc.)

## Naming Conventions

[https://hexdocs.pm/elixir/master/naming-conventions.html](https://hexdocs.pm/elixir/master/naming-conventions.html)

### Casing

**Variables, Function Names, Module Attributes, etc.**

`snake_case` is enforced.

**Atoms**

`snake_case` is recommended, or `PascalCase` is also acceptable.

**Module Names and Aliases**

`PascalCase` is enforced.

(In fact, the aliases are converted to atoms during compilation, because the modules are always represented by atoms in the Erlang VM.)

**Filenames**

`snake_case` is recommended.

### Underscore (`_foo`)

**Variables**

A value that will not be used must be assigned to `_` or to a variable starting with underscore (`_foo`).

**Function Names**

If the function name starts with underscore, the function will not be imported by default.

### Trailing bang (`foo!`)

The trailing bang signifies a function or macro where failure cases raise an exception.

The version without `!` is preferred when you want to handle different outcomes using pattern matching.

However, if you expect the outcome to always be successful, the bang variation is more convenient because it raises a more helpful error message on failure.

### Trailing question mark (`foo?`)

Functions, except those who are also valid guards, that return a **boolean** are named with a trailing question mark.

### `is_` prefix (`is_foo`)

Type checks and other boolean checks that are allowed in **guard clauses** are named with the `is_` prefix, instead of a trailing question mark.

### Special names

**length and size**

If the function name contains `size`, the operation runs in O(1) time.

If the function name contains `length`, the operation runs in O(n) time.

## Lists or Tuples?

**Lists** are stored in memory as _linked lists_. This means accessing the length of a list is a linear operation.

**Tuples** are stored _contiguously_ in memory. Getting the tuple size or accessing an element by index is fast. However, updating or adding elements to tuples is expensive because it requires creating a new tuple in memory.

## Keyword Lists

Keyword list represents the key-value pairs in a list of 2-item tuples, where the key is always an atom.

```elixir
## Since the usage of keyword lists is very common
[{:a, 1}, {:b, 2}]

## can be shortened as
[a: 1, b: 2]
```

When the keyword list is the last argument of a function, the square brackets are optional.

```elixir
## Therefore
if false, [do: :this, else: :that]

## is equivalent to
if false, do: :this, else: :that
```

## Why Atoms?

Atoms are similar to enum. They are mapped to distinct integers behind the scene.

- Comparing atoms is more efficient than comparing string;
- Declaring the same atom multiple times won’t consume more memory;
- Using atoms (instead of integers) improves code readability.

## Multiple Clauses and Guards

### Case

```elixir
case {1, 2, 3} do
  {4, 5, 6} ->
    "This clause won't match"

  {1, x, 3} ->
    "This clause will match and bind x to 2 in this clause"

  _ ->
    "This clause would match any value"
end
```

### Cond

```elixir
n = 10
cond do
  n % 3 == 0 ->
    "n is a multiple of 3"

  n % 2 == 0 ->
    "n is a even number"

  true ->
    "n is none of the above"
end
```

### With

```elixir
with {:ok, date} <- next_sunday(),
     {:ok, weather} <- weather_forecast(date) do
  IO.puts("Next sunday is a #{weather} day")
else
  {:error, :date_out_of_range} ->
    IO.puts("Cannot obtain weather forecast")

  error ->
    IO.puts("Unknown error: #{inspect(error)}")
end
```

### Anonymous Function

```elixir
f = fn
  x, y when x > 0 -> x + y
  x, y -> x * y
end

## [NOTE]
## The number of arguments in each clause needs to be the same, otherwise an error is raised.
```

## How to build an infinite loop in Elixir?

### **By Recursion**

This enables the application to store state as well. Below is an example implementation of a simple key-value store.

```elixir
defmodule KV do
  def start_link do
    Task.start_link(fn -> loop(%{}) end)
  end

  defp loop(map) do
    receive do
      {:get, key, caller} ->
        send caller, Map.get(map, key)
        loop(map)
      {:put, key, value} ->
        loop(Map.put(map, key, value))
    end
  end
end
```

### Why doesn’t the recursion result in stack overflow?

Because the compiler will apply the Tail Call Optimization (TCO).

[https://medium.com/fave-engineering/recursion-tail-call-optimization-and-recursion-ac54b01e3b18](https://medium.com/fave-engineering/recursion-tail-call-optimization-and-recursion-ac54b01e3b18)

When the function calls itself as the final statement, instead of adding a new stack frame to the call stack, it does a `goto`.

## `import` and `use`

### import

We `import` a module to access its functions and macros without referencing its fully-qualified name.

<aside>
⚠️ The use of `import` is ***discouraged*** because you cannot directly see in what module a function is defined.

</aside>

### require

We `require` a module to opt-in using the macros.

### use

We `use` a module to allow the module to inject **_any_** code in the current module.

<aside>
💡 Using a module is the same as `requir`ing it and then calling its `__using__` function.

</aside>

## Plug

Just another name for “middleware”. There are two implementations.

**The _Function_ Implementation**

It takes the `Plug.Conn` struct, optionally modifies it, and returns it.

```elixir
def hello_world_plug(conn, _opts) do
  conn
  |> put_resp_content_type("text/plain")
  |> send_resp(200, "Hello world")
end
```

**The _Module_ Implementation**

The `init/1` function initialises the options.

The `call/2` function takes the `Plug.Conn` struct, optionally modifies it, and returns it.

```elixir
defmodule MyPlug do
  def init([]), do: false
  def call(conn, _opts), do: conn
end
```

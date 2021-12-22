# Elixir - Libraries

## Web Framework

### Phoenix

> Phoenix is a web development framework written in Elixir which implements the server-side Model View Controller (MVC)
> pattern. Many of its components and concepts will seem familiar to those of us with experience in other web
> frameworks like Ruby on Rails or Python's Django.
>
> -- [Phoenix](https://hexdocs.pm/phoenix/overview.html)

## Database Management

### Ecto

> Ecto is split into 4 main components:
>
> [Ecto.Repo](https://hexdocs.pm/ecto/Ecto.Repo.html) - repositories are wrappers around the data store. Via the
> repository, we can create, update, destroy and query existing entries. A repository needs an adapter and credentials
> to communicate to the database.
>
> [Ecto.Schema](https://hexdocs.pm/ecto/Ecto.Schema.html) - schemas are used to map any data source into an Elixir
> struct. We will often use them to map tables into Elixir data but that's one of their use cases and not a requirement
> for using Ecto.
>
> [Ecto.Changeset](https://hexdocs.pm/ecto/Ecto.Changeset.html) - changesets provide a way for developers to filter and
> cast external parameters, as well as a mechanism to track and validate changes before they are applied to your data.
>
> [Ecto.Query](https://hexdocs.pm/ecto/Ecto.Query.html) - written in Elixir syntax, queries are used to retrieve
> information from a given repository. Queries in Ecto are secure, avoiding common problems like SQL Injection, while
> still being composable, allowing developers to build queries piece by piece instead of all at once.
>
> -- [Ecto](https://hexdocs.pm/ecto/Ecto.html)

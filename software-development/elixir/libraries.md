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

## Background Processing

### Oban

> Oban is a robust job processing library which uses PostgreSQL for storage and coordination.
>
> -- [Oban](https://hexdocs.pm/oban/Oban.html)

Oban consists of three libraries.

- [Oban](https://hexdocs.pm/oban/Oban.html)

  - **Free** - Distributed under Apache 2.0.
  - The core of the whole framework.
  - Provide the basic background processing features like priority queues, scheduled jobs, graceful shutdown, etc.

- [Oban Pro](https://getoban.pro/docs/pro/overview.html)

  - **Commercial** product.
  - Provide more sophisticated management like rate limiting, job encryption, etc.
  - Provide the canned solutions for batches, workflows, etc.

- [Oban Web](https://getoban.pro/docs/web/overview.html) ([demo](https://getoban.pro/oban))

  - **Commercial** product.
  - Provide the web portal to monitor and manage the enqueued jobs.

Refer to [the official website](https://getoban.pro/#feature-comparison) for the feature comparison.

## Testing

### Mock

> Mock modules for testing purposes.
>
> -- [Mock](https://hexdocs.pm/mock/Mock.html)

Use Mock when the module to be mocked is an internal module, or does not implement a
[behaviour](https://hexdocs.pm/elixir/1.4.5/behaviours.html).

### Hammox

> Hammox is a library for rigorous unit testing using mocks, explicit behaviours and contract tests.
>
> -- [Hammox](https://hexdocs.pm/hammox/Hammox.html)

Use Hammox when the module to be mocked is an external module that implements a behaviour.

### Bypass

> Bypass provides a quick way to create a custom plug that can be put in place instead of an actual HTTP server to return
> prebaked responses to client requests.
>
> -- [Bypass](https://hexdocs.pm/bypass/Bypass.html)

Use Bypass when the module under test **is** the API client to integrate with the external HTTP service.

**NOTE** If the module under test is a wrapper of the API client, it is suggested to mock the API client by _Mock_ or
_Hammox_, instead of mocking the HTTP server directly.

### Faker

> Faker is a pure Elixir library for generating fake data.
>
> -- [Faker](https://hexdocs.pm/faker/readme.html)

## Others

### Alchemy

> Safely perform refactoring experiments in production.
>
> -- [Alchemy](https://hexdocs.pm/alchemy/readme.html)

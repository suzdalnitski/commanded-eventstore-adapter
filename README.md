# EventStore adapter for Commanded

Use the PostgreSQL-based [EventStore](https://github.com/slashdotdash/eventstore) with [Commanded](https://github.com/slashdotdash/commanded).

MIT License

[![Build Status](https://travis-ci.org/slashdotdash/commanded-eventstore-adapter.svg?branch=master)](https://travis-ci.org/slashdotdash/commanded-eventstore-adapter)

## Getting started

The package can be installed from hex as follows.

1. Add `commanded_eventstore_adapter` to your list of dependencies in `mix.exs`:

    ```elixir
    def deps do
      [{:commanded_eventstore_adapter, "~> 0.2"}]
    end
    ```

2. Include `:eventstore` in the list of applications to start.

    For **Elixir 1.4**, add `:eventstore` to the extra applications list in `mix.exs`:

    ```elixir
    def application do
      [
        extra_applications: [
          :logger,
          :eventstore,
        ],
      ]
    end
    ```

    For **Elixir 1.3** and before, add `:eventstore` to the applications list in `mix.exs`:

    ```elixir
    def application do
      [
        applications: [
          :logger,
          :eventstore,
        ],
      ]
    end
    ```

3. Configure Commanded to use the event store adapter:

    ```elixir
    config :commanded,
      event_store_adapter: Commanded.EventStore.Adapters.EventStore
    ```

4. Configure the `eventstore` in each environment's mix config file (e.g. `config/dev.exs`), specifying usage of the included JSON serializer:

    ```elixir
    config :eventstore, EventStore.Storage,
      serializer: Commanded.Serialization.JsonSerializer,
      username: "postgres",
      password: "postgres",
      database: "eventstore_dev",
      hostname: "localhost",
      pool_size: 10
    ```

5. Create the `eventstore` database and tables using the `mix` task:

    ```
    mix event_store.create
    ```

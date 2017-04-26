[![GitPitch](https://gitpitch.com/assets/badge.svg)](https://gitpitch.com/onetapbeyond/gen_metrics)

# GenMetrics

Runtime metrics for GenServer and GenStage applications.

This library supports the collection and publication of GenServer and GenStage runtime metrics. Metrics data are generated by an introspection agent. No instrumentation is required within the GenServer or GenStage library or within your application source code.

## Quick Look

Given a GenStage application with the following stages: `Data.Producer`, `Data.Scrubber`, `Data.Analyzer` and a `Data.Consumer`, activate metrics collection for the entire pipeline as follows:

```elixir
alias GenMetrics.GenStage.Pipeline
pipeline = %Pipeline{name: "demo",
                     producer: [Data.Producer],
                     producer_consumer: [Data.Scrubber, Data.Analyzer],
                     consumer: [Data.Consumer]}
GenMetrics.monitor_pipeline(pipeline)
```

Metrics are published by a dedicated GenMetrics reporting process. Any application can subscribe to this process in order to receive metrics data. Sample summary metrics data for a GenStage process looks as follows:

```
# Stage Name: Data.Producer, PID<0.195.0>

%GenMetrics.GenStage.Summary{stage: Data.Producer,
                             pid: #PID<0.195.0>,
                             callbacks: 9536,
                             time_on_callbacks: 407,
                             demand: 4768000,
                             events: 4768000}

# Summary timings measured in milliseconds (ms).
```

Detailed statistical metrics data per process are also available. See the documentation for details.

## Documentation

Find detailed documentation for the GenMetrics library on [HexDocs](https://hexdocs.pm/gen_metrics).

## Installation

GenStage requires Elixir v1.4. Just add `:gen_metrics` to your list of dependencies in mix.exs:

```elixir
def deps do
  [{:gen_metrics, "~> 0.1.0"}]
end
```

## Examples

Examples using GenMetrics to collect and report runtime metrics for GenServer applications can be found in the [examples](examples) directory:

  * [genserver_events](examples/genserver_events.exs)

Examples using GenMetrics to collect and report runtime metrics for GenStage applications can also be found in the [examples](examples) directory:

  * [genstage_producer_consumer](examples/genstage_producer_consumer.exs)

  * [genstage_gen_event](examples/genstage_gen_event.exs)

  * [genstage_rate_limiter](examples/genstage_rate_limiter.exs)

All of these GenStage example applications are clones of the example applications provided in the [GenStage](http://github.com/elixir-lang/gen_stage) project repository.

## License

See the [LICENSE](LICENSE) file for license rights and limitations (Apache License 2.0).
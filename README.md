# Running otel locally

The purpose of this repository is to make it possible to run simulate sending event to otel collector then viewing it on jaeger UI locally

The reason for doing this is to make it easier to test out the otel config.yaml and also make this as a base for potential future workshop

__note__: this is work in progress and I am aware that we can have lots of improvement though i rather record current progress first.


```sh
# use `docker compose` if you are on linux
docker-compose up -d

export OTEL_EXPORTER_OTLP_ENDPOINT=http://otelcollector:4317
export OTEL_EXPORTER_OTLP_INSECURE=true
# make sure you have the util container in the same network with your service containers
# Mac have to run VM with x86_64 arch
alias otel='docker run --rm --network otel-locally_otel -e OTEL_EXPORTER_OTLP_ENDPOINT -e OTEL_EXPORTER_OTLP_INSECURE dell/opentelemetry-cli:latest'

# then can use otel to send span
otel span -a "my.foo=bar" -a "my.bar=baz" -a "card=select * where password=abc123" "span name"
```

### Refs
- [otel-cli](https://github.com/dell/opentelemetry-cli)

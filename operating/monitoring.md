# Monitoring

## Liveness Probe endpoint

```text
curl "http://localhost:18081/ping"
```

Returns the HTTP status code `200` right after basic initialisation procedures. ``

## Readiness Probe endpoint

```text
curl "http://localhost:18081/ready"
```

Returns the HTTP status code `200` when Bondy is ready to accept client WAMP \(WS\|TCP\) or HTTP connections. Otherwise returns HTTP status code `503`. 

How quickly Bondy is ready to accept connections depends on the [Coordinated Startup](../configuring/configuration-reference/general-settings.md#coordinated-startup-shutdown) configuration settings. As soon as the shutdown procedure is initiated, this endpoint will return `503.`

## Prometheus Metrics

```text
curl "http://localhost:18081/metrics" \
-H 'Content-Type: text/plain; version=0.0.4'
```


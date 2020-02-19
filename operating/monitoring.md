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

### Metrics

| Metric | Type | Description |
| :--- | :--- | :--- |
| bondy\_cluster\_dropped\_bytes | counter | The total bytes dropped by a bondy node from another node in the cluster since reset |
| bondy\_cluster\_received\_bytes | counter | The total bytes received by a bondy node from another node in the cluster since reset |
| bondy\_cluster\_sent\_bytes | counter | The total bytes sent by a bondy node from another node in the cluster since reset |
| bondy\_errors\_total | counter | The total number of errors in a bondy node since reset |
| bondy\_http\_early\_errors\_total | counter | Total number of HTTP early errors |
| bondy\_http\_errors\_total | counter | Total number of HTTP request errors |
| bondy\_http\_receive\_body\_duration\_microseconds | histogram | Request body receiving duration |
| bondy\_http\_request\_duration\_microseconds | histogram | HTTP request duration |
| bondy\_http\_requests\_total | counter | Total number of HTTP requests |
| bondy\_http\_spawned\_processes\_total | counter | Total number of spawned HTTP handlers  \(processes\) |
| bondy\_protocol\_upgrades\_total | counter | Total number of protocol upgrades |
| bondy\_received\_bytes | counter | The total bytes received by a bondy node from clients since reset |
| bondy\_registry\_tries | gauge | Registry tries count |
| bondy\_send\_errors\_total | counter | The total number of router send errors in a bondy node since reset |
| bondy\_sent\_bytes | counter | The total bytes sent by a bondy node from clients  since reset |
| bondy\_session\_duration\_seconds | histogram | A histogram of the duration of sessions |
| bondy\_sessions\_closed\_total | counter | The number of sessions closed on a bondy node since reset |
| bondy\_sessions\_opened\_total | counter | The number of sessions opened on a bondy node since reset |
| bondy\_sessions\_total | gauge | The number of active sessions on a bondy node since reset |
| bondy\_socket\_duration\_seconds | histogram | A histogram of the duration of a socket |
| bondy\_socket\_errors\_total | counter | The number of socket errors on a bondy node since reset |
| bondy\_sockets\_closed\_total | counter | The number of sockets closed on a bondy node since reset |
| bondy\_sockets\_opened\_total | counter | The number of sockets opened on a bondy node since reset |
| bondy\_sockets\_total | gauge | The number of active sockets on a bondy node |
| bondy\_wamp\_abort\_messages\_total | counter | The total number of abort messages routed by a bondy node since reset |
| bondy\_wamp\_authenticate\_messages\_total | counter | The total number of authenticate messages routed by a bondy node since reset |
| bondy\_wamp\_call\_latency\_milliseconds | histogram | A histogram of routed RPC response latencies |
| bondy\_wamp\_call\_messages\_total | counter | The total number of call messages routed by a bondy node since reset |
| bondy\_wamp\_call\_retries\_total | counter | The total number of retries for WAMP call |
| bondy\_wamp\_cancel\_messages\_total | counter | The total number of cancel messages routed by a bondy node since reset |
| bondy\_wamp\_challenge\_messages\_total | counter | The total number of challenge messages routed by a bondy node since reset |
| bondy\_wamp\_error\_messages\_total | counter | The total number of error messages routed by a bondy node since reset |
| bondy\_wamp\_event\_messages\_total | counter | The total number of event messages routed by a bondy node since reset |
| bondy\_wamp\_goodbye\_messages\_total | counter | The total number of goodbye messages routed by a bondy node since reset |
| bondy\_wamp\_hello\_messages\_total | counter | The total number of hello messages routed by a bondy node since reset |
| bondy\_wamp\_interrupt\_messages\_total | counter | The total number of interrupt messages routed by a bondy node since reset |
| bondy\_wamp\_invocation\_messages\_total | counter | The total number of invocation messages routed by a bondy node since reset |
| bondy\_wamp\_message\_bytes | histogram | A summary of the size of the wamp messages received by a bondy node |
| bondy\_wamp\_messages\_total | counter | The total number of wamp messages routed by a bondy node since reset |
| bondy\_wamp\_publish\_messages\_total | counter | The total number of publish messages routed by a bondy node since reset |
| bondy\_wamp\_published\_messages\_total | counter | The total number of published messages routed by a bondy node since reset |
| bondy\_wamp\_register\_messages\_total | counter | The total number of register messages routed by a bondy node since reset |
| bondy\_wamp\_registered\_messages\_total | counter | The total number of registered messages routed by a bondy node since reset |
| bondy\_wamp\_result\_messages\_total | counter | The total number of result messages routed by a bondy node since reset |
| bondy\_wamp\_subscribe\_messages\_total | counter | The total number of subscribe messages routed by a bondy node since reset |
| bondy\_wamp\_subscribed\_messages\_total | counter | The total number of subscribed messages routed by a bondy node since reset |
| bondy\_wamp\_unregister\_messages\_total | counter | The total number of unregister messages routed by a bondy node since reset |
| bondy\_wamp\_unregistered\_messages\_total | counter | The total number of unregistered messages routed by a bondy node since reset |
| bondy\_wamp\_unsubscribe\_messages\_total | counter | The total number of unsubscribe messages routed by a bondy node since reset |
| bondy\_wamp\_unsubscribed\_messages\_total | counter | The total number of unsubscribed messages routed by a bondy node since reset |
| bondy\_wamp\_welcome\_messages\_total | counter | The total number of welcome messages routed by a bondy node since reset |
| bondy\_wamp\_yield\_messages\_total | counter | The total number of yield messages routed by a bondy node since reset |
| cowboy\_early\_errors\_total | counter | cowboy\_early\_errors\_total Total number of Cowboy early errors |
| cowboy\_errors\_total | counter | cowboy\_errors\_total Total number of Cowboy request errors |
| cowboy\_protocol\_upgrades\_total | counter | cowboy\_protocol\_upgrades\_total Total number of protocol upgrades |
| cowboy\_receive\_body\_duration\_seconds | histogram | cowboy\_receive\_body\_duration\_seconds Request body receiving duration |
| cowboy\_request\_duration\_seconds | histogram | cowboy\_request\_duration\_seconds Cowboy request duration |
| cowboy\_requests\_total | counter | cowboy\_requests\_total Total number of Cowboy requests |
| cowboy\_spawned\_processes\_total | counter | cowboy\_spawned\_processes\_total Total number of spawned processes |
| erlang\_vm\_allocators | gauge | erlang\_vm\_allocators Allocated \(carriers\_size\) and used \(blocks\_size\) memory for the different allocators in the VM |
| erlang\_vm\_atom\_count | gauge | erlang\_vm\_atom\_count The number of atom currently existing at the local node |
| erlang\_vm\_atom\_limit | gauge | erlang\_vm\_atom\_limit The maximum number of simultaneously existing atom at the local node |
| erlang\_vm\_dirty\_cpu\_schedulers | gauge | erlang\_vm\_dirty\_cpu\_schedulers The number of scheduler dirty CPU scheduler threads used by the emulator |
| erlang\_vm\_dirty\_cpu\_schedulers\_online | gauge | erlang\_vm\_dirty\_cpu\_schedulers\_online The number of dirty CPU scheduler threads online |
| erlang\_vm\_dirty\_io\_schedulers | gauge | erlang\_vm\_dirty\_io\_schedulers The number of scheduler dirty I/O scheduler threads used by the emulator |
| erlang\_vm\_dist\_node\_state | gauge | erlang\_vm\_dist\_node\_state The current state of the distribution link |
| erlang\_vm\_dist\_port\_input\_bytes | gauge | erlang\_vm\_dist\_port\_input\_bytes The total number of bytes read from the port |
| erlang\_vm\_dist\_port\_memory\_bytes | gauge | erlang\_vm\_dist\_port\_memory\_bytes The total number of bytes allocated for this port by the runtime system |
| erlang\_vm\_dist\_port\_output\_bytes | gauge | erlang\_vm\_dist\_port\_output\_bytes The total number of bytes written to the port |
| erlang\_vm\_dist\_port\_queue\_size\_bytes | gauge | erlang\_vm\_dist\_port\_queue\_size\_bytes The total number of bytes queued by the port using the ERTS driver queue implementation |
| erlang\_vm\_dist\_proc\_heap\_size\_words | gauge | erlang\_vm\_dist\_proc\_heap\_size\_words The size in words of the youngest heap generation of the process |
| erlang\_vm\_dist\_proc\_memory\_bytes | gauge | erlang\_vm\_dist\_proc\_memory\_bytes The size in bytes of the process |
| erlang\_vm\_dist\_proc\_message\_queue\_len | gauge | erlang\_vm\_dist\_proc\_message\_queue\_len The number of messages currently in the message queue of the process |
| erlang\_vm\_dist\_proc\_min\_bin\_vheap\_size\_words | gauge | erlang\_vm\_dist\_proc\_min\_bin\_vheap\_size\_words The minimum binary virtual heap size for the process |
| erlang\_vm\_dist\_proc\_min\_heap\_size\_words | gauge | erlang\_vm\_dist\_proc\_min\_heap\_size\_words The minimum heap size for the process |
| erlang\_vm\_dist\_proc\_reductions | gauge | erlang\_vm\_dist\_proc\_reductions The number of reductions executed by the process |
| erlang\_vm\_dist\_proc\_stack\_size\_words | gauge | erlang\_vm\_dist\_proc\_stack\_size\_words The stack size, in words, of the process |
| erlang\_vm\_dist\_proc\_status | gauge | erlang\_vm\_dist\_proc\_status The current status of the distribution process |
| erlang\_vm\_dist\_proc\_total\_heap\_size\_words | gauge | erlang\_vm\_dist\_proc\_total\_heap\_size\_words The total size, in words, of all heap fragments of the process |
| erlang\_vm\_dist\_recv\_avg\_bytes | gauge | erlang\_vm\_dist\_recv\_avg\_bytes Average size of packets, in bytes, received by the socket |
| erlang\_vm\_dist\_recv\_bytes | gauge | erlang\_vm\_dist\_recv\_bytes Number of bytes received by the socket |
| erlang\_vm\_dist\_recv\_cnt | gauge | erlang\_vm\_dist\_recv\_cnt Number of packets received by the socket |
| erlang\_vm\_dist\_recv\_dvi\_bytes | gauge | erlang\_vm\_dist\_recv\_dvi\_bytes Average packet size deviation, in bytes, received by the socket |
| erlang\_vm\_dist\_recv\_max\_bytes | gauge | erlang\_vm\_dist\_recv\_max\_bytes Size of the largest packet, in bytes, received by the socket |
| erlang\_vm\_dist\_send\_avg\_bytes | gauge | erlang\_vm\_dist\_send\_avg\_bytes Average size of packets, in bytes, sent from the socket |
| erlang\_vm\_dist\_send\_bytes | gauge | erlang\_vm\_dist\_send\_bytes Number of bytes sent from the socket |
| erlang\_vm\_dist\_send\_cnt | gauge | erlang\_vm\_dist\_send\_cnt Number of packets sent from the socket |
| erlang\_vm\_dist\_send\_max\_bytes | gauge | erlang\_vm\_dist\_send\_max\_bytes Size of the largest packet, in bytes, sent from the socket |
| erlang\_vm\_dist\_send\_pend\_bytes | gauge | erlang\_vm\_dist\_send\_pend\_bytes Number of bytes waiting to be sent by the socket |
| erlang\_vm\_ets\_limit | gauge | erlang\_vm\_ets\_limit The maximum number of ETS tables allowed |
| erlang\_vm\_logical\_processors | gauge | erlang\_vm\_logical\_processors The detected number of logical processors configured in the system |
| erlang\_vm\_logical\_processors\_available | gauge | erlang\_vm\_logical\_processors\_available The detected number of logical processors available to the Erlang runtime system |
| erlang\_vm\_logical\_processors\_online | gauge | erlang\_vm\_logical\_processors\_online The detected number of logical processors online on the system |
| erlang\_vm\_memory\_atom\_bytes\_total | gauge | erlang\_vm\_memory\_atom\_bytes\_total The total amount of memory currently allocated for atoms |
| erlang\_vm\_memory\_bytes\_total | gauge | erlang\_vm\_memory\_bytes\_total The total amount of memory currently allocated |
| erlang\_vm\_memory\_dets\_tables | gauge | erlang\_vm\_memory\_dets\_tables Erlang VM DETS Tables count |
| erlang\_vm\_memory\_ets\_tables | gauge | erlang\_vm\_memory\_ets\_tables Erlang VM ETS Tables count |
| erlang\_vm\_memory\_processes\_bytes\_total | gauge | erlang\_vm\_memory\_processes\_bytes\_total The total amount of memory currently allocated for the Erlang processes |
| erlang\_vm\_memory\_system\_bytes\_total | gauge | erlang\_vm\_memory\_system\_bytes\_total The total amount of memory currently allocated for the emulator that is not directly related to any Erlang process |
| erlang\_vm\_msacc\_alloc\_seconds\_total | counter | erlang\_vm\_msacc\_alloc\_seconds\_total Total time in seconds spent managing memory |
| erlang\_vm\_msacc\_aux\_seconds\_total | counter | erlang\_vm\_msacc\_aux\_seconds\_total Total time in seconds spent handling auxiliary jobs |
| erlang\_vm\_msacc\_bif\_seconds\_total | counter | erlang\_vm\_msacc\_bif\_seconds\_total Total time in seconds spent in BIFs |
| erlang\_vm\_msacc\_busy\_wait\_seconds\_total | counter | erlang\_vm\_msacc\_busy\_wait\_seconds\_total Total time in seconds spent busy waiting |
| erlang\_vm\_msacc\_check\_io\_seconds\_total | counter | erlang\_vm\_msacc\_check\_io\_seconds\_total Total time in seconds spent checking for new I/O events |
| erlang\_vm\_msacc\_emulator\_seconds\_total | counter | erlang\_vm\_msacc\_emulator\_seconds\_total Total time in seconds spent executing Erlang processes |
| erlang\_vm\_msacc\_ets\_seconds\_total | counter | erlang\_vm\_msacc\_ets\_seconds\_total Total time in seconds spent executing ETS BIFs |
| erlang\_vm\_msacc\_gc\_full\_seconds\_total | counter | erlang\_vm\_msacc\_gc\_full\_seconds\_total Total time in seconds spent doing fullsweep garbage collection |
| erlang\_vm\_msacc\_gc\_seconds\_total | counter | erlang\_vm\_msacc\_gc\_seconds\_total Total time in seconds spent doing garbage collection |
| erlang\_vm\_msacc\_nif\_seconds\_total | counter | erlang\_vm\_msacc\_nif\_seconds\_total Total time in seconds spent in NIFs |
| erlang\_vm\_msacc\_other\_seconds\_total | counter | erlang\_vm\_msacc\_other\_seconds\_total Total time in seconds spent doing unaccounted things |
| erlang\_vm\_msacc\_port\_seconds\_total | counter | erlang\_vm\_msacc\_port\_seconds\_total Total time in seconds spent executing ports |
| erlang\_vm\_msacc\_send\_seconds\_total | counter | erlang\_vm\_msacc\_send\_seconds\_total Total time in seconds spent sending messages \(processes only\) |
| erlang\_vm\_msacc\_sleep\_seconds\_total | counter | erlang\_vm\_msacc\_sleep\_seconds\_total Total time in seconds spent sleeping |
| erlang\_vm\_msacc\_timers\_seconds\_total | counter | erlang\_vm\_msacc\_timers\_seconds\_total Total time in seconds spent managing timers |
| erlang\_vm\_port\_count | gauge | erlang\_vm\_port\_count The number of ports currently existing at the local node |
| erlang\_vm\_port\_limit | gauge | erlang\_vm\_port\_limit The maximum number of simultaneously existing ports at the local node |
| erlang\_vm\_process\_count | gauge | erlang\_vm\_process\_count The number of processes currently existing at the local node |
| erlang\_vm\_process\_limit | gauge | erlang\_vm\_process\_limit The maximum number of simultaneously existing processes at the local node |
| erlang\_vm\_schedulers | gauge | erlang\_vm\_schedulers The number of scheduler threads used by the emulator |
| erlang\_vm\_schedulers\_online | gauge | erlang\_vm\_schedulers\_online The number of schedulers online |
| erlang\_vm\_smp\_support | untyped | erlang\_vm\_smp\_support 1 if the emulator has been compiled with SMP support, otherwise 0 |
| erlang\_vm\_statistics\_bytes\_output\_total | counter | erlang\_vm\_statistics\_bytes\_output\_total Total number of bytes output to ports |
| erlang\_vm\_statistics\_bytes\_received\_total | counter | erlang\_vm\_statistics\_bytes\_received\_total Total number of bytes received through ports |
| erlang\_vm\_statistics\_context\_switches | counter | erlang\_vm\_statistics\_context\_switches Total number of context switches since the system started |
| erlang\_vm\_statistics\_dirty\_cpu\_run\_queue\_length | gauge | erlang\_vm\_statistics\_dirty\_cpu\_run\_queue\_length Length of the dirty CPU run-queue |
| erlang\_vm\_statistics\_dirty\_io\_run\_queue\_length | gauge | erlang\_vm\_statistics\_dirty\_io\_run\_queue\_length Length of the dirty IO run-queue |
| erlang\_vm\_statistics\_garbage\_collection\_bytes\_reclaimed | counter | erlang\_vm\_statistics\_garbage\_collection\_bytes\_reclaimed Garbage collection: bytes reclaimed |
| erlang\_vm\_statistics\_garbage\_collection\_number\_of\_gcs | counter | erlang\_vm\_statistics\_garbage\_collection\_number\_of\_gcs Garbage collection: number of GCs |
| erlang\_vm\_statistics\_garbage\_collection\_words\_reclaimed | counter | erlang\_vm\_statistics\_garbage\_collection\_words\_reclaimed Garbage collection: words reclaimed |
| erlang\_vm\_statistics\_reductions\_total | counter | erlang\_vm\_statistics\_reductions\_total Total reductions |
| erlang\_vm\_statistics\_run\_queues\_length\_total | gauge | erlang\_vm\_statistics\_run\_queues\_length\_total Length of normal run-queues |
| erlang\_vm\_statistics\_runtime\_milliseconds | counter | erlang\_vm\_statistics\_runtime\_milliseconds The sum of the runtime for all threads in the Erlang runtime system |
| erlang\_vm\_statistics\_wallclock\_time\_milliseconds | counter | erlang\_vm\_statistics\_wallclock\_time\_milliseconds Information about wall clock |
| erlang\_vm\_thread\_pool\_size | gauge | erlang\_vm\_thread\_pool\_size The number of async threads in the async thread pool used for asynchronous driver calls |
| erlang\_vm\_threads | untyped | erlang\_vm\_threads 1 if the emulator has been compiled with thread support, otherwise 0 |
| erlang\_vm\_time\_correction | untyped | erlang\_vm\_time\_correction 1 if time correction is enabled, otherwise 0 |
| erlang\_vm\_wordsize\_bytes | gauge | erlang\_vm\_wordsize\_bytes The size of Erlang term words in bytes |
| telemetry\_scrape\_duration\_seconds | summary | telemetry\_scrape\_duration\_seconds Scrape duration |
| telemetry\_scrape\_encoded\_size\_bytes | summary | telemetry\_scrape\_encoded\_size\_bytes Scrape size, encoded |
| telemetry\_scrape\_size\_bytes | summary | telemetry\_scrape\_size\_bytes Scrape size, not encoded |


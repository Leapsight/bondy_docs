# Features

## Router

At its core Bondy is a WAMP router, responsible for routing messages between WAMP clients, it does that by performing two main roles: _Dealer_ and _Broker_. In addition, the router is also responsible for many other tasks.

### Dealer

The Dealer is responsible for routing _remote procedure calls_ between _Callers_ and _Callees_, thus implementing Routed RPC.

In Routed RPC Caller and Callee do not know each other. The Caller makes a call request to the Router \(Dealer\) based on a known procedure, represented as a reverse URI e.g. `com.example-app.add`. The Dealer then finds a Callee who has registered an implementation of the procedure and forwards it the call. When the Callee replies with a response, the Dealer forwards the response to the Caller.

All this interaction is done asynchronously, thus neither the Caller nor the Callee are blocked. In fact, not even the Dealer is blocked.

#### Load Balancing

Bondy implements RPC load balancing. If multiple Callees \(or instances of the same Callee\) registered the same procedure, Bondy will load balance requests across those instances. Wether or not load balancing is used and which algorithm is controlled by the Callee during procedure registration.

### Broker

The Broker is responsible for routing _events_ between _Publishers_ and _Subscribers,_ thus implementing PubSub.

### Connection Management

The router is responsible for listening and handling new client connections through multiple transports and maintaining those connections.

* **Session management**, maintaining session state including the client's procedure registrations and subscriptions.
* **Transcoding**, encoding/decoding the messages according a Session's defined encoding


# Release Notes

## 0.8.6

{% hint style="info" %}
`docker pull leapsight/bondy:0.8.6`
{% endhint %}

### Added

* **Peer Discovery and Automatic Cluster join**
  * First implementation supporting a single discovery agent type \(`bondy_peer_discovery_dns_agent`\)  which uses DNS `srv` to lookup other Bondy nodes. Tested to work with Kubernetes DNS.
* **Security**
  * Authorisation
    * Added authorisation controls for all WAMP verbs \(register, unregister, call, cancel, publish, subscribe and unsubscribe\). 
    * Authorisation is managed by the existing Security subsystem which now can be configured using JSON files defined in the `bondy.conf` file \(in addition to the WAMP and HTTP/REST APIs\).
  * Authentication
    * Fixed WAMPRA \(with salted password\) authentication method.
      * This requires a rehash of the existing passwords. If you are migrating from an existing Bondy installation, the migration occurs lazily on the new user login \(as we need the user to provide the password for Bondy to be able to rehash, as Bondy never stores clear text passwords\).
* **Bondy Broker Bridge**
  * Finished Bondy Broker schema specification
  * First implementation of [Kafka Broker Bridge](configuring/broker-bridge/kafka-broker-bridge.md).

### Fixed

* **Security**
  * Authentication
    * Fixed WAMPRA \(with salted password\) authentication method.
      * This requires a rehash of the existing passwords. If you are migrating from an existing Bondy installation, the migration occurs lazily on the new user login \(as we need the user to provide the password for Bondy to be able to rehash, as Bondy never stores clear text passwords\).

### Changed

* **Configuration**
  * Refactoring of configuration via bondy.conf
  * Removed legacy config options.
  * Renamed a few a config options and introduced new ones to support static configuration via JSON files and new features like Peer Discovery and Automatic Cluster join.



### 

## 




# Release Notes

## 0.8.7

{% hint style="info" %}
`docker pull leapsight/bondy:0.8.7`
{% endhint %}

### Added

* **Phased Startup process.** The following `bondy.conf` options have been added to control when Bondy is allowed to start accepting client connections:
  * **`startup.wait_for_store_partitions` \(default: on\)** – Defines whether Bondy will wait for the db partitions to be initialised before continuing with initialisation. The HTTP listeners for the Admin API \(not the API Gateway\) are started at this point, enabling admins and tools to send requests to Bondy e.g. the Kubernetes Liveness probe can perform an HTTP GET on the `/ping` resource while Bondy finishes initialising. If the value provided is `off` then Bondy will not wait for the database to finish opening the store partitions and will disregard your configuration for the two following options assuming the configuration value was `off` for both of them.
  * **`startup.wait_for_store_hashtrees` \(default: on\)** – Defines whether Bondy will wait for the database Active Anti-entropy hashtrees to be built before continuing with initialisation. If the value provided is `off` then Bondy will not wait for the database to finish building the hashtrees and will disregard your configuration for the following option assuming the configuration value was `off` for it.
  * **`startup.wait_for_store_aae_exchange` \(default: off\)** – Defines whether Bondy will wait for the first Active Anti-entropy exchange to be finished before continuing with initialisation. All HTTP and TCP listeners will be started here enabling clients to connect via WAMP or HTTP \(API Gateway\).

### Fixed

* **Configuration**
  * Fixed a Realm update \(HTTP or WAMP\) issue that required the`private_keys` property to be present in the body.
  * Fixed a configuration issue that appears on Docker when mounting the /etc config path. All Bondy private configuration that previously resided in the advanced.config file is now managed separately \(privately\). The use of advanced.config is deprecated for now.
* **Security**
  * `com.leapsight.bondy` Admin Realm is now configurable via the Security JSON specification file
    * This was required to deal with the need for anonymous access to the Admin Realm e.g. for development purposes.
    * This will be restricted in the future as it currently allows peers to connect and \(given the correct permissions\) register WAMP Procedures which should not be enabled as this realm should only expose Bondy Admin WAMP APIs.

### Changed

* **Security**
  * Change treatment of anonymous in Security JSON specification file
    * For roles and usernames properties, the valid options are “all” or a list of roles \(including “anonymous” predefined role\)
* Dropped support for OTP versions prior to 21.2
* Upgraded `plum_db` version
* Replaced Flake IDs for KSUIDs for inter node message identification.
* Preliminary support for WAMP extended options
  * At the moment Bondy is very strict when it comes to parsing the WAMP message `options` and `details` and drops any property that is not part of the protocol. 
  * There is a new feature enabling to enunciate the extended options Bondy  should support but that has not been exposed yet to the config system as we are considering \(whilst following the protocol recommendation\) to allow any property commencing with the  _character e.g. `_my_property`instead._

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




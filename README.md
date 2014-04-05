# Vert.x Cassandra Persistor
This very simple [Vert.x][1] module allows to store and retrieve data from a [Cassandra][2] instance or cluster. It uses the the [DataStax Java Driver 2.0][3].

It is loosely based on the Vert.x [MongoDB persistor][4] and not optimized for highest performance (e.g. also no prepared statements) but straight-forward integration with Cassandra. 

* Module `com.nea.vertx~mod-cassandra-persistor~X.X.X`
* Worker Verticle
* Multi-threaded
* EventBus JSON-based
* CQL3

## Versions
* 0.0.1
    * Basic `raw` statement support

## Dependencies
This Persistor has only been developed and tested with Cassandra 2.x/CQL3. To use it you of course have to have a Cassandra instance running and accessible through the network, where this Module is running.

## Configuration
The Vert.x Cassandra Persistor takes the following configuration

    {
        "address": <address>,
        "hosts": [<hosts>],
        "keyspace": <keyspace>
    }

An exemplary configuration could look like

    {
        "address": "your.awesome.persistency",
        "hosts": ["192.168.172.33", "192.168.172.34"],
        "keyspace": "yourkeyspace"
    }

### Fields
* `address` *optional* The main address for the module. Every module has a main address. Defaults to `nea.vertx.cassandra.persistor`
* `hosts` *optional* A string array of host IPs the module connects to as contact points. Defaults to `127.0.0.1`
* `keyspace` *optional* The Cassandra keyspace to use. Defaults to `vertxpersistor`.

## Operations

### Raw
*Please use with care!*

    {
        "action": "raw",
        "statement": <cql3Statement>
    }
    
An example could look like

    {
        "action": "raw",
        "statement": "SELECT * FROM superkeyspace.tablewithinfos"
    }
    
#### Fields
`statement` A Cassandra Query Language version 3 (CQL3) compliant query that is channeled through to the driver and Cassandra. *Note: Do not forget the keyspace (e.g. `FROM keyspace.table`), even if configured, as the raw statements are not altered in any way!*

#### Returns
The `raw` action returns a `JsonArray` of `JsonObject`s in the format `columnName:columnValue` (if any result is given). *Note: Value types are not fully interpreted but generally covered as numbers, strings or collections!*

# Personal Note
*I don't know if this is very useful or already developed and published by others but I used it in private to test some ideas around Vert.x and Cassandra. As I was not able to find something similar very quickly I created this project. I hope this can be useful to you... with all its Bugs and Issues ;)* 

  [1]: http://vertx.io
  [2]: http://cassandra.apache.org/
  [3]: http://www.datastax.com/documentation/developer/java-driver/2.0
  [4]: https://github.com/vert-x/mod-mongo-persistor
# Other (splice out later)

## Performance vs Scalability

A service is `scalable` if it results in increased `performance` in a manner proportional to resources added. Increasing performance means serving more units of work (e.g. requests per second), and also ability to handle large units of work (e.g. a db query as database grows).

- If you have a `performance problem`, your system is slow for a single user.
- If you have a `scalability problem`, your system is fast for a single user but slow under heavy load.

## Latency vs Throughput

`Latency` is the time to perform some action or to produce some result.

`Throughput` is the number of such actions or results per unit of time.

Generally, you should aim for `maximal throughput` with `acceptable latency`.

## CAP Theorem

CAP theorem states that it is impossible for a distributed system to simultaneously provide all `three` of the following desirable properties:

`Consistency (C)`: All nodes see the same data at the same time. This means users can read or write from/to any node in the system and will receive the same data. It is equivalent to having a single up-to-date copy of the data.

`Availability (A)`: Every request receives a response, even if one or more nodes in the system go down, without guarantee that it contains the most recent version of the information.

`Partition tolerance (P)`: a partition is a fault in communication (usually network related) between two nodes that are running. A partition tolerant system continues to operate despite arbitrary partitioning.

## Consistency patterns

### Weak consistency

After a write, reads may or may not see it. A best effort approach is taken.

For example a phone call and you disconnect for a moment. When you later reconnect you don't hear what you missed.

### Eventual consistency

After a write, reads will eventually see it (typically within milliseconds). Data is replicated asynchronously.

### Strong consistency

After a write, reads will see it. Data is replicated synchronously. E.g. RDBM where it writes then waits streams to read replicas, then returns a response.

## Availability patterns

There are two complementary patterns to support high availability: `fail-over` and `replication`.

### Fail Over

#### Active-passive

Have a passive and active server, where only active handles traffic. Passive sends heartbeats to passive. If the passive does not receive a successful response, it takes over as the active server.

#### Active-active

Both servers are active.

#### Downsides

- Adds more complexity.
- There is a potential for loss of data if the active system fails before any newly written data can be replicated to the passive.

### Replication

#### Master-slave

The master serves reads and writes, replicating writes to one or more slaves, which serve only reads. Slaves can also replicate to additional slaves in a tree-like fashion. If the master goes offline, the system can continue to operate in read-only mode until a slave is promoted to a master or a new master is provisioned.

Disadvantages:

- complexity to promote a slave.

#### Master-master

Have two masters. Both masters serve reads and writes and coordinate with each other on writes. If either master goes down, the system can continue to operate with both reads and writes.

Disadvantages:

- Need to determine which master to write to.
- Either have loose consistency (violate ACID), or have increased write latency due to synchronization.

#### Disadvantages

- There is a potential for loss of data if the master fails before any newly written data can be replicated to other nodes.
- Read replicas can get bogged down with processing writes.
- The more read slaves, the more you have to replicate, which leads to greater replication lag.

### Availability numbers

Availability is often quantified by uptime (or downtime) as a percentage of time the service is available. E.g. 4 9's are 99.99% available.

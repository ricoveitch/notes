# ScyllaDB

- Session and yami don't require phone number

## Node

Computer running scylladb. Each node consists of `shards`. Each node is assinged a range of hash tokens which determine what rows it stores.

## Cluster

A minimum Cluster typically consists of at least three nodes. Data is replicated across the Cluster, depending on the Replication Factor.

## Replication Factor

Number of nodes where data (rows and partitions) are replicated. RF=3 means each row is replicated on three different nodes. (Done automatically)

## Replication Strategy

The Replication Strategy determines on which nodes replicas are placed.

- `SimpleStrategy`
- `Network Topology Strategy`

## Consistency Level

Number of nodes that must acknowledge read/write requests. For data to be successfully written or read back to the client, a sufficient number of nodes need to agree on the data’s correct state. ScyllaDB allows each operation (each read or write) to have its own consistency level, a feature known as tunable consistency.

- `ANY` – A write must be written to at least one replica in the cluster. A read waits for a response from at least one replica. It provides the highest availability with the lowest consistency.
- `QUORUM` – When a majority of the replicas respond, the request is honored. If RF=3, then 2 replicas respond. QUORUM can be calculated using the formula (n/2 +1) where n is the Replication Factor.
- `ONE` – If one replica responds; the request is honored.
- `LOCAL_ONE` – At least one replica in the local data center responds.
- `LOCAL_QUORUM` – A quorum of replicas in the local datacenter responds.
- `EACH_QUORUM` – (unsupported for reads) – A quorum of replicas in ALL datacenters must be written to.
- `ALL` – A write must be written to all replicas in the cluster, a read waits for a response from all replicas. Provides the lowest availability with the highest consistency.

## CQL

A query language for interacting with the ScyllaDB (or Cassandra) database.

## Coordinator Node

Within the ScyllaDB cluster, all internode communication is peer-to-peer, so there is no single point of failure. For communication outside of the cluster, such as a read or write, a ScyllaDB client will communicate with a single server node, called the coordinator. The selection of the coordinator is made with each client connection request to prevent bottlenecking requests through a single node.

## Keyspace

A Keyspace is a top-level container that stores tables with attributes that define how data is replicated on nodes. It defines a number of options that apply to all the tables it contains, most prominently of which is the replication strategy used by the Keyspace.  It is generally recommended to use one Keyspace per application, and thus a cluster may define only one Keyspace.

## Partition key

Gets hashed to get the node that the data is stored in. Because of this needs to be:

- needs to have high cardinality
- evenly distributed

A `hot` partition is when most of your traffic is going to one of a few of the same partitions.

## Clustering key

Its how the data is ordered on disk. Similar to a PK in SQL database. Allow useful range queries and aggregation. Allow useful limit. All the data within a partition is stored in continuous storage, sorted by clustering key columns.

Defining clustering key: `Create table t (...PRIMARY KEY ((app_name,env), hostname, log_datetime))`. First entry is for the partition key, the rest is for the clustering key. (sorted by hostname then log_datetime).

You can change the ordering of the clustering key (default is asc) by `CREATE TABLE T (...) WITH CLUSTERING ORDER BY (col desc)`.

## Materialized View

If you want to query something using where of a column, and you don't specify the partition key, will need to scan all partitions to find it. Can create a materialized view to take a transformation of the data. [38:00](https://www.youtube.com/watch?v=bTEfRmdBq7I). You are keeping the data twice on disk.

## Joins

Won't work since data is stored on different nodes and shards. There are 3rd party packages, but will result in full table scan.

## Scaling

- Scaling vertically (Hardware, more cpu's, ram)
- Add more read replicas
- Sharding

## Sharding

Each ScyllaDB node consists of several independent shards, which contain their share of the node’s total data. ScyllaDB creates a one shard per core (technically, one shard per hyperthread, meaning some physical cores may have two or more virtual cores). Each shard operates on a [shared-nothing architecture](https://en.wikipedia.org/wiki/Shared-nothing_architecture) basis. This means each shard is assigned its RAM and its storage, manages its schedulers for the CPU and I/O, performs its compactions (more about compaction later on), and maintains its multi-queue network connection. Each shard runs as a single thread, and communicates asynchronously with its peers, without locking.

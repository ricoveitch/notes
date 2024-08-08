# Major Components

![](images/major-components.png)

## 1. DNS

Notes [here](../../networks/networking-a-top-down-approach/2-application-layer.md#24-dnsthe-internets-directory-service).

### Multiple Load balancer use case

If your entry point is multiple load balancers can create A records for each of them.

```
example.com  A  192.0.2.1  (IP of Load Balancer 1)
example.com  A  192.0.2.2  (IP of Load Balancer 2)
example.com  A  192.0.2.3  (IP of Load Balancer 3)
```

This will work in a round robin fashion, as dns will return all of them but in a random order each time.

Tou could also use Alias records from a DNS provider to achieve more complicated routing as Weighted Round Robin, Latency-Based Routing, or Geolocation Routing (example.com -> example.com/nz).

## 2. Load Balancer

Used to distribute incoming network traffic across multiple servers. Crucial for scaling applications and efficiently managing server workloads.

Load balancers employ various `algorithms` to determine the distribution of incoming traffic. Some common algorithms include:

- `Round Robin`: Requests are sequentially and evenly distributed across all available servers in a cyclical manner.
- `Least Connections`: The load balancer assigns requests to the server with the fewest active connections, giving priority to less-busy servers.
- `IP Hash`: The client's IP address is hashed, and the resulting value is used to determine which server the request should be directed to. This method ensures that a specific client's requests are consistently routed to the same server, helping maintain session persistence.

You can have layer 4 (transport layer), and layer 7 (application layer) load balancers.

### Layer 4

Look at info at the transport layer, such as source and destinations IP's, ports, headers. It forwards network packets to and from the upstream server.

### Layer 7

Can look at application header, message, and cookies. An application load balancer can do request routing based on a path to a particular microservice, just like an API gateway.

## 3. API Gateway

Serves as a server or service that functions as an `intermediary` between external clients and the internal microservices or API-based backend services of an application.

It acts as a `reverse proxy` to route requests, simplify the API, and aggregate the results from various services.

The primary functions of an API Gateway encompass:

- `Request Routing`: The API Gateway directs incoming API requests from clients to the appropriate backend service or microservice, based on predefined rules and configurations.
- `Authentication and Authorization`: The API Gateway manages user authentication and authorization, ensuring that only authorized clients can access the services. It verifies API keys, tokens, or other credentials before routing requests to the backend services.
- `Rate Limiting and Throttling`: To safeguard backend services from excessive load or abuse, the API Gateway enforces rate limits or throttles requests from clients according to predefined policies.
- `Caching`: In order to minimize latency and backend load, the API Gateway caches frequently-used responses, serving them directly to clients without the need to query the backend services.
- `Request and Response Transformation`: The API Gateway can modify requests and responses, such as converting data formats, adding or removing headers, or altering query parameters, to ensure compatibility between clients and services.

Don't need to have one, the load balancer can just directly route to application servers. `Commonly used in microservices` architectures to provide a unified interface to a set of microservices, making it easier for clients to consume the services. E.g. if url is /api/x, depending on the x resource could route to a certain microservice.

## 4. CDN

See [here](./caching.md#cdn).

## 5. Forward Proxy vs. Reverse Proxy

### Forward Proxy

Also referred to as a "proxy server" or simply "proxy," is a server positioned in front of one or more client machines, acting as an intermediary between the clients and the internet.

When a client machine requests a resource on the internet, the request is initially sent to the forward proxy. The forward proxy then forwards the request to the internet on behalf of the client machine and returns the response to the client machine.

### Reverse Proxy

A server that sits in front of one or more web servers, serving as an intermediary between the web servers and the internet.

When a client requests a resource on the internet, the request is first sent to the reverse proxy. The reverse proxy then forwards the request to one of the web servers, which returns the response to the reverse proxy. Finally, the reverse proxy returns the response to the client.

## 6. Cache

In a distributed system, caching can occur in multiple locations, including the client, DNS, CDN, load balancer, API gateway, server, database, and more.

![](images/caches.svg)

## 7. Data Partitioning

### Horizontal Partitioning

Often referred to as `sharding`, entails `dividing the rows` of a table into smaller tables and storing them on distinct servers or database instances. This method is employed to distribute the database load across multiple servers (horizontally scaling), thereby enhancing performance.

### Vertical Partitioning

Involves `splitting the columns` of a table into separate tables. This technique aims to reduce the column count in a table and boost the performance of queries that only access a limited number of columns.

![](images/horizontal-vs-vertical-partitioning.png)

## 8. Database Replication

Maintain multiple copies of the same database across various servers or locations

The main objective of database replication is to enhance `data availability`, `redundancy`, and `fault tolerance`.

This process involves synchronizing data between the primary database and replicas, ensuring all possess the same up-to-date information.

## 9. Distributed Messaging Systems / Message Queues

Message queues receive, hold, and deliver messages. If an operation is too slow to perform inline, you can use a message queue with the following workflow:

- An application publishes a job to the queue, then notifies the user of job status
- A worker picks up the job from the queue, processes it, then signals the job is complete

The user is not blocked and the job is processed in the background. During this time, the client might optionally do a small amount of processing to make it seem like the task has completed. For example, if posting a tweet, the tweet could be instantly posted to your timeline, but it could take some time before your tweet is actually delivered to all of your followers.

E.g Amazon SQS

## 10. Microservices

Where an application is organized as an assembly of small, loosely-coupled, and autonomously deployable services.

Microservices interact with each other using lightweight protocols, such as HTTP/REST, gRPC, or message queues.

## 11. NoSQL Databases

Four main types:

- `Document-Based`: These databases store data in document-like structures, such as JSON or BSON. Each document is self-contained and can have its own unique structure, making them suitable for handling heterogeneous data. Examples of document-based NoSQL databases include MongoDB and Couchbase.
- `Key-Value`: These databases store data as key-value pairs, where the key acts as a unique identifier, and the value holds the associated data. Key-value databases are highly efficient for simple read and write operations, and they can be easily partitioned and scaled horizontally. Examples of key-value NoSQL databases include `Redis` and Amazon DynamoDB.
- `Column-Family`: These databases store data in column families, which are groups of related columns. They are designed to handle write-heavy workloads and are highly efficient for querying data with a known row and column keys. Examples of column-family NoSQL databases include `Apache Cassandra` and HBase.
- `Graph-Based`: These databases are designed for storing and querying data that has`complex relationships` and interconnected structures, such as social networks or recommendation systems. Graph databases use nodes, edges, and properties to represent and store data, making it easier to perform complex traversals and relationship-based queries. Examples of graph-based NoSQL databases include Neo4j and Amazon Neptune.

See more on key-value databases [here](../database/scylla-db.md).

## 12. Database Index

See [here](../database/indexes.md)

## 13. Distributed File Systems

Distributed file systems are storage systems designed to manage and grant access to files and directories across multiple servers, nodes, or machines, frequently distributed across a network. They allow users and applications to access and modify files as though they were situated on a local file system, despite the fact that the actual files may be physically located on various remote servers.

Distributed file systems are commonly employed in large-scale or distributed computing environments to offer fault tolerance, high availability, and enhanced performance.

E.g. Amazon S3.

## 14. Notification System

These are used to send notifications or alerts to users, such as emails, push notifications, or text messages.

## 15. Full-text Search

Full-text search allows users to search for particular words or phrases within an application or website. Upon receiving a user query, the application or website delivers the most relevant results.

To accomplish this rapidly and effectively, full-text search utilizes an `inverted index`, a data structure that associates words or phrases with the documents where they are found. E.g. a token "cat" maps to documents 2,4,7.

Elastic Search is an example of such systems.

## 16. Distributed Coordination Services

Systems or protocols designed to coordinate and manage the interactions between distributed components in a network, ensuring that they work together harmoniously.

These services are essential in distributed computing environments, where multiple machines or nodes must cooperate to perform tasks, share resources, and maintain consistency.

## 17. Heartbeat

To efficiently route requests in such a setup, servers need to know what other servers are part of the system. Furthermore, servers should know if other servers are alive and working.

To solve this, each server periodically sends a heartbeat message to a central monitoring server or other servers in the system to show that it is still alive and functioning.

## 18. Checksum

To calculate a checksum, a cryptographic hash-function like MD5, SHA-1, SHA-256, or SHA-512 is used.

When a system is storing some data, it computes a checksum of the data and stores the checksum with the data. When a client retrieves data, it verifies that the data it received from the server matches the checksum stored. If not, then the client can opt to retrieve that data from another replica.

## MISC

### Load balancer vs api gateway vs reverse proxy

- Reverse proxy is; load balancer + (rate limiting, auth, ip filtering, caching, ssl).
- Api gateway is; reverse proxy + (service discovery, Circuit breaker).

Load balancers distribute network traffic. An API gateway is typically a centralized entry point for your service layer.

### Load balancer before api gateway?

Yes generally speaking. You might need to add api gateways in the future, and easier to add one off a load balancer.

```
Client -> Load Balancer -> API Gateway -> Load Balancer -> Backend Services
```

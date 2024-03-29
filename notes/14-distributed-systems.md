# Distributed Systems

## Distributed Systems

- [Distributed Systems lecture series](https://www.youtube.com/playlist?list=PLeKd45zvjcDFUEv_ohr_HdUFe97RItdiB)
- [CSE 291 Lecture Resources](https://cseweb.ucsd.edu/classes/sp16/cse291-e/applications/lecture.html)
- [A Distributed Systems Reading List](https://dancres.github.io/Pages/)
- [Scalable Web Architecture and Distributed Systems](https://github.com/checkcheckzz/system-design-interview/blob/master/README.md#bk)
- [A Note on Distributed System](https://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.41.7628)
- [https://timilearning.com/1/](https://timilearning.com/1/)
- [https://pdos.csail.mit.edu/6.824/schedule.html](https://pdos.csail.mit.edu/6.824/schedule.html)
- [https://github.com/theanalyst/awesome-distributed-systems](https://github.com/theanalyst/awesome-distributed-systems)
- [https://github.com/aphyr/distsys-class](https://github.com/aphyr/distsys-class)
- [https://lethain.com/introduction-to-architecting-systems-for-scale/](https://lethain.com/introduction-to-architecting-systems-for-scale/)
- [https://www.somethingsimilar.com/2013/01/14/notes-on-distributed-systems-for-young-bloods/](https://www.somethingsimilar.com/2013/01/14/notes-on-distributed-systems-for-young-bloods/)
- [http://book.mixu.net/distsys/single-page.html](http://book.mixu.net/distsys/single-page.html)
- [https://www.simpleorientedarchitecture.com/8-fallacies-of-distributed-systems/](https://www.simpleorientedarchitecture.com/8-fallacies-of-distributed-systems/)
- [https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying](https://engineering.linkedin.com/distributed-systems/log-what-every-software-engineer-should-know-about-real-time-datas-unifying)
- [https://horicky.blogspot.com/2009/11/nosql-patterns.html](https://horicky.blogspot.com/2009/11/nosql-patterns.html)
- [https://www.allthingsdistributed.com/2007/10/amazons_dynamo.html](https://www.allthingsdistributed.com/2007/10/amazons_dynamo.html)
- [https://jepsen.io/analyses](https://jepsen.io/analyses)
- [https://jepsen.io/consistency](https://jepsen.io/consistency)
- [https://peter.bourgon.org/ok-log/](https://peter.bourgon.org/ok-log/)
- [https://www.rabbitmq.com/tutorials/amqp-concepts.html](https://www.rabbitmq.com/tutorials/amqp-concepts.html)
- [https://www.erlang-solutions.com/blog/an-introduction-to-rabbitmq-what-is-rabbitmq.html](https://www.erlang-solutions.com/blog/an-introduction-to-rabbitmq-what-is-rabbitmq.html)
- [https://fabxc.org/tsdb/](https://fabxc.org/tsdb/)

## Fallacies of Distributed Computing

Summary of this [article](https://pages.cs.wisc.edu/~zuyu/files/fallacies.pdf).

1. **The network is reliable**: Hardware and software can \(and will\) fail. Think about redundancy for both. On the software side, messages/calls will get lost over the wire. Mitigate with a medium that supplies more reliable messaging \(ex: message queues\). Prepare to retry/acknowledge messages, identify/ignore duplicates \(or use idempotent messages\), reorder messages \(or not\), verify integrity, etc.
2. **Latency is zero**: Latency is how much time it takes for data to move from one place to another. The minimum round-trip time between two points of this earth is determined by the maximum speed of information transmission: the speed of light. It will always take at least 30 milliseconds to send a ping from Europe to the US and back, even if the processing would be done in real time.
3. **Bandwidth is infinite**: Bandwidth is how much data can be transferred during a period of time. Bandwidth is constantly getting better, but so does the amount of information we try to squeeze through it. Also, packet loss and frame size have limitations.
4. **The network is secure**: Need to build security into solutions from Day 1. Security is a system quality attribute. Perform threat modeling to evaluate the security risks. Take measures to mitigate risks \(a tradeoff between costs, risks and their probability\). Security is usually a multi-layered solution that is handled on the network, infrastructure, and application levels.
5. **Topology doesn't change**: Try not to depend on specific endpoints or routes, if you can't be prepared to renegotiate endpoints. Either provide location transparency \(ex: service bus, multicast\) or provide discovery services. Abstract the physical structure of the network \(ex: dns\).
6. **There is one administrator**: Provide tools to diagnose and find problems. Include tools for monitoring on-going operations. Design interoperability contracts. Facilitate upgrades.
7. **Transport cost is zero**: Going from the application level to the transport level is not free \(information need to be serialized into bits to get data into the wire\). The costs \(as in cash money\) for setting and running the network are not free: hardware, peoplel bandwidth etc.
8. **The network is homogeneous**: should not cause too much trouble at the IP layer but is quite relevant at the application level. Assume interoperability will be needed sooner or later and be ready to support it from day one. Do not rely on proprietary protocols. Use standard technologies that are widely accepted.

## Distributed Consensus Algorithms

- Link to the codemesh talk

### Paxos

### Raft

- https://nexteven.com/making-sense-of-the-raft-distributed-consensus-algorithm%e2%80%8a-%e2%80%8apart-1/
- https://nexteven.com/making-sense-of-the-raft-distributed-consensus-algorithm%e2%80%8a-%e2%80%8apart-2/
- https://nexteven.com/making-sense-of-the-raft-distributed-consensus-algorithm%e2%80%8a-%e2%80%8apart-3/

### Byzantine Fault Tolerance

- Link to the codemesh talk

## Conflict-free replicated data type

## NoSQL

- [https://linkedin.github.io/school-of-sre/databases_nosql/intro/](https://linkedin.github.io/school-of-sre/databases_nosql/intro/)

### Cassandra

#### Rules of Data Modeling

DO NOT:

- **Minimize the Number of Writes**: Cassandra is optimized for high write throughput. Extra writes to improve the efficiency of your read queries, it's almost always a good tradeoff.
- **Minimize Data Duplication**: Disk space is cheap and Cassandra is architected around that fact. To get the most efficient reads, you often need to duplicate data. Cassandra doesn't have JOINs either.

DO:

- **Spread data evenly around the cluster**: You want every node in the cluster to have roughly the same amount of data. Rows are spread around the cluster based on a hash of the partition key, which is the first element of the primary key. 
- **Minimize the number of partitions read**: Partitions are groups of rows that share the same partition key. When you issue a read query, you want to read rows from as few partitions as possible. Each partition may reside on a different node.

**Model Around Your Queries**

The way to minimize partition reads is to model your data to fit your queries. Don't model around relations. Don't model around objects. Model around your queries.

1. **Determine What Queries to Support**: you may need to think about grouping by, ordering by, filtering by enforcing uniqueness.. changes to just one of these query requirements will frequently warrant a data model change.
2. **Try to create a table where you can satisfy your query by reading (roughly) one partition**: In practice, this generally means you will use roughly one table per query pattern

Some of Cassandra's fancier features, like **collections, user-defined types, and static columns**, can also be used to reduce the number of partitions that you need to read to satisfy a query. Don't forget to consider these options when designing your schema. 

#### Resources

- [Basic Rules of Cassandra Data Modeling](https://www.datastax.com/blog/basic-rules-cassandra-data-modeling)

## Big Data

- [Modern Big Data Architectures - Lambda & Kappa](https://luminousmen.com/post/modern-big-data-architectures-lambda-kappa)
- [https://linkedin.github.io/school-of-sre/big_data/intro/](https://linkedin.github.io/school-of-sre/big_data/intro/)

Big data architecture:

- Lambda architecture: stream + batch processing
- Kappa architecture: everything is a stream

Streaming Message Delivery Guarantees:

- At most once
- At least once
- Exactly once

2 main implementations of streaming system:

- Native Streaming (one by one processing)
- Micro Batching (defined by size or time constant)

## Scalability, Availability & Stability Patterns

- [https://www.slideshare.net/jboner/scalability-availability-stability-patterns](https://www.slideshare.net/jboner/scalability-availability-stability-patterns)
- [https://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html](https://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html)
- [https://horicky.blogspot.com/2009/11/nosql-patterns.html](https://horicky.blogspot.com/2009/11/nosql-patterns.html)
- [https://tom-e-white.com/2007/11/consistent-hashing.html](https://tom-e-white.com/2007/11/consistent-hashing.html)
- [https://www.microsoft.com/en-us/research/uploads/prod/2016/12/paxos-simple-Copy.pdf](https://www.microsoft.com/en-us/research/uploads/prod/2016/12/paxos-simple-Copy.pdf)
- [https://github.com/henryr/cap-faq](https://github.com/henryr/cap-faq)
- [http://ksat.me/a-plain-english-introduction-to-cap-theorem](http://ksat.me/a-plain-english-introduction-to-cap-theorem)

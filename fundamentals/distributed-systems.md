# Distributed Systems

- [A Distributed Systems Reading List](https://dancres.github.io/Pages/)
- [Scalable Web Architecture and Distributed Systems](https://github.com/checkcheckzz/system-design-interview/blob/master/README.md#bk)
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

# Basic Knowledge

## Fallacies of Distributed Computing

Summary of this [article](https://pages.cs.wisc.edu/~zuyu/files/fallacies.pdf).

1. **The network is reliable**: Hardware and software can (and will) fail. Think about redundancy for both. On the software side, messages/calls will get lost over the wire. Mitigate with a medium that supplies more reliable messaging (ex: message queues). Prepare to retry/acknowledge messages, identify/ignore duplicates (or use idempotent messages), reorder messages (or not), verify integrity, etc.

2. **Latency is zero**: Latency is how much time it takes for data to move from one place to another. The minimum round-trip time between two points of this earth is determined by the maximum speed of information transmission: the speed of light. It will always take at least 30 milliseconds to send a ping from Europe to the US and back, even if the processing would be done in real time.

3. **Bandwidth is infinite**: Bandwidth is how much data can be transferred during a period of time. Bandwidth is constantly getting better, but so does the amount of information we try to squeeze through it. Also, packet loss and frame size have limitations.

4. **The network is secure**: Need to build security into solutions from Day 1. Security is a system quality attribute. Perform threat modeling to evaluate the security risks. Take measures to mitigate risks (a tradeoff between costs, risks and their probability). Security is usually a multi-layered solution that is handled on the network, infrastructure, and application levels.

5. **Topology doesn't change**: Try not to depend on specific endpoints or routes, if you can't be prepared to renegotiate endpoints. Either provide location transparency (ex: service bus, multicast) or provide discovery services. Abstract the physical structure of the network (ex: dns).

6. **There is one administrator**: Provide tools to diagnose and find problems. Include tools for monitoring on-going operations. Design interoperability contracts. Facilitate upgrades.

7. **Transport cost is zero**: Going from the application level to the transport level is not free (information need to be serialized into bits to get data into the wire). The costs (as in cash money) for setting and running the network are not free: hardware, peoplel bandwidth etc.

8. **The network is homogeneous**: should not cause too much trouble at the IP layer but is quite relevant at the application level. Assume interoperability will be needed sooner or later and be ready to support it from day one. Do not rely on proprietary protocols. Use standard technologies that are widely accepted.

## Numbers Everyone Should Know

Summary of this [article](https://everythingisdata.wordpress.com/2009/10/17/numbers-everyone-should-know/). A table of the cost of some fundamental operations to be able to do quick _Back-of-the-envelope analysis_ and _Microbenchmarking_.

| Operation                           | Time (nanoseconds) |
| ----------------------------------- | -----------------: |
| L1 cache reference                  |                0.5 |
| Branch mispredict                   |                  5 |
| L2 cache reference                  |                  7 |
| Mutex lock/unlock                   |                 25 |
| Main memory reference               |                100 |
| System call overhead                |                400 |
| Compress 1KB bytes with Zippy       |              3 000 |
| Context switch between processes    |              3 000 |
| Send 2K bytes over 1 Gbps network   |             20 000 |
| fork() (statically-linked binary)   |             70 000 |
| fork() (dynamically-linked binary)  |            160 000 |
| Read 1MB sequentially from memory   |            250 000 |
| Roundtrip within same datacenter    |            500 000 |
| Disk seek                           |         10 000 000 |
| Read 1MB sequentially from disk     |         20 000 000 |
| Send packet CA -> Netherlands -> CA |       150 000 0000 |

## Introduction to architecting systems for scale

Combination of this [article](https://lethain.com/introduction-to-architecting-systems-for-scale/) and this [chapter](https://www.aosabook.org/en/distsys.html) of the Architecture of Open Source Applications book.

# Scalability, Availability & Stability Patterns

- [https://www.slideshare.net/jboner/scalability-availability-stability-patterns](https://www.slideshare.net/jboner/scalability-availability-stability-patterns)
- [https://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html](https://horicky.blogspot.com/2010/10/scalable-system-design-patterns.html)
- [https://horicky.blogspot.com/2009/11/nosql-patterns.html](https://horicky.blogspot.com/2009/11/nosql-patterns.html)
- [https://tom-e-white.com/2007/11/consistent-hashing.html](https://tom-e-white.com/2007/11/consistent-hashing.html)
- [https://www.microsoft.com/en-us/research/uploads/prod/2016/12/paxos-simple-Copy.pdf](https://www.microsoft.com/en-us/research/uploads/prod/2016/12/paxos-simple-Copy.pdf)
- [https://github.com/henryr/cap-faq](https://github.com/henryr/cap-faq)
- [http://ksat.me/a-plain-english-introduction-to-cap-theorem](http://ksat.me/a-plain-english-introduction-to-cap-theorem)

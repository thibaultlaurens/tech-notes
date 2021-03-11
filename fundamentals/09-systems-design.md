# Systems Design

## Introduction To Architecting Systems or Scale

- https://lethain.com/introduction-to-architecting-systems-for-scale/
- https://www.aosabook.org/en/distsys.html

### Load Balancing

### Caching

### Content distribution networks

### Off-line processing

### Database Scaling

## Back of the envelope Estimation

### Latency Numbers

| Operation                                 |         Time ns |    Time μs | Time ms | Comments                    |
| ----------------------------------------- | --------------: | ---------: | ------: | --------------------------- |
| L1 cache reference                        |          0.5 ns |            |         |                             |
| Branch mispredict                         |            5 ns |            |         |                             |
| L2 cache reference                        |            7 ns |            |         | 14x L1 cache                |
| Mutex lock/unlock                         |           25 ns |            |         |                             |
| Main memory reference                     |          100 ns |            |         | 20x L2 cache, 200x L1 cache |
| System call overhead                      |          400 ns |            |         |                             |
| Compress 1KB bytes with Zippy             |        3,000 ns |       3 μs |         |                             |
| Context switch between processes          |        3,000 ns |       3 μs |         |                             |
| Send 1K bytes over 1 Gbps network         |       10,000 ns |      10 μs |         |                             |
| fork\(\) \(statically-linked binary\)     |       70,000 ns |      70 μs |         |                             |
| Read 4K randomly from SSD                 |      150,000 ns |     150 μs |         | ~1GB/sec SSD                |
| fork\(\) \(dynamically-linked binary\)    |      160,000 ns |     160 μs |         |                             |
| Read 1MB sequentially from memory         |      250,000 ns |     250 μs |         |                             |
| Roundtrip within same datacenter          |      500,000 ns |     500 μs |         |                             |
| Read 1 MB sequentially from SSD           |    1,000,000 ns |   1,000 us |    1 ms | ~1GB/sec SSD, 4X memory     |
| Disk seek                                 |   10,000,000 ns |  10,000 μs |   10 ms | 20x datacenter roundtrip    |
| Read 1MB sequentially from disk           |   20,000,000 ns |  20,000 μs |   20 ms | 80x memory, 20X SSD         |
| Send packet CA -&gt; Netherlands -&gt; CA | 150,000,0000 ns | 150,000 μs |  150 ms |                             |

### Availability Numbers

| Availability %          | Downtime per year | Downtime per month  | Downtime per week   | Downtime per day    |
| ----------------------- | ----------------- | ------------------- | ------------------- | ------------------- |
| 90% (one nine)          | 36.53 days        | 73.05 hours         | 16.80 hours         | 2.40 hours          |
| 99% (two nines)         | 3.65 days         | 7.31 hours          | 1.68 hours          | 14.40 minutes       |
| 99.9% (three nines)     | 8.77 hours        | 43.83 minutes       | 10.08 minutes       | 1.44 minutes        |
| 99.99% (four nines)     | 52.60 minutes     | 4.38 minutes        | 1.01 minutes        | 8.64 seconds        |
| 99.999% (five nines)    | 5.26 minutes      | 26.30 seconds       | 6.05 seconds        | 864.00 milliseconds |
| 99.9999% (six nines)    | 31.56 seconds     | 2.63 seconds        | 604.80 milliseconds | 86.40 milliseconds  |
| 99.99999% (seven nines) | 3.16 seconds      | 262.98 milliseconds | 60.48 milliseconds  | 8.64 milliseconds   |

## Rate Limiter

## Consistent Hashing

## Key-Value Store

## UUID Generator

## URL Shortener

## Web Crawler

## Notification

## News Feed

## Chat

## Search Autocomplete

## Youtube

## Google

## Resources

- [Numbers Everyone Should Know](https://everythingisdata.wordpress.com/2009/10/17/numbers-everyone-should-know/)
- [School of SRE](https://linkedin.github.io/school-of-sre/systems_design/intro/)
- [The System Design Primer](https://github.com/donnemartin/system-design-primer)
- [The Architecture of Open Source Applications](https://aosabook.org/en/index.html)
- [System Design Interview](https://www.goodreads.com/book/show/54109255-system-design-interview-an-insider-s-guide)

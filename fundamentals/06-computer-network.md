# Computer Networking

Leading organizations for standardization:

- The **International Organization for Standardization** ([ISO](https://en.wikipedia.org/wiki/International_Organization_for_Standardization))
- The **American National Standards Institute** ([ANSI](https://en.wikipedia.org/wiki/American_National_Standards_Institute))
- The **Internet Engineering Task Force** ([IETF](https://en.wikipedia.org/wiki/Internet_Engineering_Task_Force))

## Network Types

Common types of networks include the following:

- **Local Area Network** (LAN): The computers are geographically close together (that is, in the same building).
- **Wide Area Network** (WAN): The computers are farther apart and are connected by telephone lines or radio waves.
- **Metropolitan Area Network** (MAN): A data network designed for a town or city.
- **Home Area Network** (HAN): A network contained within a user’s home that connects a person’s digital devices.
- **Virtual Private Network** (VPN): A network that is constructed by using public wires usually the Internet to connect to a private network, such as a company’s internal network.
- **Storage Area Network** (SAN): A high-speed network of storage devices that also connects those storage devices with servers.

![network-area-types](../.gitbook/assets/network-area-types.jpg)

### Local Area Network (LAN)

A LAN connects network devices in such a way that personal computer and workstations can share data, tools and programs. The group of computers and devices are connected together by a switch, or stack of switches, using a **private addressing scheme** as defined by the TCP/IP protocol. Private addresses are unique in relation to other computers on the local network. Routers are found at the boundary of a LAN, connecting them to the larger WAN.

Data transmits at a very fast rate as the number of computers linked are limited. LANs cover smaller geographical area (Size is limited to a few kilometers) and are privately owned. One can use it for an office building, home, hospital, schools, etc. LAN is easy to design and maintain. A Communication medium used for LAN has twisted pair cables and coaxial cables. It covers a short distance, and so the error and noise are minimized.

Early LAN’s had data rates in the 4 to 16 Mbps range. Today, speeds are normally 100 or 1000 Mbps. Propagation delay is very short in a LAN. The smallest LAN may only use two computers, while larger LANs can accommodate thousands of computers. A LAN typically relies mostly on wired connections for increased speed and security, but wireless connections can also be part of a LAN. The fault tolerance of a LAN is more and there is less congestion in this network.

### Metropolitan Area Network (MAN)

A MAN covers a larger area than that of a LAN and smaller area as compared to WAN. It connects two or more computers that are apart but resides in the same or different cities. It covers a large geographical area and may serve as an ISP (**Internet Service Provider**). MAN is designed for customers who need a high-speed connectivity. Speeds of MAN ranges in terms of Mbps. It’s hard to design and maintain a Metropolitan Area Network.

The fault tolerance of a MAN is less and also there is more congestion in the network. It is costly and may or may not be owned by a single organization. The data transfer rate and the propagation delay of a MAN is moderate. Devices used for transmission of data through MAN are: Modem and Wire/Cable. Examples of a MAN are the part of the telephone company network that can provide a high-speed DSL line to the customer or the cable TV network in a city.

### Wide Area Network (WAN)

A WAN is a computer network that extends over a large geographical area, although it might be confined within the bounds of a state or country. A WAN could be a connection of LAN connecting to other LAN’s via telephone lines and radio waves and may be limited to an enterprise (a corporation or an organization) or accessible to the public. The technology is high speed and relatively expensive.

There are two types of WAN: **Switched WAN** and **Point-to-Point WAN**. WAN is difficult to design and maintain. Similar to a MAN, the fault tolerance of a WAN is less and there is more congestion in the network. A Communication medium used for WAN is PSTN or Satellite Link. Due to long distance transmission, the noise and error tend to be more in WAN.

WAN’s data rate is slow about a 10th LAN’s speed, since it involves increased distance and increased number of servers and terminals etc. Speeds of WAN ranges from few kilobits per second (Kbps) to megabits per second (Mbps). Propagation delay is one of the biggest problems faced here. Devices used for transmission of data through WAN are: Optic wires, Microwaves and Satellites. Example of a Switched WAN is the asynchronous transfer mode (ATM) network and Point-to-Point WAN is dial-up line that connects a home computer to the Internet.

## Network Topology

![network-topology-types](../.gitbook/assets/network-topology-types.png)

A network topology describes the physical composition of a network. Topologies are either physical or logical. There are four principal topologies used in LANs.

### Bus Topology

All devices are connected to a central cable, called the **bus** or **backbone**. Bus networks are relatively inexpensive and easy to install for small networks. The data is transmitted one end to another in single direction. No bi-directional feature is in bus topology. Even though it's the simplest type of network to implement, there are limitations to it. The first limitation is the length of the main cable or bus. The longer it gets, the higher the chance of signal dropout. This limitation constrains the physical layout of the network. All devices have to be physically located near each other, for example, in the same room. Finally, if there's a break in the bus cable, the whole network fails.

### Ring topology

All devices are connected to one another in the shape of a **closed loop**, so that each device is connected directly to two other devices, one on either side of it. This form of network is more resilient than the bus topology. A break in the cable ring also affects the performance of the network. The transmission is unidirectional, but it can be made bidirectional by having 2 connections between each Network Node, it is called **Dual Ring Topology**.

### Mesh topology

The mesh topology is described as either a **physical mesh** or a **logical mesh**. In a physical mesh, each network device connects to every other network device in the network. It dramatically increases the resilience of a network but has the physical overhead of connecting all devices. Few networks today are built as a full mesh. Most networks use a partial mesh, where some machines interconnect, but others connect through one device. There's a subtle difference between a physical mesh network and a logical one. The perception is that most modern networks are mesh based, since each device can see and communicate with any other device on the network. This description is of a logical mesh network and is primarily made possible through the use of network protocols.

### Star topology

The star topology is the most commonly used network topology. Each network device connects to a centralized hub or switch. Switches and hubs can be linked together to extend and build more extensive networks. This type of typology is, by far, the most robust and scalable.

## Network Standards

## Network Protocols

- [https://linkedin.github.io/school-of-sre/linux_networking/intro/](https://linkedin.github.io/school-of-sre/linux_networking/intro/)
- [https://docs.microsoft.com/en-us/learn/modules/network-fundamentals/4-network-protocols](https://docs.microsoft.com/en-us/learn/modules/network-fundamentals/4-network-protocols)
- dns: [https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197427\(v=ws.10\)](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197427%28v=ws.10%29)
- dhcp
- tcp / udp
- OSI vs TCP/IP
- SSL
- TLS

### DNS

## IP address standards

- [https://docs.microsoft.com/en-us/learn/modules/network-fundamentals/5-ip-tcp-basics](https://docs.microsoft.com/en-us/learn/modules/network-fundamentals/5-ip-tcp-basics)

## Toolbox

From this [article](https://towardsdatascience.com/networking-tools-every-developer-needs-to-know-e17c9159b180)

- **ping**
- **dig**
- **netcat**
- **ip**
- **tracepath**
- **nmap**
- **ss**
- **tcpdump**
- **curl**: `curl | jq`
- **wget**

## Resources

- [Networking in a Day](https://cseweb.ucsd.edu/classes/sp16/cse291-e/applications/ln/lecture2.html)
- [Network Fundamentals Study Guide](https://www.webopedia.com/reference/network-fundamentals-study-guide/)
- [Fundamentals of computer networking](https://docs.microsoft.com/en-us/learn/modules/network-fundamentals/)
- [Computer Network Tutorials](https://www.geeksforgeeks.org/computer-network-tutorials)
- [The Internet](https://www.khanacademy.org/computing/computers-and-internet/xcae6f4a7ff015e7d:the-internet)

![network](NetAcad%20pictures/network.png)

![network](NetAcad%20pictures/OSI_Layers.png)

#
# Chapter 1 - Explore the Network

![UTP cable](NetAcad%20pictures/utp%20cable.png)
![Network Representations](NetAcad%20pictures/Network%20Representations.png)
![Intermediary Network Devices](netacad%20pictures/Intermediary%20Network%20Devices.png)

**Network Media**

- _Metallic wires within cables_ - data is encoded into electrical impulses
- _Glass or plastic fibers (fiber optic cable)_ - data is encoded as pulses of light
- _Wireless transmission_ - data is encoded using wavelengths from the electromagnetic spectrum

![Network Media](netacad%20pictures/Network%20Media.png)

Network infrastructures can vary greatly in terms of:

- Size of the area covered
- Number of users connected
- Number and types of services available
- Area of responsibility

![Physical Topologies](netacad%20pictures/Physical%20Topologies.png)

* **Local Area Network (LAN)** - A network infrastructure that provides access to users and end devices in a small geographical area, which is typically an enterprise, home, or small business network owned and managed by an individual or IT department.
* **Wide Area Network (WAN)** - A network infrastructure that provides access to other networks over a wide geographical area, which is typically owned and managed by a telecommunications service provider.

Other types of networks include:

- **Metropolitan Area Network (MAN)** - A network infrastructure that spans a physical area larger than a LAN but smaller than a WAN (e.g., a city). MANs are typically operated by a single entity such as a large organization.
- **Wireless LAN** **(WLAN)** - Similar to a LAN but wirelessly interconnects users and end points in a small geographical area.
- **Storage Area Network (SAN)** - A network infrastructure designed to support file servers and provide data storage, retrieval, and replication.

![Components of a Network](netacad%20pictures/Components%20of%20a%20Network.png)
![Network Fault Tolerance](netacad%20pictures/Network%20Fault%20Tolerance.png)
![Network Quality of Service](netacad%20pictures/Network%20Quality%20of%20Service.png)
![Network Scalability](netacad%20pictures/Network%20Scalability.png)

### Security Threats
![Network Security](netacad%20pictures/Network%20Security.png)

Must take into account the environment, as well as the tools and requirements of the network. It must be able to secure data while still allowing for the quality of service that is expected of the network. Securing a network involves protocols, technologies, devices, tools, and techniques to secure data and mitigate threats. Threat vectors may be external or internal. The most common external threats to networks include:

- _Viruses, worms, and Trojan horses_ - malicious software and arbitrary code running on a user device
- _Spyware and adware_ - software installed on a user device that secretly collects information about the user
- _Zero-day attacks, also called zero-hour attacks_ - an attack that occurs on the first day that a vulnerability becomes known
- _Hacker attacks_ - an attack by a knowledgeable person to user devices or network resources
- _Denial of service attacks_ - attacks designed to slow or crash applications and processes on a network device
- _Data interception and theft_ - an attack to capture private information from an organization’s network
- _Identity theft_ - an attack to steal the login credentials of a user in order to access private data

![Physical Layer](netacad%20pictures/The%20Physical%20Layer.png)
![Topology Diagrams - Logical](netacad%20pictures/Topology%20Diagrams%20-%20Logical.png)
![Topology Diagrams - Physical](netacad%20pictures/Topology%20Diagrams%20-%20Physical.png)

# Chapter 3 - Network Protocols and Communications

These are the rules of engagement for message timing.
**Access Method**
Access method determines when someone is able to send a message. If two people talk at the same time, a collision of information occurs and it is necessary for the two to back off and start again, as shown in the animation. Likewise, it is necessary for computers to define an access method. Hosts on a network need an access method to know when to begin sending messages and how to respond when collisions occur.
**Flow Control**
Timing also affects how much information can be sent and the speed that it can be delivered. If one person speaks too quickly, it is difficult for the other person to hear and understand the message. In network communication, source and destination hosts use flow control methods to negotiate correct timing for successful communication.
**Response Timeout**
If a person asks a question and does not hear a response within an acceptable amount of time, the person assumes that no answer is coming and reacts accordingly. The person may repeat the question, or may go on with the conversation. Hosts on the network also have rules that specify how long to wait for responses and what action to take if a response timeout occurs.

**_Protocol Interaction_**

- **HTTP -** is an application protocol that governs the way a web server and a web client interact. _HTTP defines the content and formatting of the requests and responses that are exchanged between the client and server_. Both the client and the web server software implement HTTP as part of the application. HTTP relies on other protocols to govern how the messages are transported between the client and server.
- **TCP** - is the transport protocol that manages the individual conversations. TCP divides the HTTP messages into smaller pieces, called segments. These segments are sent between the web server and client processes running at the destination host. TCP is also responsible for controlling the size and rate at which messages are exchanged between the server and the client.
- **IP** - is responsible for taking the formatted segments from TCP, encapsulating them into packets, assigning them the appropriate addresses, and delivering them to the destination host.
- **Ethernet** - is a network access protocol that describes two primary functions: communication over a data link and the physical transmission of data on the network media. Network access protocols are responsible for taking the packets from IP and formatting them to be transmitted over the media.

![Communicationg on a Local network](netacad%20pictures/Communicationg%20on%20a%20Local%20network.png)
![Communicating With Devices on the Same Network](netacad%20pictures/Communicating%20With%20Devices%20on%20the%20Same%20Network.png)

![Communicating to a Remote Network](netacad%20pictures/Communicating%20to%20a%20Remote%20Network.png)
![Communicating With a Device on a Remote Network](netacad%20pictures/Communicating%20With%20a%20Device%20on%20a%20Remote%20Network.png)


A protocol suite is a set of protocols that work together to provide comprehensive network communication services. A protocol suite may be specified by a standards organization or developed by a vendor.

The TCP/IP protocol suite is an open standard, meaning these protocols are freely available to the public, and any vendor is able to implement these protocols on their hardware or in their software.

A standards-based protocol is a process that has been endorsed by the networking industry and approved by a standards organization. The use of standards in developing and implementing protocols ensures that products from different manufacturers can inter operate successfully. If a protocol is not rigidly observed by a particular manufacturer, their equipment or software may not be able to successfully communicate with products made by other manufacturers.

Some protocols are proprietary which means one company or vendor controls the definition of the protocol and how it functions. Examples of proprietary protocols are AppleTalk and Novell Netware, which are legacy protocol suites. It is not uncommon for a vendor (or group of vendors) to develop a proprietary protocol to meet the needs of its customers and later assist in making that proprietary protocol an open standard.

## OSI Model

The protocols that make up the TCP/IP protocol suite can be described in terms of the OSI reference model. In the OSI model, the network access layer and the application layer of the TCP/IP model are further divided to describe discrete functions that must occur at these layers.

![Layer Protocol](netacad%20pictures/Layer%20Protocol.png)

At the network access layer, the TCP/IP protocol suite does not specify which protocols to use when transmitting over a physical medium; it only describes the hand off from the internet layer to the physical network protocols.

![Network Protocols Layered Model](netacad%20pictures/Network%20Protocols%20Layered%20Model.png)

_OSI Layers 1 and 2_ discuss the necessary procedures to access the media and the physical means to send data over a network.

_OSI Layer 3_, the network layer, maps directly to the TCP/IP Internet layer. This layer is used to describe protocols that address and route messages through an inter-network.

_OSI Layer 4_, the transport layer, maps directly to the TCP/IP Transport layer. This layer describes general services and functions that provide ordered and reliable delivery of data between source and destination hosts.

The TCP/IP application layer includes a number of protocols that provide specific functionality to a variety of end user applications.

_OSI model Layers 5, 6, and 7_ are used as references for application software developers and vendors to produce products that operate on networks.

Both the TCP/IP and OSI models are commonly used when referring to protocols at various layers. Because the OSI model separates the data link layer from the physical layer, it is commonly used when referring to these lower layers.
![Data Encapsulation in the Protocol Stack](netacad%20pictures/Data%20Encapsulation%20in%20the%20Protocol%20Stack.png)
![Data Segmentation](netacad%20pictures/Data%20Segmentation.png)

## Network Addresses

![Broadcast](netacad%20pictures/Broadcast.png)
![Unicast](netacad%20pictures/Unicast.png)

The network and data link layers are responsible for delivering the data from the source device to the destination device. Protocols at both layers contain a source and destination address, but their addresses have different purposes.

- **Network layer source and destination addresses** - Responsible for delivering the IP packet from the original source to the final destination, either on the same network or to a remote network.

- **Data link layer source and destination addresses** – Responsible for delivering the data link frame from one network interface card (NIC) to another NIC on the same network.

An IP address is the network layer, or Layer 3, logical address used to deliver the IP packet from the original source to the final destination. The IP packet contains two IP addresses:

- **Source IP address** - The IP address of the sending device, the original source of the packet.
- **Destination IP address** - The IP address of the receiving device, the final destination of the packet.

The data link, or Layer 2, physical address has a different role. The purpose of the data link address is to deliver the data link frame from one network interface to another network interface on the same network.
Before an IP packet can be sent over a wired or wireless network, it must be encapsulated in a data link frame so it can be transmitted over the physical medium.

As the IP packet travels from host-to-router, router-to-router, and finally router-to-host, at each point along the way the IP packet is encapsulated in a new data link frame. Each data link frame contains the source data link address of the NIC card sending the frame, and the destination data link address of the NIC card receiving the frame.

The Layer 2, data link protocol is only used to deliver the packet from NIC-to-NIC on the same network. The router removes the Layer 2 information as it is received on one NIC and adds new data link information before forwarding out the exit NIC on its way towards the final destination.

The IP packet is encapsulated in a data link frame that contains data link information, including a:

- **Source data link address** - The physical address of the device’s NIC that is sending the data link frame.
- **Destination data link address** - The physical address of the NIC that is receiving the data link frame. This address is either the next hop router or of the final destination device.

The data link frame also contains a trailer.

## Devices on the Same Network

To understand how devices communicate within a network, it is important to understand the roles of both the network layer addresses and the data link addresses.

**Role of the Network Layer Addresses**

The network layer addresses, or IP addresses, indicate the original source and final destination. An IP address contains two parts:

- **Network portion** – The left-most part of the address that indicates which network the IP address is a member. All devices on the same network will have the same network portion of the address.
- **Host portion** – The remaining part of the address that identifies a specific device on the network. The host portion is unique for each device on the network.

**Note**: The subnet mask is used to identify the network portion of an address from the host portion. The subnet mask is discussed in later chapters.

In this example we have a client computer, PC1, communicating with an FTP server on the same IP network.

- **Source IP address** - The IP address of the sending device, the client computer PC1: 192.168.1.110.
- **Destination IP address** - The IP address of the receiving device, FTP server: 192.168.1.9.

The network portion of both the source IP address and destination IP address are on the same network.

**Role of the Data Link Layer Addresses**

When the sender and receiver of the IP packet are on the same network, the data link frame is sent directly to the receiving device. On an Ethernet network, the data link addresses are known as Ethernet (Media Access Control) addresses. MAC addresses are physically embedded on the Ethernet NIC.

- **Source MAC address** - This is the data link address, or the Ethernet MAC address, of the device that sends the data link frame with the encapsulated IP packet. The MAC address of the Ethernet NIC of PC1 is AA-AA-AA-AA-AA-AA, written in hexadecimal notation.
- **Destination MAC address** - When the receiving device is on the same network as the sending device, this is the data link address of the receiving device. In this example, the destination MAC address is the MAC address of the FTP server: CC-CC-CC-CC-CC-CC, written in hexadecimal notation.

The frame with the encapsulated IP packet can now be transmitted from PC1 directly to the FTP server.

## Devices on a Remote Network

As an example we have a client computer, PC1, communicating with a server, named Web Server, on a different IP network.

![Network Addresses and Data Link Addresses](netacad%20pictures/Network%20Addresses%20and%20Data%20Link%20Addresses.png)

**Role of the Network Layer Addresses**

When the sender of the packet is on a different network from the receiver, the source and destination IP addresses will represent hosts on different networks. This will be indicated by the network portion of the IP address of the destination host.

- **Source IP address** - The IP address of the sending device, the client computer PC1: 192.168.1.110.

- **Destination IP address** - The IP address of the receiving device, the server, Web Server: 172.16.1.99.

Notice in the figure that the network portion of the source IP address and destination IP address are on different networks.

**Role of the Data Link Layer Addresses**

When the sender and receiver of the IP packet are on different networks, the Ethernet data link frame cannot be sent directly to the destination host because the host is not directly reachable in the network of the sender. The Ethernet frame must be sent to another device known as the router or default gateway. In our example, the default gateway is R1. R1 has an Ethernet data link address that is on the same network as PC1. This allows PC1 to reach the router directly.

- **Source MAC address** - The Ethernet MAC address of the sending device, PC1. The MAC address of the Ethernet interface of PC1 is AA-AA-AA-AA-AA-AA.

- **Destination MAC address** - When the receiving device, the destination IP address, is on a different network from the sending device, the sending device uses the Ethernet MAC address of the default gateway or router. In this example, the destination MAC address is the MAC address of R1's Ethernet interface, 11-11-11-11-11-11. This is the interface that is attached to the same network as PC1.

The Ethernet frame with the encapsulated IP packet can now be transmitted to R1. R1 forwards the packet to the destination, Web Server. This may mean that R1 forwards the packet to another router or directly to Web Server if the destination is on a network connected to R1.

It is important that the IP address of the default gateway be configured on each host on the local network. All packets to a destination on remote networks are sent to the default gateway. Ethernet MAC addresses and the default gateway are discussed in later chapters.

# Chapter 4 - Network Access

The OSI physical layer provides the means to transport the bits that make up a data link layer frame across the network media. This layer accepts a complete frame from the data link layer and encodes it as a series of signals that are transmitted onto the local media. The encoded bits that comprise a frame are received by either an end device or an intermediate device.

The process that data undergoes from a source node to a destination node is:

- The user data is segmented by the transport layer, placed into packets by the network layer, and further encapsulated into frames by the data link layer.
- The physical layer encodes the frames and creates the electrical, optical, or radio wave signals that represent the bits in each frame.
- These signals are then sent on the media, one at a time.
- The destination node physical layer retrieves these individual signals from the media, restores them to their bit representations, and passes the bits up to the data link layer as a complete frame.

There are three basic forms of network media. The physical layer produces the representation and groupings of bits for each type of media as:

- **Copper cable**: The signals are patterns of electrical pulses.
- **Fiber-optic cable**: The signals are patterns of light.
- **Wireless**: The signals are patterns of microwave transmissions.

**Bandwidth** is the capacity of a medium to carry data. Digital bandwidth measures the amount of data that can flow from one place to another in a given amount of time. Bandwidth is typically measured in kilobits per second (kb/s), megabits per second (Mb/s), or gigabits per second (Gb/s). Bandwidth is sometimes thought of as the speed that bits travel, however this is not accurate. For example, in both 10Mb/s and 100Mb/s Ethernet, the bits are sent at the speed of electricity. The difference is the number of bits that are transmitted per second.

**Throughput** is the measure of the transfer of bits across the media over a given period of time.
Due to a number of factors, throughput usually does not match the specified bandwidth in physical layer implementations. Many factors influence throughput, including:

- The amount of traffic
- The type of traffic
- The latency created by the number of network devices encountered between source and destination
  **Latency** refers to the amount of time, to include delays, for data to travel from one given point to another.
  **Goodput** is the measure of usable data transferred over a given period of time. Goodput is throughput minus traffic overhead for establishing sessions, acknowledgments, and encapsulation.

The data link layer of the OSI model (Layer 2 is responsible for:

- Allowing the upper layers to access the media
- Accepting Layer 3 packets and packaging them into frames
- Preparing network data for the physical network
- Controlling how data is placed and received on the media
- Exchanging frames between nodes over a physical network media, such as UTP or fiber-optic
- Receiving and directing packets to an upper layer protocol
- Performing error detection

The Layer 2 notation for network devices connected to a common media is called a node. Nodes build and forward frames. The OSI data link layer is responsible for the exchange of Ethernet frames between source and destination nodes over a physical network media.

![Layer 2 Data Link Addresses](netacad%20pictures/Layer%202%20Data%20Link%20Addresses.png)

The data link layer effectively separates the media transitions that occur as the packet is forwarded from the communication processes of the higher layers. The data link layer receives packets from and directs packets to an upper layer protocol, in this case IPv4 or IPv6. This upper layer protocol does not need to be aware of which media the communication will use.

## The Frame

![Frame Fields](netacad%20pictures/Frame%20Fields.png)

The data link layer prepares a packet for transport across the local media by encapsulating it with a header and a trailer to create a frame. The description of a frame is a key element of each data link layer protocol. Although there are many different data link layer protocols that describe data link layer frames, each frame type has three basic parts:

- Header
- Data
- Trailer
  All data link layer protocols encapsulate the Layer 3 PDU within the data field of the frame. However, the structure of the frame and the fields contained in the header and trailer vary according to the protocol.

There is no one frame structure that meets the needs of all data transportation across all types of media. Depending on the environment, the amount of control information needed in the frame varies to match the access control requirements of the media and logical topology.

## LAN and WAN Frames

In a TCP/IP network, all OSI Layer 2 protocols work with IP at OSI Layer 3. However, the Layer 2 protocol used depends on the logical topology and the physical media.

Each protocol performs media access control for specified Layer 2 logical topologies. This means that a number of different network devices can act as nodes that operate at the data link layer when implementing these protocols. These devices include the NICs on computers as well as the interfaces on routers and Layer 2 switches.

The Layer 2 protocol used for a particular network topology is determined by the technology used to implement that topology. The technology is, in turn, determined by the size of the network - in terms of the number of hosts and the geographic scope - and the services to be provided over the network.

A LAN typically uses a high bandwidth technology that is capable of supporting large numbers of hosts. A LAN's relatively small geographic area (a single building or a multi-building campus) and its high density of users, make this technology cost-effective.

However, using a high bandwidth technology is usually not cost-effective for WANs that cover large geographic areas (cities or multiple cities, for example). The cost of the long distance physical links and the technology used to carry the signals over those distances typically results in lower bandwidth capacity. The difference in bandwidth normally results in the use of different protocols for LANs and WANs.

Data link layer protocols include:

- Ethernet
- 802.11 Wireless
- Point-to-Point Protocol (PPP)
- HDLC
- Frame Relay


# Chapter 5 - Ethernet

![Ethernet Encapsulation](netacad%20pictures/Ethernet%20Encapsulation.png)

The minimum Ethernet frame size is 64 bytes and the maximum is 1518 bytes. This includes all bytes from the Destination MAC Address field through the Frame Check Sequence (FCS) field. The Preamble field is not included when describing the size of a frame.

Any frame less than 64 bytes in length is considered a “collision fragment” or “runt frame” and is automatically discarded by receiving stations. Frames with more than 1500 bytes of data are considered “jumbo” or “baby giant frames”.

If the size of a transmitted frame is less than the minimum or greater than the maximum, the receiving device drops the frame. Dropped frames are likely to be the result of collisions or other unwanted signals and are therefore considered invalid.

In Ethernet, every network device is connected to the same, shared media. Ethernet was once predominantly a half-duplex topology using a multi-access bus or later Ethernet hubs. This meant that all nodes would receive every frame transmitted. To prevent the excessive overhead involved in the processing of every frame, MAC addresses were created to identify the actual source and destination. MAC addressing provides a method for device identification at the lower level of the OSI model. Although Ethernet has now transitioned to full-duplex NICs and switches, it is still possible that a device that is not the intended destination will receive an Ethernet frame.

![Ethernet II Frame](netacad%20pictures/Ethernet%20II%20Frame.jpg)

**MAC Address Structure**

The MAC address value is a direct result of IEEE-enforced rules for vendors to ensure globally unique addresses for each Ethernet device. The rules established by IEEE require any vendor that sells Ethernet devices to register with IEEE. The IEEE assigns the vendor a 3-byte (24-bit) code, called the Organizationally Unique Identifier (OUI).

IEEE requires a vendor to follow two simple rules, as shown in the figure:

- All MAC addresses assigned to a NIC or other Ethernet device must use that vendor's assigned OUI as the first 3 bytes.

- All MAC addresses with the same OUI must be assigned a unique value in the last 3 bytes.

**Note**: It is possible for duplicate MAC addresses to exist due to mistakes during manufacturing or in some virtual machine implementation methods. In either case, it will be necessary to modify the MAC address with a new NIC or in software.

A Layer 2 Ethernet switch uses MAC addresses to make forwarding decisions. It is completely unaware of the protocol being carried in the data portion of the frame, such as an IPv4 packet. The switch makes its forwarding decisions based only on the Layer 2 Ethernet MAC addresses.

Unlike legacy Ethernet hubs that repeat bits out all ports except the incoming port, an Ethernet switch consults a MAC address table to make a forwarding decision for each frame.

The switch dynamically builds the MAC address table by examining the source MAC address of the frames received on a port. The switch forwards frames by searching for a match between the destination MAC address in the frame and an entry in the MAC address table.

As a switch receives frames from different devices, it is able to populate its MAC address table by examining the source MAC address of every frame. When the switch’s MAC address table contains the destination MAC address, it is able to filter the frame and forward out a single port.

## Destination on Same Network

There are two primary addresses assigned to a device on an Ethernet LAN:

- **Physical address (the MAC address)** – Used for Ethernet NIC to Ethernet NIC communications on the same network.

- **Logical address (the IP address)** – Used to send the packet from the original source to the final destination.

IP addresses are used to identify the address of the original source and the final destination. The destination IP address may be on the same IP network as the source or may be on a remote network.

Layer 2 or physical addresses, like Ethernet MAC addresses, have a different purpose. These addresses are used to deliver the data link frame with the encapsulated IP packet from one NIC to another NIC on the same network. If the destination IP address is on the same network, the destination MAC address will be that of the destination device.

The Layer 2 Ethernet frame contains:

- **Destination MAC address**
- **Source MAC address**

The Layer 3 IP packet contains:

- **Source IP address**
- **Destination IP address**

![Layer 3 Network Addresses](netacad%20pictures/Layer%203%20Network%20Addresses.png)

## Destination Remote Network

When the destination IP address is on a remote network, the destination MAC address will be the address of the host’s default gateway (the router’s NIC). Using a postal analogy, this would be similar to a person taking a letter to their local post office. All they need to do is take the letter to the post office and then it becomes the responsibility of the post office to forward the letter on towards its final destination.

Routers examine the destination IPv4 address to determine the best path to forward the IPv4 packet. This is similar to how the postal service forwards mail based on the address of the recipient.

When the router receives the Ethernet frame, it de-encapsulates the Layer 2 information. Using the destination IP address, it determines the next-hop device, and then encapsulates the IP packet in a new data link frame for the outgoing interface. Along each link in a path, an IP packet is encapsulated in a frame specific to the particular data link technology associated with that link, such as Ethernet. If the next-hop device is the final destination, the destination MAC address will be that of the device’s Ethernet NIC.

How are the IPv4 addresses of the IPv4 packets in a data flow associated with the MAC addresses on each link along the path to the destination? This is done through a process called Address Resolution Protocol (ARP). ARP provides two basic functions:

- Resolving IPv4 addresses to MAC addresses
- Maintaining a table of mappings

**Resolving IPv4 Addresses to MAC Addresses**
When a packet is sent to the data link layer to be encapsulated into an Ethernet frame, the device refers to a table in its memory to find the MAC address that is mapped to the IPv4 address. This table is called the ARP table or the ARP cache. The ARP table is stored in the RAM of the device.

The sending device will search its ARP table for a destination IPv4 address and a corresponding MAC address.

- If the packet’s destination IPv4 address is on the same network as the source IPv4 address, the device will search the ARP table for the destination IPv4 address.

- If the destination IPv4 address is on a different network than the source IPv4 address, the device will search the ARP table for the IPv4 address of the default gateway.

In both cases, the search is for an IPv4 address and a corresponding MAC address for the device.

Each entry, or row, of the ARP table binds an IPv4 address with a MAC address. We call the relationship between the two values a map - it simply means that you can locate an IPv4 address in the table and discover the corresponding MAC address. The ARP table temporarily saves (caches) the mapping for the devices on the LAN.

If the device locates the IPv4 address, its corresponding MAC address is used as the destination MAC address in the frame. If there is no entry is found, then the device sends an ARP request.

For each device, an ARP cache timer removes ARP entries that have not been used for a specified period of time. The times differ depending on the device’s operating system. For example, some Windows operating systems store ARP cache entries for 2 minutes.

# Chapter 6 - The Network Layer

The network layer, or OSI Layer 3, provides services to allow end devices to exchange data across the network. To accomplish this end-to-end transport, the network layer uses four basic processes:

- **Addressing end devices** - End devices must be configured with a unique IP address for identification on the network.

- **Encapsulation -** The network layer encapsulates the protocol data unit (PDU) from the transport layer into a packet. The encapsulation process adds IP header information, such as the IP address of the source (sending) and destination (receiving) hosts.

- **Routing -** The network layer provides services to direct packets to a destination host on another network. To travel to other networks, the packet must be processed by a router. The role of the router is to select the best path and direct packets toward the destination host in a process known as routing. A packet may cross many intermediary devices before reaching the destination host. Each router a packet crosses to reach the destination host is called a hop.

- **De-encapsulation -** When the packet arrives at the network layer of the destination host, the host checks the IP header of the packet. If the destination IP address within the header matches its own IP address, the IP header is removed from the packet. After the packet is de-encapsulated by the network layer, the resulting Layer 4 PDU is passed up to the appropriate service at the transport layer.

Unlike the transport layer (OSI Layer 4), which manages the data transport between the processes running on each host, network layer protocols specify the packet structure and processing used to carry the data from one host to another host. Operating without regard to the data carried in each packet allows the network layer to carry packets for multiple types of communications between multiple hosts.

There are several network layer protocols in existence. However, as shown in the figure, there are only two network layer protocols that are commonly implemented:

- Internet Protocol version 4 (IPv4)
- Internet Protocol version 6 (IPv6)

IP encapsulates the transport layer segment or other data by adding an IP header. This header is used to deliver the packet to the destination host. _The IP header remains the same from the time the packet leaves the source host until it arrives at the destination host._

![Characteristics of the IP Protocol](netacad%20pictures/Characteristics%20of%20the%20IP%20Protocol.png)

The process of encapsulating data layer by layer enables the services at the different layers to develop and scale without affecting the other layers. This means the transport layer segments can be readily packaged by IPv4 or IPv6 or by any new protocol that might be developed in the future.

Routers can implement these different network layer protocols to operate concurrently over a network. The routing performed by these intermediate devices only considers the contents of the network layer packet header. In all cases, the data portion of the packet, that is, the encapsulated transport layer PDU, remains unchanged during the network layer processes.

IP was designed as a protocol with low overhead. It provides only the functions that are necessary to deliver a packet from a source to a destination over an interconnected system of networks. The protocol was not designed to track and manage the flow of packets. These functions, if required, are performed by other protocols at other layers, primarily TCP at Layer 4.

## IPv4 Packet Header

An IPv4 packet header consists of fields containing important information about the packet. These fields contain binary numbers which are examined by the Layer 3 process. The binary values of each field identify various settings of the IP packet. Protocol header diagrams, which are read left to right, and top down, provide a visual to refer to when discussing protocol fields. The IP protocol header diagram in the figure identifies the fields of an IPv4 packet.

Significant fields in the IPv4 header include:

- **Version -** Contains a 4-bit binary value set to 0100 that identifies this as an IP version 4 packet.

- **Differentiated Services or DiffServ (DS) -** Formerly called the Type of Service (ToS) field, the DS field is an 8-bit field used to determine the priority of each packet. The six most significant bits of the DiffServ field is the Differentiated Services Code Point (DSCP) and the last two bits are the Explicit Congestion Notification (ECN) bits.

- **Time-to-Live (TTL) -** Contains an 8-bit binary value that is used to limit the lifetime of a packet. The packet sender sets the initial TTL value, and it is decreased by one each time the packet is processed by a router. If the TTL field decrements to zero, the router discards the packet and sends an Internet Control Message Protocol (ICMP) Time Exceeded message to the source IP address.

- **Protocol -** Field is used to identify the next level protocol. This 8-bit binary value indicates the data payload type that the packet is carrying, which enables the network layer to pass the data to the appropriate upper-layer protocol. Common values include ICMP (1), TCP (6), and UDP (17).

- **Source IPv4 Address -** Contains a 32-bit binary value that represents the source IPv4 address of the packet. The source IPv4 address is always a unicast address.

- **Destination IPv4 Address -** Contains a 32-bit binary value that represents the destination IPv4 address of the packet. The destination IPv4 address is a unicast, multicast, or broadcast address.

The two most commonly referenced fields are the source and destination IP addresses. These fields identify where the packet is coming from and where it is going. Typically these addresses do not change while travelling from the source to the destination.

The Internet Header Length (IHL), Total Length, and Header Checksum fields are used to identify and validate the packet.

Other fields are used to reorder a fragmented packet. Specifically, the IPv4 packet uses Identification, Flags, and Fragment Offset fields to keep track of the fragments. A router may have to fragment a packet when forwarding it from one medium to another with a smaller MTU.

## IPv6 Packet Header

![IPv6 Packet Header](netacad%20pictures/IPv6%20Packet%20Header.png)

The fields in the IPv6 packet header include:

- **Version -** This field contains a 4-bit binary value set to 0110 that identifies this as an IP version 6 packet.

- **Traffic Class -** This 8-bit field is equivalent to the IPv4 Differentiated Services (DS) field.

- **Flow Label -** This 20-bit field suggests that all packets with the same flow label receive the same type of handling by routers.

- **Payload Length -** This 16-bit field indicates the length of the data portion or payload of the IPv6 packet.

- **Next Header -** This 8-bit field is equivalent to the IPv4 Protocol field. It indicates the data payload type that the packet is carrying, enabling the network layer to pass the data to the appropriate upper-layer protocol.

- **Hop Limit** - This 8-bit field replaces the IPv4 TTL field. This value is decremented by a value of 1 by each router that forwards the packet. When the counter reaches 0, the packet is discarded, and an ICMPv6 Time Exceeded message is forwarded to the sending host, indicating that the packet did not reach its destination because the hop limit was exceeded.

- **Source IPv6 Address -** This 128-bit field identifies the IPv6 address of the sending host.

- **Destination IPv6 Address -** This 128-bit field identifies the IPv6 address of the receiving host.

An IPv6 packet may also contain extension headers (EH), which provide optional network layer information. Extension headers are optional and are placed between the IPv6 header and the payload. EHs are used for fragmentation, security, to support mobility and more.
Unlike IPv4, routers do not fragment routed IPv6 packets.

## Host Forwarding Decision

Another role of the network layer is to direct packets between hosts. A host can send a packet to:

- **Itself** - A host can ping itself by sending a packet to a special IPv4 address of 127.0.0.1, which is referred to as the loopback interface. Pinging the loopback interface tests the TCP/IP protocol stack on the host.

- **Local host** - This is a host on the same local network as the sending host. The hosts share the same network address.

- **Remote host** - This is a host on a remote network. The hosts do not share the same network address.

Whether a packet is destined for a local host or a remote host is determined by the IPv4 address and subnet mask combination of the source (or sending) device compared to the IPv4 address and subnet mask of the destination device.

In a home or business network, you may have several wired and wireless devices interconnected together using an intermediate device, such as a LAN switch and/or a wireless access point (WAP). This intermediate device provides interconnections between local hosts on the local network. Local hosts can reach each other and share information without the need for any additional devices. If a host is sending a packet to a device that is configured with the same IP network as the host device, the packet is simply forwarded out of the host interface, through the intermediate device, and to the destination device directly.

Of course, in most situations we want our devices to be able to connect beyond the local network segment, such as out to other homes, businesses, and the Internet. Devices that are beyond the local network segment are known as remote hosts. When a source device sends a packet to a remote destination device, then the help of routers and routing is needed. Routing is the process of identifying the best path to a destination. The router connected to the local network segment is referred to as the **default gateway**.

A default gateway:

- Routes traffic to other networks
- Has a local IP address in the same address range as other hosts on the network
- Can take data in and forward data out
  When a host sends a packet to another host, it will use its routing table to determine where to send the packet. If the destination host is on a remote network, the packet is forwarded to the default gateway.

# Chapter 7 - IP Addressing

## Dynamic IPv4 Address Assignment to a Host

In most data networks, the largest population of hosts includes PCs, tablets, smartphones, printers, and IP phones. It is also often the case that the user population and their devices change frequently. It would be impractical to statically assign IPv4 addresses for each device. Therefore, these devices are assigned IPv4 addresses dynamically using the Dynamic Host Configuration Protocol (DHCP).

A host can obtain IPv4 addressing information automatically. The host is a DHCP client and requests IPv4 address information from a DHCP server. The DHCP server provides an IPv4 address, subnet mask, default gateway, and other configuration information.

DHCP is generally the preferred method of assigning IPv4 addresses to hosts on large networks. An additional benefit of DHCP is the address is not permanently assigned to a host but is only "leased" for a period of time. If the host is powered down or taken off the network, the address is returned to the pool for reuse. This feature is especially helpful for mobile users that come and go on a network.

## Public and Private IPv4 Addresses

![IPv4 Packet Header](netacad%20pictures/IPv4%20Packet%20Header.png)

Public IPv4 addresses are addresses which are globally routed between ISP (Internet Service Provider) routers. However, not all available IPv4 addresses can be used on the Internet. There are blocks of addresses called _private addresses_ that are used by most organizations to assign IPv4 addresses to internal hosts.

In the mid-1990s private IPv4 addresses were introduced because of the depletion of IPv4 address space. Private IPv4 addresses are not unique and can be used by an internal network.

Specifically, the private address blocks are:

- **10.0.0.0 /8** or **10.0.0.0** to **10.255.255.255**

- **172.16.0.0 /12** or **172.16.0.0** to **172.31.255.255**

- **192.168.0.0 /16** or **192.168.0.0** to **192.168.255.255**

It is important to know that addresses within these address blocks are not allowed on the Internet and must be filtered (discarded) by Internet routers.

Most organizations use private IPv4 addresses for their internal hosts. However, these RFC 1918 address are not routable in the Internet and must be translated to a public IPv4 address. Network Address Translation (NAT) is used to translate between private IPv4 and public IPv4 addresses. This is usually done on the router that connects the internal network to the ISP's network.

Home routers provide the same capability. For instance, most home routers assign IPv4 addresses to their wired and wireless hosts from the private address of 192.168.1.0 /24. The home router interface that connects to the Internet service provider (ISP) network is assigned a public IPv4 address to use on the Internet.

## Special User IPv4 Addresses

There are certain addresses such as the network address and broadcast address that cannot be assigned to hosts. There are also special addresses that can be assigned to hosts, but with restrictions on how those hosts can interact within the network.

- **Loopback addresses (127.0.0.0 /8 or 127.0.0.1 to 127.255.255.254) –** More commonly identified as only 127.0.0.1, these are special addresses used by a host to direct traffic to itself. For example, it can be used on a host to test if the TCP/IP configuration is operational, such as shown in the figure. Notice how the 127.0.0.1 loopback address replies to the ping command. Also note how any address within this block will loop back to the local host, such as shown with the second ping in the figure.

- **Link-Local addresses (169.254.0.0 /16 or 169.254.0.1 to 169.254.255.254) –** More commonly known as the Automatic Private IP Addressing (APIPA) addresses, they are used by a Windows DHCP client to self-configure in the event that there are no DHCP servers available.Useful in a peer-to-peer connection.

- **TEST-NET addresses (192.0.2.0/24 or 192.0.2.0 to 192.0.2.255) –** These addresses are set aside for teaching and learning purposes and can be used in documentation and network examples.

**Note**: There are also Experimental Addresses in the block 240.0.0.0 to 255.255.255.254 that are reserved for future use.

## Legacy Classful Addressing

In 1981, Internet IPv4 addresses were assigned using _classful addressing_ as defined in [RFC 790](https://tools.ietf.org/html/rfc790), Assigned Numbers. Customers were allocated a network address based on one of three classes, A, B, or C. The RFC divided the unicast ranges into specific classes called:

- **Class A (0.0.0.0/8 to 127.0.0.0/8)** – Designed to support extremely large networks with more than 16 million host addresses. It used a fixed /8 prefix with the first octet to indicate the network address and the remaining three octets for host addresses. All class A addresses required that the most significant bit of the high-order octet be a zero creating a total of 128 possible class A networks.

- **Class B (128.0.0.0 /16 – 191.255.0.0 /16)** – Designed to support the needs of moderate to large size networks with up to approximately 65,000 host addresses. It used a fixed /16 prefix with the two high-order octets to indicate the network address and the remaining two octets for host addresses. The most significant two bits of the high-order octet must be 10 creating over 16,000 networks.

- **Class C (192.0.0.0 /24 – 223.255.255.0 /24)** – Designed to support small networks with a maximum of 254 hosts. It used a fixed /24 prefix with the first three octets to indicate the network and the remaining octet for the host addresses. The most significant three bits of the high-order octet must be 110 creating over 2 million possible networks.

**Note**: There is also a Class D multicast block consisting of 224.0.0.0 to 239.0.0.0 and a Class E experimental address block consisting of 240.0.0.0 – 255.0.0.0.

# Chapter 8 - Subnetting IP Networks

Subnetting reduces overall network traffic and improves network performance. It also enables an administrator to implement security policies such as which subnets are allowed or not allowed to communicate together.

There are various ways of using subnets to help manage network devices. Network administrators can group devices and services into subnets that are determined by:

- Location, such as floors in a building.
- Organizational unit.
- Device type.
- Any other division that makes sense for the network.

Understanding how to subnet networks is a fundamental skill that all network administrators must develop. Various methods have been developed to help understand this process. This chapter will focus on looking at the binary method.

## Subnetting Formulas

To calculate the number of subnets that can be created from the bits borrowed, we can use the formula: **2^n^** where **n = bits borrowed** .

- Borrowing 1 bit: 2^1^ = 2 subnets
- Borrowing 1 bit: 2^2^ = 4 subnets
- Borrowing 1 bit: 2^3^ = 8 subnets
- Borrowing 1 bit: 2^4^ = 16 subnets
- Borrowing 1 bit: 2^5^ = 32 subnets
- Borrowing 1 bit: 2^6^ = 64 subnets

**Note**: The last two bits cannot be borrowed from the last octet because there would be no host addresses available. Therefore, the longest prefix length possible when subnetting is /30 or 255.255.255.252.

To calculate the number of hosts that can be supported, use the formula **2^n^-2**. There are two subnet addresses that cannot be assigned to a host, _the network address_ and _the broadcast address_, so we must subtract 2.

**Creating 2 subnets**
For example when we subtract 1 bit we get 2^1^ subnets and there will be 7 host bits remaining, so host calculation is 2^7 = 128-2 = 126. This means that each of the subnets has 126 valid host addresses.

Therefore, borrowing 1 host bit toward the network results in creating 2 subnets, and each subnet can have a total of 126 hosts assigned.

**Creating 4 subnets**
We need to subtract 2 bits and we get 2^2^ subnets. There are 8-2 = 6 bits remaining so every subnet will get 2^6^ = 64 addresses. Every subnet will have a network and a broadcast address so every subnet will have 64 - 2 = 62 hosts. Address space will be:

- 192.168.1.0 (Network 0 Address)
- 192.168.1.1 (Network 0 First Host)
- 192.168.1.62 (Network 0 Last Host)
- 192.168.1.63 (Network 0 Broadcast)
- 192.168.1.64 (Network 1 Address)
- 192.168.1.65 (Network 1 First Host)
- 192.168.1.126 (Network 1 Last Host)
- 192.168.1.64 (Network 1 Broadcast)

![Subnet Mask Prefix Length](netacad%20pictures/Subnet%20Mask%20Prefix%20Length.png)
![Subnetting - Dotted Decimal Addresses](netacad%20pictures/Subnetting%20-%20Dotted%20Decimal%20Addresses.png)
![Subnetting Networks on the Octet Boundary](netacad%20pictures/Subnetting%20Networks%20on%20the%20Octet%20Boundary.png)

## Variable Length Subnet Masks

With VLSM, the subnet mask will vary depending on how many bits have been borrowed for a particular subnet, thus the “variable” part of the VLSM.

VLSM subnetting is similar to traditional subnetting in that bits are borrowed to create subnets. The formulas to calculate the number of hosts per subnet and the number of subnets created still apply.

The difference is that subnetting is not a single pass activity. With VLSM, the network is first subnetted, and then the subnets are subnetted again. This process can be repeated multiple times to create subnets of various sizes.

**Note**: _When using VLSM, always begin by satisfying the host requirements of the largest subnet. Continue subnetting until the host requirements of the smallest subnet are satisfied._

# Chapter 9 - Transport Layer

![Transport Layer Services](netacad%20pictures/Transport%20Layer%20Services.png)
![Transport Layer Protocols](netacad%20pictures/Transport%20Layer%20Protocols.png)

**Tracking Individual Conversations**
At the transport layer, each set of data flowing between a source application and a destination application is known as a conversation. A host may have multiple applications that are communicating across the network simultaneously. Each of these applications communicates with one or more applications on one or more remote hosts. It is the responsibility of the transport layer to maintain and track these multiple conversations.

**Segmenting Data and Reassembling Segments**
Data must be prepared to be sent across the media in manageable pieces. Most networks have a limitation on the amount of data that can be included in a single packet. Transport layer protocols have services that segment the application data into blocks that are an appropriate size. This service includes the encapsulation required on each piece of data. A header, used for reassembly, is added to each block of data. This header is used to track the data stream.

At the destination, the transport layer must be able to reconstruct the pieces of data into a complete data stream that is useful to the application layer. The protocols at the transport layer describe how the transport layer header information is used to reassemble the data pieces into streams to be passed to the application layer.

**Identifying the Applications**
To pass data streams to the proper applications, the transport layer must identify the target application. To accomplish this, the transport layer assigns each application an identifier called a port number. Each software process that needs to access the network is assigned a port number unique to that host.

## Transport Layer Reliability

The transport layer is also responsible for managing reliability requirements of a conversation. Different applications have different transport reliability requirements.

**IP** is concerned only with the structure, addressing, and routing of packets\*. IP does not specify how the delivery or transportation of the packets takes place. _Transport protocols specify how to transfer messages between hosts_. TCP/IP provides two transport layer protocols, Transmission Control Protocol (TCP) and User Datagram Protocol (UDP). IP uses these transport protocols to enable hosts to communicate and transfer data.

**TCP** is considered a reliable, full-featured transport layer protocol, which ensures that all of the data arrives at the destination. However, this requires additional fields in the TCP header which increases the size of the packet and also increases delay. In contrast, UDP is a simpler transport layer protocol that does not provide for reliability. It therefore has fewer fields and is faster than TCP.

![TCP Connection Establishment](netacad%20pictures/TCP%20Connection%20Establishment.png)
![TCP Session Termination](netacad%20pictures/TCP%20Session%20Termination.png)

With TCP, there are three basic operations of reliability:

- Numbering and tracking data segments transmitted to a specific host from a specific application
- Acknowledging received data
- Retransmitting any unacknowledged data after a certain period of time

**UDP** provides the basic functions for delivering data segments between the appropriate applications, with very little overhead and data checking. UDP is known as a best-effort delivery protocol. In the context of networking, best-effort delivery is referred to as unreliable because there is no acknowledgment that the data is received at the destination. With UDP, there are no transport layer processes that inform the sender of a successful delivery.

![UDP - Applications that use UDP](netacad%20pictures/UDP%20-%20Applications%20that%20use%20UDP.png)
![UDP Datagram](netacad%20pictures/UDP%20Datagram.png)


**TCP features:**

- **Establishing a Session**
- **Reliable Delivery**
- **Same-Order Delivery**
- **Flow Control**

![TCP segment](netacad%20pictures/TCP%20segment.png)

TCP is a stateful protocol. A stateful protocol is a protocol that keeps track of the state of the communication session. To track the state of a session, TCP records which information it has sent and which information has been acknowledged. The stateful session begins with the session establishment and ends when closed with the session termination.

TCP segment has 20 bytes of overhead in the header encapsulating the application layer data:

- **Source Port (16 bits) and Destination Port (16 bits)** - Used to identify the application.
  _The source port number is dynamically generated by the sending device to identify a conversation between two devices_. This process allows multiple conversations to occur simultaneously. It is common for a device to send multiple HTTP service requests to a web server at the same time. Each separate HTTP conversation is tracked based on the source ports.
  _The client places a destination port number in the segment to tell the destination server what service is being requested_. For example, when a client specifies port 80 in the destination port, the server that receives the message knows that web services are being requested. A server can offer more than one service simultaneously such as web services on port 80 at the same time that it offers File Transfer Protocol (FTP) connection establishment on port 21.

- **Sequence number (32 bits)** - Used for data reassembly purposes. TCP segments may arrive at their destination out of order. For the original message to be understood by the recipient, the data in these segments is reassembled into the original order. Sequence numbers are assigned in the header of each packet to achieve this goal.
  During session setup, an initial sequence number (ISN) is set. This ISN represents the starting value of the bytes for this session that is transmitted to the receiving application. As data is transmitted during the session, the sequence number is incremented by the number of bytes that have been transmitted. This data byte tracking enables each segment to be uniquely identified and acknowledged. Missing segments can then be identified.

- **Acknowledgment number (32 bits)** - Indicates data has been received and the next byte expected from the source.

- **Header length (4 bits)** - Known as ʺdata offsetʺ. Indicates the length of the TCP segment header.

- **Reserved (6 bits)** - This field is reserved for the future.

- **Control bits (6 bits)** - Includes bit codes, or flags, which indicate the purpose and function of the TCP segment (ACK, FIN etc).

- **Window size (16 bits)** - Indicates the number of bytes that can be accepted at one time. Flow control helps maintain the reliability of TCP transmission by adjusting the rate of data flow between source and destination for a given session. The initial window size is agreed upon when the TCP session is established during the three-way handshake. The source device must limit the number of bytes sent to the destination device based on the destination’s window size. Only after the source device receives an acknowledgment that the bytes have been received, can it continue sending more data for the session.
  Typically, the destination will not wait for all the bytes for its window size to be received before replying with an acknowledgment. As the bytes are received and processed, the destination will send acknowledgments to inform the source that it can continue to send additional bytes. The process of the destination sending acknowledgments as it processes bytes received and the continual adjustment of the source’s send window is known as **sliding windows**.
  If the availability of the destination’s buffer space decreases, it may reduce its window size to inform the source to reduce the number of bytes it should send without receiving an acknowledgment.

- **Checksum (16 bits)** - Used for error checking of the segment header and data.

- **Urgent (16 bits)** - Indicates if data is urgent.

## Port Numbers

![Port Addressing](netacad%20pictures/Port%20Addressing.png)

The Internet Assigned Numbers Authority (IANA) is the standards body responsible for assigning various addressing standards, including port numbers. There are different types of port numbers:

- **Well-known Ports (Numbers 0 to 1023)** - These numbers are reserved for services and applications. They are commonly used for applications such as web browsers, email clients, and remote access clients. By defining these well-known ports for server applications, client applications can be programmed to request a connection to that specific port and its associated service.

- **Registered Ports (Numbers 1024 to 49151)** - These port numbers are assigned by IANA to a requesting entity to use with specific processes or applications. These processes are primarily individual applications that a user has chosen to install, rather than common applications that would receive a well-known port number. For example, Cisco has registered port 1985 for its Hot Standby Routing Protocol (HSRP) process.

- **Dynamic or Private Ports (Numbers 49152 to 65535)** - Also known as ephemeral ports, these are usually assigned dynamically by the client’s OS when a connection to a service is initiated. The dynamic port is then used to identify the client application during communication.

![Socket Pairs](netacad%20pictures/Socket%20Pairs.png)

# Chapter 10 - Application Layer

![Application Layer](netacad%20pictures/Application%20Layer.png)

## TCP/IP Application Layer Protocols

![TCPIP Protocol Suite](netacad%20pictures/TCPIP%20Protocol%20Suite.png)

**_DNS_** = TCP / UDP 53 = **Domain Name System** = Translates domain names int IP addresses

**_DHCP_** = UDP client 68, server 67 = **Dynamic Host Configuration Protocol** = Dynamically assigns IP addresses to client stations at start-up.

![DHCP](netacad%20pictures/DHCP.png)

**_SMTP_** = TCP 25 = **Simple Mail Transfer Protocol** = Enables clients to send email to mail server. Enables servers to send email to other servers.

**_POP_** = TCP 110 = **Post Office Protocol** = Enables Clients to retrieve email from a mail server. Downloads email from mail server to the desktop.

**_IMAP_** = TCP 143 = **Internet Message Access Protocol** = Enables clients to access email stored on a mail server. Maintains email on the server.

![Application Layer](netacad%20pictures/Presentation%20and%20Session%20Layer.png)
![Email protocols](netacad%20pictures/Email%20Protocols.png)

**_FTP_** = TCP 20 - 21 = **File Transfer Protocol** = Sets rules that enable a user on one host to access and transfer files to and from another host over a network. Connection oriented, reliable, acknowledged.

**_TFTP_** = UDP 69 = **Trivial File Transfer Protocol** = Simple connection-less FTP, best effort, unacknowledged.

**_HTTP_** = TCP 80, 8080 = **Hypertext Transfer Protocol** = Sets rules for exchanging text, graphic, images, sound, video and other multimedia files on the World Wide Web.

![TCP - Applications that use TCP](netacad%20pictures/TCP%20-%20Applications%20that%20use%20TCP.png)

**_HTTPS_** = **Hypertext Transfer Protocol Secure** = TCP, UDP 443 = Uses encryption to secure HTTP connections. Authenticates the website to which you are connecting your browser.

![Application to Transport Layer](netacad%20pictures/Application%20Layer%20Protocol%20that%20Uses%20Particular%20Transport%20Layer%20Protocols.png)


## Presentation & Session Layer

![Presentation & Session Layer](netacad%20pictures/Presentation%20and%20Session%20Layer.png)

![Interaction of Communication Protocols](netacad%20pictures/Interaction%20of%20Communication%20Protocols.png)

![Protocol Suites and Industry Standards](netacad%20pictures/Protocol%20Suites%20and%20Industry%20Standards.png)

### Client-Server Model

In the client-server model, the device requesting the information is called a client and the device responding to the request is called a server. Client and server processes are considered to be in the application layer. The client begins the exchange by requesting data from the server, which responds by sending one or more streams of data to the client. Application layer protocols describe the format of the requests and responses between clients and servers. In addition to the actual data transfer, this exchange may also require user authentication and the identification of a data file to be transferred.

### Peer-to-Peer Networks

In the peer-to-peer (P2P) networking model, the data is accessed from a peer device without the use of a dedicated server. The P2P network model involves two parts: P2P networks and P2P applications. Both parts have similar features, but in practice work quite differently.
In a P2P network, two or more computers are connected via a network and can share resources (such as printers and files) without having a dedicated server. Every connected end device (known as a peer) can function as both a server and a client. One computer might assume the role of server for one transaction while simultaneously serving as a client for another. The roles of client and server are set on a per request basis.

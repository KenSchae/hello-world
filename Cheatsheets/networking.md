# Networking Fundamentals

## Table of Contents
1. [OSI Network Model](#open-systems-interconnect-(osi)-network-model)
2. [Protocols and Ports](#protocols-and-ports)

## Open Systems Interconnect (OSI) Network Model

A conceptual model that communicates the ways in which different systems work together in a network.

| Layer | Description   |
|-------|-------|
| Physical      | Responsible for the transmission and reception of unstructured raw data between a device and a physical transmission medium.
| Data Link     | Provides node to node data transfer between two directly connected nodes.
| Network       | Provides the functional and procedural means of transferring packets from one node to another. This is where addressing and routing happens.
| Transport     | Makes the connection between a source and a destination.
| Session       | Controls the connections between computers.
| Presentation  | Establishes context between application layer entities.
| Appliation    | Interacts with software applications that implement communications.

## Protocols and Ports

Protocols are an Application Layer component. Ports are a Transport Layer component that is matched to the protocol. The port number helps the lower layer protocols understand which application is being used in the communication.


| Service  | Protocol  | Port   |
|-------|-------|-------|
| Transferring data     | HTTP / HTTPS              | 80 / 443                  |
| File transfer         | FTP / sFTP / TFTP / SMB   | 20 21 / 22 / 69 / 445     | 
| Email                 | POP3 / IMAP / SMTP        | 110 995 / 143 993 / 25 465|
| Authentication        | LDAP / LDAPs              | 389 / 636                 |


| Network Service       | Description               |
|-------|-------|
| DHCP                  | Dynamic addresses         | 
| DNS                   | Name resolution           | 
| NTP                   | Network Time Protocol     |

### Utilities

`nslookup`

## Tranmission Control Protocol

This is a connection oriented protocol that establishes communications between a client and a server. This protocol prioritizes quality over time, therefore it contains error checking and recovery to ensure that a message is complete.

TCP uses the 3 way handshake to establish a connection. The client starts by sending a SYN message to request a connection, the server sends back an ACK message to confirm the connection, lastly the client uses a protocol (like HTTP) to send the message and get back a response.

Connections are gracefully closed with a 4 way disconnect. The server sends a FIN message and the client sends an ACK message, then they do it again.

## User Datagram Protocol

This is a connection-less protocol that prioritizes time over quality. This services is more like a broadcast than a phone call. Used for things like DNS where efficient data transfer is key.

## Intro to Binary and Hexadecimal

Converting binary to decimal. Multiply the value in the placeholder by the value of the placeholder and add the results together.

```
128 64  32  16  8   4   2   1
1   1   0   0   0   0   0   0   
128 64  0   0   0   0   0   0   =   192
```

Converting decimal to binary. Start with the highest place that you can subtract from the decimal number, then continue with the remainder until you get to 0.

Hexadecimal is base 10 where the numbers are 1 - 9 then A - F with 10 being 16.

## IP Addressing

IP addresses live in layer 3 of the OSI model. Every device on the internet must have a unique IP address. An IP address consists of two components, the network address and the host address. 

All IP addresses consist of 4 8-bit numbers separated by decimals.

```
203.0.113.10
11001011 00000000 01110001 00001010
```

### Classful vs Classless addressing 

Classless addressing is the modern approach. This approach uses a subnet mask to differentiate the network portion of the address from the host portion. The subnet mask uses 1 to mask out the network portion of the address and 0 for the host portion.

```
203.0.113.10
11001011 00000000 01110001 00001010

11111111 11111111 11111111 00000000
255.255.255.0
```

Classful addressing was the old way of determining network and host. These were the old A, B, C, D, and E networks. The public internet is still based on the first three networks. 

A network address consists of the network address followed by a host portion with only 0s. A broadcast address is the network followed by all 1s in the host portion. The host address is anything in the host portion that is not all 0s and all 1s.

### CIDR Notation

A shortcut method for writing an address that shows the number of bits in the subnet mask. 

``` 
203.0.113.10/24
```

### Reserved network addresses

These are reserved for use on private networks.

| Network       | Mask              | CIDR              |
|-------|-------|-------|
| 10.0.0.0      | 10.255.255.255    | 10.0.0.0/8        |
| 172.16.0.0    | 172.31.255.255    | 172.16.0.0/12     |
| 192.168.0.0   | 192.168.255.255   | 192.168.0.0/16    |

## Subnetting

## IPv6

### Address sizes 
**IPv4** are 32bits long in 4 octets
**IPv6** are 128bits long in 8 hextets

IPv6 are written in hex in blocks of 4 digits.
```
2001:0DB8:0002:008D:0000:0000:00A5:52F5
```

In IPv6 the network portion is the first 64 bits and the host portion (interface identifier) is the last 64 bits.

Reduce the address:
- remove leading 0s
- Eliminate sets of 0 with a ::
- Can only use one :: in an address

```
2001:DB8:2:8D::A5:52F5
```

## Ethernet and Switching

Ethernet and switching exists at layer 2. The protocols at this level govern how devices connect to each other and communicate from point to point.

CSMA/CD - Carrier Sense Multiple Access with Collision Detection

This was the original standard to describe ethernet. When one device needs to send a message to another device on the network, it will send out a pulse to all devices on the network. All devices will get the message but only the intended device will send back an acknowledgement.

### Ethernet Frame

The ethernet frame has not changed since its beginning. Speeds and hardware have changed, but not the basic form of the frame. The frame information facilitiates the communication on Ethernet. Everything except the data packet are the frame information.

| Destination Mac   | Source Mac    | Type      | Data(Packet)      | FCS       |
|-------|-------|-------|-------|-------|
| 48 bit            | 48 bit        | 16 bit    | MAX 1500 bytes    | 32 bit    |

The type field tells what type of data is being transferred
The frame check sequence (FCS) validates the frame 

### Switches

Switches work by mapping the ports on the switch to the MAC addresses of the devices connected to that port.

## Switching Features

### VLANS

Splitting a physical switch into multiple domains. Each VLAN exists on its own Layer-3 IP network. 

VLANs will sement your network based on specific functions.

## IP Routing

Address Resolution Protocol - gets a Layer-2 MAC address when all we have is a Layer-3 IP address. 

The ARP table is stored on the client device. The ARP table can be viewed on your PC. 

`arp -a`

The default Gateway and the Router are the same thing.

The router is used when the destination IP address is not on the same network as the source.

The tracert utility shows a listing of all routers that a message crosses.

`tracert -d 8.8.8.8`

## Network Services

### Network Topologies

1. LAN (Local Area Network)
2. WLAN (Wireless Local Area Network)
3. WAN (Wide Area Network)
4. SAN (Storage Area Network)
5. PAN (Personal Area Network) - Hotspot

### Network Address Translation (NAT)

The default gateway will replace the local private IP address with the public IP address assigned to the router. It will also convert public messages to private.

### Access Control Lists (ACL)

A mechanism for flagging bad servers.

## References
[Wikipedia Article](https://en.wikipedia.org/wiki/OSI_model)
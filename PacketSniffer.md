**<span class="underline">Packet Sniffing</span>**

<span class="underline"></span>

**<span class="underline">Abstract:</span>**

This article focuses on giving an insight on packet sniffing. It is one
of the common attacks hacker perform on networks. It gives the
definition of packet sniffing and how its done.

It also includes a python program that performs packet sniffing, and
another program that parses the sniffed data. It explains the process
involved in sniffing and parsing.

<span class="underline"></span>

At the end it also discuses on where sniffing is performed and how
confidential data could be treated to prevent hackers stealing it by
sniffing.

<span class="underline"></span>

**<span class="underline">Introduction:</span>**

When two computers communicate via a network, they transmit data as
packets. Packet sniffing is the process of collecting these packets
traveling through the network channel. Intruders use special program
called packet sniffer to perform packet sniffing. They could then use
parser program to extract meaningful information out of this sniffed
packets.

This article focuses on creating a packet sniffer in python. The program
will use sockets to listen to a particular IP.

**<span class="underline">Packet sniffer:</span>**

Packet sniffer is a special program that intrudes a network and collects
all the packet passing through that network. This article includes 2
files namely sniffer.py and parser.py. Both the files are compatible on
a Linux system.

The file sniffer.py collects all the packets passing through the network
to which the computer is connected.

To read from or write to a raw socket, sniffer.py first creates a new
raw INET(IPv4) socket. This program then goes into an infinite loop
listening to a particular port. Terminal will require root access to
create raw socket. The output of this program will be non-parsed data.

![](media/image1.png)

![](media/image2.png)

Output of sniffer.py

<span class="underline"></span>

**<span class="underline">Parser:</span>**

The output of the file sniffer.py is non readable. parser.py parses this
output to convert it into a readable format.

![](media/image3.png)Ethernet frame structure.

![](media/image4.png)IP header.

The first 6 bytes are for the Destination MAC address and the next 6
bytes are for the Source MAC. The last 2 bytes are for the Ether Type,
The rest includes DATA and CRC Checksum.

The IP header include the following sections:

  - **Protocol Version:** Current IP protocol(4 bits).

  - **Header Length:** Length of IP header(4 bits).

  - **Type of Service:** First 3 bits are precedence bits, then 4 bits
    for the type of service. Last bit is unused.(8 bits).

  - **Total Length:** Length of IP datagram(16 bits).

  - **Flags:** The second bit represents Don’t Fragment bit. When this
    bit is set, the IP datagram is never fragmented. The third bit
    represents the More Fragment bit. If this bit is set, then it
    represents a fragment IP datagram that has more fragment after it(3
    bits).

  - **Time to Live:** Number of hops that IP datagram will go before
    being discarded(8 bits).

  - **Protocol:** Transport layer protocol(8 bits).

  - **Header Checksum:** Hash of the IP datagram(16 bits).

  - **Source and destination IP:** Source and destination address(32
    bit).

The program imports struct and sys module of python. The function
ethernet\_head(raw\_data) uses the unpack method in the struct module to
unpack the headers. This function returns the destination MAC, source
MAC, protocol, and data.

ipv4\_head(raw\_data) will unpack the headers using unpack method and
returns version, header\_length, ttl, protocol source, and destinations
IPs. The get\_ip(addr) makes the IP address readable.

All these processes unpacks internet layer. Next the program has to
unpack transport protocol.

The function tcp\_head(raw\_data) unpacks the data as per the TCP packet
header’s structure.

![](media/image5.png)TCP Header Structure.

Similarly ICMP and UDP packets are packets are unpacked in main function
according to their structure.

![](media/image6.png)ICMP Header Structure.

![](media/image7.png)UDP Header Structure.

The output will print all the packets that were sniffed.

![](media/image8.png)

Output of parser.py

<span class="underline"></span>

**<span class="underline">Application of packet sniffer:</span>**

Packet sniffers are mostly used by the ISPs. ISP use packet sniffer to
know the sender, receiver, contents, etc.

Advertising agencies use packet sniffer to understand the user and send
targeted ads to them.

Hackers use packet sniffers to collect exploitable information. They
would then use these information to perform identity theft, confidential
information exploitation, etc.

<span class="underline"></span>

<span class="underline"></span>

<span class="underline"></span>

<span class="underline"></span>

**<span class="underline">Protection from packet sniffing:</span>**

Protection of confidential data could be done using encryption.
Encrypted data could be sniffed and unpacked, but it cannot be decrypted
without proper key. So the confidential data will be secure even if its
sniffed.

Secured Sockets Layer(SSL) and Transport Layer Security(TSL) are two
commonly used encryption technique for protection against sniffing.

**<span class="underline">GitHub repository link for the programs
explained in this article.</span>**

<https://github.com/WING-UCSP/Packet-sniffing>

**Phani Sai Teja Janpani (UCSP)**

**Uvais Mon V V N (WING)**

**Vignesh V (WING)**

**Vishal Rai (UCSP)**

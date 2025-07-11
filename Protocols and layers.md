#Protocols and Layers

A PDU(Public Data Units) is a data packet made up of control information and data encapsulated from each layer of the OSI model.

## Addressing layer

###Mac Address
MAC-addressing is utilized in Layer two ( the data-link or link-layer depending on which model you look at ) communications between hosts. This address is a 48-bit six octet address represented in hexadecimal format.

###IPv4 -> IPv6
After a little over a decade of utilizing IPv4, it was determined that we had quickly exhausted the pool of usable IP addresses. With such large chunks sectioned off for special use or private addressing, the world had quickly used up the available space. To help solve this issue, two things were done. The first was implementing **variable-length subnet masks (VLSM)** and **Classless Inter-Domain Routing (CIDR)**. This allowed us to redefine the useable IP addresses in the v4 format changing how addresses were assigned to users. The second was the creation and continued development of IPv6 as a successor to IPv4.

##Transport Layer

###TCP vs UDP

| Characteristic          | TCP                                                                 | UDP                                                       |
|-------------------------|----------------------------------------------------------------------|------------------------------------------------------------|
| Transmission            | Connection-oriented                                                  | Connectionless. Fire and forget.                          |
| Connection Establishment| TCP uses a three-way handshake to ensure that a connection is established. | UDP does not ensure the destination is listening.         |
| Data Delivery           | Stream-based conversations                                           | Packet by packet, the source does not care if the destination is active |
| Receipt of Data         | Sequence and Acknowledgement numbers are utilized to account for data. | UDP does not care.                                        |
| Speed                   | TCP has more overhead and is slower because of its built-in functions. | UDP is fast but unreliable.                               |

Three-way Handshake:
1. client sends SYN
2. Server replies with another SYN and ACK of previous SYN
3. Client send ACK

Session termination
1. client ACK data received and sends FIN and ACK
2. Server sends FIN and ACK
3. Client sends ACK

###HTTP/HTTPS

TLS(Transport Layer Security) handshake:-
1. Client and server exchange hello messages to agree on connection parameters.
2. Client and server exchange necessary cryptographic parameters to establish a premaster secret.
3. Client and server will exchange x.509 certificates and cryptographic information allowing for authentication within the session.
4. Generate a master secret from the premaster secret and exchanged random values.
5. Client and server issue negotiated security parameters to the record layer portion of the TLS protocol.
6. Client and server verify that their peer has calculated the same security parameters and that the handshake occurred without tampering by an attacker.

###FTP
File Transfer Protocol (FTP) is an Application Layer protocol that enables quick data transfer between computing devices. Uses multiple ports(20 for data tranfer and 21 to issue commands, over TCP). FTP supports user authentication as well as allowing anonymous access if configured.

###SMB (Server Message Block)
SMB is a connection-oriented protocol that requires user authentication from the host to the resource to ensure the user has correct permissions to use that resource or perform actions. In the past, SMB utilized NetBIOS as its transport mechanism over UDP ports 137 and 138. Since modern changes, SMB now supports direct TCP transport over port 445, NetBIOS over TCP port 139, and even the QUIC protocol.



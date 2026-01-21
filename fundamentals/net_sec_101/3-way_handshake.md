---
layout: default
---

# 3 Way Handshake

***

The TCP 3-Way Handshake is a process used by the Transmission Control Protocol (TCP) to establish a reliable connection between a client and a server before data transfer. It ensures that both sides are synchronized and ready to communicate.

- [TCP Structure](#tcp-structure)
- [TCP 3-Way Handshake Process](#tcp-3-way-handshake-process)

## TCP Structure

![Branching](https://tyler-nse.github.io/assets/img/net_sec_101/tcp_header.PNG)

The header of a TCP segment can range from 20-60 bytes. 40 bytes are for options. If there are no options, a header is 20 bytes else it can be of upmost 60 bytes. Header fields:

1. Source Port / Destination Port (16 bits each): Identify sending and receiving applications.

2. Sequence Number (32 bits): Position of the first byte in this segment, used for ordering.

3. Acknowledgement Number (32 bits): Next byte expected by the receiver (confirms data received).

4. Header Length (HLEN): Size of the header (5–15 words, i.e., 20–60 bytes).

5. Control Flags (1 bit each):

*   URG: Urgent data

*   ACK: Acknowledgement valid

*   PSH: Push data immediately

*   RST: Reset connection

*   SYN: Synchronize sequence numbers

*   FIN: Terminate connection

6. Window Size: Receiver’s buffer size (for flow control).

7. Checksum: Error detection (mandatory).

8. Urgent Pointer: Position of urgent data (if URG flag is set).

## TCP 3-Way Handshake Process

![Branching](https://tyler-nse.github.io/assets/img/net_sec_101/3-way_handshake.PNG)

*   Step 1 (SYN): In the first step, the client wants to establish a connection with a server, so it sends a segment with SYN(Synchronize Sequence Number) which informs the server that the client is likely to start communication and with what sequence number it starts segments with

*   Step 2 (SYN + ACK): Server responds to the client request with SYN-ACK signal bits set. Acknowledgement(ACK) signifies the response of the segment it received and SYN signifies with what sequence number it is likely to start the segments with

*   Step 3 (ACK): In the final part client acknowledges the response of the server and they both establish a reliable connection with which they will start the actual data transfer.

[back](/fundamentals/networks_and_security.html)
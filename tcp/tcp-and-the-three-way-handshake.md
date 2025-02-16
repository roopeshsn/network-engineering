# TCP and The Three-way Handshake

## Why TCP?

The need for a transport protocol arose due to the following reasons:
1. I have email and telnet applications running on my device. How does my device differentiate if the packet is destined for which application?
2. What if my device handles a packet size of X but the sender sends out a packet with a size of X+100? How will my device handle it?
3. How will my device reassemble the packets if the packets were out of order?
4. What if some packets got lost or dropped on intermediate devices? How will my device handle it?
5. How will my device handle it if there are errors in the data?

## Why is TCP being adopted by many application-level protocols?

If not, then the developers should rewrite the logic for the above scenarios, where they reinvent a protocol like TCP.

## Why 3WHS?

If a device wants to send data, it can open a connection and start sending the data. Why should it undergo a series of steps known as a 3-way handshake?

Because of the following reasons:
1. To check if the peer is listening to the desired application port or not.
2. To ensure bi-directional communication.
3. To sync sequence and acknowledgment numbers.
4. What is the buffer size to allocate for managing the state?

I am able to think of the above reasons for the need of TCP and 3WHS. Let me know if you have more points by creating an issue or a discussion.
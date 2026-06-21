## What TCP and UPD terms mean and how they are different

TCP (Transmission Control Protocol) and UDP (User Datagram Protocol) are transport standards that dictate how data travels across the internet. TCP prioritizes reliability (checking for errors and lost data), while UDP prioritizes speed and efficiency (sending data quickly without checking for errors).

++Key Differences++

1. Reliability:
  - TCP: Establishes a connection first, tracks packets, and resends missing or corrupted data.
  - UDP: Sends data blindly without establishing a connection. It does not resend lost packets.
2. Speed:
  - TCP: Slower due to handshakes, acknowledgments, and error-checking.
  - UDP: Faster because it has no overhead or waiting.
3. Best Uses:
  - TCP: Web browsing (HTTP/S), emails, and file transfers where missing data breaks the file.
  - UDP: Live video streaming, VoIP (voice calls), and online gaming where speed matters more than a dropped frame.

++Commonly Used Web and Network Ports++

Ports act as virtual doors on a server or computer, directing incoming traffic to the right application. Here are the ports most frequently used for web and network services:

| **Port** | **Protocol** | **Type** | **Description**                                                                                                |
| -------- | ------------ | -------- | -------------------------------------------------------------------------------------------------------------- |
| 80       | HTTP         | TCP      | Hypertext Transfer Protocol: Used for standard, unencrypted web traffic.                                       |
| 443      | HTTPS        | TCP      | HTTP Secure: Encrypted web traffic (used for secure logins, e-commerce, etc.).                                 |
| 22       | SSH/SFTP     | TCP      | Secure Shell / SSH File Transfer Protocol: Used for secure, remote command-line login and safe file transfers. |
| 20/21    | FTP          | TCP      | File Transfer Protocol: Used for transferring files between a client and a server.                             |
| 23       | Telnet       | TCP      | Telecommunication Network: An older protocol for unencrypted remote text communication and command-line access |

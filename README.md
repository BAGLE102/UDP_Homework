# UDP_Homework

**Name:** 况旻諭
**Student ID:** 614430005

---

## 1. Overview

This project implements a simple **UDP Echo Server and Client** in the **C language** under **POSIX/Linux**.

* The **Server** listens on a specified UDP port, receives datagrams from clients, and **echoes back** each message to the sender.
* The **Client** sends user-input messages to the server using **sendto()**, then waits for a reply with **recvfrom()** and prints the echoed message.

Both programs use **connectionless UDP sockets** and low-level system calls (`socket()`, `sendto()`, `recvfrom()`, etc.) to demonstrate datagram-based communication.

---

## 2. Files

* `614430005_UDPServer.c` — UDP echo server implementation
* `614430005_UDPClient.c` — UDP echo client implementation
* `Makefile` — Build script for GNU `make`
* `614430005_Readme.pdf` — This documentation (exported from Markdown for submission)

---

## 3. Build Instructions

To compile both the server and client:

```bash
make
```

To clean up compiled executables:

```bash
make clean
```

**Compiler:** `gcc` (or `clang`)
**C Standard:** `-std=c11`

---

## 4. Run Instructions

**Run the Server:**

```bash
./udp_server 9999
```

The server will start listening on UDP port `9999` and wait for incoming datagrams.

**Run the Client:**

```bash
./udp_client 127.0.0.1 9999
```

Then type a line and press **Enter** — the server will echo it back.
Press **Ctrl + D** to exit the client.

---

## 5. Implementation Details

Key system calls and their purposes:

| Function                         | Description                                             |
| -------------------------------- | ------------------------------------------------------- |
| `socket(AF_INET, SOCK_DGRAM, 0)` | Creates a UDP socket (IPv4).                            |
| `bind()`                         | Binds the socket to `0.0.0.0:<port>` (server side).     |
| `sendto()`                       | Sends a datagram to a specified destination address.    |
| `recvfrom()`                     | Receives a datagram and retrieves the sender’s address. |
| `inet_pton()` / `inet_ntop()`    | Converts between text and binary IP addresses.          |
| `close()`                        | Closes the socket and releases system resources.        |

> ⚙️ **UDP is connectionless**, meaning no handshake or persistent connection is established.
> Each `sendto()` corresponds to a complete, independent datagram.

---
## 6. Results

**Server-side result:**

![Server Result](https://github.com/BAGLE102/UDP_Homework/blob/main/UDP_Server.png)

**Client-side result:**
![Client Result](https://github.com/BAGLE102/UDP_Homework/blob/main/UDP_Client.png)

**Wireshark capture:**
![Wireshark Result](https://github.com/BAGLE102/UDP_Homework/blob/main/UDP_WireShark.png)

![Wireshark Result](https://github.com/BAGLE102/UDP_Homework/blob/main/UDP_data.png)
---



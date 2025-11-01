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

## 6. Example Execution

**Server Output:**

```
[SERVER] UDP echo listening on 0.0.0.0:9999
[SERVER] receive (5 bytes) from 127.0.0.1:48612
[SERVER] reply   (5 bytes) to   127.0.0.1:48612
```

**Client Output:**

```
[CLIENT] UDP echo to 127.0.0.1:9999
Enter UDP msg (Ctrl+D to quit):
Hi
[CLIENT] Receive (5 bytes) from 127.0.0.1:9999
From Server: Hi
```

---

## 7. Results

🖼️ **Server-side result:**
![Server Result](https://raw.githubusercontent.com/BAGLE102/UDP_Homework/main/Server.png)

🖼️ **Client-side result:**
![Client Result](https://raw.githubusercontent.com/BAGLE102/UDP_Homework/main/Client.png)

🖼️ **Wireshark capture:**
![Wireshark Result](https://raw.githubusercontent.com/BAGLE102/UDP_Homework/main/Wireshark.png)

---

## 8. Wireshark Observation

To capture the UDP packets exchanged between the client and server:

* If both programs run on the same machine, select **Loopback: lo** as the interface.
* Set **Capture Filter** to:

  ```
  udp port 9999
  ```
* If testing between two different hosts, choose the appropriate physical interface (e.g., `enp0s31f6`).

You should observe packets similar to the following:

| Source IP       | Destination IP  | Protocol | Length | Info         |
| --------------- | --------------- | -------- | ------ | ------------ |
| 192.168.118.141 | 192.168.118.144 | UDP      | 60     | 58668 → 9999 |
| 192.168.118.144 | 192.168.118.141 | UDP      | 1066   | 9999 → 58668 |

---

## 9. Notes

* UDP does **not guarantee delivery or order**, but it is lightweight and fast for simple message exchanges.
* Each datagram is independent — lost packets are not retransmitted automatically.
* This project demonstrates basic UDP socket usage and packet inspection using Wireshark.

---

Would you like me to also produce this as a **ready-to-submit PDF version (`614430005_Readme.pdf`)** with your name and screenshot placeholders (for server, client, and Wireshark)?

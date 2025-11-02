# UDP_Homework

**Name:** 况旻諭
**Student ID:** 614430005

---

## 1. Overview  

This project implements a simple **UDP Echo Server and Client** using the **C language** under **POSIX/Linux**.  

- The **Server** listens on a specified UDP port, receives datagrams from clients, and **echoes back** each message to the sender.  
- The **Client** sends user-input messages to the server using **sendto()**, then waits for a reply with **recvfrom()** and displays the echoed response.  

Both programs use **connectionless UDP sockets** and low-level system calls (`socket()`, `sendto()`, `recvfrom()`, etc.) to demonstrate datagram-based communication.  

---

## 2. Files  

- `614430005_UDPServer.c` — UDP echo server implementation  
- `614430005_UDPClient.c` — UDP echo client implementation  
- `Makefile` — Build script for GNU `make`  
- `614430005_Readme.pdf` — This documentation (exported from Markdown for submission)  

---

## 3. Build Instructions  

To compile both the server and client:  

```bash
make
````

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

> **Note:** UDP is **connectionless**, meaning no handshake or persistent connection is required.
> Each `sendto()` corresponds to an independent datagram.

---

## 6. Example Execution

**Server Output:**

```text
[SERVER] UDP echo listening on 0.0.0.0:9999
[SERVER] receive (5 bytes) from 127.0.0.1:48612
[SERVER] reply   (5 bytes) to   127.0.0.1:48612
```

**Client Output:**

```text
[CLIENT] UDP echo to 127.0.0.1:9999
Enter UDP msg (Ctrl+D to quit):
Hi
[CLIENT] Receive (5 bytes) from 127.0.0.1:9999
From Server: Hi
```

---

## 7. Results

**Server Output:** <img src="https://raw.githubusercontent.com/BAGLE102/UDP_Homework/main/UDP_Server.png" width="700"/>

**Client Output:** <img src="https://raw.githubusercontent.com/BAGLE102/UDP_Homework/main/UDP_Client.png" width="700"/>

**Wireshark Capture:** <img src="https://raw.githubusercontent.com/BAGLE102/UDP_Homework/main/UDP_WireShark.png" width="700"/>

**Wireshark Data Detail:** <img src="https://raw.githubusercontent.com/BAGLE102/UDP_Homework/main/UDP_data.png" width="700"/>

---

## 8. Wireshark Observation

To capture UDP packets exchanged between the client and server:

1. If both programs run on the same machine, select **Loopback: lo** as the capture interface.
2. Set the **Capture Filter** to:

   ```
   udp port 9999
   ```
3. If testing between two hosts, choose the correct physical interface (e.g., `enp0s31f6`).

Example captured packets:

| Source IP       | Destination IP  | Protocol | Length | Info         |
| --------------- | --------------- | -------- | ------ | ------------ |
| 192.168.118.141 | 192.168.118.144 | UDP      | 60     | 58668 → 9999 |
| 192.168.118.144 | 192.168.118.141 | UDP      | 1066   | 9999 → 58668 |

**Wireshark Hex Data Example:**

```text
0000  00 03 04 06 00 00 00 00  51 3e 08 00 45 00 00 22
0010  88 66 40 00 40 11 cb 71  c0 a8 32 d1 92 38 27 0f
0020  00 0e e7 12 68 65 6c 6c  6f 0a
```







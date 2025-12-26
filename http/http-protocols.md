![http-protocols](http-protocols.gif "http-protocols")

# Network Protocols Reference

A quick reference guide to essential network and application layer protocols.

---

## 🌐 HTTP (HyperText Transfer Protocol)

**The foundation of web communication**

Text-based, stateless protocol for transferring hypermedia documents between clients and servers.

| Feature | Description |
|---------|-------------|
| **Layer** | Application (Layer 7) |
| **Transport** | TCP |
| **Port** | 80 |
| **State** | Stateless |
| **Use Cases** | Web pages, REST APIs, file downloads |

### Key Characteristics

- **Request-Response model** — Client sends request, server responds
- **Methods** — GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS
- **Headers** — Metadata for requests and responses
- **Versions** — HTTP/1.0, HTTP/1.1, HTTP/2

```
Client                         Server
   │                              │
   │──── GET /index.html ────────▶│
   │◀─── 200 OK + HTML ───────────│
```

---

## ⚡ HTTP/3 & QUIC

**Next-generation web protocol built on UDP**

HTTP/3 replaces TCP with QUIC (Quick UDP Internet Connections) for faster, more reliable connections.

| Feature | Description |
|---------|-------------|
| **Layer** | Application (Layer 7) |
| **Transport** | QUIC (over UDP) |
| **Port** | 443 |
| **Encryption** | TLS 1.3 built-in (mandatory) |
| **Use Cases** | Modern web apps, streaming, mobile |

### Why QUIC over TCP?

| Problem with TCP | QUIC Solution |
|------------------|---------------|
| 3-way handshake delay | 0-RTT / 1-RTT connection setup |
| Head-of-line blocking | Independent streams per request |
| Connection drops on network change | Connection migration (keeps connection alive) |
| Separate TLS handshake | Encryption built into protocol |

```
┌─────────────────────────────────────────────────────────┐
│  TCP + TLS (HTTP/2)          QUIC (HTTP/3)             │
│  ──────────────────          ────────────────           │
│  TCP Handshake: 1 RTT        Combined: 1 RTT           │
│  TLS Handshake: 2 RTT        (or 0-RTT for repeat)     │
│  ─────────────────────       ─────────────────────      │
│  Total: 3 RTT                Total: 1 RTT (or 0)       │
└─────────────────────────────────────────────────────────┘
```

---

## 🔒 HTTPS (HTTP Secure)

**HTTP encrypted with TLS**

Secures HTTP communication using Transport Layer Security (TLS), ensuring privacy, integrity, and authentication.

| Feature | Description |
|---------|-------------|
| **Layer** | Application (Layer 7) |
| **Transport** | TCP + TLS |
| **Port** | 443 |
| **Encryption** | TLS 1.2 / TLS 1.3 |
| **Use Cases** | All secure web traffic, APIs, authentication |

### What TLS Provides

| Protection | Description |
|------------|-------------|
| **Confidentiality** | Data encrypted, unreadable to attackers |
| **Integrity** | Detects any tampering with data |
| **Authentication** | Verifies server identity via certificates |

### TLS Handshake

```
Client                                    Server
   │                                         │
   │─────── ClientHello ────────────────────▶│
   │        (supported ciphers, random)      │
   │                                         │
   │◀────── ServerHello + Certificate ───────│
   │        (chosen cipher, public key)      │
   │                                         │
   │─────── Key Exchange + Finished ────────▶│
   │                                         │
   │◀═══════ Encrypted Traffic ═════════════▶│
```

---

## 🔌 WebSocket

**Full-duplex, bidirectional communication**

Persistent connection protocol enabling real-time, two-way communication between client and server.

| Feature | Description |
|---------|-------------|
| **Layer** | Application (Layer 7) |
| **Transport** | TCP |
| **Port** | 80 (ws://), 443 (wss://) |
| **State** | Stateful (persistent connection) |
| **Use Cases** | Chat apps, live feeds, gaming, collaborative tools |

### HTTP vs WebSocket

| HTTP | WebSocket |
|------|-----------|
| Request-response only | Bidirectional |
| New connection per request | Single persistent connection |
| Client initiates | Both can send anytime |
| Higher overhead | Low overhead after handshake |

### Connection Lifecycle

```
Client                                    Server
   │                                         │
   │─────── HTTP Upgrade Request ───────────▶│
   │        Upgrade: websocket               │
   │                                         │
   │◀────── 101 Switching Protocols ─────────│
   │                                         │
   │◀═══════ Bidirectional Messages ════════▶│
   │         (frames, not HTTP)              │
   │                                         │
   │─────── Close Frame ────────────────────▶│
   │◀────── Close Frame ─────────────────────│
```

---

## 📡 TCP (Transmission Control Protocol)

**Reliable, ordered data delivery**

Connection-oriented protocol guaranteeing data arrives complete and in order.

| Feature | Description |
|---------|-------------|
| **Layer** | Transport (Layer 4) |
| **Connection** | Connection-oriented (3-way handshake) |
| **Reliability** | Guaranteed delivery, retransmission |
| **Ordering** | Maintains packet order |
| **Use Cases** | Web, email, file transfer, SSH |

### 3-Way Handshake

```
Client                                    Server
   │                                         │
   │─────── SYN ────────────────────────────▶│
   │        (I want to connect)              │
   │                                         │
   │◀────── SYN-ACK ─────────────────────────│
   │        (OK, I acknowledge)              │
   │                                         │
   │─────── ACK ────────────────────────────▶│
   │        (Connection established)         │
   │                                         │
   │◀═══════ Data Transfer ═════════════════▶│
```

### Key Mechanisms

| Mechanism | Purpose |
|-----------|---------|
| **Sequence Numbers** | Track packet order |
| **Acknowledgments** | Confirm receipt |
| **Retransmission** | Resend lost packets |
| **Flow Control** | Prevent overwhelming receiver |
| **Congestion Control** | Prevent network overload |

---

## 🚀 UDP (User Datagram Protocol)

**Fast, connectionless data transfer**

Lightweight protocol prioritizing speed over reliability — fire and forget.

| Feature | Description |
|---------|-------------|
| **Layer** | Transport (Layer 4) |
| **Connection** | Connectionless (no handshake) |
| **Reliability** | No guarantee (packets may be lost) |
| **Ordering** | No ordering guarantee |
| **Use Cases** | Video streaming, gaming, VoIP, DNS |

### TCP vs UDP

| TCP | UDP |
|-----|-----|
| Connection-oriented | Connectionless |
| Reliable delivery | Best-effort delivery |
| Ordered packets | No ordering |
| Slower (overhead) | Faster (minimal overhead) |
| Flow/congestion control | No built-in control |

### When to Use UDP

| Scenario | Why UDP |
|----------|---------|
| **Live video/audio** | Dropped frame < delayed stream |
| **Online gaming** | Low latency critical |
| **DNS queries** | Small, single request-response |
| **IoT sensors** | Lightweight, frequent updates |

```
Client                                    Server
   │                                         │
   │─────── Datagram ───────────────────────▶│  (no handshake)
   │─────── Datagram ───────────────────────▶│
   │◀────── Datagram ────────────────────────│
   │                                         │
   │        (packets may arrive out of       │
   │         order or not at all)            │
```

---

## 📧 SMTP (Simple Mail Transfer Protocol)

**Email delivery protocol**

Text-based protocol for sending emails between mail servers.

| Feature | Description |
|---------|-------------|
| **Layer** | Application (Layer 7) |
| **Transport** | TCP |
| **Port** | 25 (relay), 587 (submission), 465 (SMTPS) |
| **Security** | STARTTLS or implicit TLS |
| **Use Cases** | Sending emails, server-to-server relay |

### SMTP vs Other Email Protocols

| Protocol | Purpose |
|----------|---------|
| **SMTP** | Sending emails |
| **IMAP** | Reading emails (synced, server-stored) |
| **POP3** | Downloading emails (local storage) |

### Email Flow

```
┌─────────┐    SMTP     ┌─────────┐    SMTP     ┌─────────┐
│ Sender  │────────────▶│ Sender  │────────────▶│ Receiver│
│ Client  │   (587)     │ Server  │   (25)      │ Server  │
└─────────┘             └─────────┘             └────┬────┘
                                                     │
                                                IMAP/POP3
                                                     │
                                                     ▼
                                               ┌─────────┐
                                               │Receiver │
                                               │ Client  │
                                               └─────────┘
```

### SMTP Commands

| Command | Purpose |
|---------|---------|
| `HELO/EHLO` | Introduce client to server |
| `MAIL FROM` | Specify sender address |
| `RCPT TO` | Specify recipient address |
| `DATA` | Begin message content |
| `QUIT` | End session |

---

## 📁 FTP (File Transfer Protocol)

**File transfer between systems**

Protocol for uploading and downloading files between client and server.

| Feature | Description |
|---------|-------------|
| **Layer** | Application (Layer 7) |
| **Transport** | TCP |
| **Port** | 21 (control), 20 (data) |
| **Security** | FTPS (TLS) or SFTP (SSH) for secure transfer |
| **Use Cases** | File hosting, website deployment, backups |

### Active vs Passive Mode

| Mode | Description |
|------|-------------|
| **Active** | Server connects back to client for data (firewall issues) |
| **Passive** | Client initiates both connections (firewall-friendly) |

### FTP Connections

```
┌─────────────────────────────────────────────────────────┐
│  Client                                   Server        │
│     │                                        │          │
│     │════ Control Connection (Port 21) ═════│          │
│     │     (commands: LIST, RETR, STOR)       │          │
│     │                                        │          │
│     │──── Data Connection (Port 20/random) ─▶│          │
│     │     (actual file transfer)             │          │
└─────────────────────────────────────────────────────────┘
```

### Common Commands

| Command | Purpose |
|---------|---------|
| `USER/PASS` | Authentication |
| `LIST` | List directory contents |
| `RETR` | Download file |
| `STOR` | Upload file |
| `DELE` | Delete file |
| `MKD/RMD` | Create/remove directory |

### FTP Variants

| Variant | Description |
|---------|-------------|
| **FTP** | Plain text (insecure) |
| **FTPS** | FTP + TLS encryption |
| **SFTP** | SSH File Transfer Protocol (different protocol) |

---

## 📊 Protocol Comparison

| Protocol | Layer | Transport | Port | Reliable | Use Case |
|----------|-------|-----------|------|----------|----------|
| HTTP | App | TCP | 80 | ✅ Yes | Web pages, APIs |
| HTTP/3 | App | QUIC/UDP | 443 | ✅ Yes | Modern web |
| HTTPS | App | TCP+TLS | 443 | ✅ Yes | Secure web |
| WebSocket | App | TCP | 80/443 | ✅ Yes | Real-time apps |
| TCP | Transport | — | — | ✅ Yes | Reliable data |
| UDP | Transport | — | — | ❌ No | Fast/streaming |
| SMTP | App | TCP | 25/587 | ✅ Yes | Sending email |
| FTP | App | TCP | 21 | ✅ Yes | File transfer |

---

## 🔗 Protocol Stack

```
┌─────────────────────────────────────────────────────────┐
│                    Application Layer                     │
│   HTTP │ HTTPS │ WebSocket │ SMTP │ FTP │ DNS │ SSH    │
├─────────────────────────────────────────────────────────┤
│                    Transport Layer                       │
│              TCP          │         UDP                  │
│                           │         └── QUIC ──▶ HTTP/3 │
├─────────────────────────────────────────────────────────┤
│                    Network Layer                         │
│                         IP                               │
├─────────────────────────────────────────────────────────┤
│                    Link Layer                            │
│              Ethernet │ WiFi │ etc.                      │
└─────────────────────────────────────────────────────────┘
```

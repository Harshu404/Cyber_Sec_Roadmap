# 0.2 — How the Internet Actually Works

> 📅 **Week 2** | 🏷️ Phase 0 — Internet History
> 🔗 [Read full blog on Blogger](#) | 💼 [LinkedIn Post](#)

---

## 📖 Introduction

You type `google.com` and in less than 200 milliseconds, Google's homepage appears.

But what actually happened in those 200ms?

Your request traveled through your router, your ISP, possibly across an undersea cable at the bottom of the ocean, through massive backbone routers, reached Google's server, and came back — all in the blink of an eye.

This is exactly how that works.

---

## 🧠 The Big Picture — 5 Layers of the Internet

Think of the internet as a postal system with 5 levels:

```
YOU (Device)
    ↓
Your Router (Home Network)
    ↓
ISP — Internet Service Provider (Local Post Office)
    ↓
Internet Backbone (Highway / Motorway)
    ↓
Destination Server (Google, YouTube, etc.)
```

---

## 1️⃣ Your Device — Where It All Starts

When you type `google.com`:

1. Your browser checks its **cache** first — "Have I visited this before?"
2. If not, it asks **DNS** — "What is the IP address of google.com?"
3. DNS replies: `142.250.80.46`
4. Your browser creates an **HTTP request** (a digital letter)
5. That letter gets broken into small **packets**
6. Packets travel out through your **Network Interface Card (NIC)**

---

## 2️⃣ Your Router — Traffic Controller

Your home router does two jobs:

**Job 1 — NAT (Network Address Translation)**
- Your router has ONE public IP (given by ISP)
- Every device in your home gets a PRIVATE IP (192.168.x.x)
- NAT translates between them
- Example: Your laptop is `192.168.1.5` but the internet sees `103.21.244.10`

**Job 2 — Forwarding**
- Router decides: "This packet goes to the internet, not to my local network"
- Sends it to the ISP gateway

---

## 3️⃣ ISP — Internet Service Provider

Your ISP (Jio, Airtel, BSNL, etc.) is your door to the internet.

**What your ISP does:**
- Assigns you a **public IP address** (dynamic or static)
- Routes your traffic toward the destination
- Maintains **DNS servers** you use by default
- Controls your **bandwidth** and **speed**

**ISP Hierarchy (3 Tiers):**

| Tier | Who | Role |
|------|-----|------|
| Tier 1 | AT&T, NTT, Tata Communications | Own the global backbone |
| Tier 2 | Jio, Airtel, Comcast | Buy from Tier 1, sell to Tier 3 |
| Tier 3 | Local ISPs, small providers | Sell to homes and businesses |

Your home ISP is likely **Tier 2 or Tier 3**.

---

## 4️⃣ Internet Backbone — The Highway

The Internet Backbone is a system of **high-speed fiber optic cables** that connect ISPs, countries, and continents.

**Key facts:**
- Speed: **100 Gbps to 400 Gbps** per cable
- Operated by: Tier 1 ISPs and large tech companies (Google, Meta, Amazon)
- Google owns over **1 million km** of undersea cable
- Data travels through these at **~200,000 km/second** (2/3 speed of light)

### 🌊 Undersea Cables — The Hidden Internet

Most people think the internet is wireless. It's not.

**95% of international internet traffic travels through undersea cables.**

Facts:
- Over **400 submarine cables** currently active worldwide
- Total length: **1.3 million km** — enough to circle Earth **32 times**
- Cables are surprisingly thin — **about the width of a garden hose**
- Protected by steel wire armor near shores (shark bites are real!)
- Deepest cable: **8,000 meters** below sea level
- India connects to the world via cables landing at **Mumbai, Chennai, Cochin**

> **Fun fact:** When a ship drops anchor in the wrong place, it can cut an undersea cable and disrupt internet for an entire country.

---

## 5️⃣ IXP — Internet Exchange Points

IXPs are physical locations where different ISPs and networks **meet and exchange traffic directly** — without going through a third party.

**Why important:**
- Without IXP: Your Jio request → Goes to US → Comes back to Airtel server in India
- With IXP: Your Jio request → Goes to IXP in Mumbai → Airtel server (same city!)
- IXPs reduce **latency** and **cost** massively

**Major IXPs in India:**
- DE-CIX Mumbai
- AMS-IX India (Mumbai)
- NIXI (Chennai, Delhi, Kolkata, Mumbai)

---

## 📦 How Packets Travel — Step by Step

Every piece of data on the internet is broken into **packets** (small chunks, usually 1500 bytes).

**Example: You download a 1MB image**

```
1MB image = ~667 packets of 1500 bytes each

Each packet contains:
- Source IP (your IP)
- Destination IP (server IP)
- Sequence number (so they can be reassembled)
- The actual data (payload)
```

**The journey:**
```
Your Device
    → Router (NAT applied)
        → ISP Router
            → Backbone Router (maybe 10-15 hops)
                → IXP (if same country)
                    → Destination ISP
                        → Destination Server

Server sends response back — same process in reverse
All 667 packets may take DIFFERENT routes
All reassembled at your device using sequence numbers
```

**traceroute command shows you every hop:**
```bash
traceroute google.com        # Linux/Mac
tracert google.com           # Windows
```

---

## ⏱️ Why is it So Fast? — Latency Explained

**Latency** = Time taken for a packet to travel from source to destination.

| Connection Type | Typical Latency |
|----------------|----------------|
| Same city | 1–5 ms |
| Same country | 10–30 ms |
| India to USA | 150–200 ms |
| India to Australia | 100–150 ms |
| Satellite (old) | 500–700 ms |
| Satellite (Starlink) | 20–40 ms |

**Factors that affect speed:**
- Physical distance
- Number of hops (routers in between)
- Cable type (fiber vs copper)
- Congestion (too many users)
- Server processing time

---

## 🔁 Full Flow — google.com Example

```
1. You type: google.com
2. Browser checks cache → not found
3. DNS query → returns 142.250.80.46
4. TCP connection established (3-way handshake: SYN → SYN-ACK → ACK)
5. HTTP GET request sent
6. Request broken into packets
7. Packets leave your NIC → Router
8. Router applies NAT → sends to ISP
9. ISP routes to backbone
10. Backbone routes across undersea cables (if needed)
11. Arrives at Google's data center
12. Google server processes request
13. Sends HTML, CSS, JS back as packets
14. Packets reassembled at your device
15. Browser renders the page
Total time: ~50–200 milliseconds ⚡
```

---

## 🔑 Key Takeaways

1. **Internet = physical infrastructure** — cables, routers, servers — not magic
2. **ISPs have tiers** — Tier 1 owns the backbone, Tier 3 sells to you
3. **95% of global traffic** runs through undersea fiber cables
4. **IXPs** make local traffic faster and cheaper
5. **Packets** are how all data travels — broken up, sent separately, reassembled
6. **Latency** depends on distance, hops, and cable type

---

## 💡 Real World Analogy

The internet is like a global postal system:

| Internet | Postal System |
|----------|--------------|
| Packet | Letter/Parcel |
| IP Address | House Address |
| Router | Sorting Office |
| ISP | Local Post Office |
| Backbone | National Highway |
| Undersea Cable | International Shipping Route |
| IXP | Regional Distribution Hub |

---

## 📚 References

1. Cloudflare — How does the Internet work?
   https://www.cloudflare.com/learning/network-layer/how-does-the-internet-work/

2. TeleGeography — Submarine Cable Map
   https://www.submarinecablemap.com/

3. Wikipedia — Internet backbone
   https://en.wikipedia.org/wiki/Internet_backbone

4. Wikipedia — Internet exchange point
   https://en.wikipedia.org/wiki/Internet_exchange_point

5. Cisco — How Routers Work
   https://www.cisco.com/c/en/us/solutions/small-business/resource-center/networking/how-does-a-router-work.html

---

## 🔗 Connect

- 📝 **Blog: https://cyberharshu.blogspot.com/2026/09/%20how-internet-actually-works.html
- 💼 **LinkedIn:https://www.linkedin.com/in/harsh-prajapati101/



# 🔹 What is a Database?

A database is a system that stores and manages data so you can:

* Insert data
* Query data
* Update/delete data efficiently

---

# 🔷 SQL Databases (Relational Databases)

## 👉 What is SQL?

SQL (Structured Query Language) databases store data in **tables (rows & columns)** with a **fixed schema**.

## 🧠 Think:

Like an Excel sheet with strict structure.

---

## 🔑 Key Characteristics

* Structured data (schema required)
* Tables with relationships (foreign keys)
* ACID properties (strong consistency)
* Uses SQL language

---

## 📊 Example Structure

**Users Table**

| id | name | age |
| -- | ---- | --- |
| 1  | John | 25  |

**Orders Table**

| id  | user_id | amount |
| --- | ------- | ------ |
| 101 | 1       | 500    |

👉 `user_id` links both tables

---

## 🛠 Popular SQL Databases

* MySQL
* PostgreSQL
* Oracle Database
* Microsoft SQL Server

---

## ✅ Advantages

* Strong consistency (no data mismatch)
* Supports complex joins & queries
* Ideal for transactions (banking, payments)

---

## ❌ Disadvantages

* Hard to scale horizontally
* Schema changes are difficult
* Less flexible for changing data

---

# 🔶 NoSQL Databases (Non-Relational)

## 👉 What is NoSQL?

NoSQL databases store data in **flexible formats** (not just tables).

## 🧠 Think:

Like JSON storage — flexible, no fixed structure.

---

## 🔑 Types of NoSQL

### 1. Document-based

* Stores JSON-like data
* Example:

  ```json
  {
    "name": "John",
    "orders": [500, 200]
  }
  ```

### 2. Key-Value

* Like a hashmap
  `user_1 → {data}`

### 3. Column-based

* Optimized for analytics

### 4. Graph databases

* Focus on relationships (social networks)

---

## 🛠 Popular NoSQL Databases

* MongoDB
* Cassandra
* Redis
* DynamoDB

---

## ✅ Advantages

* Flexible schema (easy to change)
* Highly scalable (horizontal scaling)
* Faster for large-scale distributed systems

---

## ❌ Disadvantages

* Weak consistency (eventual consistency in many cases)
* No joins (or limited)
* Complex queries are harder

---

# ⚔️ SQL vs NoSQL (Core Differences)

| Feature     | SQL           | NoSQL                    |
| ----------- | ------------- | ------------------------ |
| Data format | Tables        | JSON / Key-Value / Graph |
| Schema      | Fixed         | Flexible                 |
| Scaling     | Vertical      | Horizontal               |
| Consistency | Strong (ACID) | Eventual (BASE)          |
| Joins       | Supported     | Rare                     |
| Use case    | Transactions  | Big data, real-time apps |

---

# 🎯 When to Use SQL vs NoSQL (MOST IMPORTANT)

## ✅ Use SQL when:

👉 Data is **structured & stable**
👉 You need **transactions**
👉 Relationships are important

### Real examples:

* Banking system 💰
* Payment systems
* Order management
* Inventory systems

👉 Why?
Because **data correctness matters more than speed**

---

## ✅ Use NoSQL when:

👉 Data is **unstructured or frequently changing**
👉 You need **high scalability**
👉 You handle **huge traffic / real-time data**

### Real examples:

* Social media feeds 📱
* Chat applications 💬
* Analytics / logs
* Recommendation systems

👉 Why?
Because **speed + flexibility matters more than strict consistency**

---

# 🧠 Easy Way to Remember

### 🔹 SQL = Structure + Safety

> “I cannot afford wrong data”

### 🔹 NoSQL = Speed + Scale

> “I cannot afford slow system”

---

# 🚀 Real System Design Insight (Important for you)

In real-world systems, we often use **both**:

* SQL → core data (users, payments)
* NoSQL → caching, logs, feeds

👉 Example:

* User info → MySQL
* Session/cache → Redis
* Activity feed → MongoDB

---

# 🔥 One-Liner

👉
**“Use SQL when you need strong consistency and structured data.
Use NoSQL when you need scalability, flexibility, and high performance.”**

---

# 🔷 1. What is Consistency?

## 👉 Definition

Consistency means:

> **All users see the same data at the same time (or in a defined way)**

---

## 🧠 Simple Example

You update your profile name:

* You see: "Akshith"
* Another user sees: "Old Name"

👉 This is **inconsistent**

---

## ⚠️ In Distributed Systems

Data is stored in **multiple servers (replicas)**

So the question becomes:

> When should all replicas reflect the latest data?

---

# 🔥 2. Types of Consistency

---

# 🔹 Linearizable Consistency (Strong Consistency)

## 👉 Definition

> Every read returns the **latest written value immediately**

---

## 🧠 Example

1. Write: balance = 100 → 200
2. Immediately read → must return **200**

---

## 🚨 Key Point

* No stale data ever
* Looks like **single machine behavior**

---

## ❗ Tradeoff

* Slower
* Hard to scale

---

## ✅ Use Cases

* Banking systems
* Payments
* Inventory systems

---

# 🔹 Eventual Consistency

## 👉 Definition

> Data will become consistent **eventually**, but not immediately

---

## 🧠 Example

1. Update profile picture
2. Some users still see old picture
3. After a few seconds → everyone sees new one

---

## 🚨 Key Point

* Temporary inconsistency is allowed
* System becomes consistent later

---

## ❗ Tradeoff

* Fast and scalable
* But may show stale data

---

## ✅ Use Cases

* Social media feeds
* DNS systems
* Caching layers

---

# 🔹 Causal Consistency (often misspelled as “casual”)

## 👉 Definition

> **Related operations are seen in order**, but unrelated ones may not be

---

## 🧠 Example

1. User posts: "Hello"
2. Then comments: "How are you?"

👉 Everyone must see:

* Post → then comment
  ❌ Not comment before post

---

## 🚨 Key Idea

* Maintains **cause-effect relationship**

---

## ✅ Use Cases

* Chat systems
* Social media comments

---

# ⚔️ Summary

| Type         | Guarantee            | Speed  |
| ------------ | -------------------- | ------ |
| Linearizable | Always latest        | Slow   |
| Causal       | Order of related ops | Medium |
| Eventual     | Eventually correct   | Fast   |

---

# 🔷 3. What is Quorum?

## 👉 Definition

Quorum is a technique to **balance consistency and availability**

---

## 🧠 Basic Idea

If you have **N replicas**, you define:

* W = write replicas required
* R = read replicas required

👉 Rule:

```
R + W > N
```

---

## 🧠 Example

N = 3 replicas

* W = 2 (write to 2 nodes)
* R = 2 (read from 2 nodes)

👉 Ensures:
At least one node has latest data

---

## 🔥 Why this works

Overlap between read & write ensures **fresh data**

---

## 🎯 Real Use

* Cassandra
* DynamoDB

---

# 🔷 4. Transaction Isolation Levels

This is about **how transactions interact with each other**

---

## 🧠 Why needed?

Two users updating same data:

👉 Can cause:

* Dirty reads
* Lost updates
* Inconsistent results

---

# 🔹 (1) Read Uncommitted

## 👉 Behavior

* Can read **uncommitted data**

---

## 🧠 Example

Transaction A updates balance → not committed
Transaction B reads it

👉 If A rolls back → B read wrong data

---

## ❌ Problem

* Dirty reads

---

## 🚀 Rarely used

---

# 🔹 (2) Read Committed

## 👉 Behavior

* Only reads **committed data**

---

## 🧠 Example

Transaction B cannot see uncommitted changes

---

## ❗ Problem

* Non-repeatable reads

---

## 🧠 Example

You read balance twice → different values

---

## ✅ Default in many DBs

---

# 🔹 (3) Repeatable Read

## 👉 Behavior

* Same row read twice → same result

---

## 🧠 Example

You read balance = 100
Even if another transaction updates → you still see 100

---

## ❗ Problem

* Phantom reads

---

## 🧠 Example

Query: all users with salary > 50K
New user inserted → appears later

---

# 🔹 (4) Serializable (Strongest)

## 👉 Definition

> Transactions behave as if executed **one after another**

---

## 🧠 Example

No overlap → perfect isolation

---

## ✅ Guarantees

* No dirty reads
* No non-repeatable reads
* No phantom reads

---

## ❗ Tradeoff

* Very slow
* Locks everything

---

# ⚔️ Isolation Summary

| Level            | Dirty Read | Non-repeatable | Phantom |
| ---------------- | ---------- | -------------- | ------- |
| Read Uncommitted | ✅          | ✅              | ✅       |
| Read Committed   | ❌          | ✅              | ✅       |
| Repeatable Read  | ❌          | ❌              | ✅       |
| Serializable     | ❌          | ❌              | ❌       |

---

# 🔷 5. Transaction Implementation (How DB does this)

---

## 🔹 1. Locks (Pessimistic)

* Row-level locks
* Table-level locks

### Example:

```sql
SELECT * FROM account WHERE id=1 FOR UPDATE;
```

👉 Prevents others from modifying

---

## 🔹 2. MVCC (Multi-Version Concurrency Control)

Used in:

* PostgreSQL
* MySQL

---

## 🧠 Idea:

* Keep multiple versions of data
* Readers don’t block writers

---

## 🧠 Example

Row versions:

* v1 → old
* v2 → new

Transaction sees snapshot

---

## 🔥 Benefit

* High performance
* No blocking reads

---

## 🔹 3. Optimistic Concurrency

* No locks initially
* Check conflict at commit

---

## 🧠 Example

Version column:

```
UPDATE account SET balance=200 WHERE id=1 AND version=1;
```

If version changed → retry

---

## 🔹 4. Write-Ahead Logging (WAL)

👉 Before writing data:

* Log is written first

---

## 🧠 Why?

* Crash recovery

---

---

# 🧠 Final Mental Model (VERY IMPORTANT)

### 🔹 Consistency (Distributed Systems)

* Across machines
* Tradeoff with availability

### 🔹 Isolation (Transactions)

* Within database
* Controls concurrent access

---

# 🔥One-Liners

### Consistency:

> “Defines how fresh and synchronized data is across distributed nodes.”

### Isolation:

> “Defines how concurrent transactions interact without interfering.”

### Quorum:

> “Ensures consistency by overlapping read and write nodes.”

---

# 🔷 1. What is a Cache?

## 👉 Definition

A cache is a **temporary, fast storage layer** used to store frequently accessed data.

---

## 🧠 Simple Analogy

* Database = 📚 Library (slow but permanent)
* Cache = 🧠 Your memory (fast but limited & temporary)

---

## ⚡ Why Cache is Fast?

* Stored in **RAM (memory)**, not disk
* No complex queries
* Simple key-value access

---

## 🛠 Popular Cache Systems

* Redis
* Memcached

---

## 🧠 Example

Without cache:

```
User → DB → Response (slow)
```

With cache:

```
User → Cache → Response (fast)
         ↓ (miss)
        DB → Cache → User
```

---

# 🔥 2. If Cache is Fast, Why Not Use Only Cache?

This is the **most asked interview question**.

---

## ❌ Problem 1: Data Loss (Volatile)

Cache is:

* In memory (RAM)
* Can be cleared anytime (restart/crash)

👉 If you store only in cache:

> 💥 Data is gone on restart

---

## ❌ Problem 2: Limited Size

* RAM is expensive
* Cannot store huge data like DB

---

## ❌ Problem 3: No Strong Consistency

* Cache can become **stale**
* Not reliable for critical data

---

## ❌ Problem 4: No Complex Queries

Cache:

* Key → Value lookup

Database:

* Joins, filtering, aggregation

---

## ❌ Problem 5: No Transactions

* No ACID guarantees
* Cannot handle banking-type logic

---

## 🎯 Conclusion

👉 Cache is **NOT a replacement for DB**

👉 It is a **performance optimization layer**

---

## 🧠 Final Architecture

```
        (fast)
User → Cache → DB
         ↑
     frequently used data
```

---

# 🔷 3. Write Policies (VERY IMPORTANT)

These define:

> **How data is written to cache + database**

---

# 🔹 1. Write Through

## 👉 Flow

```
Write → Cache → DB
```

---

## 🧠 Example

Update user name:

1. Update cache
2. Immediately update DB

---

## ✅ Pros

* Cache always consistent
* Simple logic

---

## ❌ Cons

* Slower writes (DB involved every time)

---

## 🎯 Use Case

* Systems needing consistency

---

# 🔹 2. Write Back (Write Behind)

## 👉 Flow

```
Write → Cache → (later) DB
```

---

## 🧠 Example

1. Update cache
2. DB updated after some time (async)

---

## ✅ Pros

* Very fast writes
* High performance

---

## ❌ Cons

* Risk of data loss (if cache crashes before DB update)

---

## 🎯 Use Case

* Logging systems
* Analytics

---

# 🔹 3. Write Around

## 👉 Flow

```
Write → DB (skip cache)
Read → Cache (if needed)
```

---

## 🧠 Example

1. Write directly to DB
2. Cache updated only when read happens

---

## ✅ Pros

* Avoids caching unnecessary data
* Keeps cache clean

---

## ❌ Cons

* First read is slow (cache miss)

---

## 🎯 Use Case

* Data that is **not frequently accessed**

---

# ⚔️ Write Policy Summary

| Policy        | Write Speed | Consistency | Risk |
| ------------- | ----------- | ----------- | ---- |
| Write Through | Slow        | High        | Low  |
| Write Back    | Fast        | Medium      | High |
| Write Around  | Medium      | Medium      | Low  |

---

# 🔷 4. Cache Replacement Policies

Cache is **limited**, so we need to remove old data.

---

# 🔹 1. LRU (Least Recently Used)

## 👉 Idea

> Remove the item **not used for the longest time**

---

## 🧠 Example

Cache:

```
A → B → C → D
```

Access A → becomes recent

Evict:
👉 B (least recently used)

---

## ✅ Pros

* Works well for most systems

---

## 🎯 Used in:

* Redis

---

# 🔹 2. LFU (Least Frequently Used)

## 👉 Idea

> Remove item used **least number of times**

---

## 🧠 Example

Access count:

```
A(5), B(2), C(1)
```

Evict:
👉 C

---

## ✅ Pros

* Keeps popular data

---

## ❌ Cons

* Old popular items may stay forever

---

# 🔹 3. Segmented LRU (SLRU)

## 👉 Idea

Split cache into:

* Recent segment
* Frequent segment

---

## 🧠 Flow

1. New item → recent segment
2. Frequently accessed → moved to frequent segment
3. Eviction happens from recent first

---

## ✅ Pros

* Combines LRU + LFU benefits
* Better real-world performance

---

# 🔥 Real System Insight (VERY IMPORTANT)

### Example: Instagram / Netflix

* Cache: feed data, recommendations
* DB: user data, transactions

---

## 🧠 Common Pattern

👉 Cache Aside (Lazy Loading)

```
Read:
  if cache hit → return
  else → DB → store in cache → return
```

👉 This is the **most used pattern**

---

# 🔥 One-Liners

### Cache:

> “Cache is a fast, temporary storage layer used to reduce database load and latency.”

### Why not only cache:

> “Because cache is volatile, limited, and lacks consistency & transactions.”

### Write policies:

> “Define how data flows between cache and database.”

---

# 🔷 1. Layers: Physical, Routing, Behavior

Think of networking as layers solving different problems.

---

## 🔹 Physical Layer (How bits travel)

## 👉 What it does

* Sends **raw bits (0s and 1s)** over medium

## 🧠 Examples

* Fiber optic cables
* Ethernet cables
* Wi-Fi signals

---

## 🧠 Analogy

> Like roads carrying vehicles

---

## 🔑 Key Idea

* Concerned with **signals, voltage, transmission**
* No understanding of data meaning

---

## 🔹 Routing Layer (How data finds destination)

## 👉 What it does

* Decides **where packets go**

---

## 🧠 Example

* Your request goes through multiple routers to reach Google

---

## 🔑 Protocol

* IP (Internet Protocol)

---

## 🧠 Analogy

> GPS deciding route from Hyderabad → Bangalore

---

## 🔹 Behavior Layer (How communication happens)

(Usually corresponds to transport + application behavior)

## 👉 What it does

* Defines **how systems talk**

---

## 🧠 Examples

* TCP (reliable)
* HTTP (web communication)

---

## 🧠 Analogy

> Language + rules of conversation

---

# 🔷 2. Connecting to the Internet (Full Journey)

Let’s trace what happens when you open a website.

---

## 🌐 Step-by-step

### 1. You connect to ISP

* ISP = Internet Service Provider
* Example: Airtel, Jio

👉 ISP gives:

* IP address
* Internet access

---

### 2. DNS Resolution

## 👉 Problem

You type:

```
google.com
```

But internet needs:

```
142.250.x.x
```

---

## 👉 Solution: DNS

* DNS = Phonebook of internet

Example:

* Google Public DNS

---

## 🧠 Flow

1. Check browser cache
2. OS cache
3. DNS server
4. Get IP

---

### 3. Request Travels

* Your request goes through:

  * Routers
  * Switches
  * Data centers

---

### 4. Server Responds

* Server processes request
* Sends response back

---

## 🧠 Final Flow

```id="xq6cl9"
Browser → ISP → DNS → Server → Response
```

---

# 🔷 3. Internal Routing: MAC Address & NAT

---

## 🔹 MAC Address (Local identity)

## 👉 Definition

* Unique identifier of device (hardware level)

---

## 🧠 Example

* Like device fingerprint

---

## 🔑 Used in:

* Local network (LAN)

---

## 🔹 NAT (Network Address Translation)

## 👉 Problem

* Limited public IPs

---

## 👉 Solution

NAT allows:

> Multiple devices → 1 public IP

---

## 🧠 Example

Home network:

```id="t2ydnt"
Phone → 192.168.0.2  
Laptop → 192.168.0.3  
Router → Public IP (1)
```

---

## 🔥 How NAT works

* Router maps:

```
private IP ↔ public IP
```

---

## 🎯 Benefit

* Saves IP addresses
* Adds security layer

---

# 🔷 4. TCP, UDP, HTTP, WebSockets

---

# 🔹 TCP (Reliable)

## 👉 Features

* Connection-oriented
* Reliable delivery
* Ordered packets

---

## 🧠 Example

* File download

---

## ❗ Cost

* Slower

---

# 🔹 UDP (Fast but unreliable)

## 👉 Features

* No connection
* No guarantee

---

## 🧠 Example

* Video streaming
* Gaming

---

## ❗ Tradeoff

* Speed > reliability

---

# 🔹 HTTP

## 👉 What it is

* Protocol for web communication

---

## 🧠 Flow

```id="ijpxi7"
Client → Request → Server  
Server → Response → Client
```

---

## ❗ Stateless

* Each request independent

---

# 🔹 WebSockets

## 👉 What it is

* Persistent connection

---

## 🧠 Example

* Chat apps
* Live notifications

---

## 🔥 Difference from HTTP

| Feature    | HTTP             | WebSocket      |
| ---------- | ---------------- | -------------- |
| Connection | Short-lived      | Persistent     |
| Direction  | Request-response | Bi-directional |

---

# 🔷 5. Communication Standards

---

# 🔹 REST

## 👉 Features

* Uses HTTP
* Resource-based

---

## 🧠 Example

```
GET /users
POST /orders
```

---

## ✅ Pros

* Simple
* Widely used

---

# 🔹 GraphQL

## 👉 Features

* Client decides data

---

## 🧠 Example

```
query {
  user {
    name
    orders
  }
}
```

---

## ✅ Pros

* No over-fetching

---

# 🔹 gRPC

## 👉 Features

* Binary protocol
* Uses HTTP/2

---

## 🧠 Example

* Microservices communication

---

## ✅ Pros

* Very fast
* Strong typing

---

# ⚔️ Summary

| Type    | Use                    |
| ------- | ---------------------- |
| REST    | Public APIs            |
| GraphQL | Flexible queries       |
| gRPC    | Internal microservices |

---

# 🔷 6. Head-of-Line Blocking

## 👉 Definition

> One slow request blocks others

---

## 🧠 Example (HTTP/1.1)

```id="fyw4n7"
Request1 (slow)  
Request2 (fast but waits)
```

---

## ❗ Problem

* Performance degradation

---

## ✅ Solution

* HTTP/2 (multiplexing)
* HTTP/3 (QUIC)

---

# 🔷 7. Video Transmission

---

# 🔹 WebRTC

## 👉 What it is

* Real-time communication

---

## 🧠 Examples

* Video calls (Zoom, Meet)

---

## 🔑 Features

* Peer-to-peer
* Low latency

---

---

# 🔹 HTTP-DASH

## 👉 What it is

* Adaptive video streaming

---

## 🧠 How it works

* Video split into chunks
* Quality changes based on network

---

## 🧠 Example

* Netflix adjusts quality

---

## 🎯 Difference

| Feature  | WebRTC       | HTTP-DASH    |
| -------- | ------------ | ------------ |
| Use case | Video calls  | Streaming    |
| Latency  | Very low     | Higher       |
| Delivery | Peer-to-peer | Server-based |

---

# 🧠 Final Big Picture

```id="6y7vfi"
User → ISP → DNS → Routing (IP) → Transport (TCP/UDP) → Protocol (HTTP/WebSocket) → Application
```

---

# 🔥 Summary

👉
**“Networking is layered: physical transmission, routing via IP, and communication via protocols like TCP/HTTP. Different protocols and standards are chosen based on trade-offs between reliability, latency, and scalability.”**

---

# 🔷 1. Primary–Replica Architecture (Master–Slave)

## 👉 What it is

A database setup where:

* One node handles **writes (Primary)**
* Others handle **reads (Replicas)**

---

## 🧠 Architecture

```text
         Writes
Client ───────► Primary DB
                  │
                  ▼
          Replication (logs)
           /      |      \
     Replica   Replica   Replica
       (read)    (read)    (read)
```

---

## 🔑 How it works

1. Write goes to **Primary**
2. Primary logs change
3. Replicas copy those changes

---

## 🔥 Types of Replication

### 🔹 Synchronous

* Write completes **only after replicas updated**
* Strong consistency
* Slower

---

### 🔹 Asynchronous

* Primary returns immediately
* Replicas updated later

👉 May cause:

> **Replication lag**

---

## ✅ Advantages

* Read scalability
* Fault tolerance

---

## ❌ Problems

* Replication lag → stale reads
* Failover complexity

---

## 🎯 Real Use

* MySQL replication
* PostgreSQL streaming replication

---

# 🔷 2. WAL (Write-Ahead Logging) & CDC (Change Data Capture)

---

# 🔹 WAL (Write-Ahead Logging)

## 👉 Idea

> **Write changes to log BEFORE writing to database**

---

## 🧠 Flow

```text
1. Write request
2. Write to WAL (log)
3. Apply to DB
```

---

## 🔥 Why important?

### ✅ Crash Recovery

* If DB crashes → replay WAL

### ✅ Replication

* Replicas read WAL and apply changes

---

## 🎯 Used in:

* PostgreSQL
* MySQL

---

# 🔹 CDC (Change Data Capture)

## 👉 Definition

> Capturing **every change in DB** and streaming it elsewhere

---

## 🧠 Example

* Insert/update/delete captured
* Sent to:

  * Kafka
  * Analytics system
  * Cache

---

## 🔥 How it works

* Reads from WAL / binlog

---

## 🎯 Tools

* Debezium

---

## 🧠 Use Cases

* Event-driven systems
* Data pipelines
* Real-time analytics

---

# 🔷 3. Write Amplification & Split Brain

---

# 🔹 Write Amplification

## 👉 Definition

> One logical write causes **multiple physical writes**

---

## 🧠 Example

You update 1 row → DB does:

* WAL write
* Index update
* Data page update
* Replication writes

👉 1 write → many operations

---

## ❗ Problem

* Increased disk I/O
* Performance impact

---

## 🎯 Seen in

* LSM-based DBs (like Cassandra)
* Heavy indexing systems

---

# 🔹 Split Brain (VERY IMPORTANT)

## 👉 Definition

> Two nodes think they are **primary at same time**

---

## 🧠 Example

Network partition:

```text
Cluster split into 2 parts

Node A → thinks primary  
Node B → also thinks primary ❌
```

---

## ❗ Result

* Conflicting writes
* Data corruption

---

## 🔥 Prevention

* Leader election (ZooKeeper, etcd)
* Quorum-based systems

---

## 🎯 Real systems

* Apache Kafka (controller election)
* ZooKeeper

---

# 🔷 4. Database Migration Steps

This is **very practical for your backend job**.

---

## 🧠 Scenario

Move from:

* Old DB → New DB
* Or schema change

---

## 🔥 Safe Migration Steps

---

## 🔹 Step 1: Prepare Schema

* Create new tables/columns
* Keep old system working

---

## 🔹 Step 2: Dual Write

```text
Application writes to:
→ Old DB
→ New DB
```

---

## 🔹 Step 3: Backfill Data

* Copy old data → new DB
* Done in batches

---

## 🔹 Step 4: Verify Data

* Compare counts
* Check consistency

---

## 🔹 Step 5: Switch Reads

```text
Old → New DB (gradual rollout)
```

---

## 🔹 Step 6: Stop Old Writes

* Disable old DB writes

---

## 🔹 Step 7: Cleanup

* Remove old DB

---

## 🔥 Important Concepts

### ✅ Idempotency

* Retry-safe operations

### ✅ Feature Flags

* Control rollout

---

# 🔷 5. Migration Across Regions (Geo Migration)

---

## 👉 Why?

* Move closer to users
* Disaster recovery
* Compliance

---

## 🔥 Challenges

* Latency
* Data consistency
* Large data transfer

---

## 🧠 Approaches

---

# 🔹 1. Snapshot + Sync

1. Take DB snapshot
2. Restore in new region
3. Sync changes

---

# 🔹 2. Continuous Replication

* Old region → new region replication
* Once synced → switch traffic

---

# 🔹 3. Blue-Green Deployment

```text
Blue (old region)
Green (new region)
```

* Run both
* Gradually shift traffic

---

# 🔹 4. Active-Active (Advanced)

* Both regions accept writes
* Needs conflict resolution

---

## ❗ Problems

### 🔥 Replication Lag

* Users may see stale data

### 🔥 Conflict Resolution

* Same record updated in 2 regions

---

## 🎯 Real Systems

* Amazon multi-region DB
* Google Spanner

---

# 🧠 Final Mental Model

### 🔹 Replication

> “Keep multiple copies of data in sync”

### 🔹 WAL

> “Log first, then apply changes”

### 🔹 CDC

> “Stream database changes as events”

### 🔹 Migration

> “Move data safely without downtime”

---

# 🔥 One-Liners

### Primary-Replica:

> “Writes go to primary, reads scale via replicas.”

### WAL:

> “Ensures durability and enables replication.”

### CDC:

> “Turns DB changes into event streams.”

### Split Brain:

> “Multiple leaders causing conflicting writes.”

### Migration:

> “Done via dual writes, backfill, and gradual cutover.”

---

# 🔷 1. Authentication (Who are you?)

Authentication answers:

> **“Is this user/service really who they claim to be?”**

---

## 🔹 SAML-based SSO (Single Sign-On)

## 👉 What it is

SAML lets users **log in once** and access multiple systems.

---

## 🧠 Flow

```text
User → App → Redirect to Identity Provider (IdP)
     → Login once → IdP sends SAML assertion → App trusts it
```

---

## 🔑 Components

* Identity Provider (IdP) → e.g. Okta
* Service Provider (SP) → your application

---

## 🎯 Example

Login to company portal → access Jira, Slack without re-login

---

## ✅ Pros

* Centralized authentication
* Enterprise-friendly

---

## ❌ Cons

* XML-based → heavy & complex

---

---

## 🔹 User Tokens (Session / JWT)

## 👉 What it is

After login, server gives a **token** → user sends it with every request

---

## 🧠 Example (JWT)

```text
Header.Payload.Signature
```

---

## 🔑 Flow

```text
Login → Server issues token → Client stores → Sends in API calls
```

---

## 🎯 Used in

* REST APIs
* Microservices

---

## ❗ Important

* Tokens can expire
* Must be signed (to prevent tampering)

---

---

## 🔹 OAuth (Authorization, often used for Authentication)

## 👉 What it is

OAuth allows:

> **One app to access another app’s data (without sharing password)**

---

## 🧠 Example

“Login with Google”

* Google OAuth 2.0

---

## 🔑 Flow

```text
User → App → Google → Consent → Token → App
```

---

## ⚠️ Important Concept

OAuth is for **authorization**, but often used for login (authentication)

👉 That’s why:

> “OAuth abused for authentication”

---

## ✅ Pros

* Secure delegation
* No password sharing

---

---

# 🔷 2. Authorization (What can you do?)

Authorization answers:

> **“What actions is this user allowed to perform?”**

---

## 🔹 Access Control Lists (ACL)

## 👉 What it is

List of permissions per resource

---

## 🧠 Example

```text
File:
  user1 → read
  user2 → read/write
```

---

## ✅ Pros

* Simple
* Easy to implement

---

## ❌ Cons

* Hard to scale for large systems

---

---

## 🔹 Rule Engines

## 👉 What it is

Dynamic authorization using rules

---

## 🧠 Example

```text
IF user.role = "admin" AND time < 6PM
THEN allow access
```

---

## 🎯 Used in

* Enterprise systems
* Banking

---

---

## 🔹 Secret Keys

## 👉 What it is

Used for:

* API authentication
* Service-to-service communication

---

## 🧠 Example

```text
API Key: abc123
```

---

## ❗ Problem

* If leaked → full access

---

## 🔥 Better Approach

* Rotate keys
* Use short-lived tokens

---

---

# 🔷 3. Attack Vectors (Where attacks come from)

---

## 🔹 Hackers (External Threats)

## 🧠 Examples

* SQL Injection
* DDoS
* Credential stuffing

---

---

## 🔹 Developers (Internal Mistakes)

## 🧠 Examples

* Hardcoding secrets
* Exposing APIs
* Poor validation

---

---

## 🔹 Malicious Code

## 🧠 Examples

* Third-party libraries
* Supply chain attacks

---

## 🎯 Example Incident

* Log4j exploit

---

---

# 🔷 4. Protecting Videos in CDNs

Used by Netflix, Hotstar, etc.

---

# 🔹 1. Token-Based Authentication

## 👉 Idea

Each video request needs a **valid token**

---

## 🧠 Flow

```text
User → Backend → Token generated → CDN validates token
```

---

## 🔑 Features

* Expiry time
* Signed URL

---

---

# 🔹 2. Domain-Based Authentication

## 👉 Idea

Only requests from allowed domains are served

---

## 🧠 Example

* Video works only on `example.com`
* Not on copied link

---

---

# 🔹 3. Server-Side Authentication

## 👉 Idea

CDN checks with backend before serving content

---

## 🧠 Flow

```text
CDN → Backend → Validate user → Allow/Deny
```

---

---

# 🔹 4. DRM (Digital Rights Management)

## 👉 What it is

Protects content from piracy

---

## 🧠 Example

* Encrypted video
* Only authorized player can decrypt

---

## 🎯 Systems

* Widevine
* FairPlay

---

## 🔑 Features

* Prevent download
* Device restrictions
* Screen recording protection (partial)

---

---

# 🧠 Final Big Picture

```text
User → Authentication → Token → Authorization → Access Resource
```

---

# 🔥 Summary

### Authentication:

> “Verifies identity using SAML, tokens, or OAuth.”

### Authorization:

> “Controls access using ACLs, rules, or keys.”

### Attack Vectors:

> “Threats can come from attackers, internal mistakes, or malicious code.”

### CDN Protection:

> “Uses tokens, domain checks, server validation, and DRM.”

---

# Observability in distributed systems



---

# Distributed Consensus with paxos


---




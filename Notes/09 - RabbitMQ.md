# RabbitMQ — Comprehensive Interview Preparation Guide

> **How to use this guide:** Read top-to-bottom for fundamentals, jump to sections for revision, and drill the **Cheat Sheet** + **Scenario Questions** before interviews.

---

## Table of Contents

1. [What is RabbitMQ?](#1-what-is-rabbitmq)
2. [Why RabbitMQ?](#2-why-rabbitmq)
3. [Core Concepts — Queue, Exchange, Bindings, Routing Key](#3-core-concepts--queue-exchange-bindings-routing-key)
4. [Exchange Types](#4-exchange-types)
5. [Producer & Consumer](#5-producer--consumer)
6. [Message Acknowledgement](#6-message-acknowledgement)
7. [Prefetch](#7-prefetch)
8. [Durability & Persistence](#8-durability--persistence)
9. [Dead Letter Queue (DLQ)](#9-dead-letter-queue-dlq)
10. [Retry Mechanism](#10-retry-mechanism)
11. [Delayed Queue](#11-delayed-queue)
12. [Priority Queue](#12-priority-queue)
13. [Ordering](#13-ordering)
14. [Scaling](#14-scaling)
15. [Clustering](#15-clustering)
16. [High Availability](#16-high-availability)
17. [RabbitMQ vs Kafka](#17-rabbitmq-vs-kafka)
18. [RabbitMQ vs BullMQ](#18-rabbitmq-vs-bullmq)
19. [Production Architecture](#19-production-architecture)
20. [Common Failures](#20-common-failures)
21. [Performance](#21-performance)
22. [Monitoring](#22-monitoring)
23. [Best Practices](#23-best-practices)
24. [Scenario Questions](#24-scenario-questions)
25. [Cheat Sheet](#25-cheat-sheet)

---

## 1. What is RabbitMQ?

### Q: What is RabbitMQ?

**A:** RabbitMQ is an open-source **message broker** that implements the **AMQP 0-9-1** protocol (and also supports STOMP, MQTT). It receives messages from **producers**, routes them through **exchanges** to **queues**, and delivers them to **consumers**. It decouples services, buffers load, and enables asynchronous communication.

```
Producer → Exchange → (Bindings) → Queue → Consumer
```

### Q: What protocol does RabbitMQ use?

**A:** Primarily **AMQP** (Advanced Message Queuing Protocol). AMQP defines wire-level framing, exchanges, queues, bindings, and delivery guarantees. RabbitMQ also supports MQTT (IoT) and STOMP (simple text protocol).

### Q: Is RabbitMQ a queue or a broker?

**A:** It is a **broker** — a middleware that manages many queues, routing logic, and delivery semantics. The queue is one component inside the broker.

---

## 2. Why RabbitMQ?

### Q: Why use a message broker like RabbitMQ?

**A:**

| Problem | How RabbitMQ Helps |
|---------|-------------------|
| Tight coupling | Services communicate via messages, not direct HTTP calls |
| Traffic spikes | Queues buffer messages; consumers process at their own pace |
| Slow downstream | Producer doesn't block waiting for slow consumers |
| Fan-out notifications | One event → many consumers via exchanges |
| Reliability | Persistence, acknowledgements, retries, DLQ |
| Microservices | Async integration, event-driven architecture |

### Q: When should you NOT use RabbitMQ?

**A:**

- **Massive event streaming / replay** → Kafka is better (log-based, retention).
- **Simple in-process job queue** in a single Node.js app → BullMQ/Redis may be simpler.
- **Hard real-time, sub-millisecond latency** → direct calls or in-memory channels.
- **Long-term event store** → RabbitMQ deletes messages after ack; not a database.

### Q: What are common use cases?

**A:** Order processing, email/SMS dispatch, image resizing pipelines, payment webhooks, audit logging, microservice integration, RPC over queues, background job processing.

---

## 3. Core Concepts — Queue, Exchange, Bindings, Routing Key

### Q: What is a Queue?

**A:** A **queue** is a buffer that stores messages until a consumer retrieves them. Messages are stored in **FIFO** order (with exceptions for priority queues). Queues are named; consumers subscribe to queue names.

```javascript
// Node.js (amqplib) — declare a durable queue
await channel.assertQueue('order.created', { durable: true });
```

### Q: What is an Exchange?

**A:** An **exchange** receives messages from producers and **routes** them to one or more queues based on exchange type, bindings, and routing keys. Producers publish to exchanges, **not directly to queues**.

```javascript
await channel.assertExchange('orders', 'topic', { durable: true });
channel.publish('orders', 'order.created.us', Buffer.from(JSON.stringify(payload)));
```

### Q: What is a Binding?

**A:** A **binding** is a link between an exchange and a queue, optionally with a **binding key** (routing pattern). It tells the exchange: "send messages matching this key/pattern to this queue."

```javascript
await channel.bindQueue('email-queue', 'orders', 'order.created.*');
```

### Q: What is a Routing Key?

**A:** A **routing key** is a string the producer attaches to each message. The exchange compares it against binding keys to decide which queue(s) receive the message.

```
Producer publishes with routing key: "order.created.us"
Binding on email-queue:              "order.created.*"  → MATCH
Binding on sms-queue:                "order.shipped.*"  → NO MATCH
```

### Q: What is the default exchange?

**A:** The **default exchange** (`""`) is a direct exchange where routing key = queue name. Publishing to `""` with routing key `my-queue` delivers directly to queue `my-queue`. Useful for simple point-to-point messaging.

### Q: What is a Virtual Host (vhost)?

**A:** A **vhost** is a logical namespace inside RabbitMQ — like a database in PostgreSQL. Exchanges, queues, and permissions are isolated per vhost. Production typically uses separate vhosts per environment (`/prod`, `/staging`).

### Q: What are important message properties?

**A:**

| Property | Purpose | Example |
|----------|---------|---------|
| `deliveryMode` | `1` = transient, `2` = persistent | Survive broker restart |
| `contentType` | Body format | `application/json` |
| `correlationId` | Link request/reply (RPC) | UUID |
| `replyTo` | Queue for RPC response | `amq.gen-xxx` |
| `messageId` | Unique ID for deduplication | UUID |
| `timestamp` | When published | Unix epoch |
| `expiration` | Per-message TTL (ms, as string) | `"30000"` |
| `priority` | 0–255 (needs `x-max-priority` queue) | `9` |
| `headers` | Custom metadata | `{ "x-retry-count": 2 }` |

```javascript
channel.publish('orders', 'order.created', Buffer.from(JSON.stringify(data)), {
  persistent: true,
  contentType: 'application/json',
  messageId: uuid(),
  timestamp: Date.now(),
  headers: { 'x-schema-version': '2' }
});
```

### Q: What is the difference between Connection and Channel?

**A:** A **connection** is a TCP link to the broker (expensive — reuse one per process). A **channel** is a virtual connection multiplexed inside it (cheap — create per thread/task). Channels are **not thread-safe**; share connections, not channels across threads.

---

## 4. Exchange Types

### Q: What are the four main exchange types?

**A:**

| Type | Routing Logic | Use Case |
|------|--------------|----------|
| **Direct** | Exact routing key match | Task distribution, routing by type |
| **Topic** | Pattern match (`*`, `#`) | Multi-tenant, geo-routing, event categories |
| **Fanout** | Ignores routing key; all bound queues | Broadcast, notifications |
| **Headers** | Match on message headers (not routing key) | Complex routing by metadata |

---

### Q: How does a Direct Exchange work?

**A:** Routes a message to queues whose **binding key exactly matches** the message routing key.

```
Exchange: "tasks" (direct)

Binding: tasks-queue  ← binding key "email"
Binding: sms-queue    ← binding key "sms"

Publish routing key "email" → only tasks-queue receives it
```

```javascript
await channel.assertExchange('tasks', 'direct', { durable: true });
await channel.bindQueue('email-workers', 'tasks', 'email');
channel.publish('tasks', 'email', Buffer.from('Send welcome email'));
```

---

### Q: How does a Topic Exchange work?

**A:** Routes using **pattern matching** on routing keys (dot-separated words).

| Wildcard | Meaning |
|----------|---------|
| `*` | Exactly one word |
| `#` | Zero or more words |

```
Routing key: "order.created.us"
Pattern "order.*.us"     → MATCH
Pattern "order.created.#" → MATCH
Pattern "order.*.eu"     → NO MATCH
```

```javascript
await channel.assertExchange('events', 'topic', { durable: true });
await channel.bindQueue('us-orders', 'events', 'order.*.us');
await channel.bindQueue('all-orders', 'events', 'order.#');
```

---

### Q: How does a Fanout Exchange work?

**A:** **Broadcasts** every message to **all** bound queues, ignoring routing key entirely.

```
Exchange: "notifications" (fanout)
  → email-queue
  → sms-queue
  → push-queue

One publish → all three queues get the message
```

```javascript
await channel.assertExchange('notifications', 'fanout', { durable: true });
await channel.bindQueue('email-queue', 'notifications', ''); // routing key ignored
```

---

### Q: How does a Headers Exchange work?

**A:** Routes based on **message headers** instead of routing key. Bindings specify header key-value pairs with `x-match: all` (all must match) or `x-match: any` (any must match).

```javascript
await channel.assertExchange('headers-ex', 'headers', { durable: true });
await channel.bindQueue('pdf-queue', 'headers-ex', '', {
  'x-match': 'all',
  'format': 'pdf',
  'lang': 'en'
});

channel.publish('headers-ex', '', Buffer.from(data), {
  headers: { format: 'pdf', lang: 'en' }
});
```

---

## 5. Producer & Consumer

### Q: What is a Producer?

**A:** A **producer** (publisher) sends messages to an exchange. It does not know which queues (or how many consumers) will receive the message.

```javascript
const amqp = require('amqplib');
const conn = await amqp.connect('amqp://localhost');
const channel = await conn.createChannel();

await channel.assertExchange('orders', 'topic', { durable: true });
channel.publish(
  'orders',
  'order.created',
  Buffer.from(JSON.stringify({ orderId: 42, amount: 99.99 })),
  { persistent: true, contentType: 'application/json' }
);
```

### Q: What is a Consumer?

**A:** A **consumer** subscribes to a queue and processes messages. It can use **push** (`consume`) or **pull** (`get`) delivery.

```javascript
await channel.assertQueue('order.created', { durable: true });
channel.consume('order.created', async (msg) => {
  const order = JSON.parse(msg.content.toString());
  await processOrder(order);
  channel.ack(msg); // acknowledge successful processing
}, { noAck: false });
```

### Q: What is Publisher Confirms?

**A:** **Publisher confirms** let the producer know the broker has accepted (and optionally persisted) a message. Without confirms, `publish()` returns immediately and you don't know if the broker received it.

```javascript
await channel.confirmSelect();
channel.publish('orders', 'order.created', Buffer.from('data'));
await channel.waitForConfirms(); // blocks until broker acks
```

### Q: What is RPC over RabbitMQ?

**A:** Request-reply pattern: client publishes to a queue with `replyTo` queue and `correlationId`; server processes and publishes response to `replyTo` with same `correlationId`.

```javascript
// Client
const { queue: replyQueue } = await channel.assertQueue('', { exclusive: true });
const correlationId = uuid();

channel.consume(replyQueue, (msg) => {
  if (msg.properties.correlationId === correlationId) {
    console.log('Response:', msg.content.toString());
  }
}, { noAck: true });

channel.sendToQueue('rpc_queue', Buffer.from('4'), {
  replyTo: replyQueue,
  correlationId
});
```

---

## 6. Message Acknowledgement

### Q: What is message acknowledgement?

**A:** **Acknowledgement (ack)** tells RabbitMQ the consumer has successfully processed a message. Until acked, the message stays **unacknowledged** on the consumer. If the consumer disconnects before acking, RabbitMQ **redelivers** the message.

| Mode | Behavior |
|------|----------|
| **Manual ack** (`noAck: false`) | Consumer must call `ack`, `nack`, or `reject` |
| **Auto ack** (`noAck: true`) | Message removed as soon as delivered — **at-most-once** |

### Q: What is the difference between ack, nack, and reject?

**A:**

| Method | Meaning | Requeue? |
|--------|---------|----------|
| `ack(msg)` | Success — remove from queue | N/A |
| `nack(msg, false, true)` | Failed — requeue for retry | Yes |
| `nack(msg, false, false)` | Failed — discard or route to DLQ | No |
| `reject(msg, true)` | Single message nack with requeue | Yes/No |

```javascript
channel.consume('tasks', async (msg) => {
  try {
    await doWork(msg);
    channel.ack(msg);
  } catch (err) {
    channel.nack(msg, false, false); // don't requeue → goes to DLQ if configured
  }
}, { noAck: false });
```

### Q: What delivery guarantees does RabbitMQ provide?

**A:**

| Guarantee | How |
|-----------|-----|
| **At-most-once** | Auto-ack; message may be lost if consumer crashes mid-process |
| **At-least-once** | Manual ack + durable queue + persistent messages (most common) |
| **Exactly-once** | **Not native** — requires idempotent consumers + deduplication |

---

## 7. Prefetch

### Q: What is prefetch (QoS)?

**A:** **Prefetch** (`basic.qos`) limits how many **unacknowledged** messages a consumer can hold at once. Prevents one slow consumer from hoarding all messages and enables **fair dispatch** across multiple consumers.

```javascript
await channel.prefetch(10); // max 10 unacked messages per consumer
channel.consume('tasks', processMessage, { noAck: false });
```

### Q: What is the difference between prefetch count and prefetch size?

**A:**

- **Prefetch count** — max number of unacked messages (most common).
- **Prefetch size** — max total body size in bytes of unacked messages (rarely used).
- **Global prefetch** — limit applies across all consumers on the channel (usually `false` = per-consumer).

### Q: How do you choose prefetch value?

**A:**

| Workload | Prefetch | Reason |
|----------|----------|--------|
| Fast, uniform tasks | 10–50 | Keep consumers busy |
| Slow, variable tasks | 1–5 | Avoid hoarding; fair distribution |
| Long-running jobs | 1 | One job at a time per consumer |
| Memory-sensitive | Low | Limit in-flight message memory |

---

## 8. Durability & Persistence

### Q: What is a durable queue?

**A:** A **durable queue** survives broker restart. The queue **definition** is stored on disk. Non-durable queues are deleted on restart.

```javascript
await channel.assertQueue('orders', { durable: true });
```

### Q: What is a persistent message?

**A:** A **persistent** message (`deliveryMode: 2`) is written to disk. Combined with durable queues, messages survive broker restart.

```javascript
channel.publish('orders', 'key', Buffer.from('data'), { persistent: true });
```

### Q: Does durable + persistent guarantee no message loss?

**A:** **Not fully.** You also need:

1. **Publisher confirms** — broker accepted the message.
2. **Manual consumer ack** — only ack after successful processing.
3. **Clustered / HA setup** — survive node failure.
4. **Mirrored or quorum queues** — replicate across nodes.

Without all of these, you can still lose messages on crash between publish and persist, or during replication lag.

### Q: Durable exchange vs durable queue?

**A:** A **durable exchange** survives restart (exchange definition). Messages still need persistent flag and a durable bound queue to survive.

---

## 9. Dead Letter Queue (DLQ)

### Q: What is a Dead Letter Queue?

**A:** A **DLQ** receives messages that cannot be processed normally — rejected without requeue, TTL expired, or queue length exceeded. Used for inspection, alerting, and manual replay.

### Q: What causes a message to be dead-lettered?

**A:**

| Reason | Header |
|--------|--------|
| Consumer `reject`/`nack` with `requeue=false` | — |
| Message TTL expired in queue | — |
| Queue max-length exceeded | — |
| Message rejected by **quorum queue** delivery limit | — |

### Q: How do you configure a DLQ?

**A:** Set `x-dead-letter-exchange` and optionally `x-dead-letter-routing-key` on the main queue.

```javascript
// DLQ setup
await channel.assertExchange('dlx', 'direct', { durable: true });
await channel.assertQueue('orders.dlq', { durable: true });
await channel.bindQueue('orders.dlq', 'dlx', 'orders.failed');

// Main queue with DLQ
await channel.assertQueue('orders', {
  durable: true,
  arguments: {
    'x-dead-letter-exchange': 'dlx',
    'x-dead-letter-routing-key': 'orders.failed'
  }
});
```

### Q: What is the difference between DLQ and retry queue?

**A:** A **DLQ** is for messages that **failed permanently** (or exhausted retries). A **retry queue** temporarily holds messages before re-routing to the main queue (via TTL + DLX). DLQ = parking lot; retry queue = waiting room.

---

## 10. Retry Mechanism

### Q: How do you implement retries in RabbitMQ?

**A:** Common patterns:

**1. Requeue with caution** (can cause infinite loops):
```javascript
channel.nack(msg, false, true); // requeue=true
```

**2. Retry queue with TTL (recommended):**
```
main-queue → (fail) → retry-queue (TTL 30s) → DLX → main-queue
After N retries → DLQ
```

```javascript
// Retry queue: messages expire after 30s, dead-letter back to main
await channel.assertQueue('orders.retry', {
  durable: true,
  arguments: {
    'x-message-ttl': 30000,
    'x-dead-letter-exchange': '',
    'x-dead-letter-routing-key': 'orders'
  }
});
```

**3. Track retry count in headers:**
```javascript
const retries = (msg.properties.headers['x-retry-count'] || 0) + 1;
if (retries > 3) {
  channel.nack(msg, false, false); // → DLQ
} else {
  channel.publish('retry-ex', 'retry', msg.content, {
    headers: { 'x-retry-count': retries }
  });
  channel.ack(msg);
}
```

**4. Use delayed message plugin** for exponential backoff.

### Q: Why not just requeue infinitely?

**A:** Infinite requeue causes **poison messages** to block consumers in a tight loop, wasting CPU and preventing other messages from being processed. Always cap retries and route to DLQ.

---

## 11. Delayed Queue

### Q: How do you delay message delivery in RabbitMQ?

**A:**

| Method | How |
|--------|-----|
| **Per-message TTL** | `expiration` property (ms as string) |
| **Per-queue TTL** | `x-message-ttl` on queue |
| **TTL + DLX** | Message sits in delay queue until TTL, then dead-letters to target |
| **Delayed Message Plugin** | `x-delay` header (ms) — most flexible |

**TTL + DLX pattern:**
```javascript
// delay-queue: TTL 60s, then route to work-queue
await channel.assertQueue('delay.60s', {
  arguments: {
    'x-message-ttl': 60000,
    'x-dead-letter-exchange': '',
    'x-dead-letter-routing-key': 'work-queue'
  }
});
channel.sendToQueue('delay.60s', Buffer.from('process later'));
```

**Delayed Message Plugin:**
```javascript
await channel.assertExchange('delayed', 'x-delayed-message', {
  arguments: { 'x-delayed-type': 'direct' }
});
channel.publish('delayed', 'routing-key', Buffer.from('data'), {
  headers: { 'x-delay': 60000 } // 60 seconds
});
```

### Q: What is the difference between queue TTL and message TTL?

**A:**

- **Queue TTL** (`x-message-ttl` on queue) — applies to **all** messages in that queue.
- **Message TTL** (`expiration` property) — per-message; can vary. Expired messages are dead-lettered or dropped.

---

## 12. Priority Queue

### Q: How do priority queues work?

**A:** Set `x-max-priority` on the queue (1–255). Messages with higher `priority` property are delivered first. Lower priority messages wait until higher ones are consumed.

```javascript
await channel.assertQueue('tasks', {
  durable: true,
  arguments: { 'x-max-priority': 10 }
});

channel.sendToQueue('tasks', Buffer.from('urgent'), { priority: 9 });
channel.sendToQueue('tasks', Buffer.from('normal'), { priority: 5 });
// 'urgent' delivered first
```

### Q: What are the limitations of priority queues?

**A:**

- Only works when **consumers are idle** — if consumer is already processing, priority doesn't preempt.
- Messages already in the queue are re-sorted on publish (small overhead).
- Not suitable for strict real-time preemption — use separate high-priority queues instead for critical paths.

---

## 13. Ordering

### Q: Does RabbitMQ guarantee message ordering?

**A:** **Per queue, single consumer** — yes, FIFO (excluding priority). **Multiple consumers** on the same queue — **no strict ordering**; messages are dispatched round-robin to available consumers.

### Q: How do you preserve order when scaling consumers?

**A:**

| Strategy | How |
|----------|-----|
| **Single consumer** | Simplest; limits throughput |
| **Partition by key** | Route `user-123` always to same queue via consistent-hash exchange |
| **Sharding** | Multiple queues, each with one consumer; hash entity ID to queue |
| **Sequence numbers** | Consumer re-orders (complex, rarely needed) |

```javascript
// Consistent hash exchange — same routing key → same queue
await channel.assertExchange('orders', 'x-consistent-hash', { durable: true });
await channel.bindQueue('shard-0', 'orders', '1');
await channel.bindQueue('shard-1', 'orders', '1');
// routing key = hash(userId) → always same shard
```

### Q: Can reordering happen on redelivery?

**A:** Yes. A failed message requeued or redelivered may be processed **after** newer messages. Design consumers to be **idempotent** and tolerate out-of-order delivery.

---

## 14. Scaling

### Q: How do you scale RabbitMQ consumers?

**A:**

1. **Add more consumers** to the same queue — RabbitMQ round-robins messages (competing consumers pattern).
2. **Increase prefetch** to keep consumers busy.
3. **Shard queues** — partition work across multiple queues for higher parallelism.
4. **Separate queues per workload** — don't mix fast and slow tasks in one queue.

```
                    ┌─ Consumer 1
Queue "tasks" ──────┼─ Consumer 2
                    └─ Consumer 3
```

### Q: How do you scale RabbitMQ brokers?

**A:**

- **Vertical scaling** — more CPU/RAM/disk IOPS on the node.
- **Clustering** — multiple nodes share metadata; queues live on one node (classic) or replicated (quorum).
- **Federation / Shovel** — connect brokers across regions.
- **Separate brokers per domain** — orders broker, notifications broker.

### Q: What is the competing consumers pattern?

**A:** Multiple consumers subscribe to the **same queue**. Each message is delivered to **only one** consumer. This horizontally scales processing throughput.

---

## 15. Clustering

### Q: What is a RabbitMQ cluster?

**A:** Multiple RabbitMQ nodes share metadata (users, vhosts, exchanges, bindings) via **Erlang distribution**. Clients can connect to any node; connections and queues may live on specific nodes.

### Q: How are queues stored in a cluster?

**A:**

| Queue Type | Storage |
|------------|---------|
| **Classic queue** | Lives on **one node** (the "home" node); mirrors optional (deprecated) |
| **Quorum queue** | **Replicated** across multiple nodes using Raft consensus |
| **Stream queue** | Replicated log (Kafka-like) |

### Q: What is Erlang cookie?

**A:** A shared secret nodes use to authenticate each other when forming a cluster. All nodes must have the same `.erlang.cookie` value.

### Q: What happens when a cluster node dies?

**A:** Depends on queue type:

- **Classic, no mirror** — queues on that node are **unavailable** until node returns.
- **Quorum queue** — survives if majority of replicas alive; automatic leader election.
- **Connections** to dead node — clients must reconnect to another node.

---

## 16. High Availability

### Q: How do you achieve HA in RabbitMQ?

**A:**

| Approach | Description |
|----------|-------------|
| **Quorum queues** | Recommended; Raft-based replication, strong consistency |
| **Classic mirrored queues** | **Deprecated** in RabbitMQ 3.13+; use quorum instead |
| **Load balancer** | HAProxy/ALB in front of cluster nodes |
| **Multi-AZ deployment** | Nodes across availability zones |
| **Federation** | Bridge brokers across DCs for disaster recovery |

```javascript
// Declare a quorum queue (HA)
await channel.assertQueue('orders', {
  durable: true,
  arguments: { 'x-queue-type': 'quorum' }
});
```

### Q: What is the minimum cluster size for quorum queues?

**A:** **3 nodes** recommended (tolerates 1 failure). Quorum requires **majority** of replicas for writes. 2-node cluster tolerates 0 failures for writes during partition.

### Q: What is split-brain and how does quorum handle it?

**A:** **Split-brain** — network partition causes two subsets of nodes to think they're primary. Quorum queues use **Raft consensus** — only the majority partition accepts writes; minority partition refuses writes, preventing duplicate processing.

### Q: What is Single Active Consumer (SAC)?

**A:** `x-single-active-consumer: true` ensures **only one consumer** is active on a queue at a time; others are standby. On active consumer failure, RabbitMQ promotes a standby. Useful for ordered processing with HA failover without multiple parallel consumers.

```javascript
await channel.assertQueue('ordered-tasks', {
  durable: true,
  arguments: {
    'x-queue-type': 'quorum',
    'x-single-active-consumer': true
  }
});
```

### Q: What are Federation and Shovel plugins?

**A:**

| Plugin | Direction | Use Case |
|--------|-----------|----------|
| **Federation** | Upstream → downstream (exchange/queue links) | Geo-distribution, cross-DC fan-out |
| **Shovel** | Pulls messages from source, pushes to destination | Migration, bridge between brokers/vhosts |

```
DC-East broker ──federation──► DC-West broker
Legacy broker ──shovel──► New cluster (migration)
```

### Q: What are Stream queues?

**A:** **Streams** are an append-only log (Kafka-like) in RabbitMQ — messages retained by size/time, consumers track offset, supports replay. Use when you need log semantics inside RabbitMQ; otherwise prefer classic/quorum queues for task processing.

---

## 17. RabbitMQ vs Kafka

### Q: RabbitMQ vs Kafka — key differences?

**A:**

| Aspect | RabbitMQ | Kafka |
|--------|----------|-------|
| **Model** | Message broker (smart broker, dumb consumer) | Distributed commit log (dumb broker, smart consumer) |
| **Message lifecycle** | Deleted after ack | Retained by time/size policy |
| **Replay** | No native replay | Consumers rewind to any offset |
| **Throughput** | Thousands–tens of thousands/sec per node | Millions/sec per cluster |
| **Ordering** | Per queue | Per partition |
| **Routing** | Flexible exchanges (direct, topic, fanout) | Topic + partition key |
| **Protocol** | AMQP, MQTT, STOMP | Custom binary protocol |
| **Use case** | Task queues, RPC, integration | Event streaming, analytics, CDC |
| **Consumer model** | Push (broker delivers) | Pull (consumer polls) |

### Q: When would you choose RabbitMQ over Kafka?

**A:**

- Complex routing (fanout, topic patterns, headers).
- Task/job queues with competing consumers.
- Request-reply (RPC) patterns.
- Lower operational overhead for moderate throughput.
- Messages should be removed after processing.

### Q: When would you choose Kafka over RabbitMQ?

**A:**

- Event sourcing, audit logs, replay.
- Very high throughput (millions of events/sec).
- Stream processing (Kafka Streams, Flink).
- Multiple independent consumer groups reading same data.
- Long retention (days/weeks/months).

---

## 18. RabbitMQ vs BullMQ

### Q: RabbitMQ vs BullMQ — key differences?

**A:**

| Aspect | RabbitMQ | BullMQ |
|--------|----------|--------|
| **Backend** | RabbitMQ server (Erlang) | Redis |
| **Language** | Polyglot (any AMQP client) | Node.js / TypeScript (primary) |
| **Deployment** | Separate broker service | Requires Redis |
| **Features** | Exchanges, routing, DLQ, clustering | Jobs, delays, retries, rate limiting, UI (Bull Board) |
| **Persistence** | Disk-based, quorum replication | Redis AOF/RDB (less durable by default) |
| **Throughput** | High (with tuning) | Very high for simple jobs (Redis in-memory) |
| **Complexity** | Higher ops overhead | Simpler for Node.js apps |
| **Multi-service** | Excellent (language-agnostic) | Best within Node.js ecosystem |

### Q: When to use BullMQ instead of RabbitMQ?

**A:**

- Single Node.js/TypeScript application needing background jobs.
- Already running Redis.
- Need built-in delayed jobs, retries, job progress, and dashboard.
- Don't need cross-language messaging or complex routing.

### Q: When to use RabbitMQ instead of BullMQ?

**A:**

- Polyglot microservices (Java, Python, Go, Node.js).
- Need message routing, fanout, topic exchanges.
- Stronger durability guarantees (quorum queues).
- Enterprise messaging patterns (RPC, federation, shovel).

---

## 19. Production Architecture

### Q: What does a production RabbitMQ architecture look like?

**A:**

```
                    ┌─────────────┐
Producers ─────────►│  HAProxy /  │
                    │  Load Bal.  │
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
         ┌─────────┐ ┌─────────┐ ┌─────────┐
         │ Node 1  │ │ Node 2  │ │ Node 3  │  (3-node cluster)
         │ Quorum  │ │ Quorum  │ │ Quorum  │
         └────┬────┘ └────┬────┘ └────┬────┘
              └────────────┼────────────┘
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
         Consumer A   Consumer B   Consumer C
              │                         │
              └──────── DLQ ◄───────────┘ (failures)
```

**Key components:**

| Component | Purpose |
|-----------|---------|
| Load balancer | Connection distribution, health checks |
| 3-node cluster | Quorum queues, fault tolerance |
| Separate vhosts | `prod`, `staging` isolation |
| DLQ + retry queues | Failure handling |
| Monitoring | Prometheus + Grafana, RabbitMQ Management |
| Alerts | Queue depth, consumer count, disk/memory |

### Q: How do producers and consumers connect in production?

**A:**

- Use **connection pooling** — one connection per process, channels per thread/task.
- Enable **publisher confirms** and **persistent messages**.
- Consumers use **manual ack**, **prefetch**, and **graceful shutdown** (finish in-flight, then close).
- Configure **heartbeats** (default 60s) to detect dead connections.
- Use **TLS** for encryption in transit.

```javascript
const conn = await amqp.connect({
  hostname: 'rabbitmq.internal',
  heartbeat: 30,
  tls: { /* ... */ }
});
// One connection, reuse; create channels as needed
```

---

## 20. Common Failures

### Q: What are common RabbitMQ failures?

**A:**

| Failure | Symptom | Fix |
|---------|---------|-----|
| **Memory alarm** | Publishers blocked cluster-wide | Increase RAM, set TTL/max-length, add consumers, drain queues |
| **Disk alarm** | All connections blocked | Free disk, enable drop-head or TTL, add storage |
| **Poison message** | Consumer loop on bad message | DLQ, retry limit, validate before ack |
| **Queue buildup** | Growing `messages_ready` | Scale consumers, optimize processing, check for stuck consumers |
| **Connection storm** | Too many connections | Connection pooling, limit per service |
| **Split brain** | Inconsistent state (classic mirrors) | Use quorum queues |
| **Unacked pile-up** | Prefetch too high + slow consumer | Lower prefetch, fix slow processing |
| **Channel errors** | `PRECONDITION_FAILED` | Declare queues with same args, handle 404/406 |

### Q: What happens when RabbitMQ hits memory high watermark?

**A:** Default **40% of RAM** triggers memory alarm. Publishers are **blocked** cluster-wide until memory frees. Consumers can still ack (which frees memory). Prevention: queue limits, lazy queues, faster consumers.

### Q: What is a poison message?

**A:** A message that **always fails** processing (bad format, missing reference). Without DLQ/retry limits, it cycles forever via requeue, blocking the queue.

---

## 21. Performance

### Q: How do you optimize RabbitMQ performance?

**A:**

| Area | Optimization |
|------|-------------|
| **Publishers** | Batch publishes, publisher confirms (async), connection reuse |
| **Consumers** | Right-size prefetch, multiple consumers, efficient deserialization |
| **Queues** | Lazy queues for large backlogs, limit queue length |
| **Hardware** | SSD for disk, sufficient RAM, fast network |
| **Messages** | Smaller payloads, compress large bodies, avoid huge headers |
| **Cluster** | Quorum queues for HA (slight write overhead vs classic) |

### Q: What are lazy queues?

**A:** `x-queue-mode: lazy` moves messages to **disk early**, keeping RAM free. Use for **large backlogs** where throughput matters more than latency.

```javascript
await channel.assertQueue('big-backlog', {
  durable: true,
  arguments: { 'x-queue-mode': 'lazy' }
});
```

### Q: How many channels per connection?

**A:** Channels are lightweight multiplexed streams. Use **one connection per process**, **one channel per thread** (channels aren't thread-safe). Hundreds of channels per connection is fine; thousands of connections is not.

---

## 22. Monitoring

### Q: What metrics should you monitor?

**A:**

| Metric | Alert When |
|--------|-----------|
| `queue.messages_ready` | Growing steadily (consumer lag) |
| `queue.messages_unacknowledged` | High for long periods (stuck consumers) |
| `queue.consumers` | Drops to 0 |
| `node.mem_used / mem_limit` | > 80% (memory alarm risk) |
| `node.disk_free` | Below watermark |
| `message_stats.publish_rate` vs `deliver_rate` | Publish >> deliver (falling behind) |
| `connection_count` | Unexpected spikes |
| DLQ depth | Any messages (investigate) |

### Q: What tools are used for monitoring?

**A:**

- **RabbitMQ Management UI** — built-in (port 15672).
- **Prometheus + rabbitmq_exporter** — scrape metrics, Grafana dashboards.
- **Datadog / New Relic** — APM integrations.
- **Alerts** — PagerDuty on queue depth, memory/disk alarms, zero consumers.

### Q: What is the management plugin?

**A:** Built-in HTTP API and web UI for monitoring connections, channels, queues, exchanges, rates, and publishing/consuming messages manually. Enable with `rabbitmq-plugins enable rabbitmq_management`.

---

## 23. Best Practices

### Q: What are RabbitMQ production best practices?

**A:**

1. **Use quorum queues** for HA (not classic mirrors).
2. **Durable queues + persistent messages** for important data.
3. **Publisher confirms + manual consumer ack** for at-least-once.
4. **Always configure DLQ** — never let poison messages requeue forever.
5. **Set prefetch** — don't use unlimited unacked messages.
6. **Idempotent consumers** — handle duplicate deliveries.
7. **Connection pooling** — one connection, multiple channels.
8. **Queue limits** — `x-max-length`, `x-message-ttl` to prevent unbounded growth.
9. **Separate vhosts** per environment.
10. **Monitor queue depth and consumer count** with alerts.
11. **Schema versioning** in message payloads for backward compatibility.
12. **Graceful shutdown** — stop consuming, drain in-flight, then close.
13. **Don't use RabbitMQ as a database** — messages should be processed and acked promptly.

### Q: Should messages contain large payloads?

**A:** **No.** Keep messages small (< 1 MB recommended). Store large files in S3/blob storage; pass a **reference URL** in the message. Large messages bloat memory and slow replication.

---

## 24. Scenario Questions

### Q: Design a notification system (email, SMS, push) for 1M users.

**A:**

```
Producer → fanout exchange "notifications"
              ├─ email-queue  → email workers (10 consumers)
              ├─ sms-queue    → sms workers (5 consumers)
              └─ push-queue   → push workers (5 consumers)
```

- Fanout ensures all channels get the event.
- Each queue has DLQ, retry with TTL backoff.
- Quorum queues, persistent messages, publisher confirms.
- Monitor depth per queue; auto-scale consumers.

---

### Q: A consumer is crashing on certain messages. Messages keep reappearing. Fix?

**A:**

1. Identify poison messages in the queue (management UI or `basic.get`).
2. Configure **DLQ** with `x-dead-letter-exchange`.
3. On failure: `nack(msg, false, false)` — routes to DLQ after max retries.
4. Add **retry count header** with exponential backoff (30s, 60s, 120s).
5. Make consumer **idempotent** and validate message schema before processing.
6. Inspect DLQ, fix bug, replay valid messages.

---

### Q: You need to process orders per user in order, but scale horizontally.

**A:**

- Use **consistent-hash exchange** with routing key = `userId`.
- N shard queues, each with 1 consumer → strict order per user.
- Different users processed in parallel across shards.

---

### Q: RabbitMQ memory alarm triggered. What do you do?

**A:**

1. **Immediate:** Check which queues have the most messages (`rabbitmqctl list_queues`).
2. Add/scaling consumers to drain backlog.
3. Enable **lazy queues** or set **max-length** / **TTL** on overflowing queues.
4. If publishers blocked, they'll resume when memory drops below watermark.
5. **Long-term:** Increase RAM, review message retention, add queue limits, consider splitting hot queues.

---

### Q: How do you migrate from classic mirrored queues to quorum queues?

**A:**

1. Create new quorum queue (e.g., `orders.v2`).
2. Dual-write or use **shovel** to migrate in-flight messages.
3. Point new consumers to quorum queue.
4. Drain classic queue, decommission.
5. Quorum queues have different semantics (no global QoS, different DLX behavior) — test thoroughly.

---

### Q: How do you ensure a payment message is never lost?

**A:**

1. **Publisher:** persistent message + `confirmSelect()` + wait for confirm.
2. **Broker:** quorum queue, 3-node cluster, durable.
3. **Consumer:** manual ack **only after** DB commit (process in transaction).
4. **Idempotency:** store `messageId` in DB to prevent duplicate charges on redelivery.
5. **DLQ** with alerting for any failed payment messages.

---

### Q: How do you implement exponential backoff retries?

**A:** Create multiple retry queues with increasing TTL (30s, 60s, 120s, 300s), each dead-lettering back to the main queue. Track `x-retry-count` in headers; route to the appropriate delay queue on failure; after max retries → DLQ.

```
fail → retry-30s (TTL) → main queue → fail → retry-60s → ... → DLQ
```

---

### Q: Consumer disconnects mid-processing — what happens?

**A:** With **manual ack**, the message stays **unacknowledged**. On disconnect, RabbitMQ **redelivers** it to another consumer (or the same one on reconnect). Design handlers to be **idempotent** — use `messageId` dedup in DB.

---

### Q: How do you gracefully shut down a consumer?

**A:**

1. Stop accepting new messages (`channel.cancel(consumerTag)`).
2. Finish processing in-flight (unacked) messages.
3. Ack/nack each one.
4. Close channel, then connection.

```javascript
process.on('SIGTERM', async () => {
  await channel.cancel(consumerTag);
  // wait for in-flight count to reach 0
  await channel.close();
  await conn.close();
  process.exit(0);
});
```

---

## 25. Cheat Sheet

### Architecture
```
Producer → Exchange → [Binding + Routing Key] → Queue → Consumer
```

### Exchange Types
| Type | Routes By |
|------|-----------|
| Direct | Exact routing key match |
| Topic | Pattern (`*`, `#`) |
| Fanout | All bound queues |
| Headers | Header key-value match |

### Reliability Checklist
- [ ] Durable queue
- [ ] Persistent messages (`deliveryMode: 2`)
- [ ] Publisher confirms
- [ ] Manual consumer ack
- [ ] Quorum queue (HA)
- [ ] DLQ configured
- [ ] Retry with limit
- [ ] Idempotent consumer

### Ack Modes
| Call | Requeue | Result |
|------|---------|--------|
| `ack` | — | Removed |
| `nack(requeue=true)` | Yes | Retry |
| `nack(requeue=false)` | No | DLQ / drop |

### Key Settings
```javascript
// Quorum HA queue
{ durable: true, arguments: { 'x-queue-type': 'quorum' } }

// DLQ
{ arguments: { 'x-dead-letter-exchange': 'dlx', 'x-dead-letter-routing-key': 'key' } }

// Prefetch
channel.prefetch(10);

// Persistent publish
channel.publish(ex, key, buf, { persistent: true });
```

### RabbitMQ vs Kafka (one-liner)
- **RabbitMQ** = smart router, messages deleted after ack, task queues.
- **Kafka** = durable log, replay, event streaming at scale.

### RabbitMQ vs BullMQ (one-liner)
- **RabbitMQ** = polyglot enterprise broker with routing.
- **BullMQ** = Redis-backed job queue for Node.js apps.

### Common Interviewer Questions
1. Explain the message flow (producer → exchange → queue → consumer).
2. Difference between direct and topic exchange?
3. How do you prevent message loss?
4. What is prefetch and why use it?
5. How do DLQ and retry queues work?
6. RabbitMQ vs Kafka — when to use which?
7. How do you scale consumers while preserving order?
8. What happens on memory/disk alarm?
9. What is a quorum queue?
10. How do you achieve exactly-once delivery? (Trick: you don't natively — idempotency + dedup.)

---

*End of RabbitMQ Interview Guide*

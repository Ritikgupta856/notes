# REST APIs — Comprehensive Interview Preparation Guide

> **How to use this guide:** Read top-to-bottom for fundamentals, jump to sections for revision, and drill the **Cheat Sheet** + **Scenario Questions** before interviews.

---

## Table of Contents

1. [What is REST?](#1-what-is-rest)
2. [REST Principles](#2-rest-principles)
3. [REST Constraints](#3-rest-constraints)
4. [HTTP Fundamentals](#4-http-fundamentals)
5. [HTTP Methods](#5-http-methods)
6. [URI Design](#6-uri-design)
7. [Resource Design](#7-resource-design)
8. [Idempotency](#8-idempotency)
9. [Statelessness](#9-statelessness)
10. [Headers](#10-headers)
11. [Status Codes](#11-status-codes)
12. [Request Lifecycle](#12-request-lifecycle)
13. [Authentication](#13-authentication)
14. [Authorization](#14-authorization)
15. [Pagination](#15-pagination)
16. [Filtering](#16-filtering)
17. [Sorting](#17-sorting)
18. [Versioning](#18-versioning)
19. [Validation](#19-validation)
20. [Rate Limiting](#20-rate-limiting)
21. [Caching](#21-caching)
22. [ETags](#22-etags)
23. [Compression](#23-compression)
24. [Error Handling](#24-error-handling)
25. [API Documentation](#25-api-documentation)
26. [OpenAPI & Swagger](#26-openapi--swagger)
27. [REST vs GraphQL](#27-rest-vs-graphql)
28. [REST vs gRPC](#28-rest-vs-grpc)
29. [Best Practices](#29-best-practices)
30. [Scenario Questions](#30-scenario-questions)
31. [Cheat Sheet](#31-cheat-sheet)

---

## 1. What is REST?

### Q: What is REST?

**A:** **REST** (Representational State Transfer) is an **architectural style** for designing networked applications, introduced by Roy Fielding in 2000. APIs that follow REST principles are called **RESTful APIs**. They use HTTP as the transport, expose **resources** via URIs, and manipulate them with standard HTTP methods.

### Q: Is REST a protocol?

**A:** **No.** REST is an **architectural style** — a set of constraints and principles. HTTP is the protocol REST APIs typically run on. Compare: REST = design philosophy; HTTP = wire protocol.

### Q: What is a resource in REST?

**A:** A **resource** is any identifiable entity — a user, order, product, or collection. Resources are addressed by **URIs** and represented in formats like JSON or XML.

```
Resource:     User with ID 42
URI:          GET /api/users/42
Representation: { "id": 42, "name": "Alice", "email": "alice@example.com" }
```

---

## 2. REST Principles

### Q: What are the core REST principles?

**A:**

| Principle | Meaning |
|-----------|---------|
| **Client-Server** | Separation of concerns; client handles UI, server handles data/logic |
| **Stateless** | Each request contains all info needed; server stores no client session |
| **Cacheable** | Responses must define themselves as cacheable or not |
| **Uniform Interface** | Consistent way to interact: URIs, HTTP methods, representations, HATEOAS |
| **Layered System** | Client can't tell if connected to end server, load balancer, or cache |
| **Code on Demand** (optional) | Server can send executable code (rarely used in APIs) |

### Q: What is HATEOAS?

**A:** **Hypermedia As The Engine Of Application State** — responses include links to related actions/resources so the client discovers the API dynamically.

```json
{
  "id": 42,
  "status": "pending",
  "name": "Alice",
  "_links": {
    "self": { "href": "/api/users/42" },
    "orders": { "href": "/api/users/42/orders" },
    "cancel": { "href": "/api/users/42/cancel", "method": "POST" }
  }
}
```

Most APIs skip full HATEOAS but use its spirit (clear, predictable URLs).

### Q: What makes an API "RESTful" vs just "HTTP API"?

**A:** A truly RESTful API follows **all** constraints (especially statelessness, uniform interface, hypermedia). Most "REST APIs" are **REST-inspired** — they use HTTP + JSON + resource URLs but may use sessions, non-standard actions, or omit HATEOAS.

---

## 3. REST Constraints

### Q: What are the six REST constraints?

**A:**

1. **Client-Server** — independent evolution of client and server.
2. **Stateless** — no server-side session state between requests.
3. **Cacheable** — leverage HTTP caching (`Cache-Control`, `ETag`).
4. **Uniform Interface** — four sub-constraints:
   - Resource identification (URI)
   - Manipulation through representations (JSON body)
   - Self-descriptive messages (Content-Type, status codes)
   - HATEOAS (hypermedia links)
5. **Layered System** — proxies, gateways, load balancers transparent to client.
6. **Code on Demand** (optional) — e.g., JavaScript sent by server.

### Q: Why are constraints useful?

**A:** They lead to **scalability** (stateless → horizontal scaling), **reliability** (cacheable → less load), **simplicity** (uniform interface → predictable patterns), and **independence** (client/server evolve separately).

---

## 4. HTTP Fundamentals

### Q: What is HTTP?

**A:** **HTTP** (HyperText Transfer Protocol) is a **request-response** application protocol. The client sends a request (method, URI, headers, body); the server returns a response (status, headers, body).

```
Client                                    Server
  │─── GET /api/users/42 HTTP/1.1 ────────►│
  │    Host: api.example.com                │
  │    Authorization: Bearer eyJ...         │
  │                                         │
  │◄── 200 OK ─────────────────────────────│
  │    Content-Type: application/json       │
  │    { "id": 42, "name": "Alice" }        │
```

### Q: What is the difference between HTTP and HTTPS?

**A:** **HTTPS** = HTTP + **TLS encryption**. Encrypts data in transit, prevents eavesdropping and tampering. All production APIs should use HTTPS.

### Q: What are the parts of an HTTP request?

**A:**

| Part | Example |
|------|---------|
| **Request line** | `POST /api/orders HTTP/1.1` |
| **Headers** | `Content-Type: application/json` |
| **Body** | `{ "productId": 7, "qty": 2 }` |

### Q: What are the parts of an HTTP response?

**A:**

| Part | Example |
|------|---------|
| **Status line** | `HTTP/1.1 201 Created` |
| **Headers** | `Location: /api/orders/99` |
| **Body** | `{ "id": 99, "status": "created" }` |

---

## 5. HTTP Methods

### Q: What HTTP methods are used in REST APIs?

**A:**

| Method | Purpose | Safe | Idempotent | Request Body |
|--------|---------|------|------------|--------------|
| **GET** | Read resource(s) | Yes | Yes | No |
| **POST** | Create resource / action | No | No | Yes |
| **PUT** | Replace entire resource | No | Yes | Yes |
| **PATCH** | Partial update | No | No* | Yes |
| **DELETE** | Remove resource | No | Yes | Optional |
| **HEAD** | GET without body (metadata only) | Yes | Yes | No |
| **OPTIONS** | Describe supported methods (CORS) | Yes | Yes | No |

*PATCH idempotency depends on implementation.

---

### Q: When do you use GET?

**A:** Retrieve data. Must be **safe** (no side effects) and **idempotent**. Never use GET for mutations.

```http
GET /api/users/42 HTTP/1.1
Authorization: Bearer <token>

→ 200 OK
{ "id": 42, "name": "Alice" }
```

### Q: When do you use POST?

**A:** Create a new resource or trigger a **non-idempotent action**.

```http
POST /api/users HTTP/1.1
Content-Type: application/json

{ "name": "Bob", "email": "bob@example.com" }

→ 201 Created
Location: /api/users/43
{ "id": 43, "name": "Bob" }
```

Also used for actions: `POST /api/orders/99/cancel`, `POST /api/auth/login`.

### Q: When do you use PUT?

**A:** **Replace** an entire resource (or create at a known URI). Idempotent — sending the same PUT twice yields the same result.

```http
PUT /api/users/42 HTTP/1.1
Content-Type: application/json

{ "name": "Alice Smith", "email": "alice@example.com", "role": "admin" }

→ 200 OK (updated) or 201 Created (if didn't exist)
```

### Q: When do you use PATCH?

**A:** **Partial update** — send only fields to change.

```http
PATCH /api/users/42 HTTP/1.1
Content-Type: application/json

{ "email": "newemail@example.com" }

→ 200 OK
{ "id": 42, "name": "Alice", "email": "newemail@example.com" }
```

Use **JSON Merge Patch** (`application/merge-patch+json`) or **JSON Patch** (`application/json-patch+json`) for standardized formats.

### Q: When do you use DELETE?

**A:** Remove a resource. Idempotent — deleting twice returns 204 (or 404 on second call).

```http
DELETE /api/users/42 HTTP/1.1

→ 204 No Content
```

### Q: When do you use HEAD?

**A:** Same as GET but **no response body** — useful for checking existence, size (`Content-Length`), or last modified date without downloading data.

```http
HEAD /api/files/report.pdf HTTP/1.1

→ 200 OK
Content-Length: 1048576
Last-Modified: Wed, 01 Jan 2025 00:00:00 GMT
```

### Q: When do you use OPTIONS?

**A:** Discover allowed methods on a resource. Critical for **CORS preflight** — browser sends OPTIONS before cross-origin POST/PUT/DELETE.

```http
OPTIONS /api/users HTTP/1.1
Origin: https://app.example.com

→ 204 No Content
Access-Control-Allow-Methods: GET, POST, OPTIONS
Access-Control-Allow-Headers: Content-Type, Authorization
```

---

## 6. URI Design

### Q: What are URI design best practices?

**A:**

| Rule | Good | Bad |
|------|------|-----|
| Use nouns, not verbs | `/users` | `/getUsers` |
| Plural collections | `/orders` | `/order` |
| Hierarchy for relationships | `/users/42/orders` | `/userOrders?userId=42` |
| Lowercase, hyphens | `/order-items` | `/OrderItems` |
| No trailing slash (pick one) | `/users/42` | `/users/42/` |
| No file extensions | `/users/42` | `/users/42.json` |

### Q: How do you handle actions that aren't CRUD?

**A:** Model as **sub-resources** or **commands** with POST:

```
POST /api/orders/99/cancel
POST /api/users/42/activate
POST /api/payments/7/refund
```

Avoid: `GET /api/cancelOrder?id=99` (GET must not mutate state).

### Q: Should URIs include versioning?

**A:** Common approaches (see [Versioning](#18-versioning)):

```
/api/v1/users/42          ← URL path (most common)
/api/users/42               ← Header: Accept-Version: v1
```

---

## 7. Resource Design

### Q: How do you design REST resources?

**A:**

1. **Identify nouns** — users, orders, products, comments.
2. **Define collections vs singletons:**
   - Collection: `GET /users` → list
   - Singleton: `GET /users/42` → one item
3. **Nest for ownership:** `GET /users/42/orders` — orders belonging to user 42.
4. **Don't nest too deep** — max 2–3 levels; use query params beyond that.
5. **Consistent envelope** for collections:

```json
{
  "data": [ { "id": 1, "name": "Alice" } ],
  "meta": { "total": 100, "page": 1, "pageSize": 20 }
}
```

### Q: How do you represent relationships?

**A:**

| Approach | Example | When |
|----------|---------|------|
| **Nested URI** | `/users/42/orders` | Strong ownership |
| **Reference ID** | `{ "userId": 42 }` in order body | Loose coupling |
| **Embedded** | `{ "user": { "id": 42, "name": "Alice" } }` | Avoid N+1 on client |
| **Link** | `{ "user": "/api/users/42" }` | HATEOAS style |

### Q: What response format should you use?

**A:** **JSON** is the standard (`Content-Type: application/json`). Use consistent field naming (camelCase in JS ecosystems, snake_case in Python/DB-aligned APIs — pick one and stick to it).

---

## 8. Idempotency

### Q: What is idempotency?

**A:** An operation is **idempotent** if performing it **multiple times** has the **same effect** as performing it once. Critical for safe retries on network failures.

| Method | Idempotent? | Notes |
|--------|-------------|-------|
| GET | Yes | Read-only |
| PUT | Yes | Full replace → same state |
| DELETE | Yes | Second delete → 404, resource still gone |
| POST | **No** | Each call may create a new resource |
| PATCH | Usually | Depends on patch logic |

### Q: How do you make POST idempotent?

**A:** Use an **Idempotency-Key** header (Stripe, many payment APIs):

```http
POST /api/payments HTTP/1.1
Idempotency-Key: 550e8400-e29b-41d4-a716-446655440000
Content-Type: application/json

{ "amount": 1000, "currency": "usd" }
```

Server stores the key; duplicate requests within a TTL return the original response without reprocessing.

```javascript
// Server-side (simplified)
const existing = await redis.get(`idempotency:${key}`);
if (existing) return JSON.parse(existing);

const result = await processPayment(body);
await redis.setex(`idempotency:${key}`, 86400, JSON.stringify(result));
return result;
```

### Q: What is the difference between safe and idempotent?

**A:**

- **Safe** — no state change on server (GET, HEAD, OPTIONS).
- **Idempotent** — may change state, but repeat calls = same result (GET, PUT, DELETE).

All safe methods are idempotent, but not vice versa (DELETE changes state but is idempotent).

---

## 9. Statelessness

### Q: What does stateless mean in REST?

**A:** The server **does not store client context** between requests. Every request must include everything needed: authentication token, resource ID, parameters. No server-side sessions tied to a connection.

### Q: How do you handle authentication in a stateless API?

**A:** Client sends credentials on **every request**:

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

JWT tokens encapsulate user identity and permissions. Server validates token without looking up session state (though it may check a revocation list).

### Q: Is using JWT truly stateless?

**A:** **Mostly.** The server doesn't store session state, but token **revocation** requires state (blacklist/whitelist) or short-lived tokens + refresh tokens. Pure statelessness is a spectrum.

### Q: What are problems with server-side sessions in REST?

**A:**

- Breaks horizontal scaling (sticky sessions or shared session store needed).
- Violates REST statelessness constraint.
- Adds infrastructure complexity (Redis session store).

---

## 10. Headers

### Q: What are important request headers?

**A:**

| Header | Purpose | Example |
|--------|---------|---------|
| `Authorization` | Credentials | `Bearer <token>`, `Basic <base64>` |
| `Content-Type` | Body format | `application/json` |
| `Accept` | Desired response format | `application/json` |
| `Accept-Language` | Locale preference | `en-US` |
| `If-None-Match` | Conditional GET (ETag) | `"abc123"` |
| `If-Match` | Optimistic concurrency | `"abc123"` |
| `Idempotency-Key` | Safe POST retries | UUID |
| `X-Request-ID` | Distributed tracing | UUID |
| `User-Agent` | Client identification | `MyApp/1.0` |

### Q: What are important response headers?

**A:**

| Header | Purpose | Example |
|--------|---------|---------|
| `Content-Type` | Body format | `application/json; charset=utf-8` |
| `Content-Length` | Body size in bytes | `1234` |
| `Location` | URI of created resource | `/api/users/43` |
| `ETag` | Resource version hash | `"v1-abc123"` |
| `Cache-Control` | Caching policy | `max-age=3600, private` |
| `Last-Modified` | Last change timestamp | `Wed, 01 Jan 2025 00:00:00 GMT` |
| `X-RateLimit-Remaining` | Rate limit info | `99` |
| `Retry-After` | When to retry (429/503) | `60` |
| `Access-Control-Allow-Origin` | CORS | `https://app.example.com` |

### Q: What is Content Negotiation?

**A:** Client specifies desired format via `Accept` header; server responds in that format or returns `406 Not Acceptable`.

```http
GET /api/users/42
Accept: application/json        → JSON response
Accept: application/xml         → XML response (if supported)
```

### Q: What is CORS and how does it work?

**A:** **CORS** (Cross-Origin Resource Sharing) lets browsers call APIs on a different origin (scheme + host + port). Without CORS headers, browsers block cross-origin responses.

**Simple request** (GET, HEAD, POST with safe headers) — server returns:
```http
Access-Control-Allow-Origin: https://app.example.com
Access-Control-Allow-Credentials: true
```

**Preflight** (PUT, DELETE, custom headers) — browser sends OPTIONS first:
```http
OPTIONS /api/users HTTP/1.1
Origin: https://app.example.com
Access-Control-Request-Method: DELETE
Access-Control-Request-Headers: Authorization

→ 204 No Content
Access-Control-Allow-Origin: https://app.example.com
Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS
Access-Control-Allow-Headers: Content-Type, Authorization
Access-Control-Max-Age: 86400
```

**Never use `Access-Control-Allow-Origin: *` with credentials.**

### Q: What is the `Vary` header?

**A:** Tells caches that the response differs based on certain request headers. Critical when caching varies by `Accept`, `Accept-Encoding`, or `Authorization`.

```http
Vary: Accept-Encoding, Authorization
```

---

## 11. Status Codes

### Q: What status codes should you know?

**A:**

### 2xx — Success

| Code | Meaning | Use |
|------|---------|-----|
| **200 OK** | Success with body | GET, PUT, PATCH |
| **201 Created** | Resource created | POST; include `Location` header |
| **204 No Content** | Success, no body | DELETE, PUT with no response needed |
| **206 Partial Content** | Range request | File downloads, pagination chunks |

### 3xx — Redirection

| Code | Meaning | Use |
|------|---------|-----|
| **301 Moved Permanently** | URI changed forever | API migration |
| **304 Not Modified** | Cached version still valid | Conditional GET with ETag |
| **307 Temporary Redirect** | Temporary move, preserve method | Maintenance redirect |
| **308 Permanent Redirect** | Permanent, preserve method | Preferred over 301 for APIs |

### 4xx — Client Errors

| Code | Meaning | Use |
|------|---------|-----|
| **400 Bad Request** | Malformed syntax / validation failure | Invalid JSON, missing fields |
| **401 Unauthorized** | Not authenticated | Missing/invalid token |
| **403 Forbidden** | Authenticated but not permitted | Insufficient permissions |
| **404 Not Found** | Resource doesn't exist | Invalid ID |
| **405 Method Not Allowed** | HTTP method not supported | POST on read-only endpoint |
| **409 Conflict** | State conflict | Duplicate email, version mismatch |
| **412 Precondition Failed** | ETag/If-Match mismatch | Optimistic locking failure |
| **415 Unsupported Media Type** | Wrong Content-Type | Sent XML, expect JSON |
| **422 Unprocessable Entity** | Semantic validation error | Valid JSON, invalid business rules |
| **429 Too Many Requests** | Rate limited | Include `Retry-After` |

### 5xx — Server Errors

| Code | Meaning | Use |
|------|---------|-----|
| **500 Internal Server Error** | Unexpected server failure | Bug, unhandled exception |
| **502 Bad Gateway** | Upstream server error | Proxy/gateway issue |
| **503 Service Unavailable** | Temporarily down / overloaded | Maintenance, circuit breaker |
| **504 Gateway Timeout** | Upstream timeout | Slow dependency |

### Q: 401 vs 403 — what's the difference?

**A:**

- **401 Unauthorized** — "Who are you?" — authentication failed or missing. Client should retry with credentials.
- **403 Forbidden** — "I know who you are, but you can't do this." — authenticated but lacks permission. Retrying with same credentials won't help.

### Q: When to use 400 vs 422?

**A:**

- **400** — syntactic error (malformed JSON, wrong type, missing required field).
- **422** — syntactically valid but semantically wrong (end date before start date, duplicate username).

---

## 12. Request Lifecycle

### Q: What happens when a REST API request is processed?

**A:**

```
1. DNS Resolution       → api.example.com → IP
2. TCP Connection       → 3-way handshake
3. TLS Handshake        → (HTTPS) certificate exchange
4. HTTP Request Sent    → Method, URI, Headers, Body
5. Load Balancer        → Route to healthy instance
6. API Gateway          → Rate limit, auth, routing (optional)
7. Middleware Chain     → Logging, CORS, auth, validation
8. Route Matching       → Map URI + method to handler
9. Controller/Handler   → Business logic
10. Service Layer       → Domain logic, transactions
11. Data Access         → Database, cache, external APIs
12. Response Formation  → Status, headers, JSON body
13. HTTP Response       → Sent to client
14. Connection          → Keep-alive or close
```

### Q: What is middleware?

**A:** Functions that process the request **before** and **after** the handler — logging, authentication, CORS, rate limiting, error handling.

```javascript
// Express.js example
app.use(requestLogger);
app.use(cors());
app.use(authenticate);
app.use('/api/users', usersRouter);
app.use(errorHandler); // catches errors from handlers above
```

### Q: What is an API Gateway?

**A:** A single entry point that handles **cross-cutting concerns**: authentication, rate limiting, SSL termination, request routing to microservices, response aggregation.

```
Client → API Gateway → User Service
                     → Order Service
                     → Payment Service
```

---

## 13. Authentication

### Q: What is authentication vs authorization?

**A:**

- **Authentication (AuthN)** — "Who are you?" — verifying identity.
- **Authorization (AuthZ)** — "What can you do?" — verifying permissions.

Authentication comes first; authorization follows.

### Q: What are common authentication methods?

**A:**

| Method | How | Use Case |
|--------|-----|----------|
| **API Key** | `X-API-Key: abc123` | Server-to-server, simple |
| **Basic Auth** | `Authorization: Basic base64(user:pass)` | Simple, internal tools (always HTTPS) |
| **Bearer Token (JWT)** | `Authorization: Bearer eyJ...` | SPAs, mobile apps, microservices |
| **OAuth 2.0** | Access token via authorization server | Third-party access, SSO |
| **mTLS** | Client certificate | Service-to-service, high security |

### Q: How does JWT authentication work?

**A:**

1. User logs in with credentials → server returns **JWT**.
2. JWT contains header, payload (user ID, roles, expiry), and signature.
3. Client sends JWT in `Authorization: Bearer <token>` on every request.
4. Server verifies signature and expiry — no DB lookup needed.

```json
// JWT Payload (decoded)
{
  "sub": "user-42",
  "role": "admin",
  "iat": 1700000000,
  "exp": 1700003600
}
```

### Q: What is OAuth 2.0?

**A:** An **authorization framework** where a user grants a third-party app limited access without sharing credentials. Flows: Authorization Code (most secure, with PKCE for SPAs), Client Credentials (machine-to-machine), Implicit (deprecated).

```
User → Auth Server (login + consent) → Authorization Code
App → Auth Server (code + client_secret) → Access Token
App → API (Access Token) → Protected Resource
```

---

## 14. Authorization

### Q: What are common authorization models?

**A:**

| Model | How | Example |
|-------|-----|---------|
| **RBAC** | Role-Based Access Control | `admin`, `editor`, `viewer` roles |
| **ABAC** | Attribute-Based | `user.department == resource.department` |
| **ACL** | Access Control Lists | Per-resource permission list |
| **Scope-based** | OAuth scopes | `read:orders`, `write:users` |

### Q: How do you implement authorization in REST?

**A:**

```javascript
// Middleware checks role before handler
function requireRole(role) {
  return (req, res, next) => {
    if (!req.user.roles.includes(role)) {
      return res.status(403).json({ error: 'Forbidden' });
    }
    next();
  };
}

router.delete('/users/:id', requireRole('admin'), deleteUser);
```

### Q: What is the principle of least privilege?

**A:** Grant only the **minimum permissions** needed. API tokens should have scoped access (`read-only` vs `read-write`), short expiry, and be revocable.

---

## 15. Pagination

### Q: What are pagination strategies?

**A:**

### Offset-Based (page number)

```http
GET /api/users?page=2&pageSize=20
```

```json
{
  "data": [ ... ],
  "meta": { "page": 2, "pageSize": 20, "total": 150, "totalPages": 8 }
}
```

**Pros:** Simple, jump to any page. **Cons:** Slow on large offsets (`OFFSET 100000`), inconsistent with concurrent inserts/deletes.

### Cursor-Based (keyset)

```http
GET /api/users?cursor=eyJpZCI6NDJ9&limit=20
```

```json
{
  "data": [ ... ],
  "meta": { "nextCursor": "eyJpZCI6NjJ9", "hasMore": true }
}
```

**Pros:** Consistent, performant at scale. **Cons:** Can't jump to arbitrary page.

### Q: When to use which?

**A:**

| Scenario | Strategy |
|----------|----------|
| Admin dashboards, small datasets | Offset |
| Infinite scroll, feeds, large tables | Cursor |
| Real-time data with frequent changes | Cursor |

---

## 16. Filtering

### Q: How do you implement filtering?

**A:** Use **query parameters** on collection endpoints:

```http
GET /api/orders?status=shipped&customerId=42
GET /api/products?category=electronics&minPrice=100&maxPrice=500
GET /api/users?role=admin&isActive=true
```

```javascript
// Server-side (simplified)
const { status, customerId, minPrice } = req.query;
const query = {};
if (status) query.status = status;
if (customerId) query.customerId = customerId;
if (minPrice) query.price = { $gte: Number(minPrice) };
const orders = await Order.find(query);
```

### Q: What about complex filters?

**A:** Support structured query syntax or POST search endpoint:

```http
GET /api/users?filter[createdAt][gte]=2025-01-01&filter[role][in]=admin,editor
POST /api/users/search   ← complex queries via request body
```

---

## 17. Sorting

### Q: How do you implement sorting?

**A:**

```http
GET /api/users?sort=createdAt          ← ascending (default)
GET /api/users?sort=-createdAt         ← descending (minus prefix)
GET /api/users?sort=lastName,firstName ← multiple fields
```

```javascript
const sortField = req.query.sort?.startsWith('-')
  ? { [req.query.sort.slice(1)]: -1 }
  : { [req.query.sort || 'createdAt']: 1 };
const users = await User.find().sort(sortField);
```

### Q: Should you allow sorting on any field?

**A:** **No.** Whitelist sortable fields to prevent slow queries on unindexed columns and injection risks.

```javascript
const ALLOWED_SORT = ['createdAt', 'name', 'email'];
const field = ALLOWED_SORT.includes(req.query.sort) ? req.query.sort : 'createdAt';
```

---

## 18. Versioning

### Q: How do you version REST APIs?

**A:**

| Strategy | Example | Pros | Cons |
|----------|---------|------|------|
| **URL path** | `/api/v1/users` | Explicit, easy to route | URL pollution |
| **Header** | `Accept: application/vnd.myapi.v1+json` | Clean URLs | Harder to test in browser |
| **Query param** | `/api/users?version=1` | Simple | Easy to forget |
| **Custom header** | `API-Version: 1` | Clean URLs | Less standard |

**Most common:** URL path versioning for major breaking changes.

### Q: What is backward compatibility?

**A:** Non-breaking changes don't require a new version:

- **Safe:** Add new fields, new endpoints, new optional query params.
- **Breaking:** Remove/rename fields, change types, change URL structure, change behavior → new version.

### Q: How do you deprecate an API version?

**A:**

1. Announce deprecation with timeline.
2. Add `Sunset` and `Deprecation` response headers.
3. Monitor usage of old version.
4. Provide migration guide.
5. Shut down after deadline.

```http
Sunset: Sat, 01 Jan 2026 00:00:00 GMT
Deprecation: true
Link: </api/v2/users>; rel="successor-version"
```

---

## 19. Validation

### Q: What should you validate in a REST API?

**A:**

| Layer | What | Example |
|-------|------|---------|
| **Syntax** | Format, types, required fields | email is string, age is number |
| **Semantic** | Business rules | endDate > startDate |
| **Authorization** | Permissions | user can only edit own profile |
| **Existence** | Referenced resources exist | productId exists in DB |

### Q: Where does validation happen?

**A:**

1. **Client-side** — UX feedback (never trust alone).
2. **API layer** — request validation middleware (return 400/422).
3. **Service layer** — business rule validation.
4. **Database** — constraints as last defense.

```javascript
// Zod validation example
const createUserSchema = z.object({
  name: z.string().min(1).max(100),
  email: z.string().email(),
  age: z.number().int().min(18).optional()
});

app.post('/api/users', (req, res) => {
  const result = createUserSchema.safeParse(req.body);
  if (!result.success) {
    return res.status(422).json({ errors: result.error.issues });
  }
  // proceed...
});
```

### Q: What is input sanitization?

**A:** Clean input to prevent **injection attacks** (SQL injection, XSS). Use parameterized queries, escape HTML, validate against allowlists. Validation ≠ sanitization — do both.

---

## 20. Rate Limiting

### Q: What is rate limiting?

**A:** Restricting the number of requests a client can make in a time window to prevent abuse, ensure fair usage, and protect server resources.

### Q: What are rate limiting algorithms?

**A:**

| Algorithm | How | Burst Behavior |
|-----------|-----|----------------|
| **Fixed Window** | N requests per minute | Burst at window boundary |
| **Sliding Window** | Rolling time window | Smoother |
| **Token Bucket** | Tokens refill at fixed rate | Allows controlled bursts |
| **Leaky Bucket** | Fixed output rate | Smooth, no bursts |

### Q: How do you communicate rate limits?

**A:** Return informative headers:

```http
HTTP/1.1 429 Too Many Requests
Retry-After: 60
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 0
X-RateLimit-Reset: 1700003600
```

```json
{ "error": "Rate limit exceeded", "retryAfter": 60 }
```

### Q: What do you rate limit by?

**A:** IP address, API key, user ID, or combination. Different tiers for free vs paid plans.

---

## 21. Caching

### Q: How does HTTP caching work for APIs?

**A:** Servers and clients use headers to control caching:

| Header | Purpose |
|--------|---------|
| `Cache-Control: max-age=3600` | Cache for 1 hour |
| `Cache-Control: no-cache` | Must revalidate with server |
| `Cache-Control: no-store` | Never cache (sensitive data) |
| `Cache-Control: private` | Only browser cache, not CDN |
| `Cache-Control: public` | CDN can cache |

```http
GET /api/products/7
→ 200 OK
Cache-Control: public, max-age=300
ETag: "v3-abc123"
```

### Q: What is a CDN and how does it cache APIs?

**A:** A **CDN** (Content Delivery Network) caches responses at edge locations. Works best for **read-heavy, public** data (product catalogs). Use `Cache-Control: public` + `ETag`. Don't cache personalized or authenticated responses at CDN without careful `Vary` headers.

### Q: What should NOT be cached?

**A:** Personalized data, auth endpoints, real-time data, anything with `Cache-Control: no-store`. User-specific responses need `Cache-Control: private` or `Vary: Authorization`.

---

## 22. ETags

### Q: What is an ETag?

**A:** An **Entity Tag** — a hash/version of a resource. Used for **conditional requests** and **optimistic concurrency control**.

### Q: How does ETag-based caching work?

**A:**

```http
# First request
GET /api/users/42
→ 200 OK
ETag: "v1-abc123"
{ "id": 42, "name": "Alice" }

# Subsequent request
GET /api/users/42
If-None-Match: "v1-abc123"
→ 304 Not Modified (no body — saves bandwidth)
```

### Q: How do ETags prevent lost updates?

**A:** **Optimistic locking** — client must send current ETag when updating:

```http
PUT /api/users/42
If-Match: "v1-abc123"
{ "name": "Alice Smith" }

→ 200 OK, ETag: "v2-def456"     (success)
→ 412 Precondition Failed        (someone else updated first)
```

### Q: Strong vs Weak ETags?

**A:**

- **Strong** (`"abc123"`) — byte-for-byte identical.
- **Weak** (`W/"abc123"`) — semantically equivalent (e.g., same data, different whitespace). Use strong for concurrency control.

---

## 23. Compression

### Q: How do you compress API responses?

**A:** Server compresses response body; client indicates support via `Accept-Encoding`:

```http
GET /api/users
Accept-Encoding: gzip, br

→ 200 OK
Content-Encoding: gzip
(binary compressed body)
```

| Algorithm | Notes |
|-----------|-------|
| **gzip** | Widely supported, good compression |
| **brotli (br)** | Better compression, slightly more CPU |
| **deflate** | Older, less common |

### Q: When should you compress?

**A:** Responses > 1 KB benefit from compression. Small responses may grow due to compression overhead. Most frameworks enable gzip/brotli via middleware (nginx, Express compression).

```javascript
// Express
const compression = require('compression');
app.use(compression());
```

### Q: Should you compress request bodies?

**A:** Clients can send `Content-Encoding: gzip` on POST/PUT for large payloads. Less common; server must explicitly support it.

---

## 24. Error Handling

### Q: How should REST APIs return errors?

**A:** Use appropriate **status codes** + consistent **error body**:

```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Request validation failed",
    "details": [
      { "field": "email", "message": "Invalid email format" },
      { "field": "age", "message": "Must be at least 18" }
    ]
  },
  "requestId": "req-abc-123"
}
```

### Q: What makes a good error response?

**A:**

1. Correct HTTP status code.
2. Machine-readable `code` (e.g., `USER_NOT_FOUND`).
3. Human-readable `message`.
4. Field-level `details` for validation errors.
5. `requestId` for debugging/support.
6. **Never expose** stack traces, SQL queries, or internal paths in production.

### Q: How do you handle errors globally?

**A:** Centralized error handler middleware:

```javascript
app.use((err, req, res, next) => {
  const status = err.status || 500;
  const response = {
    error: {
      code: err.code || 'INTERNAL_ERROR',
      message: status === 500 ? 'Internal server error' : err.message
    },
    requestId: req.id
  };
  if (status === 500) logger.error(err);
  res.status(status).json(response);
});
```

### Q: Should you return 200 with error in body?

**A:** **No.** This is an anti-pattern. Use proper status codes so clients, caches, and monitoring work correctly. `200 { "success": false }` breaks HTTP semantics.

### Q: What is RFC 7807 Problem Details?

**A:** Standard error format (`application/problem+json`) for machine-readable errors:

```json
{
  "type": "https://api.example.com/errors/validation-error",
  "title": "Validation Failed",
  "status": 422,
  "detail": "Email format is invalid",
  "instance": "/api/users",
  "errors": [{ "field": "email", "message": "Invalid format" }]
}
```

### Q: How do you handle bulk operations?

**A:** Use a collection sub-resource with POST, or batch endpoint:

```http
POST /api/v1/users/bulk
Content-Type: application/json

{ "operations": [
  { "method": "POST", "body": { "name": "Alice" } },
  { "method": "PATCH", "id": 42, "body": { "role": "admin" } }
]}
```

Return `207 Multi-Status` with per-item results, or `202 Accepted` for async bulk jobs.

---

## 25. API Documentation

### Q: Why is API documentation important?

**A:** Documentation is the **contract** between API provider and consumers. Good docs reduce integration time, support tickets, and breaking changes.

### Q: What should API documentation include?

**A:**

- Authentication setup
- Base URL and versioning
- Endpoints with methods, parameters, request/response examples
- Status codes and error formats
- Rate limits
- Pagination, filtering, sorting conventions
- Changelog and deprecation notices

### Q: What tools are used for API documentation?

**A:**

| Tool | Type |
|------|------|
| **OpenAPI (Swagger)** | Machine-readable spec → interactive UI |
| **Postman** | Collections + testing |
| **ReadMe, Stoplight** | Hosted documentation platforms |
| **Redoc** | Beautiful OpenAPI renderer |

---

## 26. OpenAPI & Swagger

### Q: What is OpenAPI?

**A:** **OpenAPI Specification** (formerly Swagger) is a **standard format** (YAML/JSON) for describing REST APIs. Defines endpoints, parameters, request/response schemas, authentication, and examples.

```yaml
openapi: 3.0.3
info:
  title: User API
  version: 1.0.0
paths:
  /users/{id}:
    get:
      summary: Get user by ID
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '404':
          description: User not found
components:
  schemas:
    User:
      type: object
      properties:
        id: { type: integer }
        name: { type: string }
        email: { type: string, format: email }
```

### Q: What is the difference between OpenAPI and Swagger?

**A:** **OpenAPI** is the specification (the standard). **Swagger** is the tooling ecosystem (Swagger UI, Swagger Editor, Swagger Codegen) originally created by SmartBear. Today: write "OpenAPI spec", view with "Swagger UI".

### Q: What can you generate from OpenAPI?

**A:**

- Interactive documentation (Swagger UI, Redoc)
- Client SDKs (TypeScript, Python, Java)
- Server stubs
- Mock servers
- Contract tests

### Q: What is design-first vs code-first?

**A:**

- **Design-first** — write OpenAPI spec, then implement. Better for team collaboration.
- **Code-first** — write code, generate spec from decorators/annotations (e.g., NestJS, FastAPI). Faster for solo devs.

---

## 27. REST vs GraphQL

### Q: REST vs GraphQL — key differences?

**A:**

| Aspect | REST | GraphQL |
|--------|------|---------|
| **Endpoints** | Multiple URLs per resource | Single endpoint (`/graphql`) |
| **Data fetching** | Fixed response shape per endpoint | Client specifies exact fields needed |
| **Over/under-fetching** | Common problem | Solved by design |
| **Versioning** | URL/header versioning | Evolve schema, deprecate fields |
| **Caching** | HTTP caching (built-in) | Complex (POST requests, custom caching) |
| **Learning curve** | Lower | Higher |
| **File upload** | Native (multipart) | Requires extensions |
| **Real-time** | WebSockets/SSE separately | Subscriptions built-in |

### Q: When to choose REST?

**A:**

- Simple CRUD APIs.
- HTTP caching is important.
- Public APIs where simplicity matters.
- File uploads/downloads.
- Team familiar with REST conventions.

### Q: When to choose GraphQL?

**A:**

- Mobile apps needing minimal data transfer.
- Complex UIs aggregating many resources.
- Rapidly evolving frontend requirements.
- Multiple clients with different data needs.

```graphql
# GraphQL — client asks for exactly what it needs
query {
  user(id: 42) {
    name
    orders(last: 5) {
      id
      total
    }
  }
}
```

---

## 28. REST vs gRPC

### Q: REST vs gRPC — key differences?

**A:**

| Aspect | REST | gRPC |
|--------|------|------|
| **Protocol** | HTTP/1.1 or HTTP/2 + JSON | HTTP/2 + Protocol Buffers (binary) |
| **Contract** | OpenAPI (optional) | `.proto` files (required) |
| **Performance** | Good (JSON text) | Excellent (binary, multiplexing) |
| **Browser support** | Native | Limited (needs gRPC-Web proxy) |
| **Streaming** | SSE, WebSockets (separate) | Bidirectional streaming built-in |
| **Code generation** | Optional | Built-in client/server stubs |
| **Human readable** | Yes (JSON) | No (binary protobuf) |
| **Use case** | Public APIs, web apps | Microservice-to-microservice |

### Q: When to choose gRPC?

**A:**

- Internal microservice communication.
- Low-latency, high-throughput requirements.
- Bidirectional streaming (chat, live feeds).
- Strongly typed contracts across languages.

### Q: When to choose REST?

**A:**

- Public-facing APIs consumed by browsers and third parties.
- Human debugging with curl/Postman.
- Simpler infrastructure (no proto compilation).

---

## 29. Best Practices

### Q: What are REST API best practices?

**A:**

1. **Use nouns for URLs**, HTTP methods for actions.
2. **Consistent naming** — plural collections, lowercase, hyphens.
3. **Proper status codes** — don't return 200 for everything.
4. **Version your API** from day one.
5. **Paginate collections** — never return unbounded lists.
6. **Validate all input** — return 400/422 with field details.
7. **Consistent error format** across all endpoints.
8. **Use HTTPS** everywhere.
9. **Authentication on every protected endpoint**.
10. **Rate limit** public APIs.
11. **Idempotency keys** for critical POST operations.
12. **ETags** for caching and concurrency.
13. **Document with OpenAPI** — keep spec in sync with code.
14. **Request IDs** for tracing (`X-Request-ID`).
15. **Don't expose internal IDs** if security-sensitive — use UUIDs.
16. **HATEOAS-lite** — at minimum, return `Location` on 201.
17. **Limit nesting** — max 2–3 levels in URIs.
18. **Graceful deprecation** — `Sunset` headers, migration guides.

### Q: What are common REST API anti-patterns?

**A:**

| Anti-Pattern | Problem | Fix |
|--------------|---------|-----|
| Verbs in URLs | `/getUser`, `/createOrder` | Use HTTP methods |
| 200 for errors | Breaks clients/caches | Proper status codes |
| No pagination | Performance disaster | Always paginate collections |
| Returning internal errors | Security risk | Generic 500 message |
| Inconsistent formats | Integration pain | Enforce schema/conventions |
| Session-based auth | Breaks statelessness | JWT/token-based |
| Ignoring versioning | Breaking changes hurt clients | Version from v1 |

---

## 30. Scenario Questions

### Q: Design a REST API for an e-commerce platform.

**A:**

```
# Users
POST   /api/v1/users                    # Register
GET    /api/v1/users/me                 # Current user profile
PATCH  /api/v1/users/me                 # Update profile

# Products
GET    /api/v1/products?category=electronics&sort=-price&page=1
GET    /api/v1/products/{id}

# Cart
GET    /api/v1/cart
POST   /api/v1/cart/items               # { productId, quantity }
PATCH  /api/v1/cart/items/{id}          # Update quantity
DELETE /api/v1/cart/items/{id}

# Orders
POST   /api/v1/orders                   # Idempotency-Key header
GET    /api/v1/orders/{id}
GET    /api/v1/orders?status=shipped&page=1
POST   /api/v1/orders/{id}/cancel

# Payments
POST   /api/v1/payments                 # Idempotency-Key required
```

- JWT auth, RBAC (customer vs admin).
- Cursor pagination for order history.
- Rate limiting on auth and payment endpoints.
- OpenAPI documentation.

---

### Q: A client reports duplicate orders when retrying POST. How do you fix it?

**A:**

1. Implement **Idempotency-Key** header on `POST /orders`.
2. Server stores `key → response` in Redis with 24h TTL.
3. On duplicate key, return stored response with `200` (not 201).
4. Make order creation transactional (DB + inventory).
5. Document the pattern for API consumers.

---

### Q: How do you handle breaking changes without breaking existing clients?

**A:**

1. Introduce `/api/v2/` with new schema.
2. Run v1 and v2 in parallel.
3. Add `Deprecation` and `Sunset` headers to v1 responses.
4. Provide migration guide and SDK updates.
5. Monitor v1 traffic; deprecate when near zero.
6. Non-breaking changes (add fields) don't need new version.

---

### Q: How do you secure a public REST API?

**A:**

1. **HTTPS** only (redirect HTTP → HTTPS).
2. **OAuth 2.0 / API keys** for authentication.
3. **RBAC** for authorization.
4. **Rate limiting** per key/IP.
5. **Input validation** and sanitization.
6. **CORS** — whitelist allowed origins.
7. **Security headers** — `X-Content-Type-Options`, `Strict-Transport-Security`.
8. **No sensitive data** in URLs (tokens in headers, not query params).
9. **Audit logging** for sensitive operations.
10. **OWASP API Security Top 10** compliance.

---

### Q: Two users edit the same resource simultaneously. How do you prevent lost updates?

**A:**

**Optimistic locking with ETags:**

1. Client A: `GET /users/42` → `ETag: "v1"`.
2. Client B: `GET /users/42` → `ETag: "v1"`.
3. Client A: `PUT /users/42` + `If-Match: "v1"` → `200 OK`, `ETag: "v2"`.
4. Client B: `PUT /users/42` + `If-Match: "v1"` → `412 Precondition Failed`.
5. Client B must refresh and retry.

Alternative: `version` field in body; reject if version mismatch → `409 Conflict`.

---

### Q: How do you handle a slow endpoint that times out?

**A:**

1. **Async pattern** — `POST /reports` returns `202 Accepted` + `{ "jobId": "abc" }`.
2. Client polls `GET /reports/jobs/abc` or receives webhook on completion.
3. `GET /reports/jobs/abc/result` when status is `completed`.
4. Set appropriate timeouts; return `503` with `Retry-After` if overloaded.

---

### Q: How do you implement webhooks?

**A:** Let clients register a callback URL; your server POSTs events on occurrence:

```http
POST https://client.example.com/webhooks/orders
X-Webhook-Signature: sha256=abc123...
X-Webhook-Id: evt_550e8400
Content-Type: application/json

{ "event": "order.shipped", "data": { "orderId": 99 } }
```

- Sign payloads (HMAC-SHA256) so clients verify authenticity.
- Retry with exponential backoff on failure (5xx, timeout).
- Use idempotency (`X-Webhook-Id`) on receiver side.
- Document event types and payload schemas in OpenAPI or separate webhook docs.

---

### Q: How do you implement field selection (sparse fieldsets)?

**A:** Let clients request only needed fields to reduce payload:

```http
GET /api/users/42?fields=id,name,email
GET /api/orders?fields=id,status&include=customer.name
```

Whitelist allowed fields server-side to prevent over-fetching sensitive data.

---

### Q: `If-Modified-Since` vs `If-None-Match` — when to use which?

**A:**

| Header | Based On | Best For |
|--------|----------|----------|
| `If-None-Match` + `ETag` | Content hash/version | Precise, avoids false cache hits |
| `If-Modified-Since` + `Last-Modified` | Timestamp | Simpler; 1-second granularity limit |

Prefer **ETags** for concurrency control and caching; use `Last-Modified` as fallback.

---

## 31. Cheat Sheet

### HTTP Methods
| Method | Action | Idempotent | Safe |
|--------|--------|------------|------|
| GET | Read | Yes | Yes |
| POST | Create / Action | No | No |
| PUT | Full replace | Yes | No |
| PATCH | Partial update | Maybe | No |
| DELETE | Remove | Yes | No |
| HEAD | Read headers only | Yes | Yes |
| OPTIONS | Capabilities / CORS | Yes | Yes |

### Status Codes (Quick Reference)
| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 304 | Not Modified |
| 400 | Bad Request |
| 401 | Unauthorized (not authenticated) |
| 403 | Forbidden (not authorized) |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Validation Error |
| 429 | Rate Limited |
| 500 | Server Error |
| 503 | Unavailable |

### URI Design
```
GET    /users              → list
POST   /users              → create
GET    /users/:id          → get one
PUT    /users/:id          → replace
PATCH  /users/:id          → partial update
DELETE /users/:id          → delete
POST   /users/:id/activate → action
```

### Essential Headers
```
Request:  Authorization, Content-Type, Accept, If-None-Match, Idempotency-Key
Response: Content-Type, Location, ETag, Cache-Control, Retry-After
```

### Pagination
```
Offset:  ?page=2&pageSize=20
Cursor:  ?cursor=abc&limit=20
```

### Error Response Template
```json
{
  "error": { "code": "ERROR_CODE", "message": "...", "details": [] },
  "requestId": "req-uuid"
}
```

### REST vs GraphQL vs gRPC (one-liner)
- **REST** — resource URLs + HTTP, universal, cacheable.
- **GraphQL** — client-driven queries, single endpoint, flexible.
- **gRPC** — binary, fast, typed, best for internal services.

### Common Interviewer Questions
1. What are REST constraints?
2. Difference between PUT and PATCH?
3. 401 vs 403?
4. What is idempotency? Which methods are idempotent?
5. How do you version APIs?
6. Offset vs cursor pagination?
7. How do ETags work?
8. How do you make POST idempotent?
9. REST vs GraphQL — when to use which?
10. How do you design error responses?

---

*End of REST APIs Interview Guide*

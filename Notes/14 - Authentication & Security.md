# Authentication & Security — Interview Preparation

> Comprehensive Q&A, scenario questions, and cheat sheet for backend, full-stack, and security-focused interviews. Includes **Better Auth** patterns as used in the **Synapse AI** project.

---

## Table of Contents

1. [Authentication](#1-authentication)
2. [Authorization](#2-authorization)
3. [Sessions](#3-sessions)
4. [Cookies](#4-cookies)
5. [JWT (JSON Web Tokens)](#5-jwt-json-web-tokens)
6. [Access Token & Refresh Token](#6-access-token--refresh-token)
7. [OAuth 2.0](#7-oauth-20)
8. [OpenID Connect (OIDC)](#8-openid-connect-oidc)
9. [Single Sign-On (SSO)](#9-single-sign-on-sso)
10. [RBAC & ABAC](#10-rbac--abac)
11. [Password Hashing (bcrypt, Argon2)](#11-password-hashing-bcrypt-argon2)
12. [HTTPS, SSL/TLS](#12-https-ssltls)
13. [CORS](#13-cors)
14. [CSRF](#14-csrf)
15. [XSS](#15-xss)
16. [SQL Injection](#16-sql-injection)
17. [Clickjacking & CSP](#17-clickjacking--csp)
18. [Cookie Security (SameSite, Secure, HttpOnly)](#18-cookie-security-samesite-secure-httponly)
19. [API Security](#19-api-security)
20. [OWASP Top 10](#20-owasp-top-10)
21. [Security Headers & Helmet](#21-security-headers--helmet)
22. [Rate Limiting](#22-rate-limiting)
23. [Secure Authentication Flow](#23-secure-authentication-flow)
24. [Better Auth (Synapse AI)](#24-better-auth-synapse-ai)
25. [Best Practices](#25-best-practices)
26. [Common Vulnerabilities](#26-common-vulnerabilities)
27. [Production Security](#27-production-security)
28. [Scenario Questions](#28-scenario-questions)
29. [Cheat Sheet](#29-cheat-sheet)

---

## 1. Authentication

### Q1. What is authentication?
**Answer:** Authentication verifies **who** a user or system is. It answers: "Are you really who you claim to be?" Examples: password login, OTP, biometrics, OAuth social login, API keys.

### Q2. What are common authentication factors?
**Answer:**
- **Something you know** — password, PIN
- **Something you have** — phone (OTP), hardware key, smart card
- **Something you are** — fingerprint, face recognition
- **Somewhere you are** — geolocation (less common)
- **MFA/2FA** combines two or more factors.

### Q3. Authentication vs identification?
**Answer:** Identification is claiming an identity (e.g., entering a username). Authentication is proving that claim (e.g., entering the correct password).

### Q4. What is credential stuffing?
**Answer:** Attackers use leaked username/password pairs from one breach to try logging into other sites. Mitigation: rate limiting, MFA, breach detection, unique passwords enforced.

### Q5. What is brute-force attack?
**Answer:** Repeatedly guessing passwords. Mitigation: rate limiting, account lockout (carefully), CAPTCHA, strong password policies, bcrypt/Argon2 slow hashing.

### Q6. Token-based vs session-based authentication?
**Answer:**
| | Session-based | Token-based (JWT) |
|---|---|---|
| State | Server stores session | Often stateless (JWT) or DB-backed |
| Storage | Session ID in cookie | Token in cookie, header, or localStorage |
| Revocation | Easy (delete session) | Harder with pure stateless JWT |
| Scale | Needs shared session store at scale | Easier horizontal scaling with stateless JWT |

### Q7. Where should authentication happen?
**Answer:** Always on the **server** (or trusted edge with full validation). Client-side checks are for UX only — never for security enforcement.

---

## 2. Authorization

### Q8. What is authorization?
**Answer:** Authorization determines **what** an authenticated user is allowed to do. It answers: "Are you permitted to access this resource or perform this action?"

### Q9. Authentication vs authorization — give an example.
**Answer:** Logging in with email/password is **authentication**. Checking whether that user can delete a document is **authorization**. You can be authenticated but not authorized.

### Q10. What are common authorization models?
**Answer:**
- **RBAC** — Role-Based Access Control (admin, editor, viewer)
- **ABAC** — Attribute-Based Access Control (department, clearance level, time of day)
- **ACL** — Access Control Lists per resource
- **Scope-based** — OAuth scopes (`read:profile`, `write:posts`)
- **Policy-based** — rules engine (OPA, Casbin)

### Q11. What is the principle of least privilege?
**Answer:** Grant only the minimum permissions needed to perform a task. Reduces blast radius if an account is compromised.

### Q12. What is privilege escalation?
**Answer:** Gaining higher permissions than intended — vertical (user → admin) or horizontal (access another user's data). Prevent with server-side checks, not client-side role flags.

---

## 3. Sessions

### Q13. What is a session?
**Answer:** A server-side record of an authenticated user's state, identified by a **session ID** sent to the client (usually in a cookie). The server looks up the session on each request.

### Q14. How does session-based auth work?
**Answer:**
1. User logs in with credentials.
2. Server validates credentials, creates a session record (user ID, expiry, metadata).
3. Server sends session ID in an HttpOnly cookie.
4. On each request, server reads cookie, looks up session, attaches user to request.
5. On logout, server deletes the session.

### Q15. Where are sessions stored?
**Answer:**
- **In-memory** — simple, lost on restart, not scalable
- **Database** — persistent, queryable, revocable (used by Better Auth in Synapse AI)
- **Redis** — fast, TTL support, ideal for distributed apps
- **Signed/encrypted cookies** — stateless session data in cookie itself


### Q19. How does Better Auth manage sessions?
**Answer:** Better Auth uses **database-backed sessions** by default. A random session token is stored in the DB and sent via an HttpOnly cookie. `auth.api.getSession()` resolves the token against the database — revocation is immediate by deleting the session row. In Synapse AI, this means logout and session invalidation are authoritative, not just client-side.

---

## 4. Cookies

### Q20. What is an HTTP cookie?
**Answer:** A small piece of data the server sends via `Set-Cookie` header; the browser automatically sends it back in the `Cookie` header on subsequent requests to matching domain/path.

### Q21. Cookie attributes explained?
**Answer:**
| Attribute | Purpose |
|---|---|
| `Name=Value` | Cookie data |
| `Domain` | Which hosts receive the cookie |
| `Path` | URL path scope |
| `Expires` / `Max-Age` | Lifetime |
| `Secure` | Only sent over HTTPS |
| `HttpOnly` | Not accessible via JavaScript |
| `SameSite` | Cross-site send restriction (Strict/Lax/None) |

### Q22. First-party vs third-party cookies?
**Answer:** First-party: set by the site you're visiting. Third-party: set by embedded resources (ads, analytics). Third-party cookies are being phased out; use first-party storage or server-side sessions instead.

### Q23. Why prefer cookies over localStorage for auth tokens?
**Answer:** localStorage is accessible to any JavaScript on the page — a single XSS vulnerability exposes the token. HttpOnly cookies cannot be read by JS, significantly reducing XSS token theft risk.

### Q24. Cookie vs session — what's the difference?
**Answer:** A cookie is a **transport mechanism**. A session is **server-side state**. The session ID is often stored in a cookie, but cookies can hold other data too.

---

## 5. JWT (JSON Web Tokens)

### Q25. What is a JWT?
**Answer:** A compact, URL-safe token with three Base64URL-encoded parts: **Header.Payload.Signature**

```
eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiIxMjM0NTY3ODkwIn0.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

### Q26. JWT structure?
**Answer:**
- **Header** — algorithm (`alg`) and type (`typ`)
- **Payload** — claims (sub, exp, iat, custom data)
- **Signature** — `HMACSHA256(base64(header) + "." + base64(payload), secret)` or asymmetric (RS256)

### Q27. How does JWT authentication work?
**Answer:**
1. User logs in; server issues signed JWT.
2. Client sends JWT in `Authorization: Bearer <token>` or cookie.
3. Server verifies signature and expiry without DB lookup (stateless).
4. Server extracts claims and authorizes the request.

### Q28. Advantages of JWT?
**Answer:** Stateless, scalable across microservices, self-contained claims, works well for mobile/SPA APIs, no server session store needed.

### Q29. Disadvantages of JWT?
**Answer:**
- Hard to revoke before expiry (need blocklist or short-lived tokens + refresh)
- Token size larger than session ID
- Storing sensitive data in payload is dangerous (payload is only encoded, not encrypted)
- If secret leaks, all tokens are compromised


### Q32. Where to store JWT in a browser app?
**Answer:** Prefer **HttpOnly Secure cookie** (with CSRF protection). Avoid localStorage. If using Authorization header, ensure XSS cannot exfiltrate it.

---

## 6. Access Token & Refresh Token

### Q33. What is an access token?
**Answer:** A short-lived token used to access protected APIs. Contains (or references) identity and permissions. Typically expires in minutes to hours.

### Q34. What is a refresh token?
**Answer:** A long-lived token used **only** to obtain new access tokens without re-login. Stored securely (HttpOnly cookie or secure storage). Rotated on each use in high-security setups.

### Q35. Why use both access and refresh tokens?
**Answer:** Short-lived access tokens limit damage if stolen. Refresh tokens allow seamless UX without frequent logins while keeping access tokens short-lived.

### Q36. Refresh token rotation?
**Answer:** Each time a refresh token is used, issue a new refresh token and invalidate the old one. Detects token theft (reuse of old refresh token triggers revocation of all sessions).

### Q37. Where to store refresh tokens?
**Answer:**
- **Web:** HttpOnly, Secure, SameSite cookie (best)
- **Mobile:** Secure enclave / Keychain / Keystore
- **Never:** localStorage, plain URL params, logs

### Q38. How does Better Auth's cookie cache relate to access/refresh?
**Answer:** Better Auth's **cookie cache** acts like a short-lived signed cache (similar to an access token) backed by a DB session (like a refresh token). The server validates the cache locally without a DB hit; when it expires, it refreshes from the database. Strategies: `compact`, `jwt`, or `jwe`.

---

## 7. OAuth 2.0

### Q39. What is OAuth 2.0?
**Answer:** An **authorization framework** (not authentication) that lets a user grant a third-party application limited access to their resources **without sharing their password**.

### Q40. OAuth 2.0 roles?
**Answer:**
- **Resource Owner** — the user
- **Client** — the app requesting access
- **Authorization Server** — issues tokens (e.g., Google, your auth server)
- **Resource Server** — API holding protected resources

### Q41. OAuth 2.0 grant types?
**Answer:**
| Grant | Use Case |
|---|---|
| **Authorization Code** (+ PKCE) | Web/mobile apps — most secure, recommended |
| **Client Credentials** | Machine-to-machine, no user |
| **Refresh Token** | Get new access token |
| **Implicit** | Deprecated — tokens in URL fragment |
| **Password (ROPC)** | Legacy — avoid; sends password to client |

### Q42. What is PKCE?
**Answer:** Proof Key for Code Exchange. Client generates `code_verifier` and sends `code_challenge` with auth request. Exchanges `code_verifier` for token. Prevents authorization code interception on public clients (SPAs, mobile).

### Q43. OAuth 2.0 flow (Authorization Code + PKCE)?
**Answer:**
1. Client redirects user to Authorization Server with `client_id`, `redirect_uri`, `scope`, `code_challenge`.
2. User authenticates and consents.
3. Server redirects back with `authorization_code`.
4. Client exchanges code + `code_verifier` for `access_token` (and optionally `refresh_token`).
5. Client calls Resource Server with `Authorization: Bearer <access_token>`.

### Q44. What are OAuth scopes?
**Answer:** Permissions requested by the client (e.g., `email`, `profile`, `repo:read`). User consents to scopes; token is limited to those scopes.

### Q45. How does Better Auth handle OAuth?
**Answer:** In Synapse AI, Better Auth's `socialProviders` config enables OAuth providers (e.g., Google). Better Auth handles the OAuth dance, stores the linked account in the `account` table, and creates a session — no manual token exchange code needed.

```typescript
// Synapse AI pattern
export const auth = betterAuth({
  socialProviders: {
    google: {
      clientId: process.env.GOOGLE_CLIENT_ID!,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET!,
    },
  },
});
```

---

## 8. OpenID Connect (OIDC)

### Q46. What is OpenID Connect?
**Answer:** An identity layer **on top of OAuth 2.0** that provides **authentication**. OAuth says "you can access this"; OIDC says "this is who the user is."

### Q47. OAuth 2.0 vs OIDC?
**Answer:**
| | OAuth 2.0 | OIDC |
|---|---|---|
| Purpose | Authorization | Authentication + Authorization |
| Token | Access token | Access token + **ID Token** (JWT) |
| User info | Via proprietary API | Standardized (`/userinfo`, claims in ID token) |

### Q48. What is an ID Token?
**Answer:** A JWT issued by the OIDC provider containing user identity claims (`sub`, `email`, `name`, `iss`, `aud`, `exp`). Used by the client to know who logged in — **not** for API authorization (use access token for that).

### Q49. Key OIDC endpoints?
**Answer:**
- `/.well-known/openid-configuration` — discovery
- `/authorize` — authentication
- `/token` — token exchange
- `/userinfo` — user profile
- `/jwks` — public keys for JWT verification

### Q50. What is the `nonce` in OIDC?
**Answer:** Random value sent in auth request, returned in ID token. Prevents replay attacks by binding the ID token to the specific auth request.

---

## 9. Single Sign-On (SSO)

### Q51. What is SSO?
**Answer:** Single Sign-On lets a user authenticate once and access multiple applications without logging in again. Common in enterprise (Google Workspace, Okta, Azure AD).

### Q52. How does SSO work?
**Answer:** A central **Identity Provider (IdP)** authenticates the user and issues tokens/assertions. **Service Providers (SPs)** trust the IdP. Protocols: SAML 2.0, OIDC, Kerberos.

### Q53. SAML vs OIDC for SSO?
**Answer:**
- **SAML** — XML-based, enterprise legacy, complex
- **OIDC** — JSON/JWT-based, modern, better for web/mobile APIs
- Many enterprises still use SAML; greenfield prefers OIDC.

### Q54. SSO security considerations?
**Answer:** Central IdP is a high-value target. Use MFA on IdP, short session lifetimes, proper logout (SLO — Single Logout), monitor for anomalous logins.

---

## 10. RBAC & ABAC

### Q55. What is RBAC?
**Answer:** Role-Based Access Control assigns permissions to **roles** (Admin, Editor, Viewer); users are assigned roles. Simple, widely used.

### Q56. RBAC example?
**Answer:**
```
Admin  → create, read, update, delete users
Editor → create, read, update posts
Viewer → read posts
```

### Q57. RBAC limitations?
**Answer:** Role explosion (too many roles), coarse granularity, hard to express context ("can edit own posts only"). ABAC or policy engines solve this.

### Q58. What is ABAC?
**Answer:** Attribute-Based Access Control evaluates policies based on **attributes** of user, resource, action, and environment.

**Example policy:** `Allow if user.department == resource.department AND user.clearance >= resource.classification AND time.hour BETWEEN 9 AND 17`

### Q59. RBAC vs ABAC?
**Answer:**
| | RBAC | ABAC |
|---|---|---|
| Model | Roles → Permissions | Attributes → Policy rules |
| Flexibility | Lower | Higher |
| Complexity | Lower | Higher |
| Best for | Simple apps, fixed roles | Fine-grained, dynamic policies |

### Q60. How to implement RBAC in an API?
**Answer:** Middleware checks `user.role` against required permission for the route. In Synapse AI with Better Auth, custom session fields or a separate permissions table can extend the session; authorization checks happen in server routes/layouts, not middleware alone.

---

## 11. Password Hashing (bcrypt, Argon2)

### Q61. Why hash passwords?
**Answer:** Never store plain-text passwords. If the database leaks, hashes prevent immediate credential exposure. Hashing is one-way — you verify by hashing the input and comparing.

### Q62. What is salting?
**Answer:** Random data prepended/appended to password before hashing. Ensures identical passwords produce different hashes. Defeats rainbow table attacks. bcrypt and Argon2 salt automatically.

### Q63. What is bcrypt?
**Answer:** Adaptive password hashing function based on Blowfish. Uses a **cost factor** (work factor, rounds) making it intentionally slow. Industry standard for years.

```javascript
const hash = await bcrypt.hash(password, 12); // cost factor 12
const valid = await bcrypt.compare(password, hash);
```

### Q64. What is the bcrypt cost factor?
**Answer:** Number of iterations as `2^cost`. Higher = slower = more secure but more CPU. 10–12 is common; increase over time as hardware improves.

### Q65. What is Argon2?
**Answer:** Winner of the Password Hashing Competition (2015). Memory-hard — resistant to GPU/ASIC attacks. Variants: Argon2d, Argon2i, **Argon2id** (recommended — hybrid).

```javascript
const hash = await argon2.hash(password, { type: argon2.argon2id, memoryCost: 65536, timeCost: 3 });
const valid = await argon2.verify(hash, password);
```

### Q66. bcrypt vs Argon2?
**Answer:**
| | bcrypt | Argon2id |
|---|---|---|
| Age | Older, battle-tested | Modern, PHC winner |
| GPU resistance | Moderate | Strong (memory-hard) |
| Tuning | Cost factor only | Memory, time, parallelism |
| Recommendation | Still fine | Preferred for new projects |

### Q67. What NOT to use for password hashing?
**Answer:** MD5, SHA-1, SHA-256 alone (too fast — billions of guesses/sec). Use bcrypt, scrypt, or Argon2id.

### Q68. Does Better Auth hash passwords?
**Answer:** Yes. Better Auth handles password hashing internally for `emailAndPassword` auth. In Synapse AI, you enable `emailAndPassword: { enabled: true }` and Better Auth applies secure hashing — you don't implement bcrypt manually.

---

## 12. HTTPS, SSL/TLS

### Q69. What is HTTPS?
**Answer:** HTTP over TLS. Encrypts data in transit between client and server. Prevents eavesdropping, tampering, and man-in-the-middle attacks. Required for Secure cookies and production auth.

### Q70. SSL vs TLS?
**Answer:** SSL (1.0–3.0) is deprecated. **TLS** (1.2, 1.3) is the modern standard. Colloquially "SSL" still used but means TLS.

### Q71. How does TLS handshake work (simplified)?
**Answer:**
1. Client sends supported cipher suites (ClientHello).
2. Server selects cipher, sends certificate (ServerHello).
3. Client verifies certificate against trusted CAs.
4. Key exchange establishes symmetric session key.
5. Encrypted communication begins.

### Q72. What is a TLS certificate?
**Answer:** Digital document binding a public key to a domain, signed by a Certificate Authority (CA). Browsers trust pre-installed CA roots.

### Q73. Why is HTTPS critical for authentication?
**Answer:** Without HTTPS, session cookies and tokens travel in plain text — anyone on the network can steal them. `Secure` cookie flag requires HTTPS.

### Q74. HSTS?
**Answer:** HTTP Strict Transport Security — response header forcing browsers to always use HTTPS for the domain. Prevents SSL stripping attacks.

---

## 13. CORS

### Q75. What is CORS?
**Answer:** Cross-Origin Resource Sharing. Browser security mechanism controlling whether a web page from origin A can call an API on origin B. Server must explicitly allow cross-origin requests via headers.

### Q76. What is same-origin policy?
**Answer:** Browsers block JS from reading responses from a different origin (scheme + domain + port). CORS is the controlled exception.

### Q77. Key CORS headers?
**Answer:**
- `Access-Control-Allow-Origin` — allowed origin(s)
- `Access-Control-Allow-Methods` — GET, POST, etc.
- `Access-Control-Allow-Headers` — allowed request headers
- `Access-Control-Allow-Credentials` — allow cookies
- `Access-Control-Max-Age` — preflight cache duration

### Q78. What is a preflight request?
**Answer:** Browser sends `OPTIONS` request before the actual request for "non-simple" requests (custom headers, PUT/DELETE, `Content-Type: application/json`). Server must respond with allowed origins/methods.

### Q79. CORS with credentials (cookies)?
**Answer:** Set `credentials: 'include'` on fetch and `Access-Control-Allow-Credentials: true` on server. `Access-Control-Allow-Origin` cannot be `*` — must be specific origin.

### Q80. CORS vs CSRF — common confusion?
**Answer:** CORS prevents **reading** cross-origin responses in JS. It does **not** prevent the browser from **sending** requests (e.g., form POST). CSRF protection is separate.

---

## 14. CSRF

### Q81. What is CSRF?
**Answer:** Cross-Site Request Forgery. Attacker tricks a logged-in user's browser into making an unwanted authenticated request to a site where the user has an active session (cookie auto-sent).

### Q82. CSRF attack example?
**Answer:** User is logged into `bank.com`. Attacker's page contains `<img src="https://bank.com/transfer?to=attacker&amount=1000">`. Browser sends the session cookie; bank processes the transfer.

### Q83. CSRF prevention methods?
**Answer:**
1. **CSRF tokens** — unpredictable token in form/header, validated server-side
2. **SameSite cookies** — `Strict` or `Lax` limits cross-site cookie sending
3. **Check Origin/Referer** headers
4. **Custom headers** — `X-Requested-With` or `Authorization` header (not sent by simple cross-site forms)
5. **Re-authentication** for sensitive actions

### Q84. SameSite=Lax vs CSRF?
**Answer:** `Lax` blocks cookies on cross-site POST but allows top-level GET navigation. Stops most CSRF but not all edge cases. Use CSRF tokens for state-changing operations.

### Q85. Do JWT in Authorization header prevent CSRF?
**Answer:** Yes, if the token is **not** in a cookie. CSRF exploits automatic cookie sending. Bearer tokens in headers must be set by JS, which cross-origin attackers cannot do (due to CORS). But cookie-stored JWTs still need CSRF protection.

---

## 15. XSS

### Q86. What is XSS?
**Answer:** Cross-Site Scripting. Injecting malicious JavaScript into a page viewed by other users. Types: Stored, Reflected, DOM-based.

### Q87. XSS types?
**Answer:**
- **Stored** — script saved in DB (comment, profile), served to all viewers
- **Reflected** — script in URL/input reflected in response (search query)
- **DOM-based** — client-side JS writes untrusted input to DOM unsafely

### Q88. XSS impact on authentication?
**Answer:** Attacker JS can steal tokens from localStorage, read non-HttpOnly cookies, perform actions as the user, keylog passwords. **HttpOnly cookies** prevent JS token theft.

### Q89. XSS prevention?
**Answer:**
- Output encoding/escaping (HTML, JS, URL context)
- Content Security Policy (CSP)
- HttpOnly cookies for session tokens
- Input validation and sanitization (DOMPurify for HTML)
- Avoid `dangerouslySetInnerHTML` without sanitization
- Use framework auto-escaping (React escapes by default)

### Q90. CSP's role against XSS?
**Answer:** CSP restricts which scripts can run. `script-src 'self'` blocks injected inline scripts. See [Clickjacking & CSP](#17-clickjacking--csp).

---

## 16. SQL Injection

### Q91. What is SQL Injection?
**Answer:** Attacker injects malicious SQL through user input, altering query logic. Can read, modify, or delete data, or bypass authentication.

### Q92. SQL Injection example?
**Answer:**
```sql
-- Login query
SELECT * FROM users WHERE email = '$input' AND password = '$hash'

-- Input: ' OR '1'='1' --
-- Becomes:
SELECT * FROM users WHERE email = '' OR '1'='1' --' AND password = ''
-- Returns all users; login bypassed
```

### Q93. SQL Injection prevention?
**Answer:**
1. **Parameterized queries / prepared statements** (primary defense)
2. ORM with parameter binding (Prisma, Drizzle — used in Synapse AI)
3. Input validation (whitelist, type checking)
4. Least privilege DB accounts (no DROP/GRANT for app user)
5. Never concatenate user input into SQL strings

### Q94. NoSQL Injection?
**Answer:** Manipulating query objects in MongoDB etc. Example: `{ "username": { "$gt": "" }, "password": { "$gt": "" } }`. Prevent with schema validation, type casting, and avoiding direct object injection from user input.

---

## 17. Clickjacking & CSP

### Q95. What is clickjacking?
**Answer:** Attacker embeds your site in a transparent iframe, overlaying deceptive UI. User thinks they click "Win a prize" but actually clicks "Delete account" on your site.

### Q96. Clickjacking prevention?
**Answer:**
- `X-Frame-Options: DENY` or `SAMEORIGIN`
- `Content-Security-Policy: frame-ancestors 'none'` (modern replacement)
- JavaScript frame-busting (less reliable)

### Q97. What is CSP (Content Security Policy)?
**Answer:** HTTP header defining allowed sources for scripts, styles, images, frames, etc. Primary defense against XSS and data injection.

### Q98. Common CSP directives?
**Answer:**
```
Content-Security-Policy:
  default-src 'self';
  script-src 'self' https://cdn.example.com;
  style-src 'self' 'unsafe-inline';
  img-src 'self' data: https:;
  frame-ancestors 'none';
  upgrade-insecure-requests;
```

### Q99. CSP `'unsafe-inline'` and `'unsafe-eval'`?
**Answer:** Allow inline scripts and `eval()`. Weakens CSP significantly. Prefer nonces (`script-src 'nonce-abc123'`) or hashes for inline scripts.

### Q100. CSP report-only mode?
**Answer:** `Content-Security-Policy-Report-Only` logs violations without blocking. Use to test policy before enforcing.

---

## 18. Cookie Security (SameSite, Secure, HttpOnly)

### Q101. HttpOnly cookies?
**Answer:** Cookie flag preventing JavaScript access (`document.cookie`). Mitigates XSS token theft. **Always set for session/auth cookies.**

### Q102. Secure cookies?
**Answer:** Cookie only sent over HTTPS connections. Prevents transmission over unencrypted HTTP. **Required in production for auth cookies.**

### Q103. SameSite attribute?
**Answer:** Controls cross-site cookie sending:
| Value | Behavior |
|---|---|
| `Strict` | Never sent on cross-site requests |
| `Lax` | Sent on top-level GET navigation only (default in modern browsers) |
| `None` | Sent on all cross-site requests — **requires Secure** |

### Q104. When to use SameSite=None?
**Answer:** Cross-site contexts: embedded widgets, OAuth redirects across domains, payment iframes. Must pair with `Secure` flag.

### Q105. Production cookie recipe for auth?
**Answer:**
```
Set-Cookie: session=abc123;
  HttpOnly;
  Secure;
  SameSite=Lax;
  Path=/;
  Max-Age=604800
```

Better Auth sets these attributes automatically on session cookies in Synapse AI.

---

## 19. API Security

### Q106. Key API security practices?
**Answer:**
- Authentication on every protected endpoint
- Authorization checks per resource (not just route)
- Input validation and schema validation (Zod)
- Rate limiting
- HTTPS only
- No sensitive data in URLs
- Proper error messages (no stack traces in production)
- API versioning
- Audit logging

### Q107. API keys vs JWT?
**Answer:**
| | API Key | JWT |
|---|---|---|
| Use | Service-to-service, public APIs | User sessions, microservices |
| Revocation | Delete key | Short expiry + refresh / blocklist |
| Identity | Identifies application | Identifies user + claims |
| Storage | Server env vars | HttpOnly cookie or header |

### Q108. How to secure REST APIs?
**Answer:** OAuth 2.0 / JWT auth, HTTPS, rate limiting, input validation, CORS configured correctly, pagination limits, idempotency keys for writes, webhook signature verification.

### Q109. What is BOLA/IDOR?
**Answer:** Broken Object Level Authorization / Insecure Direct Object Reference. User changes `GET /api/orders/123` to `124` and accesses another user's order. Fix: always verify `order.userId === req.user.id` server-side.

### Q110. GraphQL-specific security?
**Answer:** Query depth limiting, complexity analysis, disable introspection in production, authorization per resolver, rate limiting.

---

## 20. OWASP Top 10

### Q111. What is OWASP Top 10?
**Answer:** OWASP's list of the most critical web application security risks. Updated periodically (2021 version widely referenced).

### Q112. OWASP Top 10 (2021)?
**Answer:**
1. **A01 — Broken Access Control** — IDOR, missing authorization, CORS misconfig
2. **A02 — Cryptographic Failures** — weak encryption, plaintext sensitive data
3. **A03 — Injection** — SQL, NoSQL, OS, LDAP injection
4. **A04 — Insecure Design** — missing threat modeling, flawed architecture
5. **A05 — Security Misconfiguration** — default creds, verbose errors, open cloud storage
6. **A06 — Vulnerable Components** — outdated dependencies
7. **A07 — Auth Failures** — weak passwords, session issues, credential stuffing
8. **A08 — Data Integrity Failures** — insecure deserialization, unsigned CI/CD updates
9. **A09 — Logging & Monitoring Failures** — no audit trail, no alerting
10. **A10 — SSRF** — Server-Side Request Forgery

### Q113. How to discuss OWASP in interviews?
**Answer:** Pick 2–3 relevant items, explain the risk, give a real mitigation from your experience. Example: "In Synapse AI, we prevented A07 by using Better Auth's database sessions with HttpOnly cookies and server-side session validation in layouts."

---

## 21. Security Headers & Helmet

### Q114. Important security headers?
**Answer:**
| Header | Purpose |
|---|---|
| `Strict-Transport-Security` | Force HTTPS |
| `Content-Security-Policy` | XSS/injection mitigation |
| `X-Content-Type-Options: nosniff` | Prevent MIME sniffing |
| `X-Frame-Options` / `frame-ancestors` | Clickjacking prevention |
| `Referrer-Policy` | Control referrer leakage |
| `Permissions-Policy` | Restrict browser features (camera, geolocation) |
| `Cross-Origin-Opener-Policy` | Isolate browsing context |
| `Cross-Origin-Resource-Policy` | Control cross-origin resource loading |

### Q115. What is Helmet?
**Answer:** Express/Node middleware that sets secure HTTP headers with sensible defaults.

```javascript
import helmet from 'helmet';
app.use(helmet());
// Sets CSP, HSTS, X-Frame-Options, etc.
```

### Q116. Helmet in Next.js?
**Answer:** Next.js doesn't use Helmet directly but you can set headers in `next.config.js`:

```javascript
// next.config.js
headers: async () => [{
  source: '/(.*)',
  headers: [
    { key: 'X-Frame-Options', value: 'DENY' },
    { key: 'X-Content-Type-Options', value: 'nosniff' },
    { key: 'Referrer-Policy', value: 'strict-origin-when-cross-origin' },
  ],
}]
```

---

## 22. Rate Limiting

### Q117. What is rate limiting?
**Answer:** Restricting the number of requests a client can make in a time window. Prevents brute-force, DDoS, API abuse, credential stuffing.

### Q118. Rate limiting strategies?
**Answer:**
- **Fixed window** — N requests per minute
- **Sliding window** — smoother, rolling count
- **Token bucket** — burst allowed, steady rate
- **Leaky bucket** — queue requests at fixed rate

### Q119. Rate limiting implementations?
**Answer:**
- **express-rate-limit** — in-memory or Redis store
- **Redis + sliding window** — distributed apps
- **API Gateway / CDN** — Cloudflare, AWS WAF, Nginx `limit_req`
- **Better Auth** — built-in rate limiting on auth endpoints

### Q120. What to rate limit?
**Answer:** Login, signup, password reset, OTP send, API endpoints, file uploads. Return `429 Too Many Requests` with `Retry-After` header.

```javascript
import rateLimit from 'express-rate-limit';
const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 5,
  message: 'Too many login attempts',
});
app.post('/login', loginLimiter, loginHandler);
```

---

## 23. Secure Authentication Flow

### Q121. Secure login flow (email/password)?
**Answer:**
1. Client sends credentials over HTTPS
2. Server rate-limits the endpoint
3. Server looks up user by email (constant-time compare to prevent timing attacks)
4. Server verifies password with bcrypt/Argon2
5. Server regenerates session ID (prevent fixation)
6. Server sets HttpOnly, Secure, SameSite cookie
7. Server returns minimal user data (no sensitive fields)
8. Log auth events (success/failure, IP, user agent)

### Q122. Secure signup flow?
**Answer:** Validate email format, enforce password strength, hash password, send email verification link, rate limit signups, prevent user enumeration (same response for existing/non-existing email).

### Q123. Secure password reset flow?
**Answer:**
1. User requests reset with email
2. Same generic response regardless of email existence (prevent enumeration)
3. Generate cryptographically random single-use token with short expiry
4. Send link via email (HTTPS)
5. On click, validate token, allow new password, invalidate all sessions
6. Rate limit reset requests

### Q124. Secure logout flow?
**Answer:** Delete server-side session (DB row), clear auth cookie (`Max-Age=0`), optionally invalidate refresh tokens. Client clears local state.

### Q125. Email verification — why?
**Answer:** Confirms user owns the email. Prevents fake accounts, enables password reset, reduces spam. Better Auth supports `requireEmailVerification: true` in production.

### Q126. Multi-factor authentication (MFA)?
**Answer:** Second factor after password — TOTP (Google Authenticator), SMS (less secure), WebAuthn/FIDO2 (most secure). Better Auth offers 2FA via plugins.

---

## 24. Better Auth (Synapse AI)

### Q127. What is Better Auth?
**Answer:** TypeScript-first, framework-agnostic authentication library (Next.js, Express, etc.). Self-hosted, database-backed, plugin ecosystem for 2FA, organizations, passkeys, and more. Used in the **Synapse AI** project.

### Q128. Why Better Auth over Auth.js/NextAuth?
**Answer:**
- Automatic TypeScript inference (`auth.$Infer.Session`) — no manual type augmentation
- Database-backed sessions with immediate revocation
- Code-first plugin model
- Self-hosted, no per-user pricing
- Built-in email/password + OAuth with minimal config

### Q129. Better Auth core setup (Synapse AI pattern)?
**Answer:**
```typescript
// lib/auth.ts
import { betterAuth } from 'better-auth';
import { drizzleAdapter } from 'better-auth/adapters/drizzle';
import { db } from '@/lib/db';

export const auth = betterAuth({
  database: drizzleAdapter(db, { provider: 'pg' }),
  emailAndPassword: {
    enabled: true,
    requireEmailVerification: true, // production
  },
  socialProviders: {
    google: {
      clientId: process.env.GOOGLE_CLIENT_ID!,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET!,
    },
  },
  session: {
    expiresIn: 60 * 60 * 24 * 7,  // 7 days
    updateAge: 60 * 60 * 24,       // refresh every 24h
  },
});

export type Session = typeof auth.$Infer.Session;
```

### Q130. Better Auth API route handler?
**Answer:**
```typescript
// app/api/auth/[...all]/route.ts
import { auth } from '@/lib/auth';
import { toNextJsHandler } from 'better-auth/next-js';

export const { GET, POST } = toNextJsHandler(auth);
```

### Q131. Reading session on the server (Synapse AI)?
**Answer:**
```typescript
// Server Component / Route Handler
import { auth } from '@/lib/auth';
import { headers } from 'next/headers';

const session = await auth.api.getSession({
  headers: await headers(),
});

if (!session) redirect('/login');
```

### Q132. Reading session on the client?
**Answer:**
```typescript
// Client Component
import { authClient } from '@/lib/auth-client';

const { data: session, isPending } = authClient.useSession();
```

### Q133. Better Auth middleware pattern?
**Answer:** Middleware can check cookie **existence** for optimistic redirects (fast UX). **Actual session validation** must happen server-side via `getSession()` — Better Auth docs warn cookie-only checks are NOT secure for authorization.

```typescript
// middleware.ts — optimistic redirect only
import { getSessionCookie } from 'better-auth/cookies';

export function middleware(request) {
  const sessionCookie = getSessionCookie(request);
  if (!sessionCookie && isProtectedRoute(request)) {
    return NextResponse.redirect(new URL('/login', request.url));
  }
}
```

### Q134. Better Auth `nextCookies()` plugin?
**Answer:** Required for Server Actions in Next.js. Without it, auth functions in Server Actions silently fail to set cookies because Next.js requires cookies through its own `cookies()` API.

### Q135. Better Auth session revocation?
**Answer:** Delete session row in DB → immediate logout everywhere that session is used. Supports revoking single session or all user sessions. Critical for "log out all devices."

### Q136. Better Auth plugins used in production?
**Answer:** `twoFactor`, `organization` (multi-tenant), `passkey`, `jwt` (for external service interop), `customSession` (extend session data), `admin` (user management).

### Q137. Interview answer: "How did you implement auth in Synapse AI?"
**Answer:** "We used Better Auth with Drizzle ORM and PostgreSQL. Email/password and Google OAuth for login. Sessions are database-backed with HttpOnly cookies. Server Components call `auth.api.getSession()` for real authorization; middleware only does optimistic redirects. Email verification enabled in production. Type-safe sessions inferred from config — no manual JWT parsing or type augmentation."

---

## 25. Best Practices

### Q138. Authentication best practices checklist?
**Answer:**
- [ ] HTTPS everywhere
- [ ] Hash passwords with Argon2id or bcrypt (cost ≥ 12)
- [ ] HttpOnly + Secure + SameSite cookies for sessions
- [ ] Short-lived access tokens; rotate refresh tokens
- [ ] Server-side authorization on every protected resource
- [ ] Rate limit auth endpoints
- [ ] MFA for sensitive accounts
- [ ] Email verification
- [ ] Secure password reset (single-use, short-lived tokens)
- [ ] Regenerate session ID on login
- [ ] Log auth events; alert on anomalies
- [ ] Keep dependencies updated
- [ ] Never log passwords or tokens
- [ ] Environment variables for secrets (never commit)
- [ ] Principle of least privilege

### Q139. Secrets management?
**Answer:** Use environment variables, secret managers (AWS Secrets Manager, Vault). Rotate secrets periodically. Different secrets per environment. `AUTH_SECRET` in Better Auth must be strong and unique per deployment.

### Q140. User enumeration prevention?
**Answer:** Same error message for "wrong email" and "wrong password". Same response time (constant-time). Password reset: "If account exists, email sent."

### Q141. Timing attacks on login?
**Answer:** Always run password hash comparison even if user not found (compare against dummy hash) so response time doesn't reveal user existence.

---

## 26. Common Vulnerabilities

### Q142. Summary of common web vulnerabilities?
**Answer:**
| Vulnerability | Attack | Primary Defense |
|---|---|---|
| XSS | Inject JS | Escape output, CSP, HttpOnly cookies |
| CSRF | Forge requests | CSRF tokens, SameSite cookies |
| SQL Injection | Inject SQL | Parameterized queries, ORM |
| Broken Auth | Session/token theft | HTTPS, HttpOnly, server validation |
| IDOR | Access others' data | Server-side ownership checks |
| Clickjacking | Hidden iframe | X-Frame-Options, CSP frame-ancestors |
| Open Redirect | Phishing via redirect | Whitelist redirect URLs |
| SSRF | Server fetches internal URLs | Validate/block internal IPs |
| Mass Assignment | Set unintended fields | Allowlist DTO fields |
| Insecure Deserialization | Malicious object payloads | Don't deserialize untrusted data |

### Q143. What is an open redirect vulnerability?
**Answer:** `https://yoursite.com/login?redirect=https://evil.com` — after login, user sent to attacker's site. Fix: whitelist allowed redirect paths.

### Q144. What is SSRF?
**Answer:** Server-Side Request Forgery. Attacker makes server fetch internal URLs (`http://169.254.169.254/` — cloud metadata). Fix: validate URLs, block private IP ranges, use allowlists.

### Q145. What is mass assignment?
**Answer:** Sending extra fields in request body (`{ "name": "John", "role": "admin" }`). Fix: allowlist permitted fields in DTOs; never bind raw request body to DB model.

---

## 27. Production Security

### Q146. Production security checklist?
**Answer:**
- [ ] TLS 1.2+ only; valid certificates; HSTS enabled
- [ ] Security headers (CSP, X-Frame-Options, etc.)
- [ ] Rate limiting on all public endpoints
- [ ] WAF / DDoS protection (Cloudflare, AWS Shield)
- [ ] Dependency scanning (npm audit, Snyk, Dependabot)
- [ ] No debug mode in production
- [ ] Structured logging + monitoring (failed logins, 4xx/5xx spikes)
- [ ] Database backups encrypted
- [ ] CI/CD secrets not in repo
- [ ] Penetration testing / security review before launch
- [ ] Incident response plan
- [ ] GDPR/privacy compliance (data retention, right to deletion)

### Q147. How to handle a credential breach?
**Answer:** Force password reset for affected users, invalidate all sessions, notify users, rotate secrets, audit logs for suspicious activity, report per regulations (GDPR 72 hours).

### Q148. Environment separation?
**Answer:** Separate databases, secrets, and OAuth apps for dev/staging/production. Never use production credentials in development.

### Q149. Logging security events?
**Answer:** Log login success/failure, password changes, permission changes, admin actions. **Never log** passwords, tokens, or PII unnecessarily. Use structured JSON logs.

---

## 28. Scenario Questions

### S1. User reports they were logged out unexpectedly. How do you investigate?
**Answer:** Check session expiry settings (`expiresIn`, `updateAge` in Better Auth). Check if session was revoked (password change revokes all sessions). Check cookie attributes (Secure flag failing on HTTP?). Check if multiple tabs caused race condition. Review server logs for session errors.

### S2. How would you implement "Remember Me"?
**Answer:** Issue a long-lived refresh token or extend session `Max-Age` in a separate HttpOnly cookie. On return visit, silently refresh the session. Still require re-auth for sensitive actions. Rotate token on use.

### S3. SPA with JWT — where do you store the token?
**Answer:** Prefer HttpOnly cookie (with CSRF protection via SameSite + CSRF token or double-submit cookie). If using Authorization header, accept XSS risk or use short-lived token + strict CSP. Never localStorage for long-lived tokens.

### S4. How do you protect an API used by both web app and mobile app?
**Answer:** Web: HttpOnly cookie sessions. Mobile: short-lived access token + refresh token in secure storage. Shared backend validates both. OAuth 2.0 with PKCE for mobile. Rate limiting per client type.

### S5. Attacker stole a JWT. What do you do?
**Answer:** If short-lived: wait for expiry. Immediate: add token `jti` to blocklist (Redis), rotate signing secret (invalidates all tokens — nuclear option), force user re-login, invalidate refresh tokens. Prevention: short expiry, HttpOnly cookies, rotation.

### S6. How to implement role-based access in Next.js App Router?
**Answer:** In Synapse AI: extend session with role via `customSession` plugin. In protected layouts, call `auth.api.getSession()`, check `session.user.role`, redirect or return 403. Never rely on middleware alone or client-side role checks.

### S7. OAuth login works locally but fails in production. Why?
**Answer:** Redirect URI mismatch (must match exactly in OAuth app settings). `http` vs `https`. Wrong `client_id`/`client_secret` env vars. Cookie `Secure` flag on HTTP staging. CORS misconfiguration.

### S8. How to prevent password reset token reuse?
**Answer:** Single-use tokens stored hashed in DB. Delete token after use. Short expiry (15–60 min). Invalidate all sessions on password change.

### S9. Design auth for a multi-tenant SaaS (Synapse AI context).
**Answer:** Better Auth `organization` plugin for tenants. Every DB query scoped by `organizationId`. RBAC per org (owner, member). Session includes active org. Middleware/layout checks org membership before data access.

### S10. How do you test authentication security?
**Answer:** Unit tests for auth logic. Integration tests for login/logout flows. Test expired sessions, invalid tokens, IDOR attempts. OWASP ZAP or Burp Suite for penetration testing. Test rate limiting triggers 429.

### S11. Customer wants SSO with their corporate IdP.
**Answer:** Implement SAML or OIDC as Service Provider. Better Auth or dedicated IdP library. Map IdP claims to local user/roles. Just-in-time provisioning. Test SLO (Single Logout).

### S12. API returns 401 vs 403 — when to use which?
**Answer:**
- **401 Unauthorized** — not authenticated (missing/invalid token). Client should login.
- **403 Forbidden** — authenticated but not permitted. Client should not retry without different permissions.

---

## 29. Cheat Sheet

### Auth Concepts
| Term | One-liner |
|---|---|
| Authentication | Who are you? |
| Authorization | What can you do? |
| Session | Server-side auth state + cookie ID |
| JWT | Signed self-contained token |
| Access Token | Short-lived API access |
| Refresh Token | Long-lived token renewal |
| OAuth 2.0 | Delegated authorization framework |
| OIDC | Authentication layer on OAuth (ID Token) |
| SSO | One login, many apps |
| RBAC | Permissions via roles |
| ABAC | Permissions via attribute policies |
| MFA/2FA | Two+ auth factors |

### Cookie Flags
| Flag | Effect |
|---|---|
| `HttpOnly` | No JS access — anti-XSS theft |
| `Secure` | HTTPS only |
| `SameSite=Strict` | No cross-site send |
| `SameSite=Lax` | Cross-site GET only (default) |
| `SameSite=None` | All cross-site (needs Secure) |

### HTTP Status Codes (Auth)
| Code | Meaning |
|---|---|
| 401 | Not authenticated |
| 403 | Authenticated, not authorized |
| 429 | Rate limited |

### Hashing
| Algorithm | Use |
|---|---|
| bcrypt | Password hashing (cost 10–12) |
| Argon2id | Preferred password hashing |
| SHA-256 | **Not** for passwords — use for checksums |
| HMAC | Message authentication with secret |

### TLS
| Term | Meaning |
|---|---|
| HTTPS | HTTP + TLS encryption |
| TLS 1.3 | Current standard |
| HSTS | Force HTTPS via header |
| Certificate | Binds domain to public key |

### Attacks & Defenses
| Attack | Defense |
|---|---|
| XSS | Escape, CSP, HttpOnly cookies |
| CSRF | CSRF token, SameSite, custom headers |
| SQLi | Parameterized queries, ORM |
| Clickjacking | X-Frame-Options, CSP frame-ancestors |
| Brute force | Rate limit, bcrypt, MFA |
| Session hijack | HTTPS, HttpOnly, regenerate on login |
| IDOR | Server-side ownership check |
| Credential stuffing | MFA, rate limit, breach detection |

### OAuth 2.0 Grants (Quick)
| Grant | When |
|---|---|
| Auth Code + PKCE | SPAs, mobile, web apps ✅ |
| Client Credentials | Machine-to-machine |
| Refresh Token | Renew access token |
| Implicit | ❌ Deprecated |
| Password (ROPC) | ❌ Avoid |

### Security Headers (Quick)
```
Strict-Transport-Security: max-age=31536000; includeSubDomains
Content-Security-Policy: default-src 'self'; frame-ancestors 'none'
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=()
```

### Better Auth Quick Reference (Synapse AI)
```typescript
// Server session check
const session = await auth.api.getSession({ headers: await headers() });

// Client session hook
const { data: session } = authClient.useSession();

// Sign out
await authClient.signOut();

// Route handler
export const { GET, POST } = toNextJsHandler(auth);

// Middleware (optimistic only — not security boundary)
const cookie = getSessionCookie(request);
```

### OWASP Top 10 (2021) — One Line Each
1. Broken Access Control
2. Cryptographic Failures
3. Injection
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable Components
7. Auth Failures
8. Data Integrity Failures
9. Logging Failures
10. SSRF

### Production Auth Recipe
```
HTTPS → Rate Limit → Validate Input → Hash Password (Argon2id)
→ DB Session → HttpOnly+Secure+SameSite Cookie
→ Server-side getSession() → Authorization Check → Audit Log
```

### JWT Claims (Common)
| Claim | Meaning |
|---|---|
| `sub` | Subject (user ID) |
| `iss` | Issuer |
| `aud` | Audience |
| `exp` | Expiration (Unix timestamp) |
| `iat` | Issued at |
| `jti` | JWT ID (for revocation) |

### Interview Power Phrases
- "Authentication verifies identity; authorization verifies permissions."
- "Never trust the client — enforce auth server-side."
- "HttpOnly cookies prevent XSS token theft."
- "CSRF exploits automatic cookie sending; Bearer tokens in headers are CSRF-immune but XSS-vulnerable."
- "Parameterized queries are the primary SQL injection defense."
- "In Synapse AI, Better Auth gives us DB-backed sessions with immediate revocation and type-safe session inference."
- "Middleware cookie checks are UX only; `getSession()` is the security boundary."

---

*Last updated: June 2026 — covers OWASP Top 10 2021, Better Auth v1.x patterns, TLS 1.3, modern browser SameSite defaults.*

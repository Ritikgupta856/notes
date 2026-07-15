# Projects & Resume — Interview Preparation Guide

> Tailored for **Ritik Gupta** — Software Engineer @ STARTWITH BASICX PVT. LTD.  
> Portfolio: [ritikgupta.in](https://ritikgupta.in) | GitHub: [Ritikgupta856](https://github.com/Ritikgupta856)

---

## Table of Contents

1. [Tell Me About Yourself](#1-tell-me-about-yourself)
2. [Resume Walkthrough](#2-resume-walkthrough)
3. [STAR Method](#3-star-method)
4. [STARTWITH BASICX — Work Experience](#4-startwith-basicx--work-experience)
5. [Synapse AI](#5-synapse-ai)
6. [ShopCart](#6-shopcart)
7. [Cross-Project Architecture Questions](#7-cross-project-architecture-questions)
8. [Challenges & Debugging Stories](#8-challenges--debugging-stories)
9. [Optimizations You Can Talk About](#9-optimizations-you-can-talk-about)
10. [Leadership & Teamwork](#10-leadership--teamwork)
11. [Production & Deployment](#11-production--deployment)
12. [CI/CD Stories](#12-cicd-stories)
13. [Resume Tips & Mistakes](#13-resume-tips--mistakes)
14. [Scenario Questions](#14-scenario-questions)
15. [Quick Cheat Sheet](#15-quick-cheat-sheet)

---

## 1. Tell Me About Yourself

### 60-Second Version (Use in Most Interviews)

> "I'm Ritik Gupta, a Software Engineer with a BSc in Computer Science from Manipal University Jaipur. For the past year at STARTWITH BASICX, I've been building production full-stack applications — a meal planning platform, a multi-organization admin dashboard, a Next.js e-commerce store, and a document processing system using RabbitMQ and LLMs.
>
> Outside work, I built Synapse AI, an AI-powered workspace with RAG chat, and ShopCart, a full e-commerce platform deployed on AWS with Docker and CI/CD.
>
> I'm strongest in the React/Next.js and Node.js ecosystem, with hands-on experience in TypeScript, Prisma, Zustand, RabbitMQ, Docker, and cloud deployment. I'm now looking for a role where I can build scalable products end-to-end."

### 90-Second Version (Technical / Full-Stack Roles)

Add after the above:

> "On the technical side, I care about clean architecture — I introduced RabbitMQ for async LLM processing at BASICX, set up CI/CD with GitHub Actions and Docker on AWS for ShopCart, and built a full RAG pipeline with pgvector for Synapse AI."

### Tips

- Lead with current role
- End with what you want
- Don't recite resume bullet-by-bullet — tell a story

---

## 2. Resume Walkthrough

### Q: Walk me through your resume.

**Structure (2–3 minutes):**

1. **Summary** — full-stack engineer, 1+ year, React/Node/TypeScript
2. **Current role** — BASICX, May 2024–Present. Four products built end-to-end.
3. **Projects** — Synapse AI (AI workspace), ShopCart (e-commerce with cloud deployment)
4. **Skills** — Full-stack JS/TS, React/Next.js, Node, SQL + NoSQL, AWS, Docker, CI/CD

### Q: Why is your experience section stronger than projects?

**Answer:** "My professional work at BASICX involves real users, production constraints, and business requirements. My personal projects prove I can own the full lifecycle independently — from auth to deployment on AWS with CI/CD."

### Q: You have MongoDB and MySQL — when did you use which?

| Project / Work | Database | Why |
|----------------|----------|-----|
| Admin Dashboard (BASICX) | MySQL | Relational data — orgs, members, tournaments, settlements |
| Meal Planning App | MySQL/Relational | Users, meals, subscriptions |
| ShopCart | MongoDB | Products, orders, cart |
| Synapse AI | PostgreSQL + Prisma | Relational + vector embeddings for RAG |

---

## 3. STAR Method

Use for behavioral + technical "tell me about a challenge" questions.

| Letter | Meaning | Your Example Hook |
|--------|---------|-------------------|
| **S** | Situation | "At BASICX, document processing was blocking the UI…" |
| **T** | Task | "I needed to decouple LLM calls from the request cycle." |
| **A** | Action | "I introduced RabbitMQ — producer on Node.js, Python consumer for LLM, ack/retry on failure." |
| **R** | Result | "UI stayed responsive; concurrent processing became possible; failures handled automatically." |

### Ready-Made STAR Stories from Your Resume

1. **RabbitMQ + LLM document processing** (async decoupling)
2. **Next.js SSR + Zustand jewelry platform** (performance)
3. **ShopCart AWS + Docker + CI/CD** (production deployment)
4. **Meal app with i18n + payments + JWT** (production launch)
5. **Multi-org admin dashboard** (complex domain modeling in MySQL)

---

## 4. STARTWITH BASICX — Work Experience

### 4.1 Meal Planning Application

**Stack:** React.js, TypeScript, Node.js, REST APIs, JWT, i18n, Payments

**Status:** ✅ In production — 1,000+ active users

#### What It Is (Explain in 30 sec)

A scalable meal planning product for end users — plan meals, multi-language support, secure payments, authenticated via JWT.

#### Likely Interview Questions

| # | Question | How to Answer |
|---|----------|---------------|
| 1 | How did you handle authentication? | JWT access tokens in Authorization header; refresh token strategy; password hashing on server; protected routes on frontend via auth context |
| 2 | How does i18n work? | `react-i18next` — JSON locale files, `useTranslation()`, language switcher, lazy-load locale bundles |
| 3 | How did you serve 1,000+ users? | Stateless API (horizontal scale), DB indexing on frequent queries, pagination, CDN for static assets, connection pooling |
| 4 | Payment integration flow? | Create order on backend → call payment gateway → webhook verifies signature → update subscription status idempotently |
| 5 | REST API design? | Resource-based URLs (`/meals`, `/plans`, `/users`), proper HTTP methods, versioning (`/api/v1`), consistent error format |
| 6 | TypeScript benefits you saw? | Catch API contract mismatches early, typed props/state, better refactoring |
| 7 | How do you prevent duplicate payments? | Idempotent webhook handling with payment ID unique constraint; status checks before state transition |

---

### 4.2 Admin Dashboard (Multi-Organization)

**Stack:** React.js, Node.js, MySQL

**Status:** 🟡 In development

#### What It Is

Internal/admin tool for BASICX sports operations — manage organizations, members, tournaments, financial settlements, subscriptions.

#### Likely Interview Questions

| # | Question | How to Answer |
|---|----------|---------------|
| 1 | How did you model multi-tenancy? | `organization_id` on every tenant-scoped table; middleware injects org context from JWT |
| 2 | RBAC — how did roles work? | Roles: admin, org owner, member; permission checks on API layer; UI hides actions user can't perform |
| 3 | Tournament management — data model? | Tournaments → Teams → Matches → Scores; foreign keys; status enums |
| 4 | Financial settlements? | Transaction ledger table; audit trail; sum validation; export/reporting queries with indexes |
| 5 | Why MySQL? | Strong ACID for money-related data; JOINs for reports across members, tournaments, payments |
| 6 | How prevent cross-org data leak? | Row-level filtering: `WHERE organization_id = :currentOrg` on every query |
| 7 | Large table performance? | Indexes on FK columns; pagination; avoid `SELECT *`; explain plan on slow reports |

---

### 4.3 Jewelry E-Commerce Platform

**Stack:** Next.js (SSR), Razorpay, Strapi CMS, Zustand

**Status:** 🟡 Built — on hold by management

#### What It Is

Full-stack jewelry e-commerce — product catalog from headless CMS, SSR for SEO and performance, Razorpay checkout, Zustand for cart/UI state.

#### Likely Interview Questions

| # | Question | How to Answer |
|---|----------|---------------|
| 1 | Why Next.js SSR over CSR? | SEO for product pages, faster FCP/LCP, social sharing meta tags |
| 2 | How did you optimize performance? | SSR + image optimization + code splitting + Zustand (lighter than Redux) + caching Strapi responses |
| 3 | Why Strapi headless CMS? | Marketing team edits products without deploys; API-driven; separates content from code |
| 4 | Why Zustand over Redux/Context? | Minimal boilerplate, no Provider wrapping, selective subscriptions prevent re-renders |
| 5 | Razorpay integration? | Server creates order → client opens Razorpay → webhook confirms → order status updated |
| 6 | Cart persistence? | Zustand + `persist` middleware to localStorage; merge on login with server cart |

---

### 4.4 Document Processing Application (LLM + RabbitMQ)

**Stack:** React.js, Node.js, Python LLM services, RabbitMQ

**Status:** ✅ Built and delivered — client left the company

#### What It Is

Upload documents → async processing via RabbitMQ → Python LLM extracts structured data → JSON converted to dynamic forms → split-view UI for analysis.

#### Likely Interview Questions

| # | Question | How to Answer |
|---|----------|---------------|
| 1 | Why RabbitMQ instead of synchronous API call? | LLM calls take 10–60+ seconds; blocking HTTP times out; queue decouples producer from consumer; enables retry and scale |
| 2 | Explain the message flow | React uploads → Node API publishes job to queue → Python worker consumes → LLM processes → result stored → Node notifies client |
| 3 | How did async processing improve things? | UI stays responsive; workers can process multiple documents concurrently; failed jobs retry automatically |
| 4 | Message acknowledgement? | Manual ack after successful LLM + DB write; nack + requeue on transient failure; DLQ after max retries |
| 5 | Why Python for LLM? | Better ML/LLM ecosystem (LangChain, etc.); Node stays thin API layer |
| 6 | JSON-to-form conversion? | Parse LLM JSON schema → map field types to form components → React Hook Form + Zod validation |
| 7 | Split-view UI? | Left: original document; Right: extracted fields form; status indicator while processing |
| 8 | Failure handling? | Dead letter queue; retry with exponential backoff; show user-friendly error + retry button |
| 9 | RabbitMQ vs Kafka here? | RabbitMQ — task queue pattern, moderate throughput, easier ops for this scale |

#### STAR Story (Memorize This)

> **S:** Document uploads blocked the UI for 30–60 seconds while LLM processed synchronously.  
> **T:** Make processing async and improve UX without losing reliability.  
> **A:** Introduced RabbitMQ — Node.js publishes jobs, Python workers run LLM, manual ack, DLQ for failures, split-view UI with status updates.  
> **R:** UI stayed responsive; system handles concurrent uploads; failed jobs retry automatically.

---

## 5. Synapse AI

**Stack:** Next.js 16, React 19, TypeScript, Prisma, PostgreSQL, Better Auth, Zustand, TanStack Query, AI SDK v6, Razorpay  
**Links:** [GitHub](https://github.com/Ritikgupta856/ai-workspace) | [Live](https://synapse-sigma-ten.vercel.app)

### Elevator Pitch

> "Synapse is an AI-powered workspace platform — team workspaces, AI chat with document citations, RAG over integrated docs from GitHub/Linear/Notion/Slack, AI-generated tasks, and automated workflows. Built with Next.js 16, AI SDK, PostgreSQL with vector embeddings, and Better Auth."

### Key Features

| Feature | Tech |
|---------|------|
| Multi-tenant workspaces | Prisma `Workspace`, `WorkspaceMember`, roles |
| AI chat with citations | AI SDK streaming, `Message.citations` JSON |
| Document RAG | `Document.embedding` vector column in PostgreSQL (pgvector) |
| Integrations | GitHub, Linear, Notion, Slack — sync docs into workspace |
| AI-generated tasks | Task model with `generatedByAI`, `sourceRef` |
| Auth | Better Auth — DB sessions, OAuth, email/password |
| State | Zustand (client UI) + TanStack Query (server state) |
| Payments | Razorpay |

### Likely Interview Questions

| # | Question | How to Answer |
|---|----------|---------------|
| 1 | What is Synapse? | AI workspace — chat with your docs, manage tasks, automate workflows, integrate dev tools |
| 2 | How does RAG work? | Ingest docs → chunk → embed (OpenAI/Google) → store vectors in PG → on query embed question → similarity search → inject top-k chunks into prompt |
| 3 | Why PostgreSQL for vectors? | `pgvector` extension; keep relational data + embeddings in one DB |
| 4 | AI SDK vs raw OpenAI API? | Unified interface for multiple providers; built-in streaming; tool calling; easier provider swap |
| 5 | Better Auth vs NextAuth? | TypeScript-first; DB-backed sessions with instant revocation; plugin system |
| 6 | Zustand vs TanStack Query split? | Query for API data (cache, refetch); Zustand for UI state (active chat, sidebar, selections) |
| 7 | How handle streaming responses? | AI SDK `streamText` → `ReadableStream` → client `useChat` hook renders tokens incrementally |
| 8 | Integration sync architecture? | OAuth connect → store tokens encrypted → cron/webhook sync → upsert `Document` rows → re-embed on change |
| 9 | Multi-tenant isolation? | `workspaceId` on all entities; middleware resolves workspace from URL/session |
| 10 | Cost optimization for LLM? | Smaller models for simple tasks; cache embeddings; limit context window; token counting |

### Resume Bullet Suggestion

```
Synapse AI | Next.js, AI SDK, PostgreSQL, Prisma, Better Auth, Zustand
• Built an AI workspace platform with RAG-powered chat, document citations, and 
  integrations (GitHub, Linear, Notion, Slack) using vector embeddings (pgvector) in PostgreSQL.
• Implemented streaming AI responses with AI SDK v6, multi-tenant workspaces with RBAC, 
  and AI-generated task workflows.
```

### Synapse AI Deep Dive

> Covers parts NOT already in `08 - MongoDB & Prisma.md` or `14 - Authentication & Security.md`: RAG architecture, Vercel AI SDK tool-calling, multi-tenant auth with Better Auth, and workspace RBAC.

#### Product Overview

**Q: What is Synapse in one sentence?**
**Answer:** Synapse is an AI-powered multi-workspace platform where teams manage projects, tasks, notes, and documents, with a context-aware AI assistant that can call tools across those resources and answer questions grounded in workspace content via RAG.

**Q: Why did you build it?**
**Answer:** To go deeper than typical CRUD projects — it forced me to combine multi-tenant auth, RBAC, an extensible tool-calling framework, and a RAG-ready retrieval pipeline in one system, which is closer to what real AI-native products need.

**Q: What's the tech stack and why each piece?**

| Layer | Choice | Why |
|---|---|---|
| Framework | Next.js 15 (App Router) | Server components, API routes, streaming responses in one framework |
| Language | TypeScript | Type safety across API contracts and Prisma models |
| ORM | Prisma | Schema-driven modeling, migrations, type-safe queries |
| DB | PostgreSQL | Relational integrity for multi-tenant data + pgvector extension for embeddings |
| Auth | Better Auth | Modern, flexible auth library with first-class multi-tenant/org support |
| AI | Vercel AI SDK | Unified interface for streaming, tool calling, multiple model providers |

#### RAG Architecture

**Q: Walk me through your RAG pipeline end to end.**
**Answer:** Ingestion → chunking → embedding → storage → retrieval → augmentation → generation.
1. **Ingestion:** workspace documents/notes are captured as they're created or updated.
2. **Chunking:** long content is split into smaller overlapping chunks so embeddings stay semantically focused and retrieval is precise.
3. **Embedding:** each chunk is converted into a vector via an embedding model.
4. **Storage:** vectors are stored in Postgres using the `pgvector` extension, alongside metadata (workspace ID, source document, chunk index).
5. **Retrieval:** at query time, the user's question is embedded and compared against stored vectors using similarity search (cosine distance), filtered by workspace ID for tenant isolation.
6. **Augmentation:** top-k relevant chunks are injected into the LLM's context window alongside the user's question.
7. **Generation:** the LLM generates a grounded answer, ideally citing which resource the info came from.

**Q: Why chunk documents instead of embedding the whole thing?**
**Answer:** Embedding models have limited context, and a single vector for a huge document averages out its meaning, hurting retrieval precision. Smaller chunks let you retrieve the *specific* relevant section instead of a diluted whole-document match.

**Q: How do you handle chunk overlap?**
**Answer:** Overlapping chunks (e.g., a sliding window with ~10-20% overlap) prevent losing context at chunk boundaries — a sentence split across two chunks can still be understood in at least one of them.

**Q: What is "RAG-ready" vs full RAG — why frame it that way?**
**Answer:** It means the architecture (schema, embedding storage, retrieval interface) is built to support retrieval-augmented answers, even if not every workspace resource is fully indexed yet. It's an honest way to describe a system designed for extensibility rather than overclaiming complete coverage.

**Q: How do you keep RAG answers grounded and avoid hallucination?**
**Answer:** By constraining the prompt so the model is instructed to answer *primarily* from retrieved context, returning "I don't have enough information" when nothing relevant is retrieved, and optionally surfacing source citations so users can verify.

#### Vector Search & pgvector

**Q: Why pgvector over a dedicated vector DB (Pinecone, Weaviate, Qdrant)?**
**Answer:** Postgres already holds the relational data (users, workspaces, tasks). Using `pgvector` keeps vectors co-located with that data — no cross-database joins, one connection pool, one backup/migration story, and Prisma can manage it in the same schema. A dedicated vector DB makes more sense at much larger scale or when you need specialized ANN indexes.

**Q: How does similarity search actually work?**
**Answer:** Each chunk's embedding is a high-dimensional vector. A query embedding is compared against stored vectors using a distance metric — cosine similarity is most common for text embeddings — and the closest N vectors (lowest distance / highest similarity) are returned as the most relevant chunks.

**Q: What indexing strategy would you use as data scales?**
**Answer:** For small-to-medium datasets, a flat/exact search is fine. As rows grow, `pgvector` supports approximate nearest-neighbor indexes (IVFFlat, HNSW) that trade a small amount of accuracy for much faster lookups.

**Q: How do you scope retrieval to a single workspace (tenant isolation)?**
**Answer:** Every embedding row stores a `workspaceId` foreign key, and every similarity query filters `WHERE workspace_id = $1` before ranking by distance — this guarantees one workspace can never retrieve another workspace's private content.

#### Vercel AI SDK & Tool Calling

**Q: What does the Vercel AI SDK give you that raw API calls don't?**
**Answer:** A unified interface across model providers, built-in streaming (`streamText`/`useChat`), and structured tool-calling with automatic schema validation — instead of hand-rolling SSE parsing and manually parsing model output for function-call intent.

**Q: How does tool calling work in your assistant?**
**Answer:** Tools are defined with a name, description, and a typed input schema (e.g., Zod). The model decides when a tool is needed based on the user's message, the SDK validates and executes the tool call against the actual backend (e.g., "create task," "search documents"), and the result is fed back into the conversation for the model to use in its final response.

**Q: What does "context-aware" tool calling across workspace resources mean, concretely?**
**Answer:** The assistant isn't a generic chatbot — its tools operate on the current workspace's actual data (its projects, tasks, notes), so asking "what's overdue this week" triggers a tool that queries real task rows scoped to that workspace and returns a grounded answer, not a guess.

**Q: How do you handle streaming responses with tool calls in the middle?**
**Answer:** The AI SDK supports multi-step tool calling — the model can call a tool, receive the result, and continue generating, all while streaming tokens to the client, so the user sees the assistant "thinking" and responding in near real-time.

**Q: What's your "modular integration framework" for extensibility?**
**Answer:** Each tool is a self-contained module with a defined schema and handler, registered into a central tool registry — adding a new capability means writing one new tool definition rather than touching the core assistant logic.

#### Multi-Tenant Auth with Better Auth

**Q: Why Better Auth over NextAuth/Auth.js or building auth yourself?**
**Answer:** Better Auth has first-class support for organizations/workspaces out of the box (invitations, membership, roles), is fully typed for TypeScript, and integrates cleanly with Prisma — it saved building multi-tenant primitives from scratch while staying flexible enough to customize.

**Q: What does "secure multi-tenant authentication" actually mean here?**
**Answer:** A user can belong to multiple workspaces, sessions are scoped so every request resolves both "who is this user" and "which workspace are they acting in," and no query executes without that workspace context — preventing one tenant's data from ever leaking into another's session.

**Q: Walk me through the workspace invitation flow.**
**Answer:** An admin/owner sends an invite (email + role) → an invitation record is created with a token and expiry → the invitee receives a link → on acceptance, a membership record links user to workspace with the assigned role → the token is invalidated so it can't be reused.

**Q: How do you prevent a user from accessing a workspace they're not a member of?**
**Answer:** Every workspace-scoped API route/server action checks membership (user ID + workspace ID exists in the membership table) before executing any query — this check happens at the data-access layer, not just the UI, so it can't be bypassed by calling the API directly.

#### Workspace RBAC

**Q: What roles exist and what do they control?**
**Answer:** Typically Owner / Admin / Member tiers — Owner has full control including billing/deletion, Admin can manage members and settings, Member can create/edit content but not manage the workspace itself.

**Q: How is a role checked before an action executes?**
**Answer:** A permission check reads the user's role for that specific workspace (from the membership record) and compares it against the action's required role level before allowing writes like deleting a project or removing a member.

**Q: What's the difference between authentication and authorization in this system?**
**Answer:** Authentication (via Better Auth) confirms *who* the user is. Authorization (via workspace RBAC) confirms *what* that user is allowed to do inside a specific workspace — the two are checked separately, and both must pass.

#### Data Modeling (Prisma + Postgres)

**Q: Sketch the core schema relationships.**
**Answer:**
- `User` — one user, many workspace memberships
- `Workspace` — has many members, projects, notes, documents
- `Membership` — join table: `userId`, `workspaceId`, `role`
- `Project` / `Task` / `Note` / `Document` — each scoped by `workspaceId`
- `Embedding` — `chunkText`, `vector`, `workspaceId`, `sourceDocumentId`

**Q: Why join tables (Membership) instead of a direct array/relation?**
**Answer:** A join table lets you attach extra data to the relationship itself — like `role` and `joinedAt` — which a simple many-to-many relation can't do cleanly in a relational schema.

**Q: How do you keep every query tenant-safe by default?**
**Answer:** By convention, no query against workspace-owned tables runs without a `workspaceId` filter — this is best enforced with a thin data-access layer/repository pattern so every call site is forced through the same scoped functions.

#### Scenario & Follow-Up Questions

| # | Question | How to Answer |
|---|----------|---------------|
| 1 | What happens if the AI hallucinates a tool call with bad arguments? | Schema validation (Zod) rejects malformed input before execution; the SDK surfaces a validation error back to the model to retry or to the user as a graceful failure. |
| 2 | How would you scale RAG if one workspace had 100k+ documents? | Move to approximate-NN indexing (HNSW), consider a dedicated vector store if Postgres becomes the bottleneck, and add caching for frequent queries. |
| 3 | How do you avoid one workspace's AI context leaking into another? | Every retrieval query filters by `workspaceId`, and no chat session or tool call carries context across workspace boundaries. |
| 4 | What was the hardest bug you hit building this? | Fill in your actual war story — e.g., a tenant-isolation bug where a scoped filter was missing, or a tool-calling race condition during streaming. |
| 5 | How would you add a third-party integration (e.g., Slack)? | New tool module registered in the tool registry with its own schema/handler, plus an OAuth flow scoped per-workspace, following the same modular pattern as existing tools. |

#### Synapse AI Cheat Sheet

- **RAG flow:** ingest → chunk → embed → store (pgvector) → retrieve (cosine similarity, workspace-scoped) → augment prompt → generate
- **Why pgvector:** co-located with relational data, one DB, Prisma-manageable
- **Vercel AI SDK:** unified provider interface + streaming + typed tool calling
- **Better Auth:** multi-tenant primitives (orgs, invitations, roles) out of the box
- **Tenant isolation:** every query filtered by `workspaceId`, checked at data-access layer not UI
- **RBAC tiers:** Owner > Admin > Member — checked per-action, per-workspace
- **Extensibility:** new features = new tool module in registry, not core logic changes

---

## 6. ShopCart

**Stack:** React.js, Node.js, Express, MongoDB, Zustand, Stripe, Docker, AWS EC2, Nginx, GitHub Actions  
**Links:** [Live](https://shopcart.ritikgupta.in/) | [GitHub](https://github.com/Ritikgupta856/shopcart-ecommerce.git)

### Elevator Pitch

> "ShopCart is a full e-commerce platform — product catalog, cart, Stripe checkout, order management. I containerized it with Docker, set up CI/CD via GitHub Actions, and deployed on AWS EC2 behind Nginx with SSL."

### Likely Interview Questions

| # | Question | How to Answer |
|---|----------|---------------|
| 1 | Monolith or microservices? | Monolith — React frontend + Express API + MongoDB; appropriate for project scale |
| 2 | Stripe payment flow? | Create PaymentIntent on server → client confirms with Stripe.js → webhook `payment_intent.succeeded` → create order |
| 3 | Zustand for cart? | Global cart state; add/remove/update quantity; persist middleware; sync with server on checkout |
| 4 | Docker setup? | Separate containers: `frontend`, `backend`, `mongo`; `docker-compose.yml` for local + prod |
| 5 | CI/CD pipeline? | GitHub Actions: lint → build → push image → SSH deploy to EC2 → `docker-compose up -d` |
| 6 | Nginx role? | Reverse proxy; serve React build; proxy `/api` to Node; SSL termination with Let's Encrypt |
| 7 | Why EC2 over serverless? | Full control, persistent connections, learning DevOps |
| 8 | Order status lifecycle? | `pending` → `paid` → `shipped` → `delivered`; webhook drives `pending` → `paid` |
| 9 | What breaks in production? | CORS misconfig, env vars missing, webhook signature not verified, Mongo connection timeout |

### DevOps Deep-Dive (Strong Differentiator)

```
git push → GitHub Actions → Docker build → EC2 deploy
                                ↓
                    Nginx (443 SSL) → React static
                                   → /api → Express :5000
                                   → MongoDB container
```

---

## 7. Cross-Project Architecture Questions

### Q: Compare your projects — what's common?

| Pattern | Where Used |
|---------|------------|
| JWT / Session Auth | Meal app, ShopCart, Synapse (Better Auth) |
| Zustand | Jewelry e-commerce, ShopCart, Synapse |
| Prisma ORM | Synapse |
| Payment Gateway | Razorpay (jewelry, Synapse), Stripe (ShopCart) |
| Async Processing | RabbitMQ (document app) |
| Docker + CI/CD | ShopCart |
| Real-time / Streaming | Synapse (AI streaming) |

### Q: Monolith vs microservices across your work?

**Answer:** "All my projects are modular monoliths — appropriate for team size and scale. At BASICX, I separated LLM processing into a Python worker via RabbitMQ, which is service extraction where it matters, not microservices for the sake of it."

### Q: How do you choose a database?

- **MySQL** — financial/admin data, strict relations (BASICX dashboard)
- **MongoDB** — flexible product schemas (ShopCart)
- **PostgreSQL** — relational + vectors for RAG (Synapse)

---

## 8. Challenges & Debugging Stories

Prepare 3–5 real stories. Framework for each:

1. **What broke** — symptom
2. **How you found it** — logs, tools used
3. **Root cause** — one specific cause
4. **Fix** — code + process change
5. **Prevention** — test, monitoring, validation

### Suggested Stories (Fill With Your Real Details)

| # | Story | Project |
|---|-------|---------|
| 1 | RabbitMQ message lost / duplicate processing | Document app |
| 2 | Razorpay webhook fired twice → duplicate order | Jewelry / Synapse |
| 3 | Next.js hydration mismatch on SSR cart | Jewelry e-commerce |
| 4 | CORS error on EC2 deployment | ShopCart |
| 5 | LLM returned invalid JSON → form render crash | Document app |

---

## 9. Optimizations You Can Talk About

| Optimization | Project | Impact |
|--------------|---------|--------|
| Next.js SSR + code splitting | Jewelry platform | Faster page loads |
| RabbitMQ async LLM pipeline | Document app | Async processing, concurrent workers |
| DB indexes on `org_id`, FKs | Admin dashboard | Faster reports |
| Docker multi-stage builds | ShopCart | Smaller images, faster deploys |
| Vector index (IVFFlat/HNSW) | Synapse RAG | Faster similarity search |
| TanStack Query caching | Synapse | Fewer redundant API calls |
| Zustand selective subscriptions | Jewelry, ShopCart | Fewer re-renders vs Context |

---

## 10. Leadership & Teamwork

### Q: Tell me about working in a team at BASICX.

**Answer framework:** Mention code reviews, coordinating with team members, communicating blockers early, documenting API contracts.

### Q: Did you lead any feature end-to-end?

**Best examples:** Document processing app (full vertical — UI, queue, Python worker) or ShopCart (frontend to AWS deployment).

---

## 11. Production & Deployment

### Your Production Stack (ShopCart)

1. Code on GitHub
2. GitHub Actions CI/CD
3. Docker images for frontend + backend
4. AWS EC2 instance
5. Nginx reverse proxy + SSL (Let's Encrypt)
6. Environment variables for secrets

### Common Production Questions

| Question | Answer |
|----------|--------|
| How do you handle secrets? | Env vars; GitHub Secrets in CI; never in code |
| Zero-downtime deploy? | Docker compose with health checks |
| Logging? | Console → structured logs |
| Rollback? | Keep previous Docker image tag; docker-compose rollback |

---

## 12. CI/CD Stories

### ShopCart Pipeline

```yaml
on: push to main
jobs:
  build:
    - npm ci
    - npm run lint
    - npm run build
    - docker build -t shopcart-api .
    - docker push
  deploy:
    - SSH to EC2
    - docker-compose pull && docker-compose up -d
```

---

## 13. Resume Tips & Mistakes

### What's Strong on Your Resume

- Production experience at a real company
- Diverse tech stack across 4 projects
- RabbitMQ + LLM — rare and valuable
- Docker + AWS + CI/CD for a junior

### ATS Keywords for Your Profile

`React.js` `Next.js` `TypeScript` `Node.js` `Express.js` `REST API` `JWT` `MySQL` `MongoDB` `Prisma` `Zustand` `RabbitMQ` `Docker` `AWS EC2` `CI/CD` `GitHub Actions` `Nginx` `Razorpay` `Stripe` `LLM` `RAG` `AI SDK`

---

## 14. Scenario Questions

### S1: "Your payment webhook fails in production. What do you do?"

1. Check webhook logs / Razorpay dashboard for delivery status
2. Verify signature validation code and webhook secret
3. Check idempotency — are retries creating duplicates?
4. Manual reconciliation for affected orders

### S2: "RabbitMQ queue is growing — consumers can't keep up."

1. Check consumer health and error rate
2. Scale consumers horizontally
3. Increase prefetch carefully
4. Check if LLM service is slow (bottleneck)
5. DLQ inspection for poison messages

### S3: "User reports slow admin dashboard reports."

1. `EXPLAIN` slow queries
2. Add indexes on `org_id`, date columns
3. Pagination + date range filters
4. Consider materialized views or caching for heavy aggregates

### S4: "Interviewer asks you to whiteboard ShopCart order flow."

```
Browse → Add to Cart (Zustand) → Checkout → POST /api/orders
  → Create Stripe PaymentIntent → Client pays → Webhook
  → Update order status → Decrement inventory → Email confirmation
```

---

## 15. Quick Cheat Sheet

### Your Tech Map

```
BASICX Work:
  Meal App      → React + TS + Node + JWT + i18n + Payments
  Admin Dash    → React + Node + MySQL + Multi-tenant
  Jewelry Shop  → Next.js SSR + Strapi + Razorpay + Zustand
  Doc Processor → React + Node + RabbitMQ + Python LLM

Personal:
  Synapse AI    → Next.js 16 + AI SDK + PG Vector + Better Auth + Zustand
  ShopCart      → React + Node + MongoDB + Stripe + Docker + AWS
```

### 30-Second Project Picker

| If interviewer cares about… | Lead with… |
|-----------------------------|------------|
| AI / LLM | Synapse AI or Document Processing app |
| DevOps | ShopCart (Docker, AWS, CI/CD) |
| E-commerce | Jewelry platform or ShopCart |
| System design | Admin dashboard (multi-tenant) or RabbitMQ pipeline |
| Performance | Next.js SSR optimization or RabbitMQ async processing |

---

*Last updated for Ritik Gupta's resume — Manipal Jaipur, BASICX, Synapse AI, ShopCart.*

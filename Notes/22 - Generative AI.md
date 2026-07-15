# Generative AI — Interview Preparation Guide

> Aligned with **Synapse AI** ([ai-workspace](https://github.com/Ritikgupta856/ai-workspace)) and BASICX document processing (LLM + RabbitMQ).

---

## Table of Contents

1. [LLM Basics](#1-llm-basics)
2. [Tokens & Context Window](#2-tokens--context-window)
3. [Prompt Engineering](#3-prompt-engineering)
4. [Embeddings](#4-embeddings)
5. [Vector Databases](#5-vector-databases)
6. [RAG](#6-rag)
7. [AI Agents & Tool Calling](#7-ai-agents--tool-calling)
8. [MCP](#8-mcp)
9. [Streaming](#9-streaming)
10. [AI SDK (Vercel)](#10-ai-sdk-vercel)
11. [LangChain & LangGraph](#11-langchain--langgraph)
12. [OpenAI & Gemini APIs](#12-openai--gemini-apis)
13. [Structured Output & JSON Mode](#13-structured-output--json-mode)
14. [Memory & Chunking](#14-memory--chunking)
15. [Retrieval & Semantic Search](#15-retrieval--semantic-search)
16. [Fine-tuning](#16-fine-tuning)
17. [AI Security](#17-ai-security)
18. [AI Cost Optimization](#18-ai-cost-optimization)
19. [AI Architecture](#19-ai-architecture)
20. [Real Project Examples (Your Work)](#20-real-project-examples-your-work)
21. [Scenario Questions](#21-scenario-questions)
22. [Cheat Sheet](#22-cheat-sheet)

---

## 1. LLM Basics

### Q: What is an LLM?

**A:** A Large Language Model is a neural network trained on massive text data to predict the next token. It generates human-like text, code, and structured output based on input prompts. Examples: GPT-4, Gemini, Claude.

### Q: How does an LLM generate text?

**A:** Autoregressively — predicts one token at a time, feeds output back as input, until stop condition (max tokens, stop sequence, or EOS token).

### Q: What is the transformer architecture?

**A:** Uses **self-attention** to weigh relationships between all tokens in a sequence in parallel — unlike RNNs which process sequentially. Enables scaling to billions of parameters.

### Q: What is temperature?

**A:** Controls randomness in token sampling.
- **Low (0–0.3)** — deterministic, factual (good for extraction, JSON)
- **High (0.7–1.0)** — creative, varied (good for brainstorming)

### Q: Top-K and Top-P (nucleus sampling)?

**A:** **Top-K** — sample only from K most likely tokens. **Top-P** — sample from smallest set of tokens whose cumulative probability ≥ P. Reduces nonsense outputs.

---

## 2. Tokens & Context Window

### Q: What is a token?

**A:** The unit LLMs process — can be a word, subword, or character chunk. ~4 chars ≈ 1 token in English. "JavaScript" might be 1–2 tokens.

### Q: What is a context window?

**A:** Maximum tokens the model can consider in one request (input + output). GPT-4o: 128K; Gemini 1.5 Pro: up to 1M+. Exceeding it truncates or errors.

### Q: How do you count tokens?

**A:** `tiktoken` (OpenAI), `tokenlens` (used in Synapse), or provider APIs. Critical for cost estimation and chunking.

### Q: What happens when context is too large?

**A:** Truncation, higher latency, higher cost, degraded quality ("lost in the middle" problem). Solution: RAG, summarization, or sliding window.

---

## 3. Prompt Engineering

### Q: What is prompt engineering?

**A:** Designing inputs to get reliable, high-quality outputs — system prompts, few-shot examples, chain-of-thought, role assignment.

### Q: System vs user vs assistant messages?

```typescript
messages: [
  { role: 'system', content: 'You are a helpful coding assistant for Synapse workspace.' },
  { role: 'user', content: 'Explain this PR diff...' },
  { role: 'assistant', content: '...' },
]
```

### Q: Few-shot prompting?

**A:** Include examples of desired input→output in the prompt. Improves format consistency without fine-tuning.

### Q: Chain-of-thought (CoT)?

**A:** Ask model to "think step by step" before answering. Improves reasoning on math, logic, multi-step tasks.

### Q: Prompt patterns for production

| Pattern | Use Case |
|---------|----------|
| Role + constraints | "Answer only from provided context. Cite sources." |
| Output format | "Return valid JSON matching this schema…" |
| Refusal rules | "If unsure, say you don't know" |
| RAG injection | Context block + user question separated clearly |

### Synapse Example System Prompt

```
You are Synapse AI, an assistant for software teams.
Use ONLY the provided document context to answer.
Cite document titles in [brackets].
If context is insufficient, say so — do not hallucinate.
```

---

## 4. Embeddings

### Q: What are embeddings?

**A:** Dense vector representations of text capturing semantic meaning. Similar meanings → vectors close in cosine distance.

### Q: How are embeddings used?

**A:** Semantic search, clustering, recommendation, RAG retrieval, duplicate detection.

### Q: Embedding models?

| Provider | Model |
|----------|-------|
| OpenAI | `text-embedding-3-small`, `text-embedding-3-large` |
| Google | `text-embedding-004` |
| Open source | `nomic-embed`, `bge-small` |

### Q: Cosine similarity?

**A:** Measures angle between two vectors (0–1). Used to rank document chunks by relevance to query embedding.

```typescript
// Conceptual
const score = cosineSimilarity(queryEmbedding, docEmbedding);
const topK = docs.sort((a, b) => b.score - a.score).slice(0, 5);
```

### Q: Synapse — how embeddings are stored?

**A:** Prisma schema has `Document.embedding` as `Unsupported("vector")` in PostgreSQL with `pgvector` extension.

---

## 5. Vector Databases

### Q: What is a vector database?

**A:** Optimized for storing and querying high-dimensional vectors via ANN (approximate nearest neighbor) indexes.

### Q: Options?

| DB | Notes |
|----|-------|
| **pgvector** (PostgreSQL) | Synapse choice — one DB for relational + vectors |
| Pinecone | Managed, serverless |
| Weaviate | Open source, GraphQL |
| Chroma | Lightweight, dev-friendly |
| Qdrant | Rust-based, fast |

### Q: pgvector vs dedicated vector DB?

**A:** pgvector — simpler ops, ACID, joins with relational data; good up to millions of vectors. Dedicated DB — better at billion-scale ANN, managed scaling.

### Q: Index types?

**A:** IVFFlat (faster build, good recall), HNSW (better query speed/recall, more memory).

---

## 6. RAG

### Q: What is RAG?

**A:** Retrieval Augmented Generation — retrieve relevant documents from a knowledge base, inject into prompt, then generate answer grounded in that context.

### Q: Why RAG over fine-tuning?

| RAG | Fine-tuning |
|-----|-------------|
| Up-to-date data without retraining | Expensive, slow to update |
| Citations possible | No source attribution |
| Works with private docs | Needs training data |
| Lower cost | Higher upfront cost |

### Q: RAG pipeline (Synapse architecture)?

```
1. INGEST: GitHub/Notion/Linear/Slack → fetch docs
2. CHUNK: Split into ~500–1000 token chunks with overlap
3. EMBED: Generate embedding per chunk
4. STORE: PostgreSQL + pgvector
5. QUERY: User asks question → embed query → similarity search top-K
6. GENERATE: Inject chunks into prompt → stream answer with citations
```

### Q: Chunking strategies?

| Strategy | When |
|----------|------|
| Fixed size + overlap | General docs (200–500 tokens, 50 overlap) |
| Semantic chunking | Long prose — split on paragraph/topic |
| Code-aware | Split on functions/classes for code repos |
| Markdown headers | Split on `#` sections |

### Q: What is hybrid search?

**A:** Combine vector similarity + keyword (BM25) search. Better recall when exact terms matter (API names, error codes).

### Q: How handle citations?

**A:** Store `sourceUrl`, `title`, `chunkId` with each chunk. Return in `Message.citations` JSON (Synapse schema). UI renders `[Doc Title]` links.

---

## 7. AI Agents & Tool Calling

### Q: What is an AI agent?

**A:** LLM that can **plan**, **use tools**, and **iterate** — not just one-shot text generation. Loops: think → call tool → observe result → continue.

### Q: Tool calling / function calling?

**A:** Model returns structured tool invocation instead of text; runtime executes tool and feeds result back.

```typescript
import { tool } from 'ai';
import { z } from 'zod';

const createTask = tool({
  description: 'Create a task in the workspace',
  parameters: z.object({
    title: z.string(),
    priority: z.enum(['LOW', 'MEDIUM', 'HIGH', 'URGENT']),
  }),
  execute: async ({ title, priority }) => {
    return await prisma.task.create({ data: { title, priority, ... } });
  },
});
```

### Q: Agent vs chain?

| Chain | Agent |
|-------|-------|
| Fixed sequence of steps | Dynamic tool selection |
| Predictable | Flexible, can loop |
| Simpler to debug | Harder to control |

### Q: Synapse workflow agents?

**A:** `Workflow` model with JSON `config` — trigger on MANUAL/SCHEDULED/EVENT; `WorkflowRun` tracks execution. AI can generate tasks (`generatedByAI: true`).

---

## 8. MCP

### Q: What is MCP (Model Context Protocol)?

**A:** Open standard for connecting AI models to external tools and data sources — standardized tool/resource interface. Used by Cursor and growing ecosystem.

### Q: MCP vs custom tool calling?

**A:** MCP — interoperable protocol, reusable servers (GitHub, DB, filesystem). Custom tools — app-specific, tighter integration.

### Q: Interview answer?

> "MCP standardizes how LLMs connect to external systems. In Synapse, we integrate GitHub/Linear/Notion directly, but MCP is the direction for portable tool servers across AI apps."

---

## 9. Streaming

### Q: Why stream LLM responses?

**A:** Better UX (tokens appear immediately), lower perceived latency, can cancel long responses, works with HTTP SSE/chunked transfer.

### Q: AI SDK streaming?

```typescript
import { streamText } from 'ai';
import { openai } from '@ai-sdk/openai';

export async function POST(req: Request) {
  const { messages } = await req.json();
  const result = streamText({
    model: openai('gpt-4o'),
    messages,
  });
  return result.toDataStreamResponse();
}
```

### Q: Client consumption (React)?

```typescript
import { useChat } from 'ai/react';

const { messages, input, handleSubmit, isLoading } = useChat({
  api: '/api/chat',
});
```

### Q: Synapse streaming stack?

**A:** AI SDK v6 `streamText` → `streamdown` for markdown rendering → `use-stick-to-bottom` for chat scroll UX.

---

## 10. AI SDK (Vercel)

### Q: What is the AI SDK?

**A:** TypeScript library (`ai` package) for building AI apps — unified provider interface, streaming, tool calling, React hooks, structured output.

### Q: Why AI SDK over raw fetch to OpenAI?

| Benefit | Detail |
|---------|--------|
| Provider swap | `@ai-sdk/openai`, `@ai-sdk/google` — same API |
| Streaming helpers | `streamText`, `generateText` |
| React hooks | `useChat`, `useCompletion` |
| Tool calling | Built-in loop with `maxSteps` |
| Type safety | Zod schemas for tools and output |

### Q: Synapse dependencies?

```json
"ai": "^6.0.209",
"@ai-sdk/openai": "^3.0.74",
"@ai-sdk/google": "^3.0.83"
```

### Q: `generateText` vs `streamText`?

**A:** `generateText` — waits for full response (background jobs, JSON extraction). `streamText` — streams to client (chat UI).

---

## 11. LangChain & LangGraph

### Q: What is LangChain.js?

**A:** Framework for composing LLM apps — chains, retrievers, memory, agents, document loaders. More abstraction than AI SDK.

### Q: LangGraph?

**A:** State machine / graph-based agent orchestration on top of LangChain. Nodes = steps, edges = transitions. Good for complex multi-step workflows with cycles.

### Q: AI SDK vs LangChain — when to use?

| AI SDK | LangChain |
|--------|-----------|
| Next.js apps, streaming chat | Complex retrieval pipelines |
| Minimal abstraction | Many integrations out of box |
| Synapse choice | Document app Python side |

### Q: Your experience answer?

> "Synapse uses Vercel AI SDK for streaming chat and tool calling. At BASICX, the document processing worker uses Python LLM services — likely LangChain — behind RabbitMQ for heavy extraction pipelines."

---

## 12. OpenAI & Gemini APIs

### Q: OpenAI Chat Completions API?

```typescript
import { generateText } from 'ai';
import { openai } from '@ai-sdk/openai';

const { text } = await generateText({
  model: openai('gpt-4o'),
  prompt: 'Summarize this document...',
});
```

### Q: Gemini API?

```typescript
import { google } from '@ai-sdk/google';

const { text } = await generateText({
  model: google('gemini-1.5-pro'),
  prompt: '...',
});
```

### Q: When OpenAI vs Gemini?

| OpenAI | Gemini |
|--------|--------|
| Strong coding, tools ecosystem | Long context (1M tokens) |
| GPT-4o multimodal | Competitive pricing |
| Widely documented | Good Google Cloud integration |

### Q: API key security?

**A:** Server-side only (`OPENAI_API_KEY` in env). Never expose in client bundle. Route handlers proxy requests.

---

## 13. Structured Output & JSON Mode

### Q: Why structured output?

**A:** LLMs return text; apps need typed data (tasks, forms, API payloads). Structured output enforces schema compliance.

### Q: AI SDK + Zod?

```typescript
import { generateObject } from 'ai';
import { z } from 'zod';

const { object } = await generateObject({
  model: openai('gpt-4o'),
  schema: z.object({
    title: z.string(),
    tasks: z.array(z.object({
      title: z.string(),
      priority: z.enum(['LOW', 'MEDIUM', 'HIGH']),
    })),
  }),
  prompt: 'Break this feature request into tasks...',
});
```

### Q: JSON mode vs `generateObject`?

**A:** JSON mode — model told to output JSON (may still be invalid). `generateObject` — schema-validated, retried on parse failure. Prefer `generateObject` in production.

### Q: BASICX document app — JSON to form?

**A:** LLM extracts structured JSON from documents → Node receives result → React dynamically renders form fields from JSON schema. Prepare for invalid JSON with Zod validation + retry prompt.

---

## 14. Memory & Chunking

### Q: Types of memory in AI apps?

| Type | Implementation |
|------|----------------|
| Short-term | Last N messages in context window |
| Long-term | Vector store of past conversations |
| Session | DB `Chat` + `Message` tables (Synapse) |
| User prefs | User profile / settings in DB |

### Q: Synapse memory model?

```prisma
model Chat { messages Message[] }
model Message { role, content, citations }
```

Server loads recent messages per chat; optionally summarizes old messages to save tokens.

### Q: Conversation summarization?

**A:** When messages exceed threshold, summarize older messages into one system message — preserves context within token limits.

---

## 15. Retrieval & Semantic Search

### Q: Semantic search flow?

1. Embed query
2. ANN search in vector index
3. Return top-K chunks with scores
4. Optional: re-rank with cross-encoder

### Q: What is re-ranking?

**A:** Second pass with a more accurate (slower) model to reorder top-K results. Improves precision.

### Q: Metadata filtering?

```sql
-- pgvector example
SELECT title, content, embedding <=> $1 AS distance
FROM documents
WHERE workspace_id = $2 AND content_type = 'CODE'
ORDER BY distance
LIMIT 5;
```

Filter by workspace, project, integration type before vector search.

---

## 16. Fine-tuning

### Q: What is fine-tuning?

**A:** Further training base model on domain-specific dataset to specialize behavior/style.

### Q: When fine-tune vs RAG?

**Fine-tune:** Consistent tone, specialized format, classification, domain jargon.  
**RAG:** Dynamic knowledge, citations, frequently changing data.  
**Most apps:** RAG first; fine-tune only if RAG insufficient.

### Q: OpenAI fine-tuning basics?

Upload JSONL examples → train → get custom model ID → use like any model. Cost: training + higher inference.

---

## 17. AI Security

### Q: Prompt injection?

**A:** Attacker embeds instructions in user content ("ignore previous instructions…"). Mitigation: separate system/user boundaries, output validation, never execute LLM output as code blindly.

### Q: Data leakage?

**A:** Don't send secrets/PII to LLM; sanitize logs; tenant isolation in vector search (`workspace_id` filter always).

### Q: OWASP for LLM apps?

Key risks: prompt injection, insecure output handling, training data poisoning, model DoS, supply chain vulnerabilities.

### Q: API key exposure?

Server-side proxy only. Rate limit per user. Monitor usage anomalies.

---

## 18. AI Cost Optimization

### Q: Cost drivers?

Tokens in + tokens out × model price. Embeddings × document volume.

### Q: Optimization strategies?

| Strategy | Impact |
|----------|--------|
| Smaller models for simple tasks | High |
| Cache embeddings (don't re-embed unchanged docs) | High |
| Limit context (top-K chunks only) | High |
| Summarize long histories | Medium |
| Batch embedding requests | Medium |
| `gpt-4o-mini` for extraction, `gpt-4o` for complex reasoning | High |

### Q: Token budgeting?

Set `maxTokens` on output. Truncate input context. Use `tokenlens` (in Synapse) to estimate before sending.

---

## 19. AI Architecture

### Synapse Full Architecture

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  Next.js 16 │────▶│  API Routes  │────▶│  AI SDK     │
│  React 19   │     │  (streaming) │     │  OpenAI/    │
│  Zustand    │     └──────┬───────┘     │  Google     │
│  TanStack   │            │             └─────────────┘
│  Query      │            ▼
└─────────────┘     ┌──────────────┐     ┌─────────────┐
                    │  Prisma ORM  │────▶│ PostgreSQL  │
                    │              │     │ + pgvector  │
                    └──────────────┘     └─────────────┘
                            │
                    ┌───────┴───────┐
                    ▼               ▼
              GitHub API      Notion/Linear/Slack
              (integrations)  (doc sync)
```

### BASICX Document Processing Architecture

```
React UI → Node API → RabbitMQ Queue → Python LLM Worker
                │                              │
                ▼                              ▼
           Job status DB              Structured JSON result
                │                              │
                └──────── split-view UI ◀──────┘
```

### Q: Sync vs async LLM calls?

| Sync | Async (Queue) |
|------|---------------|
| Chat, quick Q&A | Long document processing |
| Streaming UX | Batch jobs |
| < 30 sec | Minutes, retries needed |

---

## 20. Real Project Examples (Your Work)

### Synapse AI — Interview Answers

**"Walk me through your AI project."**

> Synapse is an AI workspace for dev teams. Users connect GitHub, Linear, Notion, Slack — documents sync into PostgreSQL. We chunk and embed them with pgvector. In chat, we retrieve top relevant chunks (RAG), stream the answer with citations using AI SDK v6. AI can also generate tasks and run workflows. Auth is Better Auth with workspace-level RBAC.

**"Hardest AI challenge?"**

> Retrieval quality — wrong chunks = hallucinations. We improved with better chunking for code/markdown, metadata filters by workspace and project, and strict system prompts that refuse when context is insufficient.

### BASICX Document App — Interview Answers

**"How did you integrate LLM?"**

> React frontend uploads documents. Node.js publishes a job to RabbitMQ. Python worker calls LLM to extract structured fields. Result comes back as JSON, converted to a dynamic form in split-view UI. Async design reduced processing wait by 70%.

---

## 21. Scenario Questions

### S1: Design a chatbot over company docs.

RAG pipeline: ingest → chunk → embed → store. On query: embed → retrieve top-5 → prompt with context → stream answer. Add auth, workspace isolation, citation UI.

### S2: LLM returns wrong facts.

Improve retrieval (hybrid search, re-rank), tighten prompt ("answer only from context"), add confidence threshold, show citations so user verifies.

### S3: API costs spike overnight.

Check for loops (agent calling tools repeatedly), missing rate limits, large context windows, add per-user quotas, switch to cheaper model for bulk tasks.

### S4: How add GitHub integration to Synapse?

OAuth → store token → fetch repos/PRs/issues → normalize to `Document` rows → chunk → embed → available in RAG search.

### S5: Compare your two AI projects.

| | Synapse | BASICX Doc App |
|---|---------|----------------|
| Pattern | RAG + chat | Extraction pipeline |
| Async | Streaming sync | RabbitMQ async |
| Output | Natural language + citations | Structured JSON → form |
| Storage | pgvector | Job queue + DB |

---

## 22. Cheat Sheet

### Core Concepts

| Term | One-liner |
|------|-----------|
| Token | LLM input/output unit |
| Context window | Max tokens per request |
| Embedding | Vector representation of meaning |
| RAG | Retrieve docs → augment prompt → generate |
| Tool calling | LLM invokes functions |
| Streaming | Token-by-token response delivery |
| Temperature | Randomness (0=deterministic) |
| pgvector | Postgres vector extension |

### Key Packages (Your Stack)

```
ai                    — Vercel AI SDK core
@ai-sdk/openai        — OpenAI provider
@ai-sdk/google         — Gemini provider
zod                   — Schema validation
@tanstack/react-query — Server state cache
zustand               — Client UI state
@prisma/client        — DB + vector storage
better-auth           — Authentication
streamdown            — Markdown stream render
tokenlens             — Token counting
```

### RAG Checklist

- [ ] Chunk size 300–800 tokens with overlap
- [ ] Embed with consistent model
- [ ] Index vectors (HNSW/IVFFlat)
- [ ] Filter by tenant/workspace
- [ ] Top-K retrieve (K=3–7)
- [ ] Cite sources in UI
- [ ] Refuse when context insufficient
- [ ] Cache embeddings on unchanged docs

### Cost Formula

```
Cost ≈ (input_tokens × input_price) + (output_tokens × output_price)
Embedding cost ≈ total_doc_tokens × embedding_price
```

### Interview One-Liner

> "I build production AI apps with RAG — Synapse uses AI SDK streaming, pgvector retrieval, and multi-tenant workspace isolation; at BASICX I built async LLM document extraction with RabbitMQ achieving 70% faster processing."

---

*Aligned with Synapse AI (ai-workspace) and BASICX document processing experience.*

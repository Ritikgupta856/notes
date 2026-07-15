# HR Interview Questions — Complete Guide

> Tailored for **Ritik Gupta** — Software Engineer, BSc CS (Manipal Jaipur), STARTWITH BASICX

---

## Table of Contents

1. [Tell Me About Yourself](#1-tell-me-about-yourself)
2. [Why Should We Hire You?](#2-why-should-we-hire-you)
3. [Strengths](#3-strengths)
4. [Weaknesses](#4-weaknesses)
5. [Greatest Achievement](#5-greatest-achievement)
6. [Biggest Failure](#6-biggest-failure)
7. [Conflict With Teammate](#7-conflict-with-teammate)
8. [Leadership](#8-leadership)
9. [Time Management](#9-time-management)
10. [Pressure Handling](#10-pressure-handling)
11. [Career Goals](#11-career-goals)
12. [Why This Company?](#12-why-this-company)
13. [Why Are You Leaving?](#13-why-are-you-leaving)
14. [Salary Expectations](#14-salary-expectations)
15. [Relocation](#15-relocation)
16. [Work-Life Balance](#16-work-life-balance)
17. [Remote Work](#17-remote-work)
18. [Notice Period](#18-notice-period)
19. [Questions to Ask Interviewer](#19-questions-to-ask-interviewer)
20. [100+ HR Questions with Answers](#20-100-hr-questions-with-answers)
21. [Do's and Don'ts](#21-dos-and-donts)

---

## 1. Tell Me About Yourself

### Answer (60–90 seconds)

> "I'm Ritik Gupta, a Software Engineer from Jaipur with a BSc in Computer Science from Manipal University Jaipur, where I graduated with an 8.2 CGPA.
>
> For the past year at STARTWITH BASICX, I've built production applications serving real users — including a meal planning app for 1,000+ users, a multi-organization admin dashboard, a Next.js e-commerce platform, and a document processing system using RabbitMQ and LLMs.
>
> I also maintain personal projects deployed live — Wanderly, a homestay marketplace; ShopCart, a full e-commerce platform with Docker and AWS deployment; and ChatSpark, a real-time chat application.
>
> I'm passionate about full-stack development with React, Next.js, and Node.js, and I'm looking for a role where I can grow as an engineer while building products that scale."

### Tips

- Don't start from childhood
- End with why you're here (this interview)
- Match energy to interviewer (formal vs casual)

---

## 2. Why Should We Hire You?

### Answer

> "Three reasons: First, I ship production software — not just tutorials. At BASICX I've delivered apps used by 1,000+ users with payments, auth, and async processing. Second, I'm full-stack — I can own features from React UI to Node APIs to Docker deployment on AWS. Third, I learn fast and quantify impact — 30% faster page loads with Next.js SSR, 70% faster document processing with RabbitMQ. I bring both execution speed and engineering depth."

### Alternate (AI-focused roles)

> "I combine solid full-stack fundamentals with hands-on AI experience — Synapse AI uses RAG, vector embeddings, and streaming LLM responses. I understand both building the product and the AI pipeline behind it."

---

## 3. Strengths

### Pick 2–3 with examples

| Strength | Example |
|----------|---------|
| **Full-stack ownership** | Built ShopCart end-to-end: React, Node, Stripe, Docker, AWS, CI/CD |
| **Problem solving** | Introduced RabbitMQ to decouple LLM processing — 70% improvement |
| **Fast learner** | Picked up RabbitMQ, Strapi, Razorpay on the job at BASICX |
| **Attention to detail** | TypeScript across projects for fewer production bugs |
| **Persistence** | Deployed projects live with SSL, Nginx, proper DevOps |

### Answer template

> "My biggest strength is end-to-end ownership. For example, on ShopCart I didn't just build the React frontend — I designed the REST APIs, integrated Stripe, containerized with Docker, set up GitHub Actions CI/CD, and deployed on AWS EC2 with Nginx and SSL. I take a feature from idea to production."

---

## 4. Weaknesses

### Rules

- Pick a **real** weakness
- Show **what you're doing** to improve
- Don't say "I work too hard" (cliché)

### Good answers for you

**Option 1:**
> "I sometimes dive into implementation before fully documenting the approach. I've improved by writing short design notes before big features and doing quick syncs with teammates — like before I built the RabbitMQ pipeline, I mapped the flow on paper first."

**Option 2:**
> "Public speaking in large groups is outside my comfort zone. I'm fine in small team discussions and code reviews. I've been volunteering to demo features in sprint reviews to build that skill."

**Option 3:**
> "I used to optimize prematurely. I learned to ship an MVP first, measure, then optimize — like with the jewelry platform where SSR came after we identified LCP as the bottleneck."

---

## 5. Greatest Achievement

### Answer (pick one)

**Professional:**
> "Building the document processing system at BASICX. Documents that took a minute of blocking UI time now process asynchronously via RabbitMQ and Python LLM workers. We achieved a 70% reduction in processing time, and the split-view UI let users keep working while extraction ran in the background."

**Personal:**
> "ShopCart — taking a project from zero to production on AWS with full CI/CD. It proved I can own the entire lifecycle independently, not just write code in an existing codebase."

**Academic:**
> "Graduating with 8.2 CGPA from Manipal while simultaneously building and deploying multiple full-stack projects that are live today."

---

## 6. Biggest Failure

### STAR format

> **Situation:** Early in a project, I deployed ShopCart to EC2 without properly configuring environment variables for the Stripe webhook secret.  
> **Task:** Payments succeeded on Stripe but orders weren't created in our database.  
> **Action:** I checked server logs, found webhook signature verification failing, fixed env config, added a reconciliation script for missed orders, and added webhook health checks to my deployment checklist.  
> **Result:** All orders reconciled. I now have a pre-deploy checklist and never ship without testing webhooks in staging.

### Tips

- Show accountability, not blame
- End with lesson learned
- Keep it technical but understandable to HR

---

## 7. Conflict With Teammate

### Answer

> "A teammate and I disagreed on state management for the jewelry e-commerce project — they preferred Redux, I advocated Zustand for simpler cart state. Instead of arguing, we listed requirements: bundle size, learning curve, DevTools needs. We prototyped both in a day. Zustand won on simplicity and performance for our use case. The key was focusing on trade-offs, not preferences."

---

## 8. Leadership

### Q: Have you led a team?

**If no formal lead role:**

> "I haven't had a formal lead title, but I've led features end-to-end. For the document processing app, I designed the architecture, coordinated the Python LLM integration, and mentored a junior developer on RabbitMQ basics. I believe leadership is about ownership and helping others, not just a title."

---

## 9. Time Management

### Answer

> "I prioritize by impact and deadline. At BASICX, production bugs come first, then sprint commitments, then tech debt. I break large features into daily goals — for the admin dashboard, I shipped member management before tournament features because it unblocked other work. I use a simple todo list and avoid context-switching between unrelated tasks."

---

## 10. Pressure Handling

### Answer

> "I stay calm and debug systematically. When our meal planning app had a payment issue before a launch, I didn't panic — I checked logs, reproduced the issue, identified a webhook race condition, and shipped a hotfix within hours. Pressure doesn't change my process: understand → isolate → fix → prevent recurrence."

---

## 11. Career Goals

### 2-Year Goal

> "Deepen my expertise as a senior full-stack engineer — system design, scalable architectures, and AI-powered products. I want to lead larger features and mentor junior developers."

### 5-Year Goal

> "Become a tech lead or staff engineer who can architect systems and guide a small team, while still staying hands-on with code. I'm particularly interested in the intersection of full-stack development and AI."

### Avoid

- "I want your CEO's job in 3 years"
- "I don't know"

---

## 12. Why This Company?

### Research before interview — template

> "Three things attract me: [1] Your product in [domain] — I've built similar systems like [relevant project]. [2] Your tech stack aligns with my experience in React, Node, and cloud deployment. [3] I've read about [specific company value, engineering blog, open source] and it matches how I like to work — shipping fast with quality."

### Examples to customize

| Company Type | Hook from your experience |
|--------------|---------------------------|
| E-commerce | Jewelry platform, ShopCart, Razorpay/Stripe |
| AI startup | Synapse AI, document LLM pipeline |
| SaaS | Admin dashboard, multi-tenant architecture |
| DevTools | Synapse GitHub/Linear integrations |

---

## 13. Why Are You Leaving?

### Safe answers (BASICX → new role)

> "I've learned a lot at BASICX building production apps, but I'm looking for [larger scale / stronger engineering culture / AI focus / better growth opportunities]. I want to work on [specific thing the new company offers] which aligns with where I want to take my career."

### Never say

- "Bad manager" (even if true)
- "Money only" (even if true — frame as growth + compensation)
- "Boring work" (sounds ungrateful)

---

## 14. Salary Expectations

### Strategy

1. **Deflect first:** "I'd like to understand the full role and benefits before discussing numbers. What's the budget for this position?"
2. **If pressed:** Give a researched range for your city + experience level
3. **For Jaipur / remote India (2025–2026):** Software Engineer with 1 year experience — research ₹6–12 LPA depending on company; adjust for Bangalore/Mumbai/hybrid

### Answer template

> "Based on my experience building production full-stack applications and the market rate for this role in [city], I'm looking at a range of ₹X to ₹Y LPA. I'm flexible depending on the full package — learning opportunities, tech stack, and growth matter to me too."

---

## 15. Relocation

### If willing

> "Yes, I'm open to relocating for the right opportunity. I'm currently based in Jaipur and flexible."

### If not

> "I prefer remote or hybrid. I've successfully deployed and maintained production apps remotely and stay productive with clear communication."

---

## 16. Work-Life Balance

### Answer

> "I'm committed during work hours and deliver on deadlines — I've shipped production features under pressure. I also believe sustainable pace produces better code. I recharge outside work so I can bring full focus during sprints."

---

## 17. Remote Work

### Answer

> "I've managed full project lifecycles independently — ShopCart from code to AWS deployment was solo work. I communicate proactively with updates, document my work, and am comfortable with async collaboration. For complex problems, I prefer a quick call over long Slack threads."

---

## 18. Notice Period

### Typical answer

> "My notice period is [30/60/90] days as per my offer letter at BASICX. I can discuss an early release if needed, depending on my current project handover."

> **Action:** Check your actual offer letter and fill this in before interviews.

---

## 19. Questions to Ask Interviewer

### Always ask 2–3

| Category | Question |
|----------|----------|
| Role | "What does success look like in the first 90 days?" |
| Team | "How is the engineering team structured? Will I work across the stack?" |
| Tech | "What's the current tech stack, and are there planned migrations?" |
| Growth | "What does the career path look like for engineers here?" |
| Culture | "How does the team handle production incidents?" |
| Product | "What's the biggest technical challenge the team is facing right now?" |

### For AI roles

> "How do you handle LLM cost and reliability in production?"  
> "Is the AI team separate from product engineering or integrated?"

### Red flag questions (if they dodge)

- "What's the attrition rate on the engineering team?"
- "How much technical debt is there vs new feature work?"

---

## 20. 100+ HR Questions with Answers

### Background & Education

| # | Question | Short Answer |
|---|----------|--------------|
| 1 | Walk me through your resume | Education → BASICX experience → personal projects → skills |
| 2 | Why CS? | Passion for building things; logic + creativity |
| 3 | Favorite subject? | Data structures, web development, DBMS |
| 4 | CGPA 8.2 — satisfied? | Solid foundation; balanced with practical projects |
| 5 | Extracurricular activities? | Personal projects deployed live; open source on GitHub |
| 6 | College project? | Mention strongest — Wanderly or ShopCart |
| 7 | Gap in education? | No gap — continuous 2020–2024 |
| 8 | Why Manipal Jaipur? | Good CS program, practical exposure |
| 9 | Certifications? | List any (AWS, etc.) or say self-taught via production work |
| 10 | How do you stay updated? | Engineering blogs, docs, building side projects |

### Experience & Skills

| # | Question | Short Answer |
|---|----------|--------------|
| 11 | Describe your current role | Full-stack at BASICX — 4 production apps |
| 12 | Day-to-day work? | Feature dev, bug fixes, API design, code review, deployments |
| 13 | Biggest project at work? | Document processing (RabbitMQ + LLM) or Admin dashboard |
| 14 | Frontend or backend preference? | Full-stack; enjoy both; React + Node equally |
| 15 | Experience with Agile? | Sprints, standups, retros (adjust to your reality) |
| 16 | Code review experience? | Give and receive; catches bugs early |
| 17 | Most used language? | TypeScript / JavaScript |
| 18 | Database experience? | MySQL (work), MongoDB (projects), PostgreSQL (Synapse) |
| 19 | Cloud experience? | AWS EC2, S3, Amplify; Docker, Nginx, SSL |
| 20 | DevOps experience? | GitHub Actions CI/CD, Docker, EC2 deployment |

### Behavioral (STAR)

| # | Question | Story to Use |
|---|----------|--------------|
| 21 | Challenging project? | RabbitMQ document pipeline |
| 22 | Tight deadline? | Feature ship before user launch at BASICX |
| 23 | Went above and beyond? | ShopCart full DevOps when not required |
| 24 | Made a mistake? | Stripe webhook env var story |
| 25 | Disagreement with manager? | Technical decision with data-driven resolution |
| 26 | Handled criticism? | Code review feedback improved code quality |
| 27 | Learned something quickly? | RabbitMQ / Strapi / Razorpay on the job |
| 28 | Worked with difficult person? | Focus on communication, not personality |
| 29 | Motivated others? | Helped teammate debug deployment issue |
| 30 | Initiative without being asked? | Set up CI/CD for ShopCart proactively |
| 31 | Prioritized multiple tasks? | Bug fix > sprint feature > tech debt |
| 32 | Dealt with ambiguity? | Document app — requirements evolved, iterated |
| 33 | Failed to meet deadline? | Honest answer + what you learned + how you communicated early |
| 34 | Proud of code quality? | TypeScript + Prisma type safety in Wanderly |
| 35 | Received negative feedback? | Took it constructively, improved |

### Situational

| # | Question | Short Answer |
|---|----------|--------------|
| 36 | Production is down — what do you do? | Alert team → check logs → rollback or hotfix → postmortem |
| 37 | Don't know the answer in a meeting? | "I'll research and follow up by [time]" |
| 38 | Assigned work outside expertise? | Learn quickly, ask for resources, deliver MVP |
| 39 | Team member not pulling weight? | Talk to them first, then escalate if needed |
| 40 | Ethical dilemma? | User data privacy, don't ship insecure auth |
| 41 | Two managers give conflicting priorities? | Escalate, clarify priority, communicate timeline impact |
| 42 | User reports critical bug Friday evening? | Triage severity, fix if critical, communicate status |
| 43 | Asked to cut corners on security? | Push back with data (OWASP, breach risk), propose alternative |
| 44 | New technology mandated? | Embrace, allocate learning time, prototype first |
| 45 | Bored at work? | Seek challenging tasks, propose improvements, side learning |

### Motivation & Fit

| # | Question | Short Answer |
|---|----------|--------------|
| 46 | What motivates you? | Building products people use; solving hard problems |
| 47 | Dream job? | Full-stack role with ownership and modern stack |
| 48 | Preferred company size? | Open — startup agility or mid-size stability |
| 49 | Startup vs MNC? | Startup: impact and speed. MNC: scale and mentorship. Both appeal. |
| 50 | Why software engineering? | Love creating tools that solve real problems |
| 51 | Where do you see yourself in 3 years? | Senior engineer, leading features |
| 52 | Will you pursue higher studies? | Not immediately; focused on industry experience |
| 53 | Hobbies? | Coding side projects, tech reading (be genuine) |
| 54 | How handle repetitive work? | Automate it (scripts, CI/CD) |
| 55 | What kind of manager do you want? | Clear goals, trusts ownership, gives feedback |

### Compensation & Logistics

| # | Question | Short Answer |
|---|----------|--------------|
| 56 | Current CTC? | State honestly (required for HR rounds) |
| 57 | Expected CTC? | Researched range; flexible on full package |
| 58 | Notice period? | [Your actual period] |
| 59 | Holding other offers? | Be honest if asked |
| 60 | When can you join? | Notice period + optional negotiation |
| 61 | Willing to travel? | Yes for necessary team meets |
| 62 | Bond or contract? | Ask to see terms; don't commit on spot |
| 63 | Work timings? | Flexible; deliver on commitments |
| 64 | Overtime? | Occasional for production issues is fine |
| 65 | Probation concerns? | Confident in delivering value quickly |

### Personality & Self-Awareness

| # | Question | Short Answer |
|---|----------|--------------|
| 66 | Three words to describe yourself? | Dedicated, curious, reliable |
| 67 | How would colleagues describe you? | Helpful, delivers on time, strong technically |
| 68 | Superpower? | Full-stack ownership |
| 69 | Kryptonite? | Public speaking (improving) |
| 70 | Book that influenced you? | Pick one genuinely (Clean Code, etc.) |
| 71 | Role model in tech? | Be genuine — open source maintainer, etc. |
| 72 | Handle boredom? | Side projects, learning new tech |
| 73 | Perfectionist? | Balance quality with shipping; MVP then iterate |
| 74 | Introvert or extrovert? | Ambivert — fine in teams and solo deep work |
| 75 | Stress management? | Exercise, breaks, systematic debugging |

### Company-Specific

| # | Question | Short Answer |
|---|----------|--------------|
| 76 | Know about our company? | Research product, funding, tech blog |
| 77 | Why not other companies? | This role fits my skills in [X] specifically |
| 78 | What value will you add? | Production experience, full-stack, AI if relevant |
| 79 | Long-term with us? | Yes, if mutual growth continues |
| 80 | Concerns about us? | Ask thoughtfully — not "nothing" |
| 81 | Interviewed elsewhere? | Honest; shows demand |
| 82 | What if we reject you? | Ask for feedback; keep improving |
| 83 | Preferred team? | Product engineering, full ownership |
| 84 | Client-facing role OK? | Yes if technical discussions |
| 85 | On-call rotation? | Understand it's part of production ownership |

### Tricky Questions

| # | Question | How to Handle |
|---|----------|---------------|
| 86 | Why were you fired? | N/A — don't invent |
| 87 | Biggest regret? | Not starting open source earlier / not learning X sooner |
| 88 | Age / personal life? | Redirect to professional qualifications |
| 89 | Politics at work? | Stay neutral; focus on work |
| 90 | Salary history? | Honest; frame as growth to current expectation |
| 91 | Weakness that's actually strength? | Avoid cliché "perfectionist" |
| 92 | Where else interviewing? | Company names OK; don't play offers against each other aggressively |
| 93 | What if role changes? | Flexible within engineering |
| 94 | Overqualified? | Eager to learn their scale/challenges |
| 95 | Underqualified? | Fast learner + proven project delivery |

### Closing Questions

| # | Question | Short Answer |
|---|----------|--------------|
| 96 | Anything else to add? | Enthusiasm + one key strength not discussed |
| 97 | Questions for us? | Always have 2–3 ready |
| 98 | When expect to hear back? | Polite ask for timeline |
| 99 | Can we contact references? | Yes (prepare references in advance) |
| 100 | Thank you email? | Send within 24 hours — brief, reference conversation highlight |
| 101 | Follow up after no response? | One polite follow-up after 1 week |
| 102 | Negotiate offer? | Yes — based on market research, not emotion |
| 103 | Accept on spot? | "I'd like to review the full offer in writing" |
| 104 | Decline offer professionally? | Thank them, brief reason, keep door open |
| 105 | Join and get counter-offer? | Decide based on career goals, not just money |

---

## 21. Do's and Don'ts

### Do

- Research the company before every interview
- Quantify achievements (1,000+ users, 30%, 70%)
- Use STAR for behavioral questions
- Send thank-you email within 24 hours
- Ask thoughtful questions at the end
- Be honest about notice period and CTC
- Dress one level above company norm
- Test video/audio for remote interviews

### Don't

- Badmouth BASICX or any employer
- Lie about skills you don't have
- Give one-word answers
- Ask about salary in the first 5 minutes
- Say "I have no weaknesses"
- Read resume verbatim
- Interrupt the interviewer
- Forget to prepare "Tell me about yourself"

---

## Quick Revision Card

```
ABOUT ME:     Ritik Gupta | BSc CS Manipal 8.2 | SWE @ BASICX
STRENGTH:     Full-stack ownership + production delivery
ACHIEVEMENT:  70% doc processing improvement / 1000+ users
WEAKNESS:     [Real one] + how I'm improving
WHY LEAVING:  Growth + [what new company offers]
SALARY:       Research range, flexible on package
NOTICE:       [Check offer letter]
ASK THEM:     90-day success + team structure + tech challenges
```

---

*Personalized for Ritik Gupta — ritikgupta856@gmail.com | ritikgupta.in*

<div align="center">

# Shivam Govind Rao

**Full-Stack Engineer · Agentic AI Systems · I ship end-to-end and dig into whether what I built actually works**

[![Portfolio](https://img.shields.io/badge/Portfolio-www.shivamgovindrao.com-f59e0b?style=for-the-badge&logo=vercel&logoColor=black)](https://www.shivamgovindrao.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/shivam-govind-rao-138881157/)
[![X (Twitter)](https://img.shields.io/badge/X-@BLAZE07SHADOW-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/BLAZE07SHADOW)
[![Email](https://img.shields.io/badge/Email-ishivamgovindrao@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:ishivamgovindrao@gmail.com)

</div>

---

Clinics get medical records as messy, unstructured faxes — someone has to read each one and enter the data by hand. I built the system that does it instead: a HIPAA-compliant document platform, live with paying US clinics, from the AI extraction pipeline to the React interface clinicians actually use.

I like the full loop — build it, ship it, then go find out where it's actually weak. At **Diagna AI**, I own **FAXFlo** end to end: the React frontend, the Node.js/TypeScript backend, and the AI pipeline that reads and classifies each document. When OCR couldn't reliably parse the mess, I moved extraction to vision LLMs on AWS Bedrock instead of forcing OCR to work.

Before that, at **Oriserve**, I built the frontend of **VoiceGenie**, a generative-AI voice sales platform — the customer dashboard and campaign builder in React/Redux, and the public marketing site on Next.js with server-side rendering. Grew from zero to $10K MRR in eleven months.

Outside of work I build **PayOps AI**, a multi-agent system that investigates and resolves payment reconciliation failures with a human in the loop; **MotionStudio**, a browser-based video editor with a real production backend; and **ClinRAG**, a from-scratch RAG system where I benchmarked hybrid vs. dense retrieval on real clinical documents and reported the results honestly, including where hybrid didn't win.

---

## What I've Shipped

| | |
|---|---|
| **HIPAA-compliant** | Clinical platform, live with paying US clinics |
| **94%+** | AI document classification accuracy — product metric, 20+ categories |
| **40+** | REST API endpoints designed and built (FAXFlo backend) |
| **47+** | Nested iframes navigated in a legacy EHR RPA integration |
| **7 / 7** | PayOps AI golden evals passing in live mode, plus adversarial and prompt-injection cases |
| **850+** | Automated tests across the PayOps AI packages |
| **4 RAGAS metrics** | Faithfulness, relevancy, precision, recall — benchmarked dense vs. hybrid retrieval (ClinRAG) |
| **$10K MRR** | Reached in 11 months as the frontend owner (VoiceGenie) |
| **0 → 1** | Took FAXFlo from company pivot to first paying clinic |

---

## Featured Project

### [PayOps AI](https://github.com/BLAZE7SHADOW/PayOps-AI) — Multi-Agent Payment Operations

**The problem.** In a payments business, one payment lives in five places: the gateway, the order service, the ledger, webhooks, and settlement. When they disagree — money captured but the order still says failed, a refund that never hit the ledger, a webhook that died, a settlement batch that doesn't add up — an ops analyst has to open five tools, work out which system is wrong, pick a safe fix, get it approved, and check it actually worked. It is slow, easy to get wrong, and every mistake touches real money.

**What it does.** PayOps AI detects those disagreements automatically and resolves them. A **LangGraph multi-agent system** investigates each case, cites the evidence for every claim, proposes a fix from a closed catalog of allowed actions, pauses for human approval when policy requires it, executes through deterministic code, and then has an independent validator re-read the data to confirm the fix really worked. If it didn't, the system replans within limits or escalates to a person.

#### Agentic AI and multi-agent orchestration

- **Orchestrated agents, not one big prompt.** A planner routes each case to specialist agents (payment, risk, and others) that run in parallel through LangGraph `Send` fan-out, then join. Each specialist reads only the tools it owns and writes typed findings.
- **A fast path and a full path.** Simple cases are diagnosed by a typed decision model plus code templates with no LLM call at all. Only genuinely ambiguous cases go to a full Gemini investigation, so cost and latency follow difficulty.
- **Six typed decision points.** Intake screening, planning, risk scoring, grounding, replanning and fast-path diagnosis each use a narrow Jev (TypeSafe System One) decision with probabilities and confidence, and each has a deterministic fallback if the model is down or unsure.
- **Human in the loop that survives a restart.** The graph interrupts for approval and resumes from a Postgres checkpoint, so a server restart doesn't lose a pending decision. Four-eyes approval applies to higher-risk actions.
- **Grounding before resolution.** Every finding must cite evidence ids. A grounding check drops claims the evidence doesn't support before anything is proposed.
- **Verify, then replan.** An independent validator re-reads the data after execution and returns PASS, PARTIAL or FAIL. A failure triggers a bounded replan instead of a silent retry.
- **Operator controls.** A global pause and propose-only mode stop auto-execution, and operators can rate each diagnosis Right or Wrong. That feedback feeds the accuracy metric.

#### Safety by design

The product has to work with AI turned off, and the agent is only one actor alongside humans, using the same catalog, policy, executor and validator.

- Models never touch the database. They see only context built from tool outputs.
- Models never authorize or execute. Policy decides the approval tier in code, and the executor acts with idempotency keys.
- Models never do arithmetic or date math. Money is integer paise and code passes computed results in as facts.
- Customer and merchant notes are screened for injection and never enter a prompt unwrapped.
- Every state change writes a **hash-chained, tamper-evident audit log** (append-only database triggers, verify endpoint, CSV export).
- PII is scrubbed from outbound prompts, with a test that fails if a canary name, email, phone or note ever leaves the system.
- A documented threat model and a table of exactly what goes to Gemini and Jev at each call. TOTP MFA, session revoke and one role-and-permission table enforced in code and docs.

#### Measured, not claimed

- Evals run in a deterministic **REPLAY** mode from recorded cassettes, so CI never calls a live API. The live eval report is committed in the repo (7/7), alongside adversarial variants and a prompt-injection suite.
- Failure drills cover a Gemini timeout, a Jev timeout and a database serialization conflict, plus a cost and tool-call budget guard on every run.
- A 10,000-payment volume test with detection timings, and 21 scenario variants including late webhooks, partial refunds, out-of-order events and duplicates.
- The Overview page reports resolution time, auto-resolution rate, agent accuracy (from operator ratings), approval turnaround and cost per case, each with its definition shown, and traces any case to its run and to every model call.

`TypeScript` `LangGraph` `LangChain` `Gemini` `Jev (TypeSafe)` `React 19` `Express 5` `Postgres` `Drizzle` `pg-boss` `Socket.IO` `Zod` `Vitest` `Playwright`

[GitHub](https://github.com/BLAZE7SHADOW/PayOps-AI)

---

## Projects

### [ClinRAG](https://github.com/BLAZE7SHADOW/ClinRAG) — Clinical Document RAG with Hybrid Retrieval + RAGAS Evals
A RAG system over real clinical drug labels (FDA DailyMed), built with a proper evaluation harness as the actual deliverable, not a demo. Docling extraction, three chunking strategies, Cohere embeddings via Bedrock with FAISS dense retrieval, BM25 + dense hybrid search via reciprocal rank fusion, and Claude Haiku generation constrained to answer only from retrieved excerpts.

Benchmarked dense-only against hybrid on RAGAS — faithfulness, answer relevancy, context precision, context recall — across 12 hand-verified questions. **Result: hybrid wasn't a clean win.** Better recall, worse faithfulness. I scoped reranking out on purpose once the numbers didn't justify the added complexity. Documented a real extraction failure (a corrupted PDF table) as a known limitation rather than hiding it.

`Python` `RAG` `FAISS` `BM25` `AWS Bedrock` `Cohere Embed v4` `Claude Haiku` `RAGAS`

[GitHub](https://github.com/BLAZE7SHADOW/ClinRAG)

### [MotionStudio](https://motionstudio-six.vercel.app/) — Browser Video Editor on Remotion
*Live · actively building.* Frame-accurate timeline editor exporting to MP4 — free in-browser (WebCodecs + OfflineAudioContext) or via a quota-gated AWS Lambda cloud render. Google OAuth, device-based abuse prevention, background S3 asset upload so uploads render correctly on the cloud path too.

`Remotion` `React 19` `TypeScript` `Zustand` `Supabase` `AWS Lambda` `Vercel`

[Live](https://motionstudio-six.vercel.app/) · [GitHub](https://github.com/BLAZE7SHADOW/MotionStudio)

### [FAXFlo](https://www.diagna.ai) — Diagna AI
HIPAA-compliant clinical document platform — clinical inbox, dual-view AI document editor, eFax, appointment scheduling, and an internal data-quality dashboard. Distributed AWS pipeline (S3, SQS, Bedrock) with multi-model AI routing (Claude Sonnet, Amazon Nova) for document classification and extraction, plus a Python RPA service for legacy EHR write-back. Taken from company pivot to its first paying US clinic, in production.

`React 19` `Node.js` `PostgreSQL` `AWS Bedrock` `Redis/BullMQ` `Robocorp` `FastAPI`

[Live](https://www.diagna.ai)

### [VoiceGenie.ai](https://voicegenie.ai) — Oriserve
Generative-AI voice sales platform. Built the customer dashboard and AI campaign builder (React, Redux) and the public marketing site (Next.js, App Router, SSR). Grew from 0 to $10K MRR in 11 months.

`React` `Next.js` `TypeScript` `Redux` `ElevenLabs` `HubSpot` `Cal.com`

[Live](https://voicegenie.ai)

---

## Tech Stack

**Frontend**

![React](https://img.shields.io/badge/React_19-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=next.js&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)
![Framer Motion](https://img.shields.io/badge/Framer_Motion-0055FF?style=flat-square&logo=framer&logoColor=white)
![Zustand](https://img.shields.io/badge/Zustand-433e38?style=flat-square)
![Redux](https://img.shields.io/badge/Redux-764ABC?style=flat-square&logo=redux&logoColor=white)
![Remotion](https://img.shields.io/badge/Remotion-FF5C5C?style=flat-square)

**Backend**

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![BullMQ](https://img.shields.io/badge/BullMQ-DC382D?style=flat-square)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=flat-square&logo=prisma&logoColor=white)
![Drizzle](https://img.shields.io/badge/Drizzle_ORM-C5F74F?style=flat-square&logo=drizzle&logoColor=black)

**Agentic AI & Retrieval**

![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![Multi-Agent](https://img.shields.io/badge/Multi--Agent_Orchestration-8B5CF6?style=flat-square)
![Gemini](https://img.shields.io/badge/Gemini-4285F4?style=flat-square&logo=googlegemini&logoColor=white)
![AWS Bedrock](https://img.shields.io/badge/AWS_Bedrock-FF9900?style=flat-square&logo=amazon-aws&logoColor=black)
![Claude](https://img.shields.io/badge/Claude-D97706?style=flat-square)
![Amazon Nova](https://img.shields.io/badge/Amazon_Nova-FF9900?style=flat-square&logo=amazon-aws&logoColor=white)
![RAG](https://img.shields.io/badge/RAG-6366F1?style=flat-square)
![FAISS](https://img.shields.io/badge/FAISS-0467DF?style=flat-square)
![RAGAS](https://img.shields.io/badge/RAGAS-10B981?style=flat-square)
![ElevenLabs](https://img.shields.io/badge/ElevenLabs-000000?style=flat-square)

**Cloud & Automation**

![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazon-aws&logoColor=white)
![AWS Lambda](https://img.shields.io/badge/AWS_Lambda-FF9900?style=flat-square&logo=awslambda&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=flat-square&logo=supabase&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white)
![Render](https://img.shields.io/badge/Render-46E3B7?style=flat-square&logo=render&logoColor=black)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white)
![Robocorp](https://img.shields.io/badge/Robocorp-00ADEF?style=flat-square)

---

## Currently

- Finishing **PayOps AI** — accessibility and end-to-end tests, then a free hosted demo (Vercel, Render, Supabase) that runs on recorded agent responses so anyone can try it.
- Shipping new features on **MotionStudio** solo — cloud render pipeline, background asset upload, export UX.
- Extending **ClinRAG** — persisted vector store, reranking evaluation, larger document set.
- Going deeper on agentic patterns: bringing what PayOps AI does with LangGraph orchestration, grounding and evals back to the multi-model routing I've already shipped in production.

---

## GitHub Activity

<div align="center">

![GitHub Streak](https://streak-stats.demolab.com/?user=BLAZE7SHADOW&theme=dark&hide_border=true)
&nbsp;&nbsp;
![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=BLAZE7SHADOW&layout=compact&theme=dark&hide_border=true)

</div>

---

<div align="center">

**Open to Full-Stack and AI Systems roles — especially healthcare and fintech**

[www.shivamgovindrao.com](https://www.shivamgovindrao.com)

</div>

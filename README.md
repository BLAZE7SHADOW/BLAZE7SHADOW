<div align="center">

# Shivam Govind Rao

**Full-Stack Engineer · AI Systems · I ship end-to-end and dig into whether what I built actually works**

[![Portfolio](https://img.shields.io/badge/Portfolio-www.shivamgovindrao.com-f59e0b?style=for-the-badge&logo=vercel&logoColor=black)](https://www.shivamgovindrao.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/shivam-govind-rao-138881157/)
[![X (Twitter)](https://img.shields.io/badge/X-@BLAZE07SHADOW-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/BLAZE07SHADOW)
[![Email](https://img.shields.io/badge/Email-ishivamgovindrao@gmail.com-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:ishivamgovindrao@gmail.com)

</div>

---

Clinics get medical records as messy, unstructured faxes — someone has to read each one and enter the data by hand. I built the system that does it instead: a HIPAA-compliant document platform, live with paying US clinics, from the AI extraction pipeline to the React interface clinicians actually use.

I like the full loop — build it, ship it, then go find out where it's actually weak. At **Diagna AI**, I own **FAXFlo** end to end: the React frontend, the Node.js/TypeScript backend, and the AI pipeline that reads and classifies each document. When OCR couldn't reliably parse the mess, I moved extraction to vision LLMs on AWS Bedrock instead of forcing OCR to work.

Before that, at **Oriserve**, I built the frontend of **VoiceGenie**, a generative-AI voice sales platform — the customer dashboard and campaign builder in React/Redux, and the public marketing site on Next.js with server-side rendering. Grew from zero to $10K MRR in eleven months.

Outside of work I build **MotionStudio**, a browser-based video editor with a real production backend, and **ClinRAG**, a from-scratch RAG system where I benchmarked hybrid vs. dense retrieval on real clinical documents and reported the results honestly, including where hybrid didn't win.

---

## What I've Shipped

| | |
|---|---|
| **HIPAA-compliant** | Clinical platform, live with paying US clinics |
| **94%+** | AI document classification accuracy — product metric, 20+ categories |
| **40+** | REST API endpoints designed and built (FAXFlo backend) |
| **47+** | Nested iframes navigated in a legacy EHR RPA integration |
| **4 RAGAS metrics** | Faithfulness, relevancy, precision, recall — benchmarked dense vs. hybrid retrieval (ClinRAG) |
| **$10K MRR** | Reached in 11 months as the frontend owner (VoiceGenie) |
| **0 → 1** | Took FAXFlo from company pivot to first paying clinic |

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

**AI & Retrieval**

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
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=flat-square&logo=playwright&logoColor=white)
![Robocorp](https://img.shields.io/badge/Robocorp-00ADEF?style=flat-square)

---

## Currently

- Shipping new features on **MotionStudio** solo — cloud render pipeline, background asset upload, export UX.
- Extending **ClinRAG** — persisted vector store, reranking evaluation, larger document set.
- Reading and building toward agentic workflow patterns on top of the multi-model routing I've already shipped in production.

---

## GitHub Activity

<div align="center">

![GitHub Streak](https://streak-stats.demolab.com/?user=BLAZE7SHADOW&theme=dark&hide_border=true)
&nbsp;&nbsp;
![Top Languages](https://github-readme-stats.vercel.app/api/top-langs/?username=BLAZE7SHADOW&layout=compact&theme=dark&hide_border=true)

</div>

---

<div align="center">

**Open to Full-Stack and AI Systems roles — especially healthcare tech**

[www.shivamgovindrao.com](https://www.shivamgovindrao.com)

</div>

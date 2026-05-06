# GenAI Engineer | Building Production-Ready AI Systems That Scale

**GenAI Engineer at Capgemini**, focused on building enterprise-grade AI systems that move from experimentation to real, scalable products.

I work at the intersection of **LLMs, product thinking, and cloud architecture**, helping teams go beyond proofs of concept into reliable, secure, and observable GenAI solutions aligned with real business constraints.

My expertise spans **end-to-end AI architecture, Agentic Systems, and LLMOps**, with hands-on experience designing, deploying, and maintaining production-ready AI workflows. I frequently bridge technical teams and business stakeholders to ensure feasibility, robustness, and long-term value — not demos for demos' sake.

Certified as a **Microsoft Azure AI Engineer**, with 7 additional AI-focused certifications accross different clouds, I emphasize applied AI, observability, governance, and measurable outcomes in regulated and enterprise environments.

---

## 📊 Selected Impact

| Metric | Result |
|--------|--------|
| Automation efficiency for business processes | **+40%** |
| Data classification and extraction workflows | **+50% faster** |
| Conversational AI accuracy | **+35%** |
| Solution relevance using RAG and vector databases | **+30%** |

---

## 🛠️ Technical Stack

**Languages & Backend:** Python, Node.js, TypeScript, FastAPI

**LLMs & Frameworks:** LangChain, LangGraph, CrewAI, AutoGen, LlamaIndex

**Cloud & Infrastructure:** Azure AI Foundry, AWS, GCP, Docker, Kubernetes, Redis (queues & caching)

**Data & Retrieval:** MongoDB, PostgreSQL, Vector Databases (Pinecone, Qdrant, Milvus, ChromaDB)

**Observability & Evaluation:** LangSmith, tracing, prompt evaluation, monitoring, custom metrics

**Additional:** OpenAI (GPT-4), Anthropic (Claude), n8n, Git

---

## 🎓 Certifications

- **Microsoft Azure AI Engineer Associate (AI-102)**
- **Databricks Generative AI Engineer Associate**
- **Google Generative AI Leader (GCP)**
- **AWS Certified AI Praticcioner**
- Salesforce AI Specialist
- Salesforce AI Associate
- Oracle AI Foundations
- Microsoft Azure AI Fundamentals (AI-900)

---

## 🏆 Featured Projects

A selection of key projects demonstrating end-to-end AI solution delivery. Click on the titles to explore the code/documentation in this repository.

### 🏢 [AI-Powered Procurement Intelligence Platform — Enterprise Microservices](https://github.com/juliocode-job/AI-Automation-Portfolio/tree/main/Agents%20Platform%20microservices)

**Problem:** A Fortune 500 telecom provider needed to process thousands of government tenders efficiently. Manual PDF ingestion, data extraction, and classification created bottlenecks, while batch uploads caused system timeouts and silent failures in the AI pipeline compromised data integrity.

**Solution:** Contributed to an enterprise-grade microservices platform featuring LLM-based data extraction, semantic embeddings, and real-time analytics. Implemented MongoDB-based job queues with HPA scaling, exponential backoff retry mechanisms, and circuit breaker patterns. Built comprehensive observability with correlation ID tracking across services and structured logging for production debugging.

**Stack:** TypeScript, Node.js, Fastify, MongoDB, LangChain, Azure OpenAI, Azure Kubernetes Service (AKS), Azure DevOps, Docker, Zod, Pino

**Impact:** Eliminated timeouts on batch uploads (50+ documents). Reduced integration delays through comprehensive API documentation. Enabled zero-downtime deployments with blue-green strategy and automated rollbacks.

---

### 🌌 [Violeta: Enterprise-Grade Multi-Agent Orchestration Ecosystem](https://github.com/juliocode-job/AI-Automation-Portfolio/tree/main/SDK%20Violeta%20(Multi%20Agents))

**Problem:** Organizations face "Agent Sprawl"—where agent logic, prompts, and model configurations are hardcoded, fragmented, and lack centralized governance or observability as AI adoption scales.

**Solution:** Architected a modular, scalable framework that decouples agent configuration from execution logic. Features a Centralized Registry (Control Plane) for versioned metadata and a Developer SDK (Data Plane) that standardizes the development lifecycle. Includes a modular middleware system for swappable business logic and built-in tracing.

**Stack:** Python, TypeScript, LangChain, FastAPI, Kubernetes (K8s), Docker, LiteLLM, Langfuse, Azure OpenAI.

**Impact:** Enabled deployment of 50+ specialized agents with 60% reduction in production troubleshooting time. Eliminated "shadow AI" through centralized governance.

---

### 🚀 [Strategic Sourcing Intelligence Engine — MCP Server](https://github.com/juliocode-job/AI-Automation-Portfolio/tree/main/MCP%20Agent%20with%20Microservices)

**Problem:** Procurement teams spend hours manually auditing commercial proposals and spreadsheets. Static analysis tools fail to handle unstructured financial data and complex tax logic across various file formats.

**Solution:** Developed a high-performance **MCP (Model Context Protocol)** Server that allows LLMs to act as specialized procurement agents. Implemented semantic header mapping for template-less data discovery and a multi-tier delta calculation engine for 100% audit accuracy. Built a "Stateless Restore" pattern to maintain complex analysis state across tool calls.

**Stack:** Python, MCP (Model Context Protocol), Pandas, NumPy, AsyncIO, XlsxWriter, ReportLab.

**Impact:** Transforms hours of manual spreadsheet auditing into seconds of AI-driven analysis. Provides automated premium dashboards and legal-ready governance PDFs.

---

### 🔧 [AI-Powered Pull Request Automation — Autonomous Code Fixing System](https://github.com/juliocode-job/AI-Automation-Portfolio/tree/main/n8n%20bug%20fixing%20system)

**Problem:** Development teams spend significant time on repetitive bug fixes and manual PR creation. Error-to-fix cycles are slow, and there's no systematic way to ensure proposed changes are safe and minimal before human review.

**Solution:** Built an end-to-end automation system that transforms error reports into validated pull requests. Uses Claude Opus for error analysis and constraint planning, Claude Sonnet for minimal diff generation. Features a 6-layer validation system (status, confidence, diff existence, language consistency, change limits, line verification).

**Stack:** n8n, Claude Opus, Claude Sonnet, GitHub API, Webhooks.

**Impact:** Automated the entire error-to-PR pipeline while keeping humans in the loop. PRs include AI justification and confidence levels.

---

### 🎯 [Agentic Market Research Team — Autonomous AI Intelligence System](https://github.com/juliocode-job/AI-Automation-Portfolio/tree/main/Agentic%20in%20Slack%20built%20in%20Langraph)

**Problem:** Companies struggle to understand their customers' psychological drivers. Managing multiple AI agents typically requires complex orchestration and lacks persistent learning.

**Solution:** Architected a Level 5 autonomous agent system with 6 specialized AI agents that decode customer psychology. Features persistent memory via Qdrant vector database and collaborative LangGraph workflows, accessible through natural Slack commands.

**Stack:** Python, LangChain, LangGraph, Anthropic Claude, Qdrant, Slack Bolt, FastAPI, Docker.

**Impact:** 3x higher conversion rates using extracted language patterns. Reduced market research time from weeks to hours with continuous autonomous improvement.

---

### 🧠 TeamBrain MVP — Secure Enterprise AI Agent

**Problem:** Employees waste hours searching for information across siloed wikis, drives, and documents. No guarantee users only access data they're authorized to see.

**Solution:** Built an enterprise AI assistant with a secure, ACL-aware RAG pipeline. Checks user permissions before retrieving information from vector database, ensuring data security at the core of every response.

**Stack:** Python, LangChain, RAG, Flask, OpenAI GPT-4o, ChromaDB, Docker

**Impact:** Instant access to authorized information with enforced access controls, significantly reducing internal data leak risk.

---

### 🎙️ ConvoBot — Intelligent AI Meeting Assistant

**Problem:** Critical decisions and action items lost in manual note-taking during meetings.

**Solution:** Developed a voice-activated AI agent that joins meetings (Google Meet, Zoom), provides real-time transcription, and delivers intelligent summaries. Uses RAG to create a searchable knowledge base of all past conversations.

**Stack:** Voice AI, RAG, LangChain, Whisper, FastAPI

**Impact:** Automated 100% of note-taking, reduced post-meeting admin work by 90%.

---

## 💡 What I Bring

I thrive in global environments where **innovation meets execution**, building AI systems designed to scale, perform, and deliver sustained ROI. My approach emphasizes:

- **Production-first mindset:** Solutions built for reliability, not just impressive demos
- **Observability & governance:** Tracing, monitoring, and compliance for enterprise environments
- **Business alignment:** Bridging technical teams and stakeholders for measurable outcomes
- **End-to-end ownership:** From architecture to deployment to maintenance

---

---

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/servicesfromjulio/)

📫 **Let's connect** — I'm always interested in challenging GenAI problems at enterprise scale.

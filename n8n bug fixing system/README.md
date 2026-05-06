# 🤖 Pull Request Automation

> **AI-powered automated code error fixing system** that creates pull requests with minimal, validated code changes using intelligent analysis and precise block diff generation. Built to handle complex repository modifications securely with a "Human in the Loop" layer.

[![Status](https://img.shields.io/badge/Status-POC→Production-orange)]()
[![AI](https://img.shields.io/badge/AI-Claude%20Opus%20%7C%20Sonnet-blueviolet)]()
[![Orchestration](https://img.shields.io/badge/Orchestration-n8n-green)]()

---

## 📋 Table of Contents

- [Overview](#overview)
- [Project Status](#-project-status)
- [Architecture](#architecture)
- [How It Works: Full Execution Flow](#-how-it-works-full-execution-flow)
- [Validation System](#-validation-system)
- [Technology Stack](#-technology-stack)
- [Engineering Decisions & Challenges Solved](#-engineering-decisions--challenges-solved)
- [Roadmap](#-roadmap)

---

## Overview

This project implements an end-to-end automation system that transforms error reports into validated pull requests, keeping humans in the loop for final approval.

**Core Capabilities:**
- Receives stack traces/errors via REST webhook (M2M) or an accessible Graphical UI Form (for QAs and Product Owners).
- Analyzes errors and plans targeted fixes using high-context AI (Claude Opus 4.6).
- Generates precise exact-match search/replace patches using AI (Claude Sonnet 4.6).
- Constructs native Git Objects (Blob, Tree, Commit) for perfect diff rendering on GitHub.
- Validates changes through a strict 6-layer safety engine.
- Creates pull requests tagged for human review, logging approval/rejection outcomes over time.

---

## 🎯 Project Status

| Aspect | Status |
|--------|--------|
| **Current Phase** | **POC → Production Migration** |
| **Team Structure** | **Expanding Team** (Currently onboarding new engineers) |
| **Project AI Lead** | **Júlio** (Creator, currently leading the project's team) |
| **Version** | **V3** (Git Data API, Block Search/Replace, Multi-Trigger) |

### V3 Improvements 

- **Git Data API Migration:** Abandoned standard file content endpoints in favor of atomic Git Object allocation (Blob → Tree → Commit). By enforcing `mode: "100644"`, we bypass a critical GitHub bug that rendered AI patch diffs as unreadable binary files.
- **Upgraded AI Engines:** Substituted Opus 4.5 and Sonnet 4.5 for their **4.6 counterparts**, unlocking massive context windows to comfortably read entire repository files without suffering from cognitive degradation—at zero extra API cost.
- **Search & Replace Diffing:** Replaced the line-sensitive array patching with a hermetic `search_block` and `replace_block` system, ensuring code patches are only applied if the target code slice matches 100% exactly.
- **Multi-Entrypoint Architecture:** Expanded the system to support a decoupled UI Form Trigger, granting non-technical staff (Support, POs, QAs) a friendly visual dashboard to report errors organically without terminal CLI experience.
- **Network Resilience:** Introduced systematic Exponential Retries across all key model inference and GitHub communication nodes to gracefully handle timeouts and network constraints.

---

## Architecture

The system is strategically fragmented into three independent but cooperative n8n workflows.

### Workflow 1: Automation Webhook (Machine-to-Machine)
Listens purely to POST requests via strict `headerAuth`. Designed for CI/CD pipelines, crash reporting bridges (e.g., Sentry), and deeper backend integrations.

### Workflow 2: Human UI Trigger
Employs an n8n Form Trigger protected by `basicAuth` to expose a clean Graphical UI. Accepts input variables like "Error Message" and "Context", sanitizes them, and submits them to the shared AI Code Construction pipeline.

### Workflow 3: Passive PR Handler
An independent listener webhook hooked to the GitHub repository to catalog when the AI's PRs are approved (merged) or rejected (closed). 

### Shared Construction Pipeline (Simplified)

```
┌─────────────┐       ┌─────────────┐
│ WEBHOOK (M2M)│   OR  │  FORM (UI)  │
└──────┬──────┘       └──────┬──────┘
       └──────────┬──────────┘
                  ▼
┌────────────────────────────────────────┐
│         Sanitize & Clean Input         │
└─────────────────┬──────────────────────┘
                  ▼
┌────────────────────────────────────────┐
│    Claude Opus 4.6 (Constraint Maker)  │
│  Extracts File, Line, and Error Scope  │
└─────────────────┬──────────────────────┘
                  ▼
┌────────────────────────────────────────┐
│     Fetch Github Code (Raw File)       │
└─────────────────┬──────────────────────┘
                  ▼
┌────────────────────────────────────────┐
│  Claude Sonnet 4.6 (Patch Generator)   │
│ Produces Exact Search & Replace Blocks │
└─────────────────┬──────────────────────┘
                  ▼
┌────────────────────────────────────────┐
│  6-Layer Safety & Validation Engine    │
└─────────────────┬──────────────────────┘
                  ▼
┌────────────────────────────────────────┐
│ Atomic Git Data API Execution:         │
│ 1. Create BLOB (base64)                │
│ 2. Create TREE (mode: 100644)          │
│ 3. Create COMMIT (linked to tree)      │
│ 4. Update BRANCH REF                   │
└─────────────────┬──────────────────────┘
                  ▼
┌────────────────────────────────────────┐
│             OPEN GITHUB PR             │
└────────────────────────────────────────┘
```


---

## 🔄 How It Works: Full Execution Flow

### Step 1: Error Reception
The error payload (message, stack trace, context) hits either the backend webhook or the UI Form trigger and undergoes regex sanitization.

### Step 2: AI Planning (Claude Opus 4.6)
Claude Opus analyzes the error payload to establish absolute constraints. It extracts the precise `file_path`, identifies the root `line_number`, dictates a maximum mutation limit (`max_lines_to_change`), and decides if the fix is even viable.

### Step 3: Source Retrieval
The orchestrator connects to GitHub, pulling the exact target file and mapping its SHA signature securely into memory.

### Step 4: Deterministic Patch Generation (Claude Sonnet 4.6)
Armed with the Opus blueprint and the raw source code, Claude Sonnet generates a rigid `search_block` (an exact multi-line replica of the broken code including adjacent context) and the corrected `replace_block`.

### Step 5: The Validation Engine
The system parses the output and runs 6 strict deterministic validations. If rules are broken (like the `search_block` not existing perfectly in the file string), the pipeline flags the generated PR as `[NEEDS-REVIEW]`.

### Step 6: Native Git Translation
The validated strings are purged of rogue Null Bytes (`\0`) and irregular CRLF mappings. The new text is base64-encoded via the native node APIs and pushed sequentially to GitHub's Blob, Tree, and Commit endpoints, finalizing branch creation.

### Step 7: Feedback Loop
Once the human developer interacts with the PR on GitHub, Workflow 3 registers the data for metric gathering and analytical improvement.

---

## ✅ Validation System

All proposed fixes must pass these 6 logic gates before the physical PR creation:

| # | Validation | Description | Fails When |
|:-:|------------|-------------|------------|
| 1 | **Status Check** | Opus identified a viable fix | `status ≠ "fix_found"` |
| 2 | **Confidence Gate** | Sonnet feels confident executing it | `confidence = "low"` |
| 3 | **Diff Presence** | A mutation array exists | `diff[]` is empty |
| 4 | **Syntax Consistency** | Output syntax matches original syntax | `output_language ≠ original_language` |
| 5 | **Impact Limit** | Respects Opus' mutation limit | `lines_changed > max_lines_to_change` |
| 6 | **Total Idempotency**| `search_block` perfectly exists in target file | `String.includes()` returns false |

---

## 🛠 Technology Stack

| Layer | Component | Description |
|-----------|------------|---------|
| **Orchestration** | **n8n** | Complex visual event-loop architecture handling API lifecycles and HTTP retry behaviors. |
| **Logic (Planning)** | **Claude Opus 4.6** | Phenomenal large-context analytical reasoning for blueprinting technical constraints. |
| **Logic (Writing)** | **Claude Sonnet 4.6** | Highly responsive coding and text replacement generation. |
| **Version System** | **GitHub API** | Direct Git Data API (Blobs, Trees) interaction to bypass standard file creation wrappers. |

---

## 🏗 Engineering Decisions & Challenges Solved

### 1. The Binary Diff Rendering Bug
**Problem:** In V2, using the abstracted `PUT /contents/` Github route to edit files was silently corrupting MIME signatures, coercing the Github interface to render the updated files as "Binary Files" blocking all visual "Diff" validations for human reviewers.

**Solution:** Completely decoupled the commit creation process by imitating the local Git CLI inside the backend API:
* First, we generate a Git **Blob** with stringified Base64 content.
* We then assign it to a Git **Tree**, strictly locking the parameter `mode: "100644"`. This explicitly forces GitHub's interface to interpret the data as plain human-readable text.
* Finally, we mint a Git **Commit** connected to that Tree and push the **Ref** to the branch.
* *Result:* 100% bug-free visually rendered Pull Requests.

### 2. Hermetic Multi-Line Patching
**Problem:** Altering code iteratively by array indexes (lines 10 to 12) is severely fragile because formatting engines often offset arrays by 1 or 2 lines. 

**Solution:** Evolved the AI interaction into an exact string `search_block` and `replace_block` system. The AI is ordered to supply the exact broken lines alongside 2 lines of prefix/suffix context. During the Validation Engine step, the application runs a literal `includes()` array search. If spacing or formatting doesn't perfectly match, it aborts or flags the PR, guaranteeing absolute integrity of the untouched code.

### 3. Democratizing the Engine (UI Trigger)
**Problem:** Webhooks and CLI interfaces limit bug-reporting automation to developers and CI pipelines.

**Solution:** Introduced a secondary isolated workflow serving as a Form-Based UI. This provides Product Owners, Quality Assurance Analysts, and Tier-1 Support visually intuitive text areas to dump stack traces without technical friction, vastly scaling the automation's utility scope across the corporate structure.

### 4. Exponential Retry Resiliency 
**Problem:** 5 sequential HTTP POSTs for Git Data Tree construction, coupled with 2 heavy LLM inferences, created susceptibility to intermittent API timeouts, rate-limits, and network spikes.

**Solution:** Instituted rigorous node-level `Exponential Retry` configurations (`maxTries: 3`, escalating timeouts) across all vulnerable data nodes, resulting in a fault-tolerant mesh that inherently absorbs standard API latency issues without corrupting the operational loop.

---

## 🗺 Roadmap

### Observability & Refinement
- [ ] Incorporate structured JSON logging for deeper Kibana/Datadog metric analysis.
- [ ] Calculate specific token expenditure and latency per fix to baseline cost models.
- [ ] Expose dashboard for PR success/failure conversion rates.

### Scale & Intelligence
- [ ] Map Multi-repository and Enterprise Organization deployment support limits.
- [ ] Introduce heuristic learnings: dynamically updating system prompts based on logs from historically rejected PRs.
- [ ] Deploy parallel processing queues to accommodate high-volume batch error resolution.

---

<p align="center">
  <sub>Portfolio Showcase — System designed, built from scratch, and led by Júlio</sub>
</p>

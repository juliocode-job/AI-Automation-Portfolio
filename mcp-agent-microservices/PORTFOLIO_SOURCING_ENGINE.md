# Strategic Sourcing Intelligence Engine — MCP Server

### 🚀 Technical Showcase: AI-Driven Procurement & Analytics Agent

This project features a high-performance **MCP (Model Context Protocol) Server** designed to automate the complex analysis of commercial proposals in enterprise procurement environments. The engine acts as a specialized AI agent capable of processing unstructured financial data, identifying savings opportunities, and generating executive-level reports.

---

## 🛠️ Core Technologies
- **Protocol**: MCP (Model Context Protocol) for seamless AI integration.
- **Language**: Python 3.11+
- **Data Engineering**: Pandas, NumPy (Vectorized financial calculations).
- **Reporting**: XlsxWriter (Advanced Dashboards), ReportLab (Governance PDFs).
- **Orchestration**: FastMCP, AsyncIO (High-concurrency session management).

---

## 🏗️ System Architecture

The engine is built on a **Stateless & Cloud-Native** philosophy, operating as a bridge between an AI Orchestrator and Enterprise File Repositories.

### 1. Model Context Protocol (MCP) Integration
Implemented as an MCP Server using **STDIO transport**, allowing any LLM (Claude, GPT-4, etc.) to invoke complex sourcing tools. The architecture ensures process isolation while maintaining high-speed data exchange.

### 2. Intelligent Data Discovery
- **Semantic Header Mapping**: Uses fuzzy logic and vocabulary density analysis to identify pricing tables across various Excel/CSV formats without predefined templates.
- **Adaptive Column Identification**: Automatically maps "Price", "Quantity", "SKU", and "Supplier" columns using semantic scoring, handling multiple languages and internal ERP formats.

### 3. Financial Intelligence Engine
- **Multi-Tier Delta Calculation**: Implements complex tax and pricing logic (Net -> ERP Price -> Gross) with floating-base math to ensure 100% audit accuracy.
- **Dynamic Scenarios**: Supports real-time adjustments (e.g., applying discounts or removing vendors) directly via natural language prompts.

---

## 🛡️ Engineering Challenges & Solutions

### Adaptive Security Bridge (v0.5.1)
**Challenge**: Managing authentication in isolated MCP processes where session tokens are not natively inherited.
**Solution**: Developed an "Auth Bridge" that handles dynamic security contexts. The engine prioritizes tool-injected headers while maintaining robust fallbacks for local and development environments, ensuring 100% uptime regardless of the platform's security state.

### Stateless Session Orchestration
**Challenge**: Large-scale financial analysis requires state, but MCP tools are inherently stateless.
**Solution**: Implemented a "Stateless Restore" pattern where the engine re-synchronizes the analysis state across multiple tool calls by efficiently managing temporary assets and cloud repository interactions.

---

## 📊 Key Features & Deliverables

- **Premium Excel Dashboard**: Automatic generation of stacked-bar charts, financial data tables, and scope coverage reports with professional aesthetics.
- **Automated Governance PDFs**: Generation of legal-ready adjudication summaries including audit notes and risk assessments.
- **Lead-Time Analysis**: Tracking and reporting on supplier SLAs and delivery schedules.

---

## 📈 Impact
This engine transforms hours of manual spreadsheet auditing into a few seconds of AI-driven analysis, providing procurement teams with clear, data-backed insights on savings and supplier performance.

---
*Note: This project was developed as a specialized component for a major Telecommunications AI Platform.*

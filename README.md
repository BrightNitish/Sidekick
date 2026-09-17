# Agentic AI & Autonomous Systems (LangChain, LangGraph & MCP)

A complete repository covering production-grade Agentic AI architectures, progressing from foundational tool calling to stateful cyclic workflows, browser automation with the Model Context Protocol (MCP), and an autonomous evaluator-in-the-loop assistant.

---

## 🌟 Flagship Project: Sidekick Agent

**Sidekick** is an autonomous assistant built with **LangChain (`create_agent`)** and **LangGraph**. It wraps a worker agent inside a closed-loop evaluator harness that verifies results against explicit user-defined success criteria, orchestrates external tools via the **Model Context Protocol (MCP)**, and integrates human-in-the-loop approvals before high-stakes operations.

### Architecture Workflow

User Request + Success Criteria
               │
               ▼
┌───────────────────────────────┐
│     Worker Agent (Layer 3)     │ ◄─────────┐
│  - Middleware Pipeline        │            │
│  - MCP Playwright Browser     │            │
│  - Sandbox & System Tools     │            │
└──────────────┬────────────────┘            │
               │ Output & Tools Used         │ Retry with Feedback
               ▼                             │ (Up to MAX_ATTEMPTS)
┌───────────────────────────────┐            │
│       Evaluator Loop          │            │
│  - Structured Output Parsing  │── Rejected ┘
│  - Criteria Verification      │
└──────────────┬────────────────┘
               │ Passed / User Clarification Needed
               ▼
          Final Answer
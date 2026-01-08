# BasecampAgent Overview
BasecampAgent is a hybrid, local-first agentic AI system designed to maximize performance by dynamically offloading tasks between disparate hardware units.

Unlike traditional agent frameworks that rely on cloud APIs or heavy abstractions, Basecamp is built to run entirely on-device, leveraging the unique strengths of the AMD Strix Halo APU and RDNA 4 eGPU architectures. It features a custom "Infinite Context" memory management system to maintain high performance within strict VRAM constraints.

# No-Framework Agency
Basecamp is built on raw Python and llama.cpp (via llama-cli). By avoiding frameworks like Langchain or CrewAI, the system achieves:
- Minimal Latency: No middle-man abstractions between the orchestrator and the LLM.
- Hardware Transparency: Direct control over which model runs on which silicon.
- Privacy: 100% local inference with zero external API calls.

# System Architecture
Basecamp operates as a two-tier hierarchy to balance speed (inference) with depth (reasoning).

**1. The Orchestrator (Fast Logic)**
- Hardware: AMD RX 9070 (16GB VRAM).
- Role: Handles the primary chat interface, tool routing, and immediate task execution.

**2. The Heavy Agent / Summarizer (Deep Thinking)**
- Hardware: AMD Strix Halo (8060S iGPU) via 128GB Unified Memory.
- Role: Handles "Deep Research" (long-chain reasoning) and recursive memory summarization.

# Technical Features
- Hardware-Locked Tooling: A mutex-based locking system ensures that heavy tasks do not collide or crash the iGPU.
- Hardened Toolset:
  - smart_search: Parallel web scraping and synthesis.
  - deep_think: Delegated long-form reasoning.
  - execute_command: Direct Ubuntu bash integration.
  - write_file/read_workspace_file: Local workspace management.
- State-Aware Injection: High-visibility hardware status (Busy/Available) is injected into every prompt turn, allowing the agent to manage its own queueing.

# Software Stack
- Engine: llama.cpp

- Language: Python 3.12+

- Database: SQLite3 (Persistent message logging)

- Networking: Flask/Requests (Inter-agent communication)


# Future Roadmap:

 -Recursive Memory Management: Automatically slices and summarizes conversation history using the Strix Halo to keep the Orchestrator lean.
 -Vocal Integrations: Allowing the system to communicate through a voice-first system, rather than a CLI.

 # NOTE:
  This page does not walk you through the installation or usage of the system. 
  Additionally, while I may make occasional updates to the system, I intend to pivot towards a Langchain/Deepagents based system for convinience and ease-of-use.

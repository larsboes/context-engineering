# Resources — Context Engineering

Gesammelte Quellen aus dem Talk. Primärquellen first. Sekundärquellen danach.

---

## 📄 Papers & Essays (Primärquellen)

### Context Rot — die zentrale Evidenz
**Hong, Troynikov, Huber — Chroma Research · July 2025**
*"Context Rot: How Increasing Input Tokens Impacts LLM Performance"*
→ https://research.trychroma.com/context-rot

Testet 18 LLMs (GPT-4.1, Claude 4, Gemini 2.5, Qwen3). Zeigt: Accuracy sinkt nicht-linear mit Input-Länge, auch auf simplen Tasks. Die Grundlage für Slide 10.

### Anthropic Engineering — das pragmatische Playbook
**Anthropic Engineering Blog · September 2025**
*"Effective Context Engineering for AI Agents"*
→ https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents

*"Context is a finite resource with diminishing marginal returns."* Primärquelle für die n²-pairwise-relationships Aussage (KV-Cache non-linearity). Plus die drei Long-Horizon-Techniken: Compaction, Structured Note-taking, Sub-Agent Architectures.

### Skills Guide — Progressive Disclosure offiziell definiert
**Anthropic · Complete Guide to Building Skills for Claude** (post-Sonnet 4.5)
Die kanonische Definition des 3-Level Progressive Disclosure Patterns (YAML Metadata / SKILL.md Body / Linked Files). Auch die YAML-Frontmatter-Spec (`name`, `description`, 1024 char limit, kebab-case).

### Externalization — die akademische Dachsicht
**arXiv:2604.08224 · 9 April 2026**
*"Externalization in LLM Agents: A Unified Review of Memory, Skills, Protocols and Harness Engineering"*
→ https://doi.org/10.48550/arXiv.2604.08224

Das Paper hinter Slide 35. Three-Layer-Evolution: Weights → Context → Harness seit 2022.

### Lost in the Middle — der Attention-Decay
**Liu et al. 2023 · arXiv:2307.03172**
*"Lost in the Middle: How Language Models Use Long Contexts"*
→ https://arxiv.org/abs/2307.03172

20% Accuracy-Loss bei Info in der Mitte langer Contexts. Erklärt warum 1M-Context-Windows nicht das Problem lösen.

### Many-shot Jailbreaking — Security × Context
**Anil, Durmus, Panickssery, Sharma et al. · Anthropic · April 2024**
*"Many-shot Jailbreaking"* (NeurIPS 2024)
→ https://www.anthropic.com/research/many-shot-jailbreaking

Zentrale Aussage: Jailbreak-Erfolg skaliert als Power Law mit Context-Länge. Größere Context-Windows sind messbar exploitablerer. Grundlage für die Kai-Bridge auf Slide 15.

### Indirect Prompt Injection — der andere Angriffsvektor
**Greshake et al. · arXiv:2302.12173 · AISec@CCS 2023**
*"Not what you've signed up for"*
→ https://arxiv.org/abs/2302.12173

Angriff muss nicht vom User kommen — poisoned Dokument im RAG reicht. Der strukturelle Grund warum Simons Lethal Trifecta Sinn ergibt.

---

## 🎤 Talks (Video / Transkripte)

### Mario Zechner — "Building Pi in a World of Slop"
Scale AI · 2025
Der Talk hinter Slide 17-22. Terminus Paradox, "mess around and find out", "My context wasn't my context", "bash is all you need".

### Mario Zechner — "I Hated Every Coding Agent, So I Built My Own"
AI Engineer London · 2025
Tiefere Version. Pi technical details, System Prompt philosophy, hooks.

### Lucas Meijer — "A Love Letter to Pi"
Structure Conference
Stilistisches Vorbild für Akt II. Humility-first opening, metaphor-pivots, mid-talk reveal of the "Love Letter" frame.

### Pranav Marla — "Getting More Out of Lua in Fluent Bit"
Fidelity Investments · KubeCon
Quelle für Lua-in-FluentBit Gotchas: Global-by-default, LuaJIT 5.1 Version Trap, Float Precision, Truthiness, Main Function Hygiene. Stage-Material für Q&A zu Slide 26-27.

### IndyDevDan (Channel)
Playlist mit Fokus auf Harness Engineering, Agent Experts, Meta-Agentics, 5 Agent Patterns, Pi Teams.
→ https://www.youtube.com/@indydevdan

---

## ✍️ Posts & Essays

### Armin Ronacher — Pi: The Minimal Agent Within OpenClaw
Januar 2026
→ https://lucumr.pocoo.org/2026/1/31/pi/

Zentrale Quote-Quelle (Slide 32). Plus die Rationale hinter "MCP → CLI" replacement und der OpenClaw-Validation.

### Simon Willison — Prompt Injection & The Lethal Trifecta
Laufend seit 2022, regelmäßige Updates
→ https://simonwillison.net/tags/prompt-injection/

Die drei gefährlichen Fähigkeiten in einem Agent: (1) Private Data, (2) Untrusted Content, (3) External Comms.

### Simon Willison — Claude Skills
Oktober 2025
→ https://simonwillison.net/2025/Oct/16/claude-skills/

*"I expect we'll see a Cambrian explosion in Skills which will make this year's MCP rush look pedestrian by comparison."*

### Simon Willison — Code Execution with MCP
November 2025
→ https://simonwillison.net/2025/Nov/4/code-execution-with-mcp/

*"I don't use MCP at all any more when working with coding agents."*

### Simon Willison — Designing Agentic Loops
September 2025
→ https://simonwillison.net/2025/Sep/30/designing-agentic-loops/

Pragmatische Agent-Definition + Sandbox-Advice + "An AI agent is an LLM wrecking its environment in a loop" (quoting Solomon Hykes).

### Anthropic — Code Execution with MCP
→ https://www.anthropic.com/engineering/code-execution-with-mcp

Das paralleler Pfad zum Skills-Ansatz. 150.000 → 2.000 Tokens = 98.7% Reduktion.

### Cognition — Don't Build Multi-Agents
Walden Yan
→ https://cognition.ai/blog/dont-build-multi-agents

Zwei Prinzipien: *"Share context, share full agent traces, not just individual messages"* + *"Actions carry implicit decisions, and conflicting decisions carry bad results"*. Wichtiger Gegenpunkt zur Subagent-Begeisterung.

### IBM — Was ist ein Kontextfenster?
Oktober 2024 · auf IBM Think
→ https://www.ibm.com/de-de/think/topics/context-window

Deutsche Grundlagen-Quelle. Quadratische Self-Attention + Connection zu Many-shot Jailbreaking.

---

## 🛠️ Tools im Talk

### Pi Agent (Mario Zechner)
→ https://github.com/badlogic/pi-mono

Minimal agent, 4 Tools, <1000 Tokens System Prompt, TypeScript Extensions, Session Branching.

### OpenClaw
→ https://openclaw.ai/

OSS Desktop AI Assistant. Pi ist der agentic core.

### Claude Code
→ https://claude.com/claude-code

Anthropic's Coding Agent. MCP, Agent Skills, Dynamic Loading, Memory.

### Anthropic Agent Skills (offizielle Engineering-Seite)
→ https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills

Anthropic's offizielle Einführung zu Agent Skills.

### Docker MCP Gateway
→ https://docs.docker.com/ai/mcp-catalog-and-toolkit/mcp-gateway/

Infrastruktur-Layer: ein Endpoint, Container-isoliert, Katalog mit 200+ MCP Servern, zur Laufzeit zuschaltbar.

### Docker Dynamic MCP
→ https://docs.docker.com/ai/mcp-catalog-and-toolkit/dynamic-mcp/

Ergänzend zum Gateway: dynamisches Laden von MCP Servern bei Bedarf.

### TerminalBench
→ https://terminalbench.com/

Benchmark für Coding Agents. Terminus (minimal agent) schlägt dort Systeme mit 10x mehr Tooling.

### Chroma (Vector DB + Context Rot Research Team)
→ https://www.trychroma.com

### cchistory (Mario Zechner)
→ https://cchistory.mariozechner.at/

Tool das System-Prompt-Änderungen in Claude Code über Releases tracked. Slide 15 Screenshot kommt von hier.

---

## 🎯 Die Quotes die ihr euch merken solltet

Für eure eigenen Slides, Blogposts oder Diskussionen.

- Mario: *"We are in the mess around and find out phase of coding agents."*
- Mario: *"My context wasn't my context."*
- Mario: *"Bash is all you need."*
- Armin: *"I fully replaced all my CLIs or MCPs for browser automation with a skill that just uses CDP."*
- Simon: *"If your agent combines [private data, untrusted content, external comms], an attacker can easily trick it into accessing your private data and sending it to that attacker."*
- Simon: *"I expect we'll see a Cambrian explosion in Skills."*
- IndyDevDan: *"Agentic engineering is knowing what your agents are doing so well you don't have to look."*
- IndyDevDan: *"Generic agents execute and forget. Agent experts execute and learn."*
- IndyDevDan: *"Complexity should be earned, not assumed."*
- Cognition: *"Share context, share full agent traces, not just individual messages."*
- Tobi Lütke: *"[Context engineering is] the art of providing all the context for the task to be plausibly solvable by the LLM."*

---

## 🏁 Wenn ihr 10 Minuten habt

Lest in dieser Reihenfolge:
1. [Chroma Context Rot](https://research.trychroma.com/context-rot) — 3 min, gibt euch den mechanistischen Kern
2. [Anthropic Effective Context Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — 5 min, das Playbook
3. [Armin Ronacher — Pi](https://lucumr.pocoo.org/2026/1/31/pi/) — 2 min, die philosophische Position

Fertig. Alles andere ist Tiefenbohrung.

---

*Falls ein Link down ist oder ich was Wichtiges vergessen habe: PR oder Issue in diesem Repo. Danke.*

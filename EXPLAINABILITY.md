# EXPLAINABILITY — AgentiLoop Desktop Agent

> **Admissibility & Transparency Report for OpenGAP / Agent Passport**  
> *Agent Name:* AgentiLoop Desktop Agent (`agentiloop-agent`)  
> *Specification:* OpenGAP v0.1.0  
> *Domain:* Developer Tools / Native Autonomous Desktop Agent Harness  

---

## 1. Overview & Operational Purpose

The **AgentiLoop Desktop Agent** (`agentiloop-agent`) is a native autonomous desktop AI agent harness and runtime. Built to operate seamlessly on local machines with multi-platform CLI extensions, AgentiLoop wires 23 LLM providers (including Claude, Codex, OpenAI, DeepSeek, Gemini, and Ollama) and on-device Apple Intelligence into an autonomous task execution loop.

The agent carries out end-to-end developer workflows: reading and refactoring codebases, building Xcode and Swift projects, generating unified diffs, running sandboxed terminal commands, and driving desktop applications via the native Accessibility subsystem. All operations prioritize local sovereignty, deterministic verification, and transparent human oversight.

---

## 2. How the Agent Decides (Decision-Making Logic)

AgentiLoop Desktop Agent operates across a deterministic, multi-stage decision pipeline:

```
[User Intent / Task Prompt] ──> [Task Decomposition & Safety Gate] ──> [Model Provider Routing]
                                                                                │
                                                                                ▼
[User Output / Audit Log] <── [Verification & Diff Gate] <── [Tool & Shell Execution]
```

### 2.1 Autonomous Task Planning & Loop Iteration
- **Decision:** Determines whether an incoming developer goal requires single-step answers or multi-turn agentic execution loops.
- **Rules:**
  - Evaluates user goal complexity; constructs a structured, dependency-ordered plan for multi-action coding tasks.
  - Iterates across available tools (coding diff engine, shell executor, accessibility driver) until task success criteria are achieved.
  - Re-evaluates plan status after each tool response; adjusts subsequent steps dynamically upon encountering build or execution errors.

### 2.2 Provider Selection & Token Compaction
- **Decision:** Selects optimal LLM inference providers and determines when conversation context requires summarization.
- **Rules:**
  - Directs reasoning tasks to user-configured primary providers, monitoring rate limits and response latencies.
  - Automatically executes failovers across the 23-provider chain upon detecting HTTP 429 quota exhaustion or network timeouts.
  - Triggers context compaction and prompt distillation when cumulative message tokens approach provider context boundaries.

### 2.3 Surgical Code Modification & Diff Verification
- **Decision:** Determines whether to read files, search symbols, or apply unified diffs during code refactoring.
- **Rules:**
  - Generates minimal unified diffs targeting specific line ranges rather than rewriting entire files.
  - Verifies target file presence, line markers, and indentation before applying file patches.
  - Dispatches test builds (e.g. `swift build`, `cargo test`) to confirm that code modifications compile cleanly without regressions.

### 2.4 Shell Safety Classification & Privilege Gating
- **Decision:** Analyzes proposed terminal commands and determines execution risk tiers before spawning processes.
- **Rules:**
  - Scans command strings for dangerous patterns, unauthorized deletions, or unsafe environment modifications.
  - Classifies operations into Read-Only (auto-executed), Safe Write (sandboxed), and Privileged/Root (requires human approval).
  - Enforces execution timeouts to terminate runaway scripts or unresponsive background daemons.

---

## 3. Data Sources & Inputs Used

| Data Input | Source | Purpose | Data Handling & Privacy |
| :--- | :--- | :--- | :--- |
| User Prompts & Instructions | GUI Input Bar / Voice / CLI arguments | Directs tasks, code generation, and automation | Processed ephemerally, never logged to external servers |
| Local Workspace Codebase | Project folders selected by user | Provides context for bug fixes and feature development | Read locally on disk, patches applied in place |
| Terminal Output & Build Logs | Host shell environment (`stdout`/`stderr`) | Supplies compiler diagnostics and execution telemetry | Captured in local session memory, no PII retained |
| Application UI Element Trees | Native OS Accessibility subsystem | Allows GUI automation of development applications | Queried on demand, sensitive fields strictly ignored |

AgentiLoop Desktop Agent complies with operational security and privacy standards:
- **No Cloud Data Exfiltration:** All source code, local files, and configuration data remain strictly within the user's host environment.
- **Epistemic Isolation:** Session memories and tool execution results are partitioned per task, preventing cross-project state pollution.
- **Sanitized Model Payloads:** Prompts dispatched to upstream providers are stripped of local credentials and unreferenced file contents.
- **Data Minimization:** Only relevant file sections, targeted diffs, and essential error traces are transmitted during LLM inference.

---

## 4. Known Limitations & Failure Modes

Reviewers, auditors, and users should note the following operational constraints:

1. **Accessibility Permission Revocation:**
   - *Limitation:* If macOS Accessibility permissions are revoked, GUI automation features become unavailable.
   - *Mitigation:* Graceful degradation to CLI/terminal operations and proactive diagnostic prompts guiding permission re-enablement.

2. **Upstream Provider Rate Limits:**
   - *Limitation:* Burst API usage across frontier models can trigger HTTP 429 throttling.
   - *Mitigation:* Automated failover through the configured fallback chain and support for local offline models (Ollama/Apple Intelligence).

3. **Complex Merge Conflicts on Rapid Edits:**
   - *Limitation:* External file modifications during multi-step agent edits can invalidate line markers in proposed diffs.
   - *Mitigation:* Re-reading file contents before patch application and rolling back changes upon diff rejection.

4. **Long-Running Process Timeouts:**
   - *Limitation:* Massive compilations or slow network downloads may exceed default execution thresholds.
   - *Mitigation:* Configurable step timeouts and asynchronous task monitoring with manual cancellation options.

---

## 5. Verification, Safety & Human Oversight

- **Real-Time Human Approval Gate:** Potentially hazardous shell commands, root escalations, and critical file deletions mandate explicit human authorization.
- **Emergency Session Interrupt:** Users can instantly halt the agentic loop at any moment via the GUI stop button, global hotkey, or CLI interrupt signal.
- **Step Quota Guardrails:** Hard execution step quotas and token caps prevent runaway iterative loops and excessive billing.
- **Structured Audit Logging:** Every executed tool action, shell command, applied diff, and provider switch is recorded in a tamper-resistant local activity log.

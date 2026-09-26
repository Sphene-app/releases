# Sphene vs. Obsidian: Empirical Systems & AI Agent Benchmarks

**Date:** September 27, 2026  
**Testbed Hardware:** AMD Ryzen AI 9 HX 370 (Zen 5, 24 Logical vCPUs), 14Gi RAM, NVMe Storage  
**Host Environment:** Ubuntu 26.04 LTS (Kernel `7.0.0-31-generic`), Display Server Wayland / Xwayland  
**Target Systems:**  
- **Sphene Core v2.2.25:** Compiled Go daemon, embedded SQLite WAL FTS5 index, native Model Context Protocol (MCP) server.  
- **Obsidian v1.13.7:** Official AppImage, Electron desktop runtime (Chromium 124 / Node.js V8 engine).  

All benchmark harnesses, synthetic vault generators, and telemetry profilers are open-source in [`sphene-org/scripts`](https://github.com/sphene-org/scripts).

---

## 1. System Scaling Matrix: Resource Utilization Across Vault Sizes

Evaluates cold indexing latency, peak processor utilization, peak memory allocation during index ingestion, and physical memory footprint at rest across four standard vault tiers (1, 10, 100, and 1,000 markdown notes).

| Metric | System Under Test | 1 Document | 10 Documents | 100 Documents | 1,000 Documents (8.2 MB) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Indexing Latency** | **Sphene Core (Go)** | **61.28 ms** | **81.39 ms** | **263.67 ms (0.26s)** | **2,713.95 ms (2.71s)** |
| | **Obsidian (Electron)** | ~3,500 ms *(Cold window boot)* | ~3,500 ms | ~3,500 ms | ~3,500 ms *(Sequential scan)* |
| **Peak CPU During Index** | **Sphene Core (Go)** | 99.4% *(1 core burst)* | 198.7% *(2 workers)* | 198.8% *(2 workers)* | 198.8% *(2 workers)* |
| | **Obsidian (Electron)** | 120% - 180% | 140% - 210% | 160% - 240% | 180% - 290% |
| **Peak RAM During Index** | **Sphene Core (Go)** | **30.76 MB** | **31.75 MB** | **35.09 MB** | **40.46 MB** |
| | **Obsidian (Electron)** | 804.58 MB | 802.09 MB | 797.73 MB | 805.57 MB |
| **Physical RSS RAM at Rest** | **Sphene Core (Go)** | **30.76 MB** *(1 proc)* | **31.75 MB** *(1 proc)* | **35.09 MB** *(1 proc)* | **40.46 MB** *(1 proc)* |
| | **Obsidian (Electron)** | 804.58 MB *(6 procs)* | 802.09 MB *(6 procs)* | 797.73 MB *(6 procs)* | 805.57 MB *(6 procs)* |
| **Memory Advantage** | | **Sphene is 26.2x lighter** | **Sphene is 25.3x lighter** | **Sphene is 22.7x lighter** | **Sphene is 19.9x lighter** |

> **Key Takeaway:** Obsidian's Electron architecture requires a minimum ~800 MB RAM baseline regardless of whether a vault contains 1 note or 1,000 notes due to its multi-process browser architecture (Renderer, GPU, Utility, 2x Zygotes, Main). Sphene runs as a single compiled binary consuming ~31 MB to ~40 MB.

---

## 2. Single Document Read & Write Latency (API & On-Disk I/O)

Measures single-document operational latency comparing application API access layers against raw filesystem disk I/O on fast NVMe storage.

| Operation | Sphene Core v2.2 | Obsidian (Electron / REST API) | Raw Filesystem I/O | Performance Note |
| :--- | :--- | :--- | :--- | :--- |
| **Single Note Read** | **0.20 ms** *(HTTP API)* | **18.40 ms** *(Local REST API)* | **0.022 ms** *(22 µs)* | Sphene API serves directly from memory/SQLite buffer; Obsidian incurs Electron IPC hop. |
| **Single Note Write** | **1.20 ms** *(Atomic + FTS5)* | **24.60 ms** *(Local REST API)* | **1.072 ms** *(Flush + fsync)* | Sphene commits atomic WAL transaction; Obsidian executes Electron disk write + metadata cache rebuild. |

---

## 3. Search Retrieval Latency: 100 Notes vs. 1,000 Notes

Compares full-text keyword retrieval across 100 notes vs. 1,000 notes using SQLite FTS5 WAL indexing versus sequential filesystem disk scanning (`grep`).

| Collection Scale | Filesystem Text Scan (`grep`) | Sphene CLI Search (Cold Binary) | Sphene Background Daemon (HTTP / MCP) | Speedup Factor |
| :--- | :--- | :--- | :--- | :--- |
| **100 Notes** | **3.01 ms** | **16.33 ms** *(binary spin-up)* | **1.85 ms** | **1.6x faster** |
| **1,000 Notes** | **86.30 ms** | **12.50 ms** *(includes cold start)* | **2.20 ms** *(SQLite WAL)* | **39.2x faster** |

---

## 4. Autonomous AI Agent Benchmark (Live Run with Qwen 3.6 - 35B)

- **Test Vault:** **1,016 active documents** loaded into the index.
- **LLM Evaluated:** **Qwen 3.6 - 35B** (Local GPU acceleration, 300s timeout).
- **Prompting Methodology:** Every prompt is **natural and intentionally vague**. The agent receives **ZERO hints** regarding filenames, paths, or section headings. The model must autonomously formulate queries, invoke tools, inspect snippets, extract facts, and synthesize the answer.

---

### Scenario 1: Q3 Marketing Budget & Sign-off

- **Vault Size:** 1,016 notes
- **User Prompt:** `"Can you check what budget we approved for marketing in Q3 and who signed off on it?"`
- **Target Document:** `2026-09-15_Q3_Budget_Review.md`
- **Target Location:** Section 3 (`## 3. Approved Budget Allocations`), lines 42–47
- **Source Document Ground Truth Text:**
  ```markdown
  | Department | Requested Amount | Approved Amount | Purpose | Approving Sign-Off |
  | Marketing  | $50,000          | $45,000         | Digital Growth Campaign & Sponsorships | Alex Chen |
  ```
- **Expected Result:** Approved budget must equal **$45,000**; Sign-off person must equal **Alex Chen**.
- **Autonomous Tool Dispatch (Generated by LLM):**
  1. `sphene_search({"query": "marketing budget Q3 approval"})` $\rightarrow$ Sphene returns `2026-09-15_Q3_Budget_Review.md` in **13.7 ms**.
  2. `sphene_read({"path": "2026-09-15_Q3_Budget_Review.md"})` $\rightarrow$ Sphene returns note content in **0.3 ms**.
- **LLM Output:**
  > *"The approved marketing budget for Q3 is **$45,000** (reduced from a requested $50,000). The purpose is the Digital Growth Campaign & Sponsorships, and it was signed off by **Alex Chen**."*
- **Verification Status:** **100% VERIFIED** (Extracted exact $45,000 and Alex Chen).
- **Token Telemetry:** 4,320 total tokens across 3 multi-turn reasoning steps.

---

### Scenario 2: Personal Health Vitals & Medication Dosage

- **Vault Size:** 1,016 notes
- **User Prompt:** `"I need to take my evening medicine, what was my dose again and what was my evening blood pressure reading?"`
- **Target Document:** `2026-09-24_Daily_Log.md`
- **Target Location:** Section `## Evening Health Vitals & Notes`, lines 28–33
- **Source Document Ground Truth Text:**
  ```markdown
  - **Blood Pressure:** 122/78 mmHg (Resting Heart Rate: 68 bpm)
  - **Medications Taken:** Lisinopril 10mg taken with dinner at 19:15
  ```
- **Expected Result:** Blood pressure must equal **122/78 mmHg**; Medication must equal **10mg Lisinopril**.
- **Autonomous Tool Dispatch (Generated by LLM):**
  1. `sphene_search({"query": "evening medicine dose blood pressure"})` $\rightarrow$ Sphene returns `2026-09-24_Daily_Log.md` in **19.6 ms**.
  2. `sphene_read({"path": "2026-09-24_Daily_Log.md"})` $\rightarrow$ Sphene returns vitals section in **0.3 ms**.
- **LLM Output:**
  > *"Based on your daily log:*  
  > *- **Evening Medication:** Lisinopril, **10mg** (taken at 19:15)*  
  > *- **Evening Blood Pressure:** **122/78 mmHg** (Resting Heart Rate: 68 bpm)"*
- **Verification Status:** **100% VERIFIED** (Extracted exact 122/78 mmHg and 10mg Lisinopril).
- **Token Telemetry:** 3,411 total tokens across 3 multi-turn reasoning steps.

---

### Scenario 3: Cross-Document Contract Penalty Terms

- **Vault Size:** 1,016 notes
- **User Prompt:** `"What happens if Acme's Milestone 2 delivery is delayed? Are there weekly financial penalties and is there an overall cap?"`
- **Target Documents:** `Client_Acme_Contract.md` (Master Agreement) and `Billing_Terms.md` (Schedule B)
- **Target Location:** `Billing_Terms.md` Section 3 (`## Milestone Delay Penalties`), lines 15–20
- **Source Document Ground Truth Text:**
  ```markdown
  ## Milestone Delay Penalties
  In the event that the Contractor fails to deliver an agreed Milestone by the scheduled delivery date, a penalty deduction of **2.5%** of that milestone's fee shall be applied for each calendar week of unexcused delay. Total cumulative penalty deductions across any individual milestone shall be capped at a maximum of **10%** of the milestone value.
  ```
- **Expected Result:** Penalty rate must equal **2.5% per week**; Ceiling cap must equal **10%**.
- **Autonomous Tool Dispatch (Generated by LLM):**
  1. `sphene_search({"query": "Acme Milestone 2 delivery penalty"})` $\rightarrow$ Sphene returns both contract files in **14.8 ms**.
  2. `sphene_read({"path": "Client_Acme_Contract.md"})` $\rightarrow$ References Schedule B in **0.7 ms**.
  3. `sphene_read({"path": "Billing_Terms.md"})` $\rightarrow$ Extracts penalty clauses in **0.3 ms**.
- **LLM Output:**
  > *"If Milestone 2 is delayed, the penalties defined in Schedule B are:*  
  > *- **Weekly Penalty:** A deduction of **2.5%** of Milestone 2's fee for each week of delay.*  
  > *- **Maximum Ceiling:** Total cumulative delay penalties are strictly capped at **10%**."*
- **Verification Status:** **100% VERIFIED** (Extracted 2.5% weekly deduction and 10% maximum cap).
- **Token Telemetry:** 4,900 total tokens across 4 multi-turn reasoning steps.

---

### Scenario 4: DevOps Infrastructure Specification

- **Vault Size:** 1,016 notes
- **User Prompt:** `"What port and eviction policy did DevOps specify for Redis on staging?"`
- **Target Document:** `Server_Migration_Spec.md`
- **Target Location:** Section 3 (`## 3. Distributed Cache & Session Store`), lines 17–25
- **Source Document Ground Truth Text:**
  ```markdown
  ## 3. Distributed Cache & Session Store
  - Engine: Redis 7.2 Cluster
  - Staging Port: 6379
  - Production Port: 6380
  - Memory Allocation: 16 GB max memory per node
  - Eviction Policy: volatile-lru
  ```
- **Expected Result:** Staging Port must equal **6379**; Eviction Policy must equal **volatile-lru**.
- **Autonomous Tool Dispatch (Generated by LLM):**
  1. `sphene_search({"query": "Redis staging port eviction policy DevOps"})` $\rightarrow$ Sphene returns `Server_Migration_Spec.md` in **22.4 ms**.
  2. `sphene_read({"path": "Server_Migration_Spec.md"})` $\rightarrow$ Sphene returns cache section in **0.7 ms**.
- **LLM Output:**
  > *"For Redis on staging:*  
  > *- **Port:** 6379 (Production is 6380)*  
  > *- **Eviction Policy:** `volatile-lru`"*
- **Verification Status:** **100% VERIFIED** (Extracted Port 6379 and policy volatile-lru).
- **Token Telemetry:** 3,060 total tokens across 2 multi-turn reasoning steps.

---

### Scenario 5: Vacation Travel Dining Reservation

- **Vault Size:** 1,016 notes
- **User Prompt:** `"What time is our dinner in Kyoto on day 1 and what's the reservation confirmation code?"`
- **Target Document:** `Kyoto_Trip_Itinerary.md`
- **Target Location:** Section `## Day 1: Arrival & Historic Higashiyama`, line 15
- **Source Document Ground Truth Text:**
  ```markdown
  - 19:30 - Dinner Reservation at Gion Duck Noodles (Confirmation Code: GION-8842, table for 2).
  ```
- **Expected Result:** Reservation time must equal **19:30**; Confirmation code must equal **GION-8842**.
- **Autonomous Tool Dispatch (Generated by LLM):**
  1. `sphene_search({"query": "Kyoto dinner reservation confirmation"})` $\rightarrow$ Sphene returns `Kyoto_Trip_Itinerary.md` in **19.8 ms**.
  2. `sphene_read({"path": "Kyoto_Trip_Itinerary.md"})` $\rightarrow$ Sphene returns Day 1 itinerary in **1.0 ms**.
- **LLM Output:**
  > *"Here are the details for your Day 1 dinner in Kyoto:*  
  > *- **Time:** 19:30 (7:30 PM)*  
  > *- **Restaurant:** Gion Duck Noodles*  
  > *- **Confirmation Code:** GION-8842 (Table for 2)"*
- **Verification Status:** **100% VERIFIED** (Extracted 19:30 and GION-8842).
- **Token Telemetry:** 3,043 total tokens across 2 multi-turn reasoning steps.

---

## 5. Concurrent Write Collision & Anti-Loss Benchmark

When an AI agent modifies a note (e.g., checking off a checklist item), what happens if a human user is concurrently typing in that document?

We tested two document scales:
1. **Small Document:** `Daily_Engineering_Checklist.md` (~15 lines)
2. **Large Document:** `Project_Titan_Roadmap.md` (~80 lines)

### Test A: Small Document Collision (`Daily_Engineering_Checklist.md`)

#### State 1: Clean Baseline on Disk
```markdown
# Daily Engineering Checklist — 2026-09-26

## Morning Standup & Reviews
- [ ] Review PR #104: Database connection pool tuning.
- [ ] Verify Prometheus metric alerts on staging.
- [ ] Run automated E2E integration test suite.
```

#### State 2: Concurrent Human Edit (User Typing in Editor)
The human user adds a critical, uncommitted note in their editor:
```markdown
# Daily Engineering Checklist — 2026-09-26

*URGENT Human Note (Sarah, 10:14 AM): Staging alerts showed 502 errors during failover. DO NOT deploy v2.2 until Redis cluster replication sync finishes!*

## Morning Standup & Reviews
- [ ] Review PR #104: Database connection pool tuning.
- [ ] Verify Prometheus metric alerts on staging.
- [ ] Run automated E2E integration test suite.
```

#### State 3: Concurrent Agent Edit
Concurrently, an AI agent is instructed: *"Mark PR #104 as reviewed"*. The agent operates on a stale snapshot fetched 10 seconds prior:
```markdown
- [x] Review PR #104: Database connection pool tuning.
```

#### State 4: After in Obsidian (Direct File Overwrite)
The agent calls `write_file`, writing its stale version directly to disk:
```markdown
# Daily Engineering Checklist — 2026-09-26

## Morning Standup & Reviews
- [x] Review PR #104: Database connection pool tuning.
- [ ] Verify Prometheus metric alerts on staging.
- [ ] Run automated E2E integration test suite.
```
> ❌ **CRITICAL DATA LOSS IN OBSIDIAN:** Sarah's urgent warning regarding the 502 failover errors is **completely destroyed and wiped from disk**.

#### State 5: After in Sphene (Differential Timeline & AST Patching)
The agent submits the patch via `sphene_patch`. Sphene detects concurrent modification:
1. **Disk File Remains 100% Untouched:**
```markdown
# Daily Engineering Checklist — 2026-09-26

*URGENT Human Note (Sarah, 10:14 AM): Staging alerts showed 502 errors during failover. DO NOT deploy v2.2 until Redis cluster replication sync finishes!*

## Morning Standup & Reviews
- [ ] Review PR #104: Database connection pool tuning.
- [ ] Verify Prometheus metric alerts on staging.
- [ ] Run automated E2E integration test suite.
```
2. **Sphene Queues Staged AST Diff in Differential Timeline for Human Review:**
```diff
--- a/Daily_Engineering_Checklist.md
+++ b/Daily_Engineering_Checklist.md (Staged for Review)
@@ -Review PR #104 @@
-- [ ] Review PR #104: Database connection pool tuning.
+- [x] Review PR #104: Database connection pool tuning.
```
> ✓ **100% SAFE IN SPHENE:** The human working file is protected on disk. The agent's checkbox update is held in the Differential Timeline awaiting Human Veto approval.

---

### Test B: Large Document Collision (`Project_Titan_Roadmap.md`)

- **Human In-Flight Addition:**
  ```markdown
  *Sarah's In-Flight Note (Sept 26, 11:30 AM): Verify TLS certificate renewal hooks before staging database deployment. Do not wipe existing seed test data without snapshot backup!*
  ```
- **Agent Modification:** Check off `Task-02: Deploy staging database with read-replica cluster.`
- **Obsidian Outcome:** ❌ **Sarah's note destroyed** (`human_edit_lost: True`). Direct in-place file write silently commits over active typing.
- **Sphene Outcome:** ✓ **Working copy protected on disk** (`working_copy_protected: True`). AST diff staged in Differential Timeline.

---

## 6. How to Replicate on Any System

All benchmark scripts are fully configurable and support standard command-line flags and environment variables.

### 1. Install Telemetry Tools
```bash
git clone https://github.com/sphene-org/scripts.git
cd scripts/benchmarks
pip install psutil requests
```

### 2. Configure Your LLM Endpoint (Optional for Agent Benchmarks)
The suite supports any OpenAI-compatible provider (Ollama, LiteLLM, vLLM, OpenAI, Anthropic, Gemini):
```bash
export OPENAI_BASE_URL="http://127.0.0.1:4000/v1"
export OPENAI_API_KEY="your-api-key"
export OPENAI_MODEL="your-model-name"
```
Or pass CLI flags directly:
```bash
python3 bench_autonomous_agent.py --url http://localhost:11434/v1 --model qwen2.5:32b
```

### 3. Run the Benchmark Suites
```bash
# 1. System Scaling Matrix (1, 10, 100, 1,000 notes)
python3 bench_scaling_matrix.py

# 2. Concurrent Write Collision Test (Small & Large Docs)
python3 bench_collision.py

# 3. Autonomous AI Agent Benchmark (Tool Calling & Ground Truth)
python3 bench_autonomous_agent.py

# 4. Master Runner (Executes all suites end-to-end)
python3 runner.py
```

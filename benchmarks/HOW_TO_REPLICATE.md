# How to Replicate Sphene Benchmarks on Any System

This guide provides clear, step-by-step instructions for reproducing all Sphene system and AI agent benchmarks on your own Linux or macOS machine.

All benchmark harnesses and scripts are fully open source in the [`sphene-org/scripts`](https://github.com/sphene-org/scripts) repository.

---

## 1. Prerequisites

- **Operating System:** Linux (Ubuntu, Debian, Fedora, Arch) or macOS
- **Python:** Python 3.8+ with `psutil` and `requests`
- **Sphene Binary:** Download the latest compiled binary from [Releases](https://github.com/sphene-org/releases) or your package manager
- **Obsidian (Optional for comparative UI telemetry):** Official [Obsidian AppImage](https://obsidian.md/download)
- **AI Agent Backend (Optional for Agent Benchmarks):** Any OpenAI-compatible LLM endpoint (local or remote, e.g. Ollama, LiteLLM, vLLM, or OpenAI/Anthropic/Gemini).

---

## 2. Replication in 3 Steps

### Step 1: Clone the Scripts Repository
```bash
git clone https://github.com/sphene-org/scripts.git
cd scripts/benchmarks
pip install psutil requests
```

### Step 2: Run the Hardware & Systems Benchmark
```bash
# Measures cold startup, physical RAM (RSS), and search latency
python3 runner.py
```
This tests:
1. **Memory at Rest:** Measures the actual physical RAM (RSS) of the background daemon compared to desktop apps.
2. **Search Speed:** Measures exact-match and partial-match queries over 1,000 iterations to calculate min, median ($p50$), and 95th percentile ($p95$) response times.
3. **Multi-Tasking Concurrency:** Runs 10 and 50 simultaneous parallel query workers to ensure zero file locks or freezes.

### Step 3: Run the Real AI Agent Workflows
```bash
# Runs against local LLM endpoint (default: http://127.0.0.1:4000/v1)
python3 bench_real_agent.py
```
This executes 6 real-world everyday note scenarios, testing actual prompt tokens, response speed, and asserting 100% ground-truth accuracy:
1. **Executive Meeting Notes:** Extracts approved budget and sign-off names ($45,000 / Alex Chen).
2. **Personal Daily Journal:** Retrieves medical vitals and daily prescriptions (122/78 mmHg / Lisinopril).
3. **Legal Master Agreements:** Synthesizes linked terms across multiple documents (2.5% weekly delay penalty / 10% liability cap).
4. **DevOps Architecture Spec:** Extracts target cache configuration parameters (Port 6379 / `volatile-lru` policy).
5. **Vacation Travel Itinerary:** Schedule extraction of dinner reservations (19:30 / Confirmation `GION-8842`).
6. **Project Task List:** Tests task status updates while protecting human uncommitted notes from being overwritten.

---

## 3. What the Numbers Mean (In Plain English)

| Everyday Question | What the Benchmark Proves |
| :--- | :--- |
| **"Will this slow down my laptop or drain battery?"** | **No.** Sphene uses ~45 MB of RAM—less than a single browser tab. In comparison, Electron-based desktop apps run 6 separate background processes that consume ~800 MB. |
| **"How fast is search when I have hundreds or thousands of notes?"** | **Instantaneous.** Searching for a phrase takes 2 to 3 milliseconds ($p50$), compared to almost a full second (~800 ms) for traditional file-by-file text scans. |
| **"Can an AI agent corrupt or overwrite what I was typing?"** | **No.** When an AI updates a note, Sphene queues the change in a visual "Review / Approve" staging area (Human Veto). Traditional desktop plugins overwrite files on disk immediately, which silently wipes out in-flight human typing. |
| **"Does an AI assistant waste my API tokens and money?"** | **No.** When asking an AI about your notes, Sphene supplies only the exact relevant section (~110–290 tokens), saving 56% to 71% in API token costs on every question compared to dumping the entire document. |

---

## 4. Ground-Truth Verified Agent Results

All tests run against a live LLM recording actual prompt tokens, completion tokens, time-to-first-token (TTFT), and programmatically verifying that the extracted answers match ground truth:

| User Scenario | Document Type | Obsidian (Whole File) | Sphene (Targeted MCP) | Token Savings | Ground Truth Verified |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Budget Extraction** | Meeting Minutes | 667 prompt tokens | 290 prompt tokens | **56.5%** | **Yes** ($45k / Alex Chen) |
| **Health Vitals** | Daily Journal | 392 prompt tokens | 113 prompt tokens | **71.2%** | **Yes** (122/78 / Lisinopril) |
| **Contract Penalty** | Legal Agreement | 486 prompt tokens | 161 prompt tokens | **66.9%** | **Yes** (2.5% / 10% cap) |
| **DevOps Server Spec** | Tech Architecture | 395 prompt tokens | 147 prompt tokens | **62.8%** | **Yes** (Port 6379 / volatile-lru) |
| **Dining Reservation** | Travel Itinerary | 480 prompt tokens | 198 prompt tokens | **58.8%** | **Yes** (19:30 / GION-8842) |
| **Task Checkoff** | Project Roadmap | Direct Overwrite | Staged AST Diff | **100% Safe** | **Yes** (Sarah's Note Saved) |

# Sphene Official Releases & Changelog

Welcome to the official release repository for **Sphene Knowledge Hub** — the sovereign, local-first knowledge base with hardened agent sandboxing and zero-knowledge synchronization.

This repository tracks the official semantic version changelog and hosts pre-compiled, cryptographically verified binary distributions for all supported architectures.

---

## 📦 Binary Distributions

Pre-compiled binary releases are available on the [Releases Page](https://github.com/Sphene-app/releases/releases) for:

| Platform | Architecture | Binary Artifact | Notes |
| :--- | :--- | :--- | :--- |
| **Linux** | AMD64 (`x86_64`) | `sphene-linux-amd64` | Stripped, path-trimmed, UPX LZMA compressed |
| **Linux** | ARM64 (`aarch64`) | `sphene-linux-arm64` | Stripped, path-trimmed, UPX LZMA compressed |
| **Windows** | AMD64 (`x86_64`) | `sphene-windows-amd64.exe` | Stripped, path-trimmed, UPX LZMA compressed |
| **macOS** | Apple Silicon (`arm64`) | `sphene-darwin-arm64.tar.gz` | M1/M2/M3/M4 Apple Silicon optimized |
| **macOS** | Intel (`x86_64`) | `sphene-darwin-amd64.tar.gz` | Intel Mac 64-bit |
| **Docker** | Multi-Arch | `sphene-image.tar.gz` | Alpine container with embedded daemon |

---

## 🔒 Cryptographic Verification

Every release includes an immutable `SHA256SUMS` file generated during official compilation. To verify the integrity of your downloaded artifact:

```bash
# Verify downloaded files against the cryptographic manifest
sha256sum -c SHA256SUMS --ignore-missing
```

---

## 🚀 Quick Install

To install or update Sphene on any Linux or macOS machine with a single sovereign command:

```bash
curl -sSL https://raw.githubusercontent.com/Sphene-app/scripts/main/install.sh | bash
```

---

## 📚 Ecosystem Repositories

- **Main Website & Downloads:** [https://sphene.app](https://sphene.app) | [Download Hub](https://sphene.app/download/)
- **Zero-Lock-In Cryptographic Toolkit:** [Sphene-app/scripts](https://github.com/Sphene-app/scripts)
- **Model Context Protocol (MCP) Interface:** [Sphene-app/mcp](https://github.com/Sphene-app/mcp)

---

## 📄 License & Terms of Use

Sphene binary distributions, documentation, and core software are proprietary software protected under the [Sphene Proprietary Software License & Terms of Use](LICENSE). All rights reserved.

<p align="center">
  <h1 align="center">OpenCode Sentinel</h1>
</p>

<p align="center">
  <a href="https://opencode.ai">
    <picture>
      <source srcset="packages/console/app/src/asset/logo-ornate-dark.svg" media="(prefers-color-scheme: dark)">
      <source srcset="packages/console/app/src/asset/logo-ornate-light.svg" media="(prefers-color-scheme: light)">
      <img src="packages/console/app/src/asset/logo-ornate-light.svg" alt="OpenCode logo" width="200">
    </picture>
  </a>
</p>

<p align="center">
  <a href="doc/README.zh-CN.md">简体中文</a> | English
</p>

---

## 📖 Introduction

**OpenCode Sentinel** is a **security-enhanced version** of OpenCode, specifically designed for development environments within **corporate intranets** or **offline networks**.

Compared to the original version, it allows you to **connect only to private AI servers**, completely cutting off external network access. This not only ensures that code data absolutely never leaves the intranet but also completely resolves application freezes caused by unstable external network connections.

**Why Choose Sentinel?**

- 📦 **Offline Ready**: Provides a one-click packaging tool that pre-downloads all dependencies, allowing you to simply copy the package to an intranet machine, unzip, and run.
- 🛡️ **Strict Access Control**: Supports a "whitelist" mode, allowing you to force the application to **only connect to internal AI services**, blocking all other insecure network requests.
- ⚡ **Zero Lag**: Optimized network connection logic with intelligent timeout and retry mechanisms ensures the interface never freezes due to network jitter.
- 🏢 **Private Model Support**: Seamlessly integrates with enterprise private deployments of DeepSeek, vLLM, Ollama, and other large model services.

> **Version Info**: Based on [anomalyco/opencode](https://github.com/anomalyco/opencode) v1.1.28 ([commit dac7357](https://github.com/anomalyco/opencode/commit/dac73572e0ecf708d2968bb981e3fe65743dfbda)).

👉 **[View Detailed Changelog](doc/MODIFICATIONS.md)**

## 🚀 Offline Deployment Workflow

This project provides a one-click packaging tool, allowing you to complete deployment in an isolated environment in just three steps.

### 1. Prepare Build Environment
On a machine with **internet access** (Windows/macOS/Linux), install the basic dependencies:
- **[Bun](https://bun.sh)**
- **[Node.js](https://nodejs.org/)**
- **Clone this repository**

```bash
git clone https://github.com/oneoflzx/opencode-sentinel.git; cd opencode-sentinel
```

### 2. Generate Offline Package
Run the packaging script on the **internet-connected** machine to automatically pull all dependencies and generate a self-contained installation package:

```bash
bun offline-scripts/pack.ts
```
> 🎉 Upon success, an `opencode-offline.tar.gz` file will be generated in the current directory.

### 3. Install in Target Environment
Transfer `opencode-offline.tar.gz` to the target host and extract it. Run the corresponding installation script based on your operating system (the script automatically configures the Node.js environment and PATH):

| OS | Command | Note |
| :--- | :--- | :--- |
| **Linux / macOS** | `./install.sh` | Recommended to run with bash |
| **Windows** | `.\install.bat` | Or run `install.ps1` with PowerShell |

Directory structure after extraction:
```text
dir/
├── install.sh    # Linux/macOS install script
├── install.bat   # Windows install script
├── deps/         # Offline dependencies
├── bin/          # Executable binaries
└── node/         # Built-in Node.js environment
```

---

## ⚙️ Configuration Guide

Before the first run, configure security policies and model access in `~/.config/opencode/opencode.json`.

### Core Configuration Example

```json
{
  "$schema": "https://opencode.ai/config.json",
  "network": {
    "policy": "whitelist",
    "whitelist": [
      "my-private-llm.com"
    ]
  },
  "provider": {
    "my_provider": {
      "options": {
        "baseURL": "https://my-private-llm.com/v1",
        "apiKey": "sk-private-key"
      },
      "models": {
        "qwen3-32b": { "name": "Qwen3-32B" }
      }
    }
  }
}
```

### Configuration Options

#### Network Policy (`network`)
- **`policy`**:
  - `allow-all`: Allow all outbound connections (not recommended for sensitive environments).
  - `deny-all`: Deny all outbound connections.
  - `whitelist`: **Recommended**. Only allow access to domains in the whitelist.
- **`whitelist`**: Array of domain strings, supporting exact matches and subdomain matches.

#### Model Provider (`provider`)
Follows the standard OpenCode configuration format.

---

## ▶️ Run

After installation and configuration, start the application directly:

```bash
# Ensure environment variables are loaded (or restart terminal)
opencode
```

<p align="center">
  <img src="doc/OpenCode-Sentinel.png" alt="OpenCode Sentinel Screenshot" width="800">
</p>

## 📚 Documentation

- **Modifications**: See [MODIFICATIONS.md](doc/MODIFICATIONS.md) for detailed code changes.
- **Original Docs**: Visit [opencode.ai/docs](https://opencode.ai/docs).

---

<p align="center">
  <i>Built with ❤️ for the open source community.</i>
</p>

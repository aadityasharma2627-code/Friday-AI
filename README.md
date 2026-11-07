<div align="center">
  <!-- Add your own logo here later, e.g. <img alt="Friday-AI" src="assets/logo.png" width="400"> -->
  <h1>Friday-AI</h1>

  <p><i>Personal AI, on your own device.</i></p>

  <p>
    <img src="https://img.shields.io/badge/python-%3E%3D3.10-blue" alt="Python">
    <img src="https://img.shields.io/badge/license-Apache%202.0-green" alt="License">
    <a href="https://github.com/open-jarvis/OpenJarvis"><img src="https://img.shields.io/badge/based%20on-OpenJarvis-blue" alt="Based on OpenJarvis"></a>
    <a href="https://arxiv.org/abs/2605.17172"><img src="https://img.shields.io/badge/upstream%20paper-arXiv%3A2605.17172-b31b1b.svg" alt="Upstream paper"></a>
    <a href="https://github.com/aadityasharma2627-code/Friday-AI/stargazers"><img src="https://img.shields.io/github/stars/aadityasharma2627-code/Friday-AI?style=flat" alt="Stars"></a>
  </p>
</div>

---

> **[Quick Start](#quick-start)** · **[Installation](#installation)** · **[Agents](#built-in-agents)** · **[Skills](#skills)** · **[Upstream Docs](https://open-jarvis.github.io/OpenJarvis/)** · **[Upstream Paper](https://arxiv.org/abs/2605.17172)**
>
> The upstream docs are written for OpenJarvis. When you follow them, use `friday` wherever they say `jarvis`.

> **Note:** Friday-AI is an independent fork of [OpenJarvis](https://github.com/open-jarvis/OpenJarvis). It is not affiliated with or endorsed by the OpenJarvis maintainers, Stanford, or Marvel.

## Why Friday-AI?

Most personal AI assistants still send every request to a cloud API, so your "personal" AI depends on someone else's server. Friday-AI follows the local-first approach of OpenJarvis: the model runs on your own computer through [Ollama](https://ollama.com), and the cloud is used only if you choose to set it up.

The underlying framework is built around three ideas:

- **Shared building blocks** for building on-device agents
- **Evaluations** that treat energy, FLOPs, latency and cost as important as accuracy
- **A learning loop** that improves models using your local trace data

Friday-AI keeps all of that and gives it a new name and identity, as a personal assistant you can run, modify and build on.

## Installation

Friday-AI currently installs from source.

**Requirements:** Python 3.10 to 3.13, Git, [uv](https://docs.astral.sh/uv/) and [Ollama](https://ollama.com).

```bash
git clone https://github.com/aadityasharma2627-code/Friday-AI.git
cd Friday-AI
uv sync --extra server
ollama pull qwen3.5:2b
uv run friday doctor
```

| Platform | Notes |
|---|---|
| **macOS · Linux · WSL2** | Run the commands above in a terminal |
| **Windows (PowerShell)** | If `uv` is not found, use `python -m uv`. On Python 3.14 use `uv sync --extra server --python 3.12` |
| **Browser interface** | `friday gui` needs Node.js 22+ and a source checkout |
| **Memory and document search** | Needs the Rust extension, which is an extra build step |

## Quick Start

```bash
friday                               # start chatting (default: chat-simple)
friday ask "What is the capital of France?"
friday doctor                        # check your installation
friday gui                           # start the graphical browser interface
friday init --preset <name> --force  # replace config with a starter preset
```

> Prefix `friday ...` with `uv run`, or activate the virtual environment first.
> `--force` overwrites your existing config, so back it up before using it.

| Preset | What it does |
|---|---|
| `morning-digest-mac` / `morning-digest-linux` / `morning-digest-minimal` | Spoken daily briefing from email, calendar, health, news |
| `deep-research` | Multi-hop research across indexed docs with citations |
| `code-assistant` | Agent with code execution, file I/O and shell access |
| `scheduled-monitor` | Stateful agent on a schedule with memory |
| `chat-simple` | Lightweight conversation, no tools |

Example:

```bash
friday init --preset morning-digest-minimal --force
friday connect gdrive          # one sign-in covers Gmail / Calendar / Tasks
friday digest --fresh          # generate and play your first briefing
```

### Skills

Skills teach agents how to use tools better. Every skill is a tool: agents find them in a catalog and use them when needed.

```bash
# Install skills from public sources
friday skill install hermes:arxiv
friday skill sync hermes --category research

# Use skills with any agent
friday ask "Use the code-explainer skill to explain this Python code: for i in range(5): print(i*2)"

# Optimize skills from your trace history
friday optimize skills --policy dspy

# Benchmark the impact
friday bench skills --max-samples 5 --seeds 42
```

Skills can be imported from [Hermes Agent](https://github.com/NousResearch/hermes-agent), [OpenClaw](https://github.com/openclaw/skills), or any GitHub repository. They follow the [agentskills.io](https://agentskills.io/specification) open standard.

### Built-in Agents

Friday-AI includes eight agents across three execution modes (on-demand, scheduled, continuous):

| Agent | Type | What it does |
|-------|------|-------------|
| `morning_digest` | Scheduled | Daily briefing from email, calendar, health, news, with audio |
| `deep_research` | On-demand | Multi-hop research with citations across web and local docs |
| `monitor_operative` | Continuous | Long-horizon monitoring with memory, compression and retrieval |
| `orchestrator` | On-demand | Multi-turn reasoning with automatic tool selection |
| `native_react` | On-demand | Thought, action, observation loop agent |
| `operative` | Continuous | Persistent autonomous agent with state management |
| `native_openhands` | On-demand | Generates and executes Python code |
| `simple` | On-demand | Single-turn chat, no tools |

## Privacy and Safety

- With Ollama and a local model, prompts are processed on your machine.
- Cloud models, web search and integrations send data to outside services and may cost money.
- If an API key such as `OPENAI_API_KEY` is set, setup may suggest a cloud model as the default.
- Code and shell tools can act on your real files. Enable them only when you need them.
- Never commit API keys or your config file to Git.

## What Changed from OpenJarvis

- Renamed the project from OpenJarvis to Friday-AI (Python package `friday_ai`, command `friday`)
- Rewrote the README and Code of Conduct

All original code is by the OpenJarvis authors.

## Community

- **This project:** [github.com/aadityasharma2627-code/Friday-AI](https://github.com/aadityasharma2627-code/Friday-AI)
- **Upstream project:** [github.com/open-jarvis/OpenJarvis](https://github.com/open-jarvis/OpenJarvis)
- **Upstream docs:** [open-jarvis.github.io/OpenJarvis](https://open-jarvis.github.io/OpenJarvis/)

## Contributing

Contributions are welcome. Please follow the [Code of Conduct](CODE_OF_CONDUCT.md).

```bash
git clone https://github.com/aadityasharma2627-code/Friday-AI.git
cd Friday-AI
uv sync --extra dev
uv run pre-commit install
uv run pytest tests/ -v
```

## About

Friday-AI is built on top of [OpenJarvis](https://github.com/open-jarvis/OpenJarvis), part of [Intelligence Per Watt](https://www.intelligence-per-watt.ai/), a research initiative studying the intelligence efficiency of AI systems. OpenJarvis is developed at [Hazy Research](https://hazyresearch.stanford.edu/) and the [Scaling Intelligence Lab](https://scalingintelligence.stanford.edu/) at [Stanford SAIL](https://ai.stanford.edu/). Credit for the original framework goes to its authors.

## Citation

Friday-AI is based on OpenJarvis. If you use the underlying framework in research, please cite the original paper:

```bibtex
@misc{saadfalcon2026openjarvispersonalaipersonal,
      title={OpenJarvis: Personal AI, On Personal Devices},
      author={Jon Saad-Falcon and Avanika Narayan and Robby Manihani and Tanvir Bhathal and Herumb Shandilya and Hakki Orhun Akengin and Gabriel Bo and Andrew Park and Matthew Hart and Caia Costello and Chuan Li and Christopher Ré and Azalia Mirhoseini},
      year={2026},
      eprint={2605.17172},
      archivePrefix={arXiv},
      primaryClass={cs.LG},
      url={https://arxiv.org/abs/2605.17172},
}
```

## License

[Apache 2.0](LICENSE). See [NOTICE](NOTICE) for attribution.

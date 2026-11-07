# Contributing to Friday-AI

Thank you for your interest in contributing to Friday-AI! This guide explains how to set up
the project and submit your first pull request.

Friday-AI is a fork of [OpenJarvis](https://github.com/open-jarvis/OpenJarvis) (Apache-2.0).
Most of the code comes from the OpenJarvis authors, and credit for it belongs to them.

---

## Ways to Contribute

### Good first contributions

- Documentation improvements and typo fixes
- Bug reports with steps to reproduce
- Test coverage improvements
- Windows setup fixes and notes (for example, Python 3.14 and DNS or network issues)

### Ideal contributions

- Bug fixes with tests
- Performance improvements
- New tools, engines or agents that follow the existing registry pattern
  (see `docs/development/contributing.md`)
- New channel integrations (Telegram, Discord, Slack, etc.)

### Please open an issue first

These need more discussion before you start a pull request:

- New core features or major changes to existing ones
- Large refactors
- Changes to core abstractions (`BaseAgent`, `InferenceEngine`, etc.)

### May not be accepted

- Changes that break backwards compatibility in the public API
- Changes that add large new dependencies without a good reason
- Changes that make the user experience harder

### Upstream bugs

If a bug exists in the original OpenJarvis code too, please consider reporting it to the
[upstream project](https://github.com/open-jarvis/OpenJarvis/issues) as well, so everyone
benefits.

---

## Getting Started

### Prerequisites

| Requirement | Version | Notes |
|---|---|---|
| Python | 3.10 to 3.13 | Python 3.14 may fail on Windows |
| [uv](https://docs.astral.sh/uv/) | Latest | Package manager |
| [Ollama](https://ollama.com) | Latest | For running local models |
| Node.js | 22+ | Only needed for the browser interface and the WhatsApp channel |

### Setup

```bash
git clone https://github.com/aadityasharma2627-code/Friday-AI.git
cd Friday-AI
uv sync --extra dev
```

On Windows, if `uv` is not found, use `python -m uv` instead of `uv`.

### Pre-commit hooks

We use [pre-commit](https://pre-commit.com/) to run linting and formatting checks before each commit:

```bash
uv run pre-commit install
```

This installs Git hooks that run [Ruff](https://docs.astral.sh/ruff/) on every commit. If
the hooks fail, fix the issues and commit again.

For more detail on code conventions and project structure, see the
[development guide](docs/development/contributing.md).

---

## Proposing Changes

### Small changes

For typos, doc improvements and simple bug fixes, open a pull request directly.

### Larger changes

For new features, refactors or new dependencies, please
[open an issue](https://github.com/aadityasharma2627-code/Friday-AI/issues) first to discuss
the approach. This catches design problems early and saves everyone time.

If you want to work on an existing issue, leave a comment on it so others know it is taken.
If you cannot finish it, comment again so someone else can pick it up.

---

## Pull Request Process

### Before submitting

1. Run the tests:
   ```bash
   uv run pytest tests/ -v
   ```
2. Run the linter:
   ```bash
   uv run ruff check src/ tests/
   ```
3. Check the formatting:
   ```bash
   uv run ruff format --check src/ tests/
   ```
4. Add tests for new functionality
5. Follow the existing registry pattern for new components

### Commit messages

We use [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: add FAISS memory backend
fix: handle empty tool responses in orchestrator
docs: update engine discovery documentation
test: add coverage for BM25 backend
refactor: simplify agent base class helpers
```

Keep the first line under 72 characters. Reference related issues, for example `fixes #42`.

### What makes a good pull request

- **Focused:** one feature, fix or refactor per pull request
- **Tested:** includes unit tests for new code
- **Documented:** updates docstrings and docs if you add public API
- **Backwards compatible:** avoids breaking existing interfaces without discussion

---

## Contribution Areas

| Area | What to build |
|---|---|
| **Intelligence** | Model catalog entries, routing strategies |
| **Engines** | New inference backends |
| **Agents** | New agent types and improvements |
| **Tools** | New tools (browser, API clients, etc.) |
| **Learning** | Router policies, reward functions, training |
| **Evals** | New datasets, scorers and benchmark configs |
| **Channels** | Chat platform integrations |
| **Rust** | Rust extension work, see the `rust/` directory |

---

## Licensing

Friday-AI is licensed under the [Apache License 2.0](LICENSE). By contributing, you agree
that your contributions will be licensed under the same license. Please keep the existing
license headers and copyright notices in files you edit.

---

## Code of Conduct

This project follows a [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you agree to
follow it.

---

## Questions?

- Open an [issue](https://github.com/aadityasharma2627-code/Friday-AI/issues) on GitHub
- Read the upstream [documentation](https://open-jarvis.github.io/OpenJarvis/) for guides
  and API reference (use `friday` wherever it says `jarvis`)
- Or contact the maintainer at aadityasharma2627@gmail.com

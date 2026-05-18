# claude-code-setting
Personally customized Claude Code setup — installation guides, reinstallation procedures, and integrations I use day-to-day.

This repo is a personal reference. Feel free to adapt anything here for your own workflow, but the configurations and choices reflect my own environment (GPU server, NFS-shared HuggingFace cache, Korean/English mixed terminal, etc.).

---

## What's Inside

| Path | Description |
|---|---|
| [`installation/`](./installation) | First-time install guide for Claude Code (Native installer + npm). |
| [`reinstallation/`](./reinstallation) | Clean re-installation procedure for fixing broken installs, including troubleshooting (PATH, EACCES, nvm). |
| [`claude-code-slack/`](https://github.com/jwyang21/claude-code-slack) | Git submodule — Slack integration setup for Claude Code. |
| `LICENSE` | MIT. |

---

## Quick Start

### Clone with submodules
The `claude-code-slack/` directory is a submodule, so clone recursively:
```bash
git clone --recurse-submodules https://github.com/jwyang21/claude-code-setting.git
```
If you already cloned without `--recurse-submodules`:
```bash
cd claude-code-setting
git submodule update --init --recursive
```

### Pick your path
- **Fresh install** → see [`installation/README.md`](./installation/README.md)
- **Something broke / want a clean reinstall** → see [`reinstallation/README.md`](./reinstallation/README.md)
- **Slack integration** → see [`claude-code-slack/`](https://github.com/jwyang21/claude-code-slack)

---

## Why This Repo Exists

Claude Code's official docs cover the canonical setup well, but real-world environments (shared GPU servers, NFS-backed caches, `nvm`-managed Node versions, mixed Native/npm installs) tend to expose edge cases the official guide skims over. This repo captures:

- The minimum reliable installation path I use on `gpusvr3`-style shared Linux servers
- Recovery procedures when the install gets into a bad state (mixed Native + npm, stale PATH, `EACCES` from prior `sudo` installs)
- Optional add-ons (e.g., [`oh-my-claudecode`](https://github.com/Yeachan-Heo/oh-my-claudecode) plugin, Slack integration)

If you're setting up Claude Code on a clean laptop, the official Anthropic docs are probably enough. If you're on a shared server, in a container, or recovering from a partially-uninstalled mess, this repo may save you some time.

---

## Requirements

- **OS**: Linux / macOS / WSL2 (Windows native untested)
- **Disk**: ~500MB for Claude Code binary + config
- **Network**: Outbound HTTPS to `claude.ai`, `api.anthropic.com`, and npm/Node sources if using npm install
- **Account**: Claude Pro, Max, Team, Enterprise, or Console (API) — free tier does not include Claude Code
- **(Optional) Node.js 18+**: only required for the npm install path; not needed for the Native installer

---

## License

MIT — see [`LICENSE`](./LICENSE).

---

## References

[1] Claude Code official docs — https://docs.claude.com/en/docs/claude-code/overview  
[2] Claude Code setup guide — https://docs.claude.com/en/docs/claude-code/setup  
[3] Troubleshoot install & login — https://docs.claude.com/en/docs/claude-code/troubleshoot-install  
[4] `oh-my-claudecode` plugin — https://github.com/Yeachan-Heo/oh-my-claudecode

# Installation
A manual for installing Claude Code from scratch.

Claude Code provides two installation methods:
- **Option A (recommended): Native installer** — self-contained binary, no Node.js required, auto-updates.
- **Option B: npm** — for users who prefer the Node.js ecosystem (e.g., pinning versions, CI/CD).

Pick **one** and skip the other.

---

## Option A. Native Installer (Recommended)

### A-1. Install Claude Code
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

### A-2. (Optional) Add Claude Code to `$PATH`
If the installer prints a message like below, run the suggested command to make `claude` available anywhere.

Example output:
```
✔ Claude Code successfully installed!
  Version: 2.1.143
  Location: ~/.local/bin/claude                  # the install path (*)
  Next: Run claude --help to get started

⚠ Setup notes:
    ● Native installation exists but ~/.local/bin is not in your PATH. Run:
    echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

Then jump to **Step 2. Run Claude Code**.

---

## Option B. npm Installation

Use this only if you specifically want the npm-based install. Requires **Node.js 18+**.

### B-1. Check Node.js version
```bash
node -v                                          # expected: v18.x.y or higher
```
If Node.js 18+ is already installed, go to **Step B-4**. Otherwise, continue to **Step B-2**.

### B-2. Install `nvm`
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
```

### B-3. Restart shell and install Node.js LTS
```bash
source ~/.bashrc
nvm install --lts
nvm use --lts
node -v                                          # verify: v22.x.y (current LTS) or v20.x.y
```

### B-4. Install Claude Code via npm
```bash
npm install -g @anthropic-ai/claude-code
```
> Do **NOT** use `sudo`. If you hit permission errors, configure an npm-global directory in your home (e.g. `~/.npm-global`) and add it to `$PATH`.

---

## Step 2. Run Claude Code and Set Up

### 2-1. Run Claude Code
```bash
claude
```

### 2-2. Login with your account
Inside the Claude Code session:
```
/login
```

### 2-3. (Optional) Install [`oh-my-claudecode`](https://github.com/Yeachan-Heo/oh-my-claudecode)
A multi-agent orchestration plugin for Claude Code [1]. Entirely optional — Claude Code works fine without it, but recommended (personal opinion).

Inside the Claude Code session, run [2]:
```
/plugin marketplace add https://github.com/Yeachan-Heo/oh-my-claudecode
/plugin install oh-my-claudecode
```

### 2-4. Restart the Claude Code session
```
/exit
```
Then in your terminal:
```bash
claude
```
And inside the new session, run setup:
```
/oh-my-claudecode:omc-setup
```
(or simply `/setup` — both work.)

### 2-5. Finish `oh-my-claudecode` setup
During setup, you may be asked to provide an **Exa API key** and/or **GitHub authorization token**. Whether to enable Exa / GitHub / other external services is entirely up to you.

Once setup completes, you're ready to use Claude Code.

# 3. Manage global setting
You can set global configurations via editing a file `~/.claude/settings.json`.

For example, I am using a customized global setting (refer to `installation/settings.json` as an example).
- This file is just an example. You can edit the setting in whichever way you want.

## 3-1. Security alert
The configuration in `installation/settings.json` enables bypassPermissions + skipDangerousModePermissionPrompt. 

All tool calls (Bash/Write/Edit) run WITHOUT confirmation, including destructive ones (e.g., `rm`, `git push` `--force`, etc). 

If you are to use `installation/settings.json`, consider disabling bypassPermissions and skipDangerousModePermissionPrompt by removing `permissions.defaultMode` and `skipDangerousModePermissionPrompt` from the file.

(Especially, when you are working on shared/critical systems) 

## 4. Recommended `statusline`: oh-my-claudecode (OMC)

Rich statusline showing rate-limit usage, thinking mode, session info, context usage, and tool-call counts.

**Example output:**

```
[OMC#4.14.0] | 5h:17%(3h22m) wk:33%(2d13h) sn:0%(2d13h) extra:85%($211.80/$250.00) | thinking | session:0m | ralph:1/100 | ultrawork+ralph | ctx:4% | 🔧6
```

### 4-1. Required files to set `statusline`

All paths are under `~/.claude/`.

| Path | Role |
|------|------|
| `~/.claude/settings.json` | Declares `statusLine.command` and enables the OMC plugin/marketplace. ⚠️  Also contains personal settings (theme, model, permissions) — if the target server already has its own, **merge only the `statusLine` block** rather than overwriting. |
| `~/.claude/.omc/hud-config.json` | HUD element config — decides which segments render (rateLimits, thinking, sessionHealth, ralph, activeSkills, contextBar, callCounts). Overrides the default "minimal" preset. |
| `~/.claude/hud/omc-hud.mjs` | HUD entrypoint script. Resolves which installed OMC plugin version to load. |
| `~/.claude/hud/omc-hud-with-effort.sh` | Bash wrapper that appends `\| effort:<level>` via `jq`. Must be executable (`chmod +x`). |
| `~/.claude/hud/lib/config-dir.mjs` | Helper module imported by `omc-hud.mjs` to resolve `CLAUDE_CONFIG_DIR`. |

### 4-2. Prerequisites (install on each server, respectively)

- **Node.js** — runs `omc-hud.mjs`
- **jq** — wrapper uses it to extract `.effort.level`; without jq the effort segment is silently skipped
- **OMC plugin** at `~/.claude/plugins/cache/omc/oh-my-claudecode/<version>/` — either replicate the plugin tree, or run `/oh-my-claudecode:omc-setup` once on each server

### 4-3. Optional files to control `statusline` (keeps behavior fully identical)

| Path | Role |
|------|------|
| `~/.claude/settings.local.json` | Per-host permission allowlist (Bash/Skill auto-allow). |
| `~/.claude/.omc-config.json` | OMC runtime config (default execution mode, team config, task tool choice). |
| `~/.claude/CLAUDE.md` | Global OMC operating principles loaded into every session. |

### 4-4. Do NOT copy these files between servers

- `~/.claude/scripts/ensure-omc-hud-minimal.mjs` — orphan script that resets HUD config back to "minimal" if a `SessionStart` hook re-fires it.
- `~/.claude/statusline.sh` — older custom statusline script, no longer wired into anything via `settings.json`.

---

# References
[1] https://github.com/Yeachan-Heo/oh-my-claudecode  
[2] https://github.com/Yeachan-Heo/oh-my-claudecode/blob/main/README.md  
[3] https://docs.claude.com/en/docs/claude-code/overview

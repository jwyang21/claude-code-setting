# Clean Re-installation
A guide for cleanly reinstalling Claude Code when it's broken or misbehaving.

Reinstallation depends on **how you originally installed Claude Code**. The native installer and npm install leave files in different places, so running the wrong uninstall command leaves a half-removed install. Identify your install method first, then follow the matching path.

---

## Step 1. Identify your install method
```bash
which claude
```

| Output path | Install method | Go to |
|---|---|---|
| `~/.local/bin/claude` (or similar under `$HOME`) | Native installer | **Option A** |
| `~/.npm-global/bin/claude`, `~/.nvm/.../bin/claude`, `/usr/local/bin/claude` | npm | **Option B** |
| `claude not found` | Not installed (or already broken) | Either option works |

---

## Option A. Native Installer

### A-1. Uninstall
The native installer ships with a built-in uninstall command:
```bash
claude uninstall
```

### A-2. Reinstall
```bash
curl -fsSL https://claude.ai/install.sh | bash
```

> If the install fails with `another process is currently installing Claude`, remove stale lock files under `~/.local/state/` and retry.

Then jump to **Step 3. Verify**.

---

## Option B. npm Installation

### B-1. Uninstall
```bash
npm uninstall -g @anthropic-ai/claude-code
```

### B-2. Clean npm cache
Prevents reinstall failure due to a corrupted cache:
```bash
npm cache clean --force
```

### B-3. Check Node.js version
```bash
node -v                                          # required: v18+ (current LTS: v22)
```
If below 18, upgrade via `nvm`:
```bash
nvm install --lts
nvm use --lts
```

### B-4. Reinstall
```bash
npm install -g @anthropic-ai/claude-code
```
> Do **NOT** use `sudo`. See **Troubleshooting** below if you hit `EACCES`.

---

## Step 2. (Optional) Wipe Config / Cache
Skip this if you want to keep your login, settings, MCP configs, and session history.

```bash
rm -rf ~/.claude         # user settings, allowed tools, MCP configs, sessions
rm -f  ~/.claude.json    # auth & top-level config
rm -rf ~/.cache/claude   # optional cache cleanup
```
> ⚠️ This wipes authentication too — you'll need to `/login` again after reinstall.

---

## Step 3. Verify
```bash
claude --version
which claude
```
For a deeper check (config, PATH, dependencies):
```bash
claude doctor
```

---

## Troubleshooting

### `command not found: claude`
PATH issue. Check the npm global prefix (or `~/.local/bin` for native):
```bash
npm config get prefix                            # for npm installs
# the printed path + /bin must be in $PATH
echo $PATH
```
For native installs, ensure `~/.local/bin` is in `$PATH`:
```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
```

### `EACCES: permission denied` (npm only)
Caused by a previous `sudo` install. Switch to a user-level npm prefix:
```bash
mkdir -p ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```
Then retry `npm install -g @anthropic-ai/claude-code`.

### `claude` not found in a new shell (nvm users)
`nvm use` only affects the current shell. Confirm nvm init is in your shell rc file:
```bash
grep nvm ~/.bashrc
```
If missing, add the nvm init block (from `~/.nvm/nvm.sh`) to `~/.bashrc`.

### Mixed install (both native and npm present)
`which -a claude` will show multiple paths. Uninstall the non-target one first, then reinstall.

---

## Quick Reference (One-liner)

**npm reinstall** (keeps config):
```bash
npm uninstall -g @anthropic-ai/claude-code && npm cache clean --force && npm install -g @anthropic-ai/claude-code
```

**Native reinstall** (keeps config):
```bash
claude uninstall && curl -fsSL https://claude.ai/install.sh | bash
```

Add `rm -rf ~/.claude ~/.claude.json` before reinstall if you want a fully fresh state (auth, settings, history wiped).

---

# References
[1] https://docs.claude.com/en/docs/claude-code/setup  
[2] https://docs.claude.com/en/docs/claude-code/troubleshooting  
[3] https://github.com/anthropics/claude-code
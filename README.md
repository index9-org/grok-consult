# consult

Grok Build plugin: ask local **Claude Code** and/or **Codex CLI** for a second opinion. Grok stays the daily driver. Never auto-invoke.

You need **one** of Claude or Codex, not both.

## Install

```bash
grok plugin install index9-org/grok-consult --trust
```

Reload plugins (`r` in the Plugins tab, or a new session).

## Requires

- [Grok Build](https://docs.x.ai/build/overview)
- bash and python3 (macOS/Linux already have these)
- **Claude Code** (`claude` on PATH, `claude auth login`) — Claude Pro or Claude Max — **and/or**
- **Codex CLI** (`codex` on PATH, `codex login`) — ChatGPT subscription; Codex is included

No Anthropic or OpenAI API keys. Max 5x is not required; Pro works with tighter limits.

## Use

From Grok: “ask Claude …” or “ask Codex …”. Skills: `claude-consult`, `codex-consult`.

Shell:

```bash
# from the plugin directory, or after install via $GROK_PLUGIN_ROOT
./scripts/claude-consult --mode opinion --stdin <<'EOF'
Review this plan: …
EOF
```

Shell tool timeout for Grok: **960000 ms**. Wrapper default kill: 900s.

Never `--bare`. Never `claude` / `codex` directly from Grok.

## Develop / publish

```bash
./scripts/validate   # grok plugin validate + selftest (no live model calls)
./scripts/publish    # validate, then grok plugin tag --push (needs origin)
```

Bump `version` in `.grok-plugin/plugin.json`, then `./scripts/publish`.

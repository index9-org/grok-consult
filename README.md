# consult

From Grok Build, ask your local Claude Code, Codex CLI, or Cursor Agent CLI for a second opinion. Grok stays the daily driver. Never auto-invoke.

You only need one of those CLIs. If you have more than one, you can ask Grok for them at once.

## Install

```bash
grok plugin install index9-org/grok-consult --trust
```

Reload plugins (`r` in the Plugins tab, or a new session).

## Requires

- [Grok Build](https://docs.x.ai/build/overview)
- bash, python3, and git
- **Claude Code** (`claude` on PATH, `claude auth login`): Claude Pro or Max. Not a separate Claude Code product.
- **and/or Codex CLI** (`codex` on PATH, `codex login`): included with ChatGPT. Not a separate Codex subscription.
- **and/or Cursor Agent CLI** (`cursor-agent` on PATH, `cursor-agent login`): a Cursor subscription. The binary is `cursor-agent`, not the editor binary named `cursor`.

No Anthropic, OpenAI, or Cursor API keys.

The wrappers only spawn those local CLIs. Each CLI then talks to its own service with your existing login.

Cursor consult is not hermetic: it inherits `~/.cursor` config, project `AGENTS.md` / `.cursor/rules`, and any already-approved MCP servers. Read-only modes use Cursor ask mode (no `--force`). `implement` applies edits without confirmation.

## Use

From Grok: "ask Claude …", "ask Codex …", or "ask Cursor …". If you ask for more than one, Grok runs one of each together. Never two `implement` runs in the same repo. Skills: `claude-consult`, `codex-consult`, `cursor-consult`.

```bash
# plugin directory, or $GROK_PLUGIN_ROOT after install
./scripts/claude-consult --mode opinion --stdin <<'EOF'
Review this plan: …
EOF
```

Same for `codex-consult` and `cursor-consult`. Modes: `opinion` (default), `review`, `read`, `implement`. Optional `--model` and `--effort` (`low` | `medium` | `high` | `xhigh` | `max`) on Claude/Codex. Cursor has no `--effort`; put it in `--model` (`claude-opus-5-thinking-high`, `grok-4.6[effort=high]`). Claude defaults to `opus`; Codex to `gpt-5.6-sol`; Cursor omits `--model` and uses the CLI selected model.

Grok shell timeout: 960000 ms. Wrapper default kill: 900s.

Never `--bare` (that skips Claude OAuth). Never call `claude`, `codex`, `cursor-agent`, or `cursor` directly from Grok.

## Maintainers

Bump `version` in `.grok-plugin/plugin.json`, then:

```bash
./scripts/validate   # grok plugin validate + selftest (no live model calls)
./scripts/publish    # validate, then grok plugin tag --push (needs origin)
```

MIT · [index9](https://www.index9.dev/) · [repo](https://github.com/index9-org/grok-consult)

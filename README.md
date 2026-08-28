# consult

From Grok Build, ask your local Claude Code or Codex CLI for a second opinion. Grok stays the daily driver. Never auto-invoke.

You only need one CLI installed (Claude or Codex). If you have both, you can ask Grok for both at once.

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

No Anthropic or OpenAI API keys.

The wrappers only spawn those local CLIs. Claude and Codex then talk to their own services with your existing login.

## Use

From Grok: "ask Claude …" or "ask Codex …". If you ask for both, Grok runs one of each together. Skills: `claude-consult`, `codex-consult`.

```bash
# plugin directory, or $GROK_PLUGIN_ROOT after install
./scripts/claude-consult --mode opinion --stdin <<'EOF'
Review this plan: …
EOF
```

Same for `codex-consult`. Modes: `opinion` (default), `review`, `read`, `implement`. Optional `--model` and `--effort` (`low` | `medium` | `high` | `xhigh` | `max`). Claude defaults to `opus`; Codex to `gpt-5.6-sol`. Effort defaults to `high` (`read`: `medium`).

Grok shell timeout: 960000 ms. Wrapper default kill: 900s.

Never `--bare` (that skips Claude OAuth). Never call `claude` or `codex` directly from Grok.

## Maintainers

Bump `version` in `.grok-plugin/plugin.json`, then:

```bash
./scripts/validate   # grok plugin validate + selftest (no live model calls)
./scripts/publish    # validate, then grok plugin tag --push (needs origin)
```

MIT · [index9](https://www.index9.dev/) · [repo](https://github.com/index9-org/grok-consult)

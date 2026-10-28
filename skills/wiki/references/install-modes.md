# Supported installation modes

Resolve the installed product root from the invoking skill's own location, not
from the user-vault working directory:

```bash
PRODUCT_ROOT=/absolute/path/to/installed/obsidian-plugin
CORE="$PRODUCT_ROOT/scripts/obsidian-plugin.py"
test -f "$CORE"
```

## Portable Agent Skills

Every host loads the same `skills/<name>/SKILL.md` files. Use
`scripts/setup-multi-agent.sh --host <host>` (preview by default, `--apply` to
link) or link each `skills/<name>/` directory at the host's direct
`<skill-root>/<name>/SKILL.md` discovery path. Codex, OpenCode, Gemini, ZCode,
Cursor, Windsurf and any other Agent Skills host invoke the skills by their
plain names, such as `wiki` or `wiki-ingest`. Run the host from the user vault,
or configure the vault explicitly. Host-specific hooks and plugin manifests are
optional adapters, never core workflow logic.

## Host plugin adapters

A host that installs the package as a plugin may namespace the skills and cache
the product assets in an ephemeral, read-only location. Mutable vault state must
still resolve from `--vault`, the workspace configuration or the project, never
from the plugin cache or a host plugin-root variable.

Claude Code is the one shipped plugin adapter. Install it through its
marketplace, or load a checkout with `claude --plugin-dir /path/to/obsidian-plugin`,
and invoke skills as `/obsidian-plugin:<name>`.

## Product clone

A source clone is product/development code, not an automatically installed
plugin and not the recommended user vault. Create a separate vault:

```bash
python3 "$CORE" init /path/to/vault \
  --generated-at <ISO-UTC> --operation-id init-reviewed
python3 "$CORE" init /path/to/vault \
  --generated-at <ISO-UTC> --operation-id init-reviewed \
  --approved-plan-sha256 <reviewed-sha256> --apply
```

Adopt an existing Obsidian vault non-destructively:

```bash
python3 "$CORE" adopt /path/to/vault \
  --generated-at <ISO-UTC> --operation-id adopt-reviewed
python3 "$CORE" adopt /path/to/vault \
  --generated-at <ISO-UTC> --operation-id adopt-reviewed \
  --approved-plan-sha256 <reviewed-sha256> --apply
```

Both commands default to dry-run. New user vaults receive no upstream product
remote.

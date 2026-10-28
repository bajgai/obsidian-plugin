# Plugin namespace

The project is named `obsidian-plugin`. The Python package is
`obsidian_plugin`, the CLI is `scripts/obsidian-plugin.py`, and transaction
and report schema identifiers use the `obsidian-plugin.` prefix.

The optional Claude Code adapter exposes `/obsidian-plugin:wiki`,
`/obsidian-plugin:save`, and the other skills under the same prefix. Its
manifest uses `obsidian-plugin`; no reserved host-name exception is needed.

## Load a checkout

```bash
claude --plugin-dir /absolute/path/to/obsidian-plugin
python3 scripts/obsidian-plugin.py --help
```

## Marketplace configuration

The configured marketplace is `bajgai-obsidian-plugin`, backed by
`bajgai/obsidian-plugin`. Its published manifest maps the historical
`agricidaniel-obsidian` plugin identity to `obsidian-plugin`.

After the renamed package is published, install it with:

```bash
claude plugin marketplace add bajgai/obsidian-plugin
claude plugin install obsidian-plugin@bajgai-obsidian-plugin
claude plugin list --json
```

The local source rename does not publish or update an installed plugin.
Restart the host after changing its installed plugin or skill links.

## Vault compatibility

`.obsidian-wiki.json` and the `OBSIDIAN_WIKI_*` environment variables remain
the canonical configuration. The alternate `.obsidian-plugin.json` and
`OBSIDIAN_PLUGIN_*` names are read-only fallbacks.

Python imports, script paths, plugin invocations, and persisted schema IDs
must use the new names. Existing bundles or workspace configuration created
with a previous schema prefix are not automatically converted: back them up,
review their schema fields, and use the current schema before applying them.
Vault notes and captured source payloads do not need to be renamed.

Run `make test` to check the portable package, hooks, and executable contracts.
An installed-plugin listing alone does not verify a host's skill loading.

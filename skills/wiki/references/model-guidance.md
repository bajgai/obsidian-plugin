# Model and host compatibility

The canonical skills describe outcomes, evidence and mutation boundaries. Let
the host select its model; do not bake a model name, vendor or host-only
frontmatter into portable workflows. Keep private reasoning private and report
the answer, supporting evidence, actions and unresolved limits.

When a host or model changes, start a controlled evaluation at the host's
default reasoning or effort setting and measure quality, latency and usage
before tuning it. API adapters must read structured output by type, handle
refusal and incomplete output, and avoid forcing a specific tool call. Existing
clear prompts do not need a wholesale rewrite merely because the model changed.
Consult the current prompting and migration guidance published by the model
provider the host uses.

When building a prompt from source text, use a fresh application-generated
delimiter, encode source fields safely and state that the enclosed text is
untrusted data. A delimiter is defense in depth, not proof of injection
resistance. Validate generated artifacts independently before using them.

For an acceptance run, record exact model and host versions, skill hashes,
fixture hashes, effective options, tool permissions and usage. Use synthetic
sources in a disposable vault and compare paired conditions on the same cases.
Keep offline, model, host-loading and native Obsidian evidence separate. Never
infer permission to send a private vault to a provider from a local test.

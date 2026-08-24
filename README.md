# Dobbel

A consent-first Agent Skill for building a **digital twin of your own writing voice** without committing or uploading your corpus.

Dobbel models how a consenting subject moves through prose: cadence, reasoning movement, compression, emphasis, and register. It is deliberately narrower than a whole-person digital twin. It does not claim to be the person, simulate their private mind, or publish as them.

Dobbel separates three things that are often collapsed:

1. **Voice evidence**: subject-authored text used to learn cadence and reasoning movement.
2. **Fact authority**: current sources used to support claims.
3. **Publication authority**: the human who reviews and approves the exact final artefact.

That separation is the product. The Dobbel is an editorial writing-voice twin, not an impersonation engine.

## What is included

- A concise `SKILL.md` workflow compatible with agents that load Agent Skills packages.
- A local-only provenance manifest schema.
- A deterministic, standard-library context builder with consent and hash checks.
- A package validator, synthetic tests, and CI.
- Safety rules for consent, attribution, privacy, and human ratification.

No corpus, voice profile, personal example, or generated draft is included.

## Quick start

```bash
git clone https://github.com/AntreasAntoniou/dobbel.git
cd dobbel
python3 scripts/validate_package.py
cp examples/voice-manifest.example.json examples/voice-manifest.local.json
python3 scripts/build_voice_context.py --hash examples/source.example.md
```

Replace the example source with text you authored, record its printed SHA-256 in the local manifest, then build a context pack:

```bash
python3 scripts/build_voice_context.py \
  --manifest examples/voice-manifest.local.json \
  --task "Describe a small software release" \
  --audience "other maintainers" \
  --register technical \
  --max-chars 12000 \
  --output voice-context.local.md
```

The output is deterministic for the same manifest, source bytes, and CLI arguments. It is deliberately marked as local evidence and a draft input—not publishable prose.

## Install as a skill

```bash
npx skills add AntreasAntoniou/dobbel
```

Or copy/symlink this repository into the skills directory used by your agent. The directory name should remain `dobbel`, with `SKILL.md` at its root.

## Test

```bash
python3 -m unittest discover -s tests -v
python3 scripts/validate_package.py
```

The test suite creates neutral synthetic fixtures in temporary directories. It does not depend on or inspect a private corpus.

## Safety model

Dobbel refuses unconsented subjects, non-subject-authored voice evidence, hash drift, and autonomous attribution. See [references/safety-and-consent.md](references/safety-and-consent.md) and [SECURITY.md](SECURITY.md).

## Relation to other Dobbels

The Dobbel family covers consented digital-twin work. This public skill owns the narrow **writing-voice** layer: subject-authored evidence in, human-ratified prose out. It does not perform the believed-human embodiment, full personality simulation, dialogic reconstruction, or identity persistence associated with a whole-person doppel.

## Relation to agent and knowledge graphs

Dobbel is one authorship boundary around a broader agent work graph. It does **not** implement a knowledge graph, integrate with Anthropic's knowledge-graph cookbook, or modify Karpathy's `autoresearch`. The [composition map](docs/COMPOSITION.md) distinguishes execution topology from knowledge topology and links the primary sources precisely.

## License

MIT. See [LICENSE](LICENSE).

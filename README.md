# Voice Builder

A consent-first Agent Skill for helping people write with more of their own voice—without committing or uploading their corpus.

Voice Builder separates three things that are often collapsed:

1. **Voice evidence**: subject-authored text used to learn cadence and reasoning movement.
2. **Fact authority**: current sources used to support claims.
3. **Publication authority**: the human who reviews and approves the exact final artefact.

That separation is the product. The skill is an editorial instrument, not an impersonation engine.

## What is included

- A concise `SKILL.md` workflow compatible with agents that load Agent Skills packages.
- A local-only provenance manifest schema.
- A deterministic, standard-library context builder with consent and hash checks.
- A package validator, synthetic tests, and CI.
- Safety rules for consent, attribution, privacy, and human ratification.

No corpus, voice profile, personal example, or generated draft is included.

## Quick start

```bash
git clone https://github.com/AntreasAntoniou/voice-builder.git
cd voice-builder
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
npx skills add AntreasAntoniou/voice-builder
```

Or copy/symlink this repository into the skills directory used by your agent. The directory name should remain `voice-builder`, with `SKILL.md` at its root.

## Test

```bash
python3 -m unittest discover -s tests -v
python3 scripts/validate_package.py
```

The test suite creates neutral synthetic fixtures in temporary directories. It does not depend on or inspect a private corpus.

## Safety model

Voice Builder refuses unconsented subjects, non-subject-authored voice evidence, hash drift, and autonomous attribution. See [references/safety-and-consent.md](references/safety-and-consent.md) and [SECURITY.md](SECURITY.md).

## Relation to autoresearch

Karpathy's March 2026 [`autoresearch`](https://github.com/karpathy/autoresearch) release demonstrates a small, measurable loop in which an agent edits one training file, runs a fixed-time experiment, and keeps or discards the change. Voice Builder does **not** integrate with or modify autoresearch. It is one possible communication layer around a broader agent workflow. See [docs/COMPOSITION.md](docs/COMPOSITION.md) for the precise, unaffiliated conceptual map.

## License

MIT. See [LICENSE](LICENSE).

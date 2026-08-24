# Five skills around a measurable agent loop

In March 2026, Andrej Karpathy released [`autoresearch`](https://github.com/karpathy/autoresearch), a deliberately small single-GPU research loop. Its human-edited `program.md` directs an agent that changes `train.py`, runs a fixed five-minute experiment, evaluates `val_bpb`, records the result, and keeps or discards the change. The upstream [`program.md`](https://github.com/karpathy/autoresearch/blob/master/program.md) is the precise source for that loop.

The five skills in this release are **not an autoresearch fork, integration, benchmark, or endorsement**. They have not been tested together with autoresearch. They are an unaffiliated conceptual control plane for teams that want to carry the same “small real loop” idea into broader agent work.

| Skill | Conceptual role around the loop | What it does not claim |
| --- | --- | --- |
| [Agent Orchestra](https://github.com/AntreasAntoniou/agent-orchestra) | Defines isolated roles, lanes, hand-offs, and an integration owner when one worker loop becomes several. | It does not improve `val_bpb` or replace the experiment contract. |
| [Plus Ultra](https://github.com/AntreasAntoniou/plus-ultra) | Adds independent proposals, an arbiter, one application pass, and fresh verification for higher-stakes changes. | It is not the upstream keep/discard algorithm. |
| [Cross Agent Sync](https://github.com/AntreasAntoniou/cross-agent-sync) | Carries concise, source-linked progress between agent harnesses without merging their private state. | It is not distributed training or a shared-memory claim. |
| [Visual QA](https://github.com/AntreasAntoniou/visual-qa) | Tests dashboards and operator UIs at deterministic viewports with independent visual review. | It does not evaluate model quality and is irrelevant when no UI exists. |
| [Voice Builder](https://github.com/AntreasAntoniou/voice-builder) | Turns verified results into subject-ratified explanation while keeping voice evidence local. | It is not autonomous publication, impersonation, or part of the training loop. |

## The puzzle-piece view

```text
human objective + measurable loop
              │
       Agent Orchestra ── isolated workers and one integrator
              │
          Plus Ultra ───── adversarial plan and fresh verification
              │
       actual experiment / engineering loop
          ┌───┴──────────────┐
Cross Agent Sync          Visual QA (only for a UI)
 durable hand-offs        deterministic visual evidence
          └───┬──────────────┘
        Voice Builder
 local evidence → human-ratified public explanation
```

The composition is intentionally optional. A three-file experiment should remain three files unless another layer solves a demonstrated coordination, verification, UI, or communication problem.

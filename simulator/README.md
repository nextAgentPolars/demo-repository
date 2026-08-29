# Polaris Apex Theory — Runtime Convergence Simulator (P1–P5)

A single-file, zero-build, interactive simulator for the five properties of
the Apex Theory (`P1–P5`) — the process-governance layer of the Polaris
project. Where the Go demo in this repository shows the **evidence** layer
(claims anchored to digests), this page shows the **process** layer: how work
advances, closes, recovers, and resumes while a governance boundary stays in
charge.

Open `polaris-apex-theory-simulator.html` in any browser. No toolchain, no
dependencies beyond CDN scripts.

## The scenario

A point travels from `START` to `GOAL` across a 500×500 plane, passing three
checkpoints (`CP1–CP3`) on the way. Four segments, four acceptance gates. Two
forces work against it:

- **Noise W** — a persistent random disturbance applied to every step.
- **The Ψ gate** — a threshold on perpendicular deviation from the ideal
  path. Cross it and the segment trips.

You can tune both live with the sliders in the header.

## The five properties

**P1 — Stable Holding.** Whatever passes external acceptance is *sealed*.
Sealed points never join a rollback, never move under noise, never get
rewritten by later work. The seal carries a coordinate checksum — held means
held, and the checksum is the receipt.

**P2 — Continuous Advance.** The unglamorous part: bounded steps toward the
next checkpoint, shrinking as the distance closes, with noise on top. Advance
is a means, never an argument for closure.

**P3 — Verifiable Closure.** The heart of the system. Acceptance is decided
by an *external* gate that sees only a projection of the current state —
position, live Ψ violations, open deviations, consecutive stable frames. It
cannot see the trajectory history and it cannot hear the system's opinion of
itself. Rejection reasons are machine-recomputable facts. The verifier does
not own the authority to lower its own bar, and the panel proves it: the
internal self-check ("GREEN · I think I've arrived") sits right next to the
external verdict, and the two disagree freely.

**P4 — Recoverable Failure.** When the Ψ gate trips, the run falls back to
the last snapshot — truncating the *active* segment only, never the sealed
ones. Every trip opens an entry in the deviation ledger, and an entry closes
only after the system has returned to steady forward progress. Note the
closing condition deliberately: *can advance again*, not *arrived*. If
deviations could only close at acceptance time, and acceptance required zero
open deviations, P3 and P4 would deadlock each other forever. And P4 is
honest about its edge: after too many consecutive trips it stops and says so.
Broken can come back; not every failure comes back for free.

**P5 — Resumable Restart.** Kill the process mid-run. The state space
collapses — but the sealed segments and persisted snapshots survive, and the
run resumes from the last snapshot without replaying any external side effect
that already happened.

## Experiments worth running

1. **The headline demo — green ≠ proven.** Crank Noise W up, sprint for the
   finish, and watch the middle panel. The internal self-check stays GREEN
   the whole way; the external gate keeps refusing to let the run close,
   because the consecutive-stable-frames counter keeps getting wiped to zero.
   Closure authority never belonged to the executor.
2. **Shock test (P1).** Inject an external shove mid-run. The live point
   jumps; every sealed point reports 0 px of drift. Holding is a property,
   not a habit.
3. **Lower-the-bar test (P3).** Try to talk the gate into relaxing. It
   refuses — in the exact same words, every time. The acceptance criterion is
   not a negotiation.
4. **Crash test (P5).** Interrupt the process at any point and watch it
   reattach to the same trunk from persisted fact.

## Why it lives next to the Go demo

Both artifacts teach the same discipline from two sides:

| | receipt-demo (Go) | this simulator |
|---|---|---|
| Layer | Evidence | Process |
| Question | *Can I trust this claim?* | *Is this run allowed to close?* |
| Mechanism | Digest anchoring, append-only ledger | External gate, deviation ledger, snapshot rollback |
| Shared rule | Facts live outside the speaker | Closure lives outside the executor |

If you run one after the other, the pattern is hard to miss: nothing in the
system ever grades its own homework.

## Files

- `polaris-apex-theory-simulator.html` — the entire simulator, one file.

## License

Apache-2.0 for the demo code, same as the rest of this repository. Not
licensed for model training without written permission.

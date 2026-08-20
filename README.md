## Jeramie Hicks

I build infrastructure for autonomous systems that have to answer for what they did.

Founder of [**Neuruh**](https://github.com/NeuruhAI).

---

### The thesis

Most agent frameworks are built to make a model *act*. The hard part is not
acting — it is the four questions that come after:

- Was this action **authorized** before it happened, by something other than the model?
- Was the blast radius **bounded** while it happened?
- Can anyone **prove** afterwards what actually ran?
- Is the system allowed to **learn** from the result, and under whose authority?

A system that cannot answer those cannot be trusted with anything that matters.
So the governing rule in everything I build is:

> **Model output is evidence, never command authority.**

That is a structural constraint, not a policy document. The model's response is
recorded as evidence. It cannot select the command. The command was declared by
an operator, validated against a typed capability, cleared by a deterministic
policy gate, executed with an exact argument tuple inside a contained working
directory, and written to a hash-chained receipt ledger. Remove the model
entirely and the authorization path is unchanged.

---

### Run it in one minute

No API key, no model, no account. Python 3.11+.

```bash
git clone https://github.com/NeuruhAI/neuruh-sovereign-agent-starter.git
cd neuruh-sovereign-agent-starter
python -m venv .venv && source .venv/bin/activate
pip install .
neuruh-sovereign-agent examples/starter.synthetic.json --out-dir run-output
```

Then verify the run with two tools that know nothing about the agent that
produced it:

```bash
neuruh-agent-run-manifest validate run-output/manifest.json   # VALID run-... sha256:...
neuruh-agent-receipt verify run-output/receipts.jsonl         # PASS: 3 receipts
```

Change one byte of `receipts.jsonl` and `verify` fails. That is the whole point.

---

### What I build

**Governed agent runtimes.** Execution paths where authority is established
before an action and proven after it, and where a language model is one input
among several rather than the control plane.

**Decision and evidence systems.** Deterministic ALLOW / DENY / ESCALATE
boundaries, typed capability manifests with fail-closed argument validation,
evidence envelopes that carry provenance and can abstain rather than guess, and
append-only ledgers that make state changes reconstructable.

**Receipt and attestation infrastructure.** Hash-chained receipts, content-bound
run manifests that record the exact released version of everything that ran, and
verifiers that are independent of the systems they check.

**Local-first AI infrastructure.** Provider-neutral inference health, loopback
inference paths, and a starter that rejects remote endpoints at the
configuration boundary rather than trusting them at call time.

**Real-world intelligence systems.** Applied work that turns messy public and
commercial records into decisions someone acts on. That work is commercial and
stays private; the governance rails underneath it are what I publish.

---

### The chain

```text
observation
  -> evidence          what was seen, with provenance
  -> decision          ALLOW / DENY / ESCALATE, deterministically
  -> authority         who permitted this, bounded and single-use
  -> governed execution  exactly one declared command, contained
  -> receipt           tamper-evident proof of what ran
  -> outcome           what actually happened afterwards
  -> calibration       what the system may learn from it
```

Each stage is a separate installable package with its own tests, not a feature
of a monolith. Any stage that cannot prove its inputs fails closed.

---

### Selected work

| Project | What it is |
|---|---|
| [`neuruh-sovereign-agent-starter`](https://github.com/NeuruhAI/neuruh-sovereign-agent-starter) | The composition above, runnable end to end from one config file. Start here. |
| [`neuruh-governed-exec`](https://github.com/NeuruhAI/neuruh-governed-exec) | Exact executable and argv allowlisting, no shell, worktree containment that survives symlink escape. |
| [`neuruh-policy-gate`](https://github.com/NeuruhAI/neuruh-policy-gate) | Deterministic ALLOW / DENY / ESCALATE with content-derived policy versioning. |
| [`neuruh-capability-registry`](https://github.com/NeuruhAI/neuruh-capability-registry) | Typed capability manifests; arguments are validated before policy or execution is reached. |
| [`agent-receipt`](https://github.com/NeuruhAI/agent-receipt) | Portable hash-chained receipt format and a standalone CLI verifier. |
| [`neuruh-agent-run-manifest`](https://github.com/NeuruhAI/neuruh-agent-run-manifest) | Content-bound run identity, independently validatable. |
| [`neuruh-inference-health`](https://github.com/NeuruhAI/neuruh-inference-health) | Provider-neutral health aggregation for local-first and mixed inference stacks. |
| [`nimdp-validator`](https://github.com/NeuruhAI/nimdp-validator) | Scores a specification for launch readiness and can fail a CI job on the result. |

Beyond the runnable core, 26 further packages implement the governed promotion
lifecycle: evidence provenance, human approval checkpoints, delegated authority,
outcome calibration, reversibility contracts, canary evaluation, rollback
receipts, deployment authorization, drift detection, and canonical-state
reconciliation that fails closed as `ambiguous` rather than picking a winner.

---

### Current public work

The active surface is the **[Neuruh Public Commons](https://github.com/NeuruhAI/public-commons)** —
33 independently versioned Python packages plus specifications, synthetic
contract fixtures, and a failure lab whose job is to prove that invalid states
get rejected. Apache-2.0. Every dependency resolves to an immutable tag; nothing
points at a branch.

These are alpha releases. Small, dependency-free, and tested — but the
interfaces are still moving, so pin the tag.

What is public is the rails. Production policies, authority topology, scoring,
connectors, prompts, and customer data are not, and every fixture in every
public repository is synthetic. The rule is written down in
[`PUBLIC_PRIVATE_BOUNDARY.md`](https://github.com/NeuruhAI/public-commons/blob/main/PUBLIC_PRIVATE_BOUNDARY.md).

---

Organization: [github.com/NeuruhAI](https://github.com/NeuruhAI)

---
title: "Can you prove a proof is axiom-free?"
parent: Addendum
nav_order: 0
---

# Can you prove that a proof doesn't use a specific axiom?
{: .no_toc }

*March 9, 2026 · `P04.S04`*

---

In P04 we saw that `#print axioms` traces which axioms a theorem depends on. A natural follow-up question from the lecture: can we express *within the logic* that a proposition was proved without using a particular axiom (say, `Classical.choice`)? For example, could we write a type `ConstructivelyProvable P` that is inhabited exactly when `P` has a proof that avoids classical reasoning?

**The short answer is no.** Proof irrelevance makes this inexpressible as a `Prop` in Lean. But the question touches on deep issues in type theory, and the longer answer is worth exploring.

## Why proof irrelevance prevents this

Recall from P04 S02 that `Prop` is proof-irrelevant: any two proofs `h₁ h₂ : P` are definitionally equal. The kernel does not compare them — it only checks that *a* proof exists.

This means there is no predicate on proofs that could distinguish "proved constructively" from "proved classically." Both proofs inhabit the same type, and the type system considers them identical. You cannot pattern-match on a proof's internal structure, and you cannot ask which axioms were invoked during its construction.

As [*Theorem Proving in Lean 4*](https://lean-lang.org/theorem_proving_in_lean4/axioms_and_computation.html) puts it:

> "Elements of a type `p : Prop` should play no role in computation, and so the particular construction of a term `prf : p` is 'irrelevant.'"

The proof term is the only place where axiom dependencies live. Proof irrelevance erases exactly what you would need to track.

## `#print axioms` is meta-level

`#print axioms` and its metaprogramming counterpart `Lean.Environment.collectAxioms` work by inspecting the actual proof term in the environment *before* erasure. This is a **meta-level** operation — it examines the syntax tree of the proof, not its logical content. You could write a Lean 4 metaprogram or linter that checks whether `Classical.choice` appears in the transitive closure of a definition's dependencies, but this remains external to the logic.

```lean
-- This is a meta-level check, not a proposition:
#print axioms Nat.add_comm
-- [propext, Quot.sound]

-- There is no way to write:
-- theorem add_comm_is_constructive : AxiomFree Nat.add_comm := ...
-- because AxiomFree would need to inspect the proof term.
```

## What about partial workarounds?

Several mechanisms provide *related* guarantees without solving the full problem:

### `Decidable` (lives in `Type`, not `Prop`)

`Decidable P` carries computational content: it's either `isTrue (h : P)` or `isFalse (h : ¬P)`. Because it lives in `Type`, proof irrelevance doesn't apply — different `Decidable` instances are distinguishable. But `Decidable` characterizes *decidability*, not constructive provability. A proposition can be constructively provable without being decidable (e.g., `True`), and having a `Decidable` instance says nothing about whether the underlying proof of `P` used classical axioms.

### `noncomputable`

Lean requires definitions that use `Classical.choice` to produce data to be marked `noncomputable`. This is a partial signal — it tells you computational content was lost. But it only applies to definitions producing data in `Type`, not to proofs in `Prop`.

### Double negation translation

A classical result (Glivenko, 1929): a proposition `P` is provable in classical propositional logic if and only if `¬¬P` is provable in constructive propositional logic. So `¬¬P` internally characterizes classical provability. But this is the wrong direction — it tells you what *classical* logic can prove, not whether a specific proof of `P` *avoided* classical logic. See the [nLab page on double negation](https://ncatlab.org/nlab/show/double+negation) for the general theory.

### Gödel encoding (in principle)

You could, in principle, encode "there exists a derivation of `P` in CIC without `Classical.choice`" as an arithmetic statement using Gödel numbering. This would be a proposition within the theory. But it would be a statement about *syntax* (the existence of a derivation), not *semantics* (the meaning of the proof), and would be enormously impractical.

## Lean's official stance

Leonardo de Moura stated on the [Lean Zulip](https://leanprover-community.github.io/archive/stream/270676-lean4/topic/Compartmentalization.20of.20axioms.20in.20Lean.204.html) that Lean does not attempt to compartmentalize axioms:

> "The bare-bones system can be used for constructive mathematics. That being said, a lot of the proof automation we are building is using axioms such as `propext`."

He noted that `simp`, `split`, and `by_cases` all rely on classical axioms, and recommended users who prioritize constructive mathematics consider Agda or Coq.

A [separate discussion](https://leanprover-community.github.io/archive/stream/348111-std4/topic/How.20classical.20is.20std4.3F.html) revealed that even simple lemmas like `Nat.min_succ_succ` depend on `Classical.choice` because `split` invokes `Classical.em` rather than looking for `Decidable` instances. Mario Carneiro noted that Std4 "tries to avoid classical logic when it can be accomplished without significant difficulty," but fixing this requires changes to Lean's core.

## How other systems handle this

**Agda** sidesteps the problem by not having proof irrelevance by default. Its module system structurally enforces axiom discipline: if you don't import or postulate LEM, anything that type-checks is axiom-free with respect to classical logic. The `--safe` flag forbids `postulate` entirely. But this is an *organizational* guarantee (which axioms are in scope), not a *propositional* one (a type expressing axiom-freeness).

**Coq** has `Print Assumptions` (analogous to `#print axioms`) and faces the same fundamental limitation. Its optional `SProp` (strict propositions) provides proof irrelevance where desired, but doesn't help with axiom tracking.

## Research frontier

The most directly relevant recent work is Jonathan Chan's [*Internalizing Extensions in Lattices of Type Theories*](https://arxiv.org/abs/2510.26839) (2025), which proposes using the Dependent Calculus of Indistinguishability (DCOI) to make axiom dependencies a type-level property. Each set of axioms corresponds to a *dependency level*, and terms carry level annotations alongside their types. However, Chan identifies exactly our obstacle: proof irrelevance causes dependency information to "leak downward," collapsing the level distinctions for `Prop`-valued terms. This remains an open problem.

[Two-Level Type Theory](https://arxiv.org/abs/1705.03307) (Annenkov, Capriotti, Kraus, Sattler, 2017) demonstrates a related idea: maintaining an *inner* type theory (where mathematics happens) and an *outer* type theory (where meta-reasoning happens) within a single formal system. This doesn't directly solve axiom tracking, but shows how multiple type-theoretic levels can coexist, with the outer level expressing properties that the inner level cannot express about itself.

## The deeper point

This limitation is not a bug in Lean's design — it is a *consequence* of a deliberate trade-off. Proof irrelevance buys you erasure (proofs cost nothing at runtime) and simplicity (you never need to worry about *which* proof you have). The price is that properties of proof terms — including axiom provenance — are invisible to the logic. The information exists (in the proof term), a meta-level tool can inspect it (`#print axioms`), but no proposition within the theory can express it.

This is an instance of a general phenomenon: a formal system cannot fully characterize its own provability predicate without stepping outside itself. Gödel's incompleteness theorems are the most famous manifestation, but the pattern recurs throughout logic and type theory.

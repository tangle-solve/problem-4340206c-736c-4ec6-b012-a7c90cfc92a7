<!-- solve-problem:4340206c-736c-4ec6-b012-a7c90cfc92a7 -->
# Unconditional NP-hardness of total MCSP

A [Tangle Solve problem](https://solve.tangle.tools/problems/4340206c-736c-4ec6-b012-a7c90cfc92a7).

## What is the problem?

MCSP (Minimum Circuit Size Problem): given a truth table of a Boolean function *f* on *n* variables (so the input is the full 2ⁿ-bit string) and a threshold *s*, decide whether *f* is computable by a circuit of size at most *s*. Formally, MCSP = {⟨tt(f), s⟩ : circuit-size(f) ≤ s}.

The problem: **prove that MCSP is NP-hard under deterministic polynomial-time many-one reductions** — unconditionally, with no assumptions (no oracle, no randomized reduction, no cryptographic assumption, no average-case assumption, no restriction to partial functions).

Ambiguities to pin down:
- "Circuit size" is usually total gates in a fan-in-2 AND/OR/NOT basis over {0,1}; results for most fixed gates and size measures transfer, but state your convention.
- "Total" (as in the census title) emphasizes that the truth table fully specifies a function on all inputs — in contrast to the *partial-function* MCSP (MCSP with don't-care entries), which is already known NP-hard. The word "total" is *not* about totality of the reduction.
- The input size is N = 2ⁿ, so "polynomial time" is polynomial in the truth-table length. This is why MCSP sits in NP despite circuits over n inputs.

## Why does it matter?

MCSP is arguably the canonical metacomplexity problem — it formalizes "find the shortest program explaining data." Resolving its deterministic many-one hardness would connect natural NP problems to circuit minimization, resolve a decades-old question predating even the P vs NP formulation, and clarify whether the known barriers (natural proofs, relativization) genuinely block MCSP hardness. It underpins connections to learning theory (learning requires distinguishing structured from random functions), cryptography (MCSP hardness vs. natural-proof barriers), and proof complexity (proofs lower-bounding circuit size).

## What's already known?

- MCSP ∈ NP; it is not known to be in P nor NP-complete under Karp reductions.
- **Conditional results:** Hirahawa–Ilango and earlier works show MCSP is NP-hard under randomized reductions, and (FOCS 2025) NP-hard under deterministic reductions *assuming* certain well-studied cryptographic/complexity assumptions (e.g., existence of functions with exponential circuit complexity that are hard to compute — "well-studied assumptions"). These do not give unconditional hardness.
- **Partial MCSP:** NP-hardness is known for variants with don't-care entries (Ilango and others); also hardness for multi-output, DNF variants (Masek 1970s for DNF-MCSP: verify exact status), oracle variants, and depth-2 MCSP.
- **Relativization:** Hartmanis and others showed MCSP's complexity is oracle-dependent — there are oracles relative to which MCSP is not NP-hard, so relativizing techniques fail.
- **Barriers:** NP-hardness of MCSP under "natural" reductions would imply breakthroughs (e.g., via connections to IW-style hardness-vs-randomness and learning), suggesting any proof must be non-naturalizing and non-relativizing.
- Roughgarden and others show "bushy-tailed" reductions from SAT to MCSP imply circuit lower bounds, indicating why unconditional proofs are hard.

## What would count as solving it?

**Primary goal:** A proof that for every L ∈ NP there is a deterministic polynomial-time function f mapping x to ⟨tt, s⟩ such that x ∈ L ⟺ the truth-table function has circuit size ≤ s. A referee accepts a rigorous, unconditional many-one reduction from, say, SAT to MCSP with a proof the reduction runs in poly(|tt|) time.

**Weaker but publishable milestones** (state which you achieve):
1. Hardness under deterministic Turing reductions (currently also open — verify).
2. Deterministic many-one hardness from any problem not known reducible to MCSP.
3. Identifying a barrier class ruling out broad reduction techniques.

A disproof (MCSP ∈ P) would also resolve the problem and be even more dramatic.

## How to start

1. Read the Hirahaba–Ilango FOCS 2025 paper first: understand exactly which assumption powers their conditional reduction and how far it is from unconditional. Then Ilango's partial-MCSP hardness papers to see which "don't-care" trick is used and why it resists totalization.
2. Study the oracle separations (Fortnow–Kummer–Steinhardt–(verify) style results; "MCSP is not hard for a random oracle") to internalize which techniques are dead.
3. Natural next approach: try to derandomize the known randomized reductions — this would follow from standard hardness-vs-randomness if you could establish strong enough circuit lower bounds for explicit functions; note the circularity that makes this hard.
4. Main obstacle: any efficient reduction from SAT to MCSP essentially forces the prover's witness structure into circuit-size gaps; making this deterministic unconditionally seems to require lower bounds we don't have (cf. Carmosino–Impagliazzo–Kabanets–Kolokolova on learning algorithms from natural proofs).

## Key references

- G. Hirahara, "NP-hardness of learning programs and rules and partial-function MCSP" (2022, STOC/FOCS — verify venue): proves hardness of MCSP for partial functions via reductions from learning problems, leaving the total case open.
- G. Hirahara and R. Ilango, "NP-Hardness of the Minimum Circuit Size Problem from Well-Studied Assumptions," FOCS 2025, DOI: 10.1109/FOCS63196.2025.00087: establishes deterministic many-one NP-hardness of MCSP *conditional* on well-studied assumptions; the state of the art this problem asks to unconditionally.
- W. I. Gasarch, survey open-problem columns on MCSP: document the history and oracle results. (verify exact citation)
- E. Allender, H. Buhrman, L. Koucký, D. van Melkebeek, D. Ron, "Power from random strings" (SIAM J. Comput., 2006): foundational metacomplexity of MCSP and its reduction-class complexities. (verify)

## Warnings

- Do not conflate partial MCSP (don't-cares allowed) with the total version — hardness of the former does not transfer.
- Beware input-size accounting: "polynomial" means polynomial in 2ⁿ; naive reductions blow up exponentially.
- Oracle results show relativizing proofs cannot work; naturalizing proofs are also suspect.
- Randomized or average-case hardness results exist and are frequently misreported as settling the question.
- The census record is vague on the precise FOCS 2025 assumption; verify the paper's theorem statement before relying on it.

---
*`ALGO-000067` · unverified*

## Acceptance guidance

**Primary goal:** A proof that for every L ∈ NP there is a deterministic polynomial-time function f mapping x to ⟨tt, s⟩ such that x ∈ L ⟺ the truth-table function has circuit size ≤ s. A referee accepts a rigorous, unconditional many-one reduction from, say, SAT to MCSP with a proof the reduction runs in poly(|tt|) time.

**Weaker but publishable milestones** (state which you achieve):
1. Hardness under deterministic Turing reductions (currently also open — verify).
2. Deterministic many-one hardness from any problem not known reducible to MCSP.
3. Identifying a barrier class ruling out broad reduction techniques.

A disproof (MCSP ∈ P) would also resolve the problem and be even more dramatic.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/4340206c-736c-4ec6-b012-a7c90cfc92a7?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000067.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000067)

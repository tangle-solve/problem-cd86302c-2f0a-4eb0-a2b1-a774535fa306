<!-- solve-problem:cd86302c-2f0a-4eb0-a2b1-a774535fa306 -->
# Truly subquadratic min-plus convolution

A [Tangle Solve problem](https://solve.tangle.tools/problems/cd86302c-2f0a-4eb0-a2b1-a774535fa306).

## What is the problem?

Given two integer sequences \(a_0,\dots,a_{n-1}\) and \(b_0,\dots,b_{n-1}\), compute the **(min,+)-convolution** \(c\), where
\[c_k = \min_{0\le i\le k} (a_i + b_{k-i}), \quad k=0,\dots,2n-2.\]
The trivial algorithm is \(O(n^2)\). The open question: does there exist \(\varepsilon>0\) such that (min,+)-convolution of two *arbitrary* integer sequences can be computed in \(O(n^{2-\varepsilon})\) time ("truly subquadratic") on a word-RAM with reasonable assumptions (e.g., \(\operatorname{poly}(n)\)-bounded integers and standard \(O(\log n)\)-bit word operations)? Note: if integers are bounded by \(O(n)\), an \(O(n^{3/2}\log n)\)-time algorithm exists, so the problem is genuinely about *unbounded/arbitrary* weights. Some authors conjecture no truly subquadratic algorithm exists (the (min,+)-convolution conjecture); the problem can be attacked in either direction: upper bound (algorithm) or lower bound (conditional hardness).

## Why does it matter?

A subquadratic algorithm would immediately give near-\(O(nW^{1-\varepsilon})\) or \(O(2^{(1-\varepsilon)n})\) improvements for 0/1 knapsack, subset sum (weighted), longest common subsequence variants, and a wide class of "convolution-type" dynamic programs central to operations research and string algorithms. It would also refute the (min,+)-convolution hardness conjecture, collapsing a large web of conditional lower bounds. Conversely, a proof of hardness (under standard conjectures) would firm up the foundations of fine-grained complexity.

## What's already known?

- **Restricted inputs:** Bounded weights (values in \([0, n]\) or \([0, O(n)]\)) admit \(O(n \sqrt{W})\)-type algorithms via partitioning into blocks (Bremner et al.; Chan; Bringmann). Sequences with small difference domains, convex or concave sequences (SMAWK, linear time), and monotone-separable cases all have fast algorithms. None handles arbitrary weights.
- **Equivalences:** Cygan, Mucha, Węgrzycki, Włodarczyk (2017) show (min,+)-convolution is subquadratic-equivalent to many problems, including knapsack, coin change, sorting \(X+Y\) in a specific sense, and tree sparsity — so progress anywhere transfers.
- **Lower bound attempts:** Under the (min,+)-convolution conjecture, no subquadratic algorithm exists; this is used as a basis for hardness of many problems. There is no unconditional lower bound (that would require major circuit/RAM breakthroughs). A related result: (min,+)-matrix-product-based SETH lower bounds do *not* directly apply here.
- **Approaches tried and failed:** FFT rounding (fails because min is not linear), replacing min with smooth softmax (error control fails for adversarial weights), Fredman's trick-style algebraization (works for (min,+) *matrix products* via Grønlund-Pettie-type techniques, but convolution's structure resists similar treatment).

## What would count as solving it?

Either of:
1. **Upper bound:** a randomized (Las Vegas or bounded-error Monte Carlo) or deterministic algorithm computing exact (min,+) convolution of arbitrary length-\(n\) integer sequences in \(O(n^{2-\varepsilon})$ time for some fixed $\varepsilon>0$, with correctness proof for all integer inputs. A referee would demand exactness (no approximation) and a full running-time analysis.
2. **Lower bound:** a proof that no such algorithm exists under a well-stated complexity assumption, or an unconditional lower bound (extremely ambitious).
Partial credit variants: \(O(n^2/\log^{\omega} n)\) speedups (known for some \(\omega>0\) via bit tricks — verify current state), or subquadratic algorithms for broader weight ranges.

## How to start

1. Read Cygan–Mucha–Węgrzycki–Włodarczyk (2017) Section on equivalences — understanding *why* knapsack reduces to convolution clarifies the structural bottleneck.
2. Read Chan's "More on accelerated banded dynamic programming" / Bremner et al. "Fast (min,+) convolutions for bounded weights" to internalize why bounded weights work (block-to-monotone reformulations) and where the technique breaks for unbounded weights.
3. Study Grønlund–Pettie's subcubic (min,+) matrix multiplication: try to adapt its Fredman's-trick combinatorial argument to the one-dimensional convolution case; identify the obstacle (verify whether the obstacle is fundamentally the "all pairs vs. single sequence" structure).
4. Try relaxations: can you compute convolution for inputs where one sequence has small entropy, or after monotone-envelope decomposition, with error that can be repaired in subquadratic time?

## Key references

- M. Cygan, M. Mucha, K. Węgrzycki, M. Włodarczyk, "On Problems Equivalent to (min,+)-Convolution," ICALP 2017, arXiv:1702.07669. Establishes subquadratic equivalences between (min,+) convolution and knapsack, coin change, and other problems, making it the canonical hardness-basis reference.
- V. Vassilevska Williams, "Hardness of Easy Problems: Basing Hardness on Popular Conjectures such as STR" (survey),IWPEC 2015. Surveys fine-grained reductions and the role of (min,+) convolution as a hardness conjecture.
- D. Bremner et al. / T. M. Chan, work on (min,+) convolution with bounded weights giving \(O(n\sqrt{W})\)-type bounds (verify exact authorship/bounds: Chan, "More on accelerated banded dynamic programming..."). Provides the state of the art for restricted inputs.
- K. Bringmann and M. Künnemann, works on fine-grained hardness for knapsack/subset sum (verify). Context for conditional lower bounds conditioned on this exact problem.

## Warnings

- "Subquadratic" must be *truly* subquadratic (\(n^{2-\varepsilon}\)), not \(O(n^2/\log n)\); polylog speedups are known or trivial via word tricks and don't count.
- Bounded-weight algorithms are often cited as if they solve the problem — they do not; the census statement says *arbitrary* sequences.
- Approximation is not a solution; exactness is required (approximate (min,+) convolution is already well understood — verify current bounds).
- The word-RAM model matters: assuming unreasonably wide words or unit-cost arithmetic on huge integers trivializes or breaks the problem.
- A claimed lower bound must be conditional and precisely stated; unconditional superlinear lower bounds for such problems are far beyond current technique.

---
*`ALGO-000078` · unverified*

## Acceptance guidance

Either of:
1. **Upper bound:** a randomized (Las Vegas or bounded-error Monte Carlo) or deterministic algorithm computing exact (min,+) convolution of arbitrary length-\(n\) integer sequences in \(O(n^{2-\varepsilon})$ time for some fixed $\varepsilon>0$, with correctness proof for all integer inputs. A referee would demand exactness (no approximation) and a full running-time analysis.
2. **Lower bound:** a proof that no such algorithm exists under a well-stated complexity assumption, or an unconditional lower bound (extremely ambitious).
Partial credit variants: \(O(n^2/\log^{\omega} n)\) speedups (known for some \(\omega>0\) via bit tricks — verify current state), or subquadratic algorithms for broader weight ranges.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/cd86302c-2f0a-4eb0-a2b1-a774535fa306?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000078.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000078)

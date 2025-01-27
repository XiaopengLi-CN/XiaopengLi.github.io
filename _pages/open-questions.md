---
title: Open Questions
permalink: /open-questions/
published: true
---

Here is a list of (possibly) interesting open questions that I care about.

## Dynamic Dictionaries

A dynamic dictionary is a data structure maintaining a set of $n$ elements from the universe $[U]$, supporting single-element insertions, deletions, and membership queries (i.e., asking whether an element $x$ belongs to the current set). Hash tables are well-studied randomized implementation of dynamic dictionaries, supporting all types of operations within constant expected time.

- **Open Question**: Is there a deterministic algorithm that achieves $O(1)$ time for insertions, deletions, and queries?
  - Many people believe no. If a lower bound is proven, it gives a separation between randomized and deterministic algorithms on this clean problem, which is regarded the second most important derandomization problem left in theoretical computer science (the most important one is whether `RP = P`).

### Succinct Dynamic Dictionaries

A dictionary must use at least $\log \binom{U}{n}$ bits of space because this is the entropy of the set it maintains. If some implementation of dictionary uses $\log \binom{U}{n} + R$ bits of space, we say the **redundancy** is $R$ bits. The optimal trade-off between redundancy and single-operation time is interesting for not only (succinct) dynamic dictionaries but also many other (succinct) data structure problems.

What we know about this problem:

- [\[Bender et al., STOC 2022\]](https://arxiv.org/abs/2111.00602) gives the best upper bound when $R \ge n$: one can achieve $O(k)$ time per operation with $R = O(n \log^{(k)} n)$ bits of redundancy.
- [\[Li et al., FOCS 2023\]](https://arxiv.org/abs/2306.02253) shows the above upper bound is optimal for $R \ge n$. For the range $1 \le R < n$, a lower bound of $\Omega(\log (n/R) + \log^* n)$ time per operation is given.
- [\[Li et al., SODA 2024\]](https://arxiv.org/abs/2310.20536) shows that for $n / \log^{100} n \le R \le n$, we can actually give algorithms that match the proven lower bound $\Omega(\log (n/R) + \log^* n)$.

What we do not know:

- **Open Question:** What is the optimal tradeoff when $R \ll n / \text{poly} \log n$? Is the lower bound tight?

Back to the topic of derandomization. As we already know the best tradeoff for randomized succinct dynamic dictionaries for a wide range of parameters, it is natural to ask:

- **Open Question:** Is there a deterministic succinct dynamic dictionary that achieves the same time-space tradeoff as randomized ones?
  - This is the succinct variant of the very important open question of derandomizing (non-succinct) dynamic dictionaries. We believe that succinctness gives extra tool to prove cell-probe lower bounds, thus this might (or might not) be more doable than the initial question.

## 1-Dimensional Dynamic Succinct Data Structures

See [Story of 1-Dimensional Dynamic Succinct Data Structures](https://XiaopengLi-CN.github.io/posts/2023/08/1dim-dsds) for backgrounds.

**Open Questions** about applications of Dynamic Succincter:
- For arithmetic coding with $O(1)$ alphabet and point updates (single-element updates), is there a data structure with $O(n / \text{poly} \log n)$ redundancy and $O(1)$ operation time? If not, what is the best trade-off curve we can achieve?
  - By the way, we did not study arithmetic coding with large alphabets. This might also be interesting.
- For rank/select (or other 1D problems) with insertions and deletions allowed, what is the best redundancy achievable when the time is optimal $O(\log n / \log \log n)$? Can we prove any nontrivial lower bound?

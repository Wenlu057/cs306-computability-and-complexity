# Proof: $L = \{0^n 1^n \mid n \geq 0\}$ is Not Regular

## Theorem

The language $L = \{0^n 1^n \mid n \geq 0\}$ is not regular.

---

## Proof (by contradiction using the Pumping Lemma)

### Step 1: Assume for contradiction that $L$ is regular

If $L$ is regular, then the **Pumping Lemma** guarantees the existence of a pumping length $p \geq 1$ such that any string $s \in L$ with $|s| \geq p$ can be split into three parts $s = xyz$ satisfying:

- **(i)** $|y| \geq 1$ — the middle piece is non-empty
- **(ii)** $|xy| \leq p$ — the first two pieces together have length at most $p$
- **(iii)** For all $i \geq 0$, $xy^i z \in L$ — we can "pump" $y$ any number of times and stay in $L$

---

### Step 2: Choose a specific string in $L$

Pick $s = 0^p 1^p$.

- This string is in $L$ because it has $p$ zeros followed by $p$ ones.
- Its length is $2p \geq p$, so the Pumping Lemma must apply to it.

---

### Step 3: Analyze how $s$ can be split into $s = xyz$

By condition **(ii)**, $|xy| \leq p$.

Since the first $p$ characters of $s = 0^p 1^p$ are **all 0s**, both $x$ and $y$ must consist **entirely of 0s**. We can write:

| Part | Value | Constraint |
|------|-------|------------|
| $x$  | $0^a$ | $a \geq 0$ |
| $y$  | $0^b$ | $b \geq 1$ (by condition (i)) |
| $z$  | $0^{p-a-b} 1^p$ | remaining 0s plus all 1s |

with $a + b \leq p$.

---

### Step 4: Pump and derive a contradiction

Consider pumping with $i = 2$ (repeat $y$ twice):

$$xy^2z = 0^a \cdot 0^{2b} \cdot 0^{p-a-b} \cdot 1^p = 0^{p+b} \; 1^p$$

- Number of 0s: $p + b$
- Number of 1s: $p$
- Since $b \geq 1$, we have $p + b > p$

**The number of 0s is strictly greater than the number of 1s.**

Therefore $xy^2z \notin L$, because $L$ requires equal numbers of 0s and 1s.

This **violates condition (iii)** of the Pumping Lemma.

---

### Step 5: Conclusion

We have reached a contradiction: the Pumping Lemma says we should be able to pump $y$ and stay in $L$, but pumping produces a string **not** in $L$.

Therefore our assumption in Step 1 is false, and **$L$ is not regular**. $\blacksquare$



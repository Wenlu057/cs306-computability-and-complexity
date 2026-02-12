# Proof: $L = \{ww \mid w \in \Sigma^*\}$ is Not Regular

## Theorem

The language $L = \{ww \mid w \in \Sigma^*\}$ over $\Sigma = \{0, 1\}$ is not regular.

> **Intuition:** $L$ is the set of all strings that are some string $w$ repeated twice. For example: $\varepsilon$, $00$, $11$, $0101$, $01100110$ are all in $L$.

---

## Proof (by contradiction using the Pumping Lemma)

### Step 1: Assume for contradiction that $L$ is regular

If $L$ is regular, then the **Pumping Lemma** guarantees the existence of a pumping length $p \geq 1$ such that any string $s \in L$ with $|s| \geq p$ can be split into three parts $s = xyz$ satisfying:

- **(i)** $|y| \geq 1$ — the middle piece is non-empty
- **(ii)** $|xy| \leq p$ — the first two pieces together have length at most $p$
- **(iii)** For all $i \geq 0$, $xy^i z \in L$ — we can "pump" $y$ any number of times and stay in $L$

---

### Step 2: Choose a specific string in $L$

Pick $s = 0^p 1 \; 0^p 1$.

Let's verify $s \in L$: set $w = 0^p 1$, then $s = ww$. ✓

The length of $s$ is $2p + 2 \geq p$, so the Pumping Lemma must apply to it.

---

### Step 3: Analyze how $s$ can be split into $s = xyz$

By condition **(ii)**, $|xy| \leq p$.

Since the first $p$ characters of $s = 0^p 1 \; 0^p 1$ are **all 0s**, both $x$ and $y$ must consist **entirely of 0s**. We can write:

| Part | Value | Constraint |
|------|-------|------------|
| $x$  | $0^a$ | $a \geq 0$ |
| $y$  | $0^b$ | $b \geq 1$ (by condition (i)) |
| $z$  | $0^{p-a-b} 1 \; 0^p 1$ | remaining 0s, then $1 0^p 1$ |

with $a + b \leq p$.

---

### Step 4: Pump and derive a contradiction

Consider pumping with $i = 2$ (repeat $y$ twice):

$$xy^2z = 0^a \cdot 0^{2b} \cdot 0^{p-a-b} \; 1 \; 0^p \; 1 = 0^{p+b} \; 1 \; 0^p \; 1$$

For this string to be in $L$, it must have the form $ww$ for some $w$. Since the total length is $2p + 2 + b$, each half would need length $p + 1 + \frac{b}{2}$.

**Key observation:** The string $0^{p+b} 1 \; 0^p 1$ has its two $1$s in **asymmetric positions**:

- The first half (first $p + 1 + b/2$ characters) and second half do not match, because the first half has more leading 0s than the second half.

More concretely, if we split $0^{p+b} 1 \; 0^p 1$ into two equal halves:

- **First half:** $0^{p+b} 1 \; 0^{(p-b)/2}$ — starts with $p+b$ zeros
- **Second half:** $0^{(p+b)/2} 1$ — starts with fewer zeros

The first half $\neq$ second half because they begin with different numbers of 0s (since $b \geq 1$).

Therefore $xy^2z \notin L$.

This **violates condition (iii)** of the Pumping Lemma.

---

### Step 5: Conclusion

We have reached a contradiction: the Pumping Lemma says we should be able to pump $y$ and stay in $L$, but pumping produces a string **not** in $L$.

Therefore our assumption in Step 1 is false, and **$L = \{ww \mid w \in \Sigma^*\}$ is not regular**. $\blacksquare$

---

## Alternative Argument for Step 4 (Simpler)

If you prefer a cleaner argument at Step 4:

The pumped string is $0^{p+b} \; 1 \; 0^p \; 1$, which has total length $2p + b + 2$.

- If $b$ is **odd**, the total length is odd, so the string **cannot** be split into two equal halves. Therefore it cannot be of the form $ww$, and $xy^2z \notin L$.

- If $b$ is **even**, the midpoint splits the string into $0^{p+b} 1 \; 0^{b/2}$ and $0^{p - b/2} 1$. The first half starts with $p+b$ zeros while the second starts with $p - b/2$ zeros. Since $b \geq 1$, these are different, so $xy^2z \notin L$.

Either way, we reach a contradiction. ✓

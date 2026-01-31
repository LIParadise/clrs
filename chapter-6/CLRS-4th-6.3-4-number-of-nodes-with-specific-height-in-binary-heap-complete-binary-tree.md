# 6.3-4 Show that at most $\lceil \frac{n}{2^{h+1}} \rceil$ nodes have height $h$ in any $n$-element heap

First we note that there are $\lceil \frac{n}{2} \rceil$ leaves in a binary heap:
Using $0$-indexed scheme, `left(i)` is $2\cdot i + 1$. We ask, what's the invariant for indices that have no left child?

$$
\begin{align*}
2 \cdot i + 1 &\geq n \\
i             &\geq \frac{n-1}{2} = \begin{cases}
    \frac{2m+1-1}{2} = m = \lfloor \frac{n}{2} \rfloor & n = 2m+1 \\
    \frac{2m-1}{2} = m - \frac{1}{2} & n = 2m
    \end{cases}
\end{align*}
$$

Note that $i \geq \left( m \in \mathbb{N} \right) - \frac{1}{2}$ is equivalent to $i \geq m$, thus we conclude that $i \geq \lfloor \frac{n}{2} \rfloor$.
The $\lfloor \cdot \rfloor$ is intentional, as we immediately see:

The size of the set of indices where $i \geq \lfloor \frac{n}{2} \rfloor$ is exactly $(n-1) - \left(i \geq \lfloor \frac{n}{2} \rfloor\right) + 1$.
Since $n = \lfloor \frac{n}{2} \rfloor + \lceil \frac{n}{2} \rceil$, this equals to $\lceil \frac{n}{2} \rceil$ as intended.

So the number of leaves i.e. the number of height $0$ nodes is as expected.
How about the number of height $1$ nodes?

If we purge all the leaves, then the new leaves are exactly those with height $1$ in the original tree!
Thus we only need to handle this following inequality, and mathematical induction we're done; note the new tree have exactly $\lfloor \frac{n}{2} \rfloor$ nodes:

$$
\lceil \frac{\lfloor \frac{n}{2} \rfloor}{2} \rceil
\overset{?}{\leq}
\lceil \frac{n}{2^{1+1}} \rceil
$$

Where LHS is considering leaf count of the pruned new smaller complete binary tree, whereas RHS is the exercise proposition applied on the old tree with height $1$.
Which obviously holds, since the numerator $\lfloor \frac{n}{2} \rfloor \leq \frac{n}{2}$.

## Remarks

These terminology actually vary quite a bit... humankind is great at confusing themselves.

| complete binary tree | full binary tree       | perfect binary tree |
| -------------------- | ---------------------- | ------------------- |
| heap                 | either 2 or 0 children | $h \iff 2^{h+1}-1$  |

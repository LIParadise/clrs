# Cycle Property

[Given](https://en.wikipedia.org/wiki/Minimum_spanning_tree#Cycle_property) undirected simple graph $G$ where edge weights are distinct, if edge $(u, v)$ were the _heaviest_ edge in some cycle $C \subseteq G$, then $(u, v)$ is _not_ contained in _any_ MST of $G$.

Proof is a copy-'n-paste: say $T$ contains $(u, v)$, $T \setminus \{(u, v)\}$ is composed of two trees by edge count and acyclic;
$(u, v)$ in some cycle where it's the heaviest edge, in particular there's cycle,
so there's some edge $(a, b)$ in that cycle s.t. $\left( T \setminus \{(u, v)\} \right) \cup \{(a, b)\}$ is a spanning tree of $G$.
Note the new tree has strictly lower overall weight.

# Distinct Weight Undirected Graphs Have Unique MST

Say there are two spanning trees both of which are MST: $T_1$ and $T_2$. Being distinct, there's some edge $e_1$ that's in $T_1 \setminus T_2$.
$T_2$ being a spanning tree, $T_2 \cup \{e_1\}$ contains cycle; edge weights being distinct, there's _some_ $e_h$ that's heaviest in that cycle. But $e_h$ shall not be in _any_ MST.

## Deleting Heaviest Weight Edges in Cycles Results in MST

Note the result of such a procedure is a spanning tree.
If we could argue that any edge $e \in G.E \setminus T$ is the heaviest in _some_ cycle (not necessarily unique), the lemma follows directly via similar proof technique while proving the [cycle property](#cycle-property).

This is a bit tricky: consider Mandarin character "日" in which there are 6 vertices; starting from the left upper corner labeling $1$ and clock-wise $2 \cdots 6$.
If edge $(1, 6)$ were removed since it's the heaviest in the upper small cycle $\{1, 3, 4, 6\}$,
some other edges in that upper cycle may ultimately got purged still in the end: e.g. maybe $(3, 6)$ i.e. the horizontal bar in the middle of the glyph is the heaviest in the lower small cycle.

In other words, while adding an edge $e$ back to $T$ does results in a cycle, the cycle is probably _not_ the one which made the algorithm decide to discard $e$.

Say we perturb the graph a bit: the set of edge weights is finite, so if $\varepsilon$ were small enough, if we label each edge (in some arbitrary order) and add $\varepsilon \times \text{(edge index)}$ to the edges's weights,
$w^\prime (e_i) < w^\prime(e_j) \iff w(e_i) < w(e_j) \lor \left( w(e_i) = w(e_j) \land i < j\right)$,
such that $G^\prime$ has distinct weights.
I.e $\varepsilon$ break ties whilst preserving the original ordering of weights.

In particular the index/enumeration could be chosen s.t. the sequence of discarded edges have decreasing indices.

As such our algorithm may be seen as running on the perturbated version of $G$, $G^\prime$, arriving at $T^\prime$
$T^\prime$ is spanning tree, and all purged edges are _the_ heaviest weight in _some_ cycle,
and finally the edges have distinct weights, thus [cycle property](#cycle-property) applies here,
i.e. $T^\prime$ is indeed MST of $G^\prime$.

So we need to argue that $T^\prime$ is "basically equivalent" to $T$, in the sense that their weights should agree as long as we make the perturbation small enough. So we need some sort of continuity here: the _weight of MST_ function, a mapping from (the set of all possible weight distributions $w$ on some given fixed graph $G = (V, E)$) to (weight of resulting MST), should be continuous.

Say $w$ and $w^\prime$ differs only on one edge: $w^\prime(e) - w(e) = \varepsilon > 0$, and respectively have $T$ and $T^\prime$ as their MST.
It's immediate that $w^\prime ( T^\prime ) \geq w(T)$. We argue that $w^\prime(T^\prime) - w(T) \leq \varepsilon$.
If $e \not \in T$, then $w^\prime(T) = w(T)$, so we may choose $T^\prime = T$.

OTOH if $e \in T \land e \in T^\prime$, we have the following chain of inequality s.t. $w^\prime(T^\prime) = w(T) + \varepsilon$:

$$
\begin{align*}
w^\prime (T^\prime) &= w(T^\prime) + \varepsilon & e \in T \land e \in T^\prime, w(x) \neq w^\prime(x) \iff x=e \\
    &\geq w(T) + \varepsilon & T \text{ MST w.r.t. } w \\
    &=    w^\prime(T)        & e \in T \\
    &\geq w^\prime(T^\prime) & T^\prime \text{ MST w.r.t. } w^\prime
\end{align*}
$$

Finally if $e \in T \land e \not \in T^\prime$, we have $w^\prime(T^\prime) \leq w(T) + \varepsilon$:

$$
\begin{align*}
w^\prime(T) &\geq w^\prime(T^\prime) & T^\prime \text{ MST w.r.t. } w^\prime \\
    &=    w(T^\prime)               & e \not \in T^\prime \\
    &\geq w(T)                      & T \text{ MST w.r.t. } w \\
    &=    w^\prime(T) - \varepsilon & e \in T
\end{align*}
$$

And since the graph is finite, we conclude that the mapping from (the set of weight distributions on some fixed $G=(V, E)$) to (the weight of resulting MST) is indeed _continuous_ w.r.t <i>$\sup$ norm</i> (attainable thus indeed $\max$ since finite): for all $\delta$, if $\sup (w^\prime-w) \leq \frac{\delta}{\lvert V \rvert}$, we may repeatedly apply the above lemma, and as such $\lvert w^\prime(G) - w(G) \rvert \leq \delta$.

Thus the algorithm of deleting heaviest weight in cycle works, even if there were edges sharing same edge weights: we record the order of edges we delete, and there exists some perturbation to edge weights s.t. the resulting perturbated graph have distinct edge weights, plus its MST is comprised of the same exact edges and vertices as that obtained in our algorithm. Such perturbation may be made arbitrary small, and by continuity of weight of MST over weight distributions, we're done.

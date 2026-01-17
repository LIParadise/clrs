# Finite G DAG, exists v s.t. for all u in G exists unique walk from v to u, then undirected version of G is tree

## Minimally Connected

Note that CLRS refer to what we refer to as _walk_ (any sequence of vertices connected by edges within the graph) as simply _paths_, thus the original question is stated as (emphasis mine):

> Let $G=(V, E)$ be a directecd acyclic graph in which there is a vertex $v_0 \in V$ such that there exists a unique _path_ from $v_0$ to every vertex $v \in V$. Prove that the undirected version of $G$ forms a tree.

First note that the undirected version of $G$, $G^\prime$, is clearly connected. We prove $G^\prime$ is tree via the fact that trees are minimally connected.

Consider any edge $(u, v) \in E$.

Consider the set of vertices, $W \subset V$, of which unique walk from $v_0$ contains $v$. In $G$, there's no way to reach $W$ if $(u, v)$ were kicked out of $E$, which is what we do here: we kick $(u, v)$ out of $G$, and claim the undirected version of the directecd graph, $G^{\prime \prime}$, would be disconnected.

Lemma: $v \in V$, then $\deg_\text{in}(v) = 1 \iff v \neq v_0$ and $\deg_\text{in}(v) = 0 \iff v = v_0$.
Proof: Consider $x \neq v_0$. $\deg_\text{in}(x)$ must be exactly $1$, for there must exist some in degree s.t. $v_0$ may reach $x$, and if there are no less than two, since any pair of its parents in $G$ must respectively have unique walk from $v_0$ by premise, in turn meaning now there's two walks to $x$, contradicting with the unique walk premise, meaning $\deg_\text{in}(x) = 1$. Now consider $v_0$: $\deg_\text{in}(v_0) > 0$ immediately leads to cycles, contradicting with $G$ being directecd acyclic graph.

Lemma: $w \in W$, then $w$'s out degrees are towards some $w^\prime \in W$.
Proof: consider edge $(w, x)$, since there's unique walk from $v_0$ to $w$, the unique walk from $v_0$ to $x$ equals the unique walk from $v_0$ to $w$ followed by one last edge $(w, x)$. That $w \in W$ by definition means the unique walk $v_0$ to $w$ contains $v$. Thus $x \in W$.

By these two lemmas, we see that for any $w \in \left(W \setminus \{v\} \right)$, their undirected edges are pointing towards some other vertex in $W$, while the only in degree of $v$ in $G$ has no undirected counterpart in $G^{\prime \prime}$. I.e. all edges of $W$ in $G^{\prime \prime}$ connects to itself. I.e. $W$ is a connected component disconnected from $v_0$.

The above argument holds for any edge within $G$. Meaning $G^\prime$, the undirected version of $G$, is minimally connected. Thus $G^\prime$ is tree.

## Edge Argument

By the in degree lemma, $G^\prime$ is clearly such that $\lvert E_{G^\prime} \rvert = \lvert V_{G^\prime} \rvert - 1$ and _connected_, i.e. a tree.

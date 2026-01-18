# Given DAG, What Are Number of Walks between Every Possilbe Pair of Vertices?

> Give an efficient algorithm to count the total number of paths in a directed acyclic graph. The count should include all paths between all pairs of vertices and all paths with 0 edges. Analyze your algorithm.

N.B. as usual CLRS's _path_ is indeed _walk_, so the problem is asking for number of walks between vertices.

## Mine

Topologically sort the DAG into array $\{ \nu_1, \nu_2, \nu_3, \cdots, \nu_n \}$. Let $W: (V, V) \to \mathbb{N}$ be number of walks. Note that $i > j \implies W(\nu_i, \nu_j) = 0$ and $W(\nu_i, \nu_i) = 1$. Consider $W(\nu_i, \nu_j)$ when $i < j$.

First, given $i$, assign all vertices a counter initialized to $0$ except that of $\nu_i$ set to $1$.
For $k \in [i+1, n]$, $\nu_k$'s counter is set to sum of that of the vertices strictly before $\nu_k$ but not earlier than $\nu_i$ who has edge entering $\nu_k$ i.e. sum over $\nu_k$'s in-degrees that are no earlier than $\nu_i$ in the topological ordering.
We claim this counter is exactly $W(\nu_i, \nu_j)$ for all $i < j$.
Proof is straightforward by considering loop invariant that each vertex <i>before $\nu_k$ and no earlier than $\nu_i$</i> is assigned correctly their $W$ value, the fact we have a topological ordering, and walks from $\nu_i$ to $\nu_j$ may be partitioned by the _last_ vertex visited right before $\nu_j$.

Total runtime is $O(V^3)$: since we have a topological ordering, for any $i$, $\nu_i$ has at most $(n-i)$ out-degrees, meaning for each $i$ we'd spent $O({\left( n-i \right)}^2)$ time, meaning in total we spent _sum of squares_ time calculating all $W(\nu_i, \nu_j)$ where $i < j$, and finally we know $\sum\limits_{k=1}^{n}{k^2} = \frac{1}{6} n (n+1) (2n+1) \in O(n^3)$.

### Alternative Way

Notice that given $i < j$, $W(i, j)$ is sum of that of $\nu_i$'s out-degrees, plus one if $(\nu_i, \nu_j) \in E$, thanks to DAG and topological ordering:

$$
W(i, j) =
    \left( \sum\limits_{(i, k) \in E \land k \neq j} W(k, j) \right) +
    \left( \begin{cases} 1 & (i, j) \in E \\ 0 & (i, j) \not \in E \end{cases} \right)
$$

Thus the algorithm may also be done by fixing some _end_ point $j$ and calculate all $W(i, j)$ where $i < j$ by considering $\left\{ W(j-1, j), W(j-1, j), \cdots, W(1, j) \right\}$. Time complexity is the same, though.

### Verdict

[gemini](https://gemini.google.com/share/4b0fff236b03)

Note the problem asked only _total number of walks between all pairs_, rather than number of walks between each possible pairs, so our method is taking a detour.

To see how we may accelerate the process via not considering per pair information, note that <i>total number of walks starting from $\mu$ i.e. $N(\mu)$</i> is such that:

$$N(\mu) = 1 + \sum\limits_{(\mu, \nu) \in E} N(\nu)$$

Thus after topological sort, we assign each vertex a counter zero, and going back the topological ordering, each summing over their respective out-degrees. Time complexity is therefore $O(V+E)$: don't forget to add 'em up, though.

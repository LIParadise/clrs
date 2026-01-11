# [gzc/CLRS](https://github.com/gzc/CLRS/blob/b7d3df5ba834b2a15007d0f0fc320f1dfc9f4041/C22-Elementary-Graph-Algorithms/22.3.md)

```
DFS-VISIT(u)
	STACK.push(u)
	while !STACK.empty
		u <- STACK.top()
		if COLOR[u] = GRAY:
			COLOR[u] <- BLACK
			f[u] <- time <- time+1
			STACK.pop()
			continue
		if COLOR[u] = WHITE:
			COLOR[u] <- GRAY
			d[u] <- time <- time+1
		for each v in Adj[u] from tail down to head
			do if color[v] = WHITE
				then π[v] <- u
					 STACK.push(v)
```

## Analysis

Note that the algorithm presented here uses $O(E)$ space: a node might got pushed many times, e.g. consider

$$G = (V = \{\mathrm{root}, a, b\}, E = \{(\mathrm{root}, a), (\mathrm{root}, b), (a, b)\}$$

Then we see that $b$ would be pushed onto the stack _twice_.

Runtime is still linear in graph size i.e. $O(V + E)$, though:
Each vertex has its adjacency list traversed exactly _once_, i.e. when it became the stack top for the first time.
Since each adjacency list is traversed exactly once, the total number of pushes is sum of their lengths, thus $O(E)$ time manipulating the stack.
Then of course we have to spend $O(V)$ time maintaining the vertex properties.
Thus the total runtime is still linear in the graph size.

# Mine

```
DFS-Visit(u):
    let s be freshly allocated stack
    u.color = Gray
    u.d = ++global_time
    u.pi = Nil
    s.push(u)
    while s is not empty: // invariant: (in stack) if and only if (gray, discovery time is set, and predecessor is known)
        v = s.peek_top()
        if v.i < v.adj_list.len:
            // the trick, assuming 0-indexed adjacency lists,
            // and all vertices have their `i` attribute initialized to zero
            j = v.i++
            if v.adj_list[j].color == White:
                v.adj_list[j].color = Gray
                v.adj_list[j].pi = v
                v.adj_list[j].d = ++global_time
                s.push(v.adj_list[j])
            else if (v.adj_list[j].color == Gray) && (v.pi != v.adj_list[j]):
                // loop invariant: predecessor is set
                // back edge detected
                // CLRS 4th lemma 20.11: directed G yields back edges iff cyclic
                // same lemma applies to undirected graph: multi-graphs must be cyclic,
                // so back edges are those connected to (proper ancestor sans parent)
                G.is_cyclic = true
        else:
            v.f = ++global_time
            v.color = Black
            s.pop_top()
```

Idea: we're gonna forget where we are when we eagerly process the new node, so we'd need some state tracking where we were.
Space is better with $O(V)$, since number of gray vertices is less than number of all vertices.
Runtime is no different from CLRS's original implementation. Actually we may see that the call stack in CLRS is replaced with explicit stack.

## Analysis

> [gemini](https://gemini.google.com/share/0fe9dbbb8efe)
> By storing the index `i`, you've effectively replaced the implicit instruction pointer of the CPU's call stack with an explicit variable.
> This is essentially how compilers implement recursion under the hood or how you would implement a non-recursive DFS in a memory-constrained environment.

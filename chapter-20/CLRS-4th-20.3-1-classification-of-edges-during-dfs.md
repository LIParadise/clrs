# CLRS 20.3-1 what are the possible edge combinations during _any point in time_ in a DFS run?

## Directed Graph

| row to column | white         | gray                | black                |
| ------------- | ------------- | ------------------- | -------------------- |
| white         | ALL           | back, cross         | cross                |
| gray          | tree, forward | back, tree, forward | cross, tree, forward |
| black         | NONE          | back                | ALL                  |

- white -> white
    - In the beginning of DFS
- white -> gray
    - back if r is going to be descendant of c and time is after c.d before r.d
    - cross if c is picked to start DFS first, there exists edge $(r, c)$, and there's no path from c to r in directed graph G
    - Not forward: if c were to be descendant of r, meaning c remain white after r gray
    - Not tree: same argument as forward edge
- white -> black
    - cross: same argument as (white -> gray)
    - Not forward: same argument as (white -> gray)
    - Not tree: same argument as (white -> gray)
    - Not back: if r were descendant to c, then c remain gray until r turns black.
- gray -> white
    - white path theorem applied to the path of length 1 i.e. $\{(r, c)\}$: c is descendant to r.
        - tree edge: child
        - forward edge: non-child proper descendant 
        - not cross edge for c descendant to r.
    - Besides white path theorem...
        - Not back: back means c proper ancestor to r in DFS tree, meaning c is gray before r is gray.
- gray -> gray
    - both c and r are being traversed
        - Back edge: when c is ancestor to r
        - Tree edge: when c is descendant to r, and c has not yet done its further DFS
        - Forward edge: same as tree edge
        - Not cross edge: c and r are both in the call stack of DFS, they are in the same tree.
- gray -> black
    - Is there some instant $(r, c)$, r is ongoing, while c is done?
        - Cross edge: DFS started at c first and no path from c to r, and fresh new DFS starts at r
        - Tree edge: when c is child to r, r discovers c and still going, and c had completed
        - Forward edge: same as tree edge, for r may have multiple out degrees
        - Not back edge: if r descendant to c, then r turns black earlier than c turns black
- black -> white
    - Is there some instant $(r, c)$, r is finished, while c haven't even been discovered?
        - Impossible: r is not finished until it explored all its out degree
- black -> gray
    - Is there some instant $(r, c)$, r is finished, while c is ongoing?
        - Back edge: r is descendant to c, r is done, but c is ongoing
        - Not forward: if r were ancestor to c, r is not finished until after c finished
        - Not tree: same as not forward
        - Cross edge: for $(r, c)$ to be cross edge, c must have completed and turn black earlier than r does
- black -> black
    - In the end of DFS

## Undirected Graph

| row to column | white      | gray       | black      |
| ------------- | ---------- | ---------- | ---------- |
| white         | tree, back | tree, back | NONE       |
| gray          | tree, back | tree, back | tree, back |
| black         | NONE       | tree, back | tree, back |

Note in particular this is **not** simply filtering the table obtained in [directed graph](#directed-graph), for it's symmetrical. Anyhow, here's filtered version:

| row to column | white      | gray       | black      |
| ------------- | ---------- | ---------- | ---------- |
| white         | tree, back | back       | NONE       |
| gray          | tree       | tree, back | tree       |
| black         | NONE       | back       | tree, back |

Then we need to do a bitflag $\lor$ operation with its transpose after filtering:

| row to column | white      | gray       | black      |
| ------------- | ---------- | ---------- | ---------- |
| white         | tree, back | tree, back | NONE       |
| gray          | tree, back | tree, back | tree, back |
| black         | NONE       | tree, back | tree, back |

## Reference

[github CLRS solutions](https://github.com/gzc/CLRS/blob/b7d3df5ba834b2a15007d0f0fc320f1dfc9f4041/C22-Elementary-Graph-Algorithms/22.3.md)

# Master Theorem

## Case 1 Leaves

## Case 2 Balanced

This is slightly trickier, but in general when you see $f(n) = {\left( \lg{x} \right)}^k \cdot n^{\log_b a}$
(some likes to denote the _polylogarithmic_ term as $\log^k {(x)}$ i.e. move where the exponent lives)
Then we'd have

$$ T(n) = \left( \log^{k+1} {(n)} \right) \cdot n^{\log_b a} $$

## Case 3 Root

$$
    \begin{cases}
        T(n) = a \cdot T \left( \frac{n}{b} \right) + f(n) &
        f(n) \in \Omega \left( n^{\varepsilon + \log_b a} \right) \land \varepsilon > 0 \\
        a \cdot f \left( \frac{n}{b} \right) \leq c \cdot f(n) & c<1
    \end{cases}
$$

Note the [regularity][CSSE 130246] [condition][CSSE 4854] is there to _eliminate some of the "uglier" functions_: math, as usual, contains some weird examples that a generic $\Omega$ captures little of its full glory. The general idea, however, is that the function _shrinks fast enough_ when we go diving into the recursion tree.

Some napkin math: say $f(n) = n^{\varepsilon + \log_b a}$ for some concrete $\varepsilon \in \mathbb{R}$. Then we have:

$$
\begin{align*}
    a \cdot f \left( \tfrac{n}{b} \right)
    & = a \cdot {\left( \tfrac{n}{b} \right)} ^ {\varepsilon + \log_b a} \\
    & = a \cdot \left( n^{\varepsilon + \log_b a} \right) \cdot {\left( {\tfrac{1}{b}} \right)}^{\varepsilon + \log_b a} \\
    & = f(n) \cdot \frac{ a }{b^{\varepsilon + \log_b a}} \\
    & = f(n) \cdot \frac{ a }{ a \cdot b^\varepsilon }
\end{align*}
$$

And since for generic recursion we are expecting $b > 1$, a _nice_ $f(n)$ automatically satisfies the regularity condition.
To illustrate this further, consider the layer of which depth is $d$:

$$
\begin{align*}
    a^d \cdot f \left( \tfrac{n}{b^d} \right)
    & = a^d \cdot {\left( \tfrac{n}{b^d} \right)} ^ {\varepsilon + \log_b a} \\
    & = a^d \cdot \left( \frac{n^{\log_b a}}{b^{d \cdot \log_b a} = a^d} \right) \cdot \left( \frac{n^\varepsilon}{b^{d \cdot \varepsilon}} \right) \\
    & \in \Theta \left( n^{ \varepsilon + \log_b a} \right)
\end{align*}
$$

Note that when $\varepsilon = 0$, we see that $f$ does remain the same when we dive deeper. By setting $\varepsilon < 0$ this explains also the why the first case is about [leaves](#case-1-leaves).

### Irregularities

This is mainly copied from [here][CSSE 130246].

	
$$
\begin{align}
f(n) & = a^{2 \lfloor \log_{b^2} n \rfloor (1+\frac{\varepsilon}{\log_b a}) } \\
     & \leq a^{\left( 2 \cdot \left( -1 + \tfrac{1}{2} \log_b n \right) \cdot (1+\frac{\varepsilon}{\log_b a}) \right)} \\
     & \in \Omega \left( a^{\log_b n \cdot (1+\frac{\varepsilon}{\log_b a}) } \right) \\
     & = \Omega \left( a^{\log_b n} \cdot a^\frac{\varepsilon \cdot \log_b n}{\log_b a} \right) \\
     & = \Omega \left( n^{\log_b a} \cdot a^{\varepsilon \cdot \log_a n} \right) \\
     & = \Omega \left( n^{\log_b a} \cdot n^\varepsilon \right)
\end{align}
$$

Note that $a^{\left( 2 \cdot \left( -1 \right) \cdot (1+\frac{\varepsilon}{\log_b a}) \right)}$ is a constant which is discarded in $(2)$.
Consider when $n = b^{2m + 1}$ for some $m \in \mathbb{Z}^+$, then $f(\tfrac{n}{b}) = f(n)$ thanks to the $\lfloor ~ \rfloor$ operator.
We conclude that $f$ fails to satisfy the regularity condition.
Colloquially, in the recursion tree, some layers of the tree refuses to cut down on the <i>divide and combine cost $f(n)$</i>


[CSSE 130246]: https://cs.stackexchange.com/questions/130246
[CSSE 4854]: https://cs.stackexchange.com/questions/4854


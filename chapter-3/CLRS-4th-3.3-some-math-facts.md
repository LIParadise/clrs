# Some Math Facts

- Stirling

$$
\begin{align*}
n! &= \Gamma(n+1) \\
   &\approx \sqrt{2 \pi n} \left( \tfrac{n}{e} \right)^n \left( 1+ \tfrac{1}{12n} + \tfrac{1}{288n^2} + \tfrac{-139}{51840n^3} + \cdots \right) \\
n! &\in \sqrt{2 \pi n} \left( \tfrac{n}{e} \right)^n \times \left( e^{\tfrac{1}{12n+1}}, e^{\tfrac{1}{12n}} \right)
\end{align*}
$$

## Calculus

- Boundedness Theorem and Extreme Value Theorem

$f$ real valued function defined on some _closed_ interval on $\mathbb{R}$ and $f$ is continuous. Then $f$ attains its maximum/minimum within $[a, b]$.

Proof: If no supremum/infimum may be defined for $f$ on $[a, b]$, then we may construct a sequence on which $f$ diverges.
By [Heine-Borel](https://math.stackexchange.com/questions/465936) and the fact closed intervals on $\mathbb{R}$ is _compact_ thus _sequentially compact_,
i.e. within any sequence lies some subsequence that converges into some point in the set, here $c \in [a, b]$;
being continuous means all sequences converging to $c$ should converge to $f(c) \in \mathbb{R}$, a contradiction.

Alternative proof see [also](https://mathcenter.oxford.emory.edu/site/math111/proofs/extremeValueTheorem).

- Fermat's Theorem

If $f$ real valued, $f^\prime(c)$ well-defined and $f$ attains relative extrema at $c$, then $f^\prime(c) = 0$.

[Proof](https://tutorial.math.lamar.edu/classes/calci/DerivativeAppsProofs.aspx#Extras_DerAppPf_Fermat)
By $f^\prime (c)$ well-defined, we see $\lim\limits_{\xi \to 0}{ \frac{f(c + \xi) - f(c)}{\xi} } = f^\prime (c) \in \mathbb{R}$;
being relative extrema forces its left limit and right limit to differ in sign, meaning for the limit to exist, it must be zero.

- Rolle's Theorem

$f$ real valued, contiuous on $[a, b] \subset \mathbb{R}$, differentiable on $(a, b) \subset \mathbb{R}$, $f(a) = f(b)$, then exists some $c \in (a, b)$ s.t. $f^\prime (c) = 0$.

[Proof](https://tutorial.math.lamar.edu/classes/calci/DerivativeAppsProofs.aspx):
By extreme value theorem WLOG suppose $f$ attains maximum on some $f(c) > f(a) = f(b)$ where $c \in (a, b)$.
Since $f^\prime$ is defined on $(a, b)$, by Fermat's theorem $f^\prime(c) = 0$.

- Mean Value Theorem

$f$ real valued, contiuous on $[a, b] \subset \mathbb{R}$, differentiable on $(a, b) \subset \mathbb{R}$, then exists some $c \in (a, b)$ s.t.

$$(b-a) \cdot f^\prime (c) = f(b) - f(a)$$

[Proof](https://tutorial.math.lamar.edu/classes/calci/DerivativeAppsProofs.aspx):
Let $g(x) = f(x) - f(a) - (x-a) \cdot \frac{f(b) - f(a)}{b-a}$, then $g$ satisfies Rolle's theorem's prerequisites, so there's some $c \in (a, b)$ s.t. $g^\prime(c) = 0$.

- Cauchy's Mean Value Theorem

Let $f$ and $g$ both continuous on closed interval in $\mathbb{R}$ and differentiable on its interior, then in the interior exists some $c$ satisfying:

$$ (f(b) - f(a)) \cdot g^\prime(c) = (g(b) - g(a)) \cdot f^\prime(c) $$

In some sense this is saying for differentiable parametric function $\mathbb{R} \to (\mathbb{R}, \mathbb{R})$ there is _probably_ some tangent that's parallel to the line passing through the end points...
Except this is not entirely true: the point satisfying Cauchy may actually be _stationary **cusps**_ e.g. $(0, 1)$ for $(t^3, 1-t^2)$, s.t. there's no tangent that's parallel to the line passing through the end points.

Note that Rolle is special case for MVT, which is in turn special case for MVT, but proof is the other way: $h$ satisfies prerequisites for Rolle, and the result follows.

$$ h(x) \coloneqq (g(b)-g(a))f(x) - (f(b)-f(a))g(x) $$

- Taylor-Peano

If $f \in \mathrm{C}^1$ i.e. $f^\prime$ well-defined, then the error term is $o((x-a))$; note this theorem merely states the fact it's _faster_, but not _how_ faster: it could be super slow, like $x^\tfrac{1}{3}$, etc.

$$ f(x) = f(a) + f^\prime(a)(x-a) + o((x-a)) $$

- Analytic Function

A function is _analytic_ if it's $\mathrm{C}^\infty$, plus for all $\xi$ in its domain, there's some open set $A$ containing $\xi$ that the power series expansion (Taylor expansion) based on $\xi$ converges to $f(x)$ _pointwise_ on that open set, i.e.

$$ f(x) = \sum\limits_{k=0}^{\infty}{ (x-\xi)^k \frac{f^{(k)}(\xi)}{k!} } , \{x, \xi\} \subset A$$

Note it's a definition that's strictly stronger than being $\mathrm{C}^\infty$, we'd expect some counter example, like these two: both are analytical on $\mathbb{R} \setminus \{0\}$, but at $0$, the series expansion are both simply the zero function, meaning even though the radius of convergence is infinite, they do not converge to the original function.

$$
\begin{align*}
f(x) &= \begin{cases}
        0 & x\leq 0 \\
        e^{-\frac{1}{x}} & x > 0
        \end{cases} \\
g(x) &= \begin{cases}
        0 & x = 0 \\
        e^{-\frac{1}{x^2}} & x \neq 0
        \end{cases} \\
\end{align*}
$$

Note that being analytical at one point automatically implies that the function is analytical within some open set.

- Taylor-Lagrange

Suppose $f \in \mathbb{R} \to \mathbb{R}$ is $k$ times differentiable at $a$. Then we may write the following; proof [see](#cauchy-mvt-and-error-term-analysis) [also](#iteratively-applying-lhôpital):

$$
\begin{align*}
f(x) &= \sum\limits_{i=0}^{k} { \left( \frac{f^{(i)}(a)}{i!} (x-a)^i \right) } + r_k(x) \\
r_k(x) &= q_k(x) (x-a)^k \in o(\lvert x-a \rvert^k) \\
\lim\limits_{x \to a}{q_k(x)} &= 0
\end{align*}
$$

### Some Surprising Facts

Differentiable [only](https://www.reddit.com/r/math/comments/stp86v) at one [single point](https://math.stackexchange.com/questions/4580113) is possible: $x^2 \times \begin{cases} x=1 & x\in\mathbb{Q} \\ x=0 & x\not\in \mathbb{Q} \end{cases}$ or $\lvert z \rvert^2$ on the complex [plane](https://www.reddit.com/r/math/comments/stp86v/comment/hx8njlw).

It's possible to find functions that are [derivative is discontinuous on a nowhere dense set of positive measure](https://math.stackexchange.com/a/423279/595630): keyword being combine these with the (fat) Cantor set, and that if function converges while its derivative converges _uniformly_, the limit remains differentiable:

$$
\begin{align*}
f(x) &= \begin{cases}
            x^2 \sin( \frac{1}{x} ) & x \neq 0 \\
            0 & x = 0
        \end{cases} \\
g(x) &= \begin{cases}
        x^2 (1-x)^2 \sin \left( \frac{1}{\pi x (1-x)}\right) & x \in (0, 1) \\
        0 & x \not \in (0, 1)
        \end{cases}
\end{align*}
$$

You may have an $f: \mathbb{R} \to \mathbb{R}$ that's _smooth everywhere_ but _not analytical at **any** point_ via [Fourier series](https://en.wikipedia.org/wiki/Non-analytic_smooth_function#A_smooth_function_that_is_nowhere_real_analytic): $f(x) = \sum\limits_{k \in \mathbb{Z}^+}{ \left( e^{-\sqrt{2^k}} \cos{(2^k x)} \right)}$: its radius of convergence is zero on some _dense_ subset in $\mathbb{R}$, and since being analytical at one point implies being analytical on some open set, $f$ cannot be analytical on any point in $\mathbb{R}$.

### Proofs

#### Taylor-Lagrange

##### Cauchy MVT and Error Term Analysis

This proof, albeit elementary, assumes a slightly stronger condition: <i>$f^{(n)}$ is well-defined and **continuous** around some open interval in which lies $a$</i>, s.t. Cauchy's MVT applies. This is the proof used in [wiki](https://en.wikipedia.org/wiki/Taylor%27s_theorem#Statement_of_the_theorem). Consider $P_{n-1}$ and associated error terms:

$$
\begin{align*}
P_{n-1}(x) &= \sum\limits_{k=0}^{n-1}{ \frac{f^{(k)}(a)}{k!} (x-a)^k} \\
R_{n-1}(x) &= f(x) - P_{n-1}(x) = f(x) - \sum\limits_{k=0}^{n-1}{ \frac{f^{(k)}(a)}{k!} (x-a)^k} \\
G_{n-1}(x) &= (x-a)^n
\end{align*}
$$

Observed that $R_{n-1}^{(k)}(a) = G_{n-1}^{(k)}(a) = 0$ for integers $0 \leq k \leq (n-1)$.
By Cauchy's MVT, consider interval $[a, x]$, we know there's some $c_1 \in (a, x)$ s.t.:

$$
\begin{align*}
\frac{R_{n-1}(x)}{G_{n-1}(x)} &= \frac{R_{n-1}(x) - 0}{G_{n-1}(x) - 0} \\
&= \frac{R_{n-1}(x) - R_{n-1}(a)}{G_{n-1}(x) - G_{n-1}(a)} \\
&= \frac {R_{n-1}^\prime(c_1)} {G_{n-1}^\prime(c_1)} \\
\frac{R_{n-1}(x)}{G_{n-1}(x)} &= \frac{R_{n-1}^{(1)}(c_1)}{G_{n-1}^{(1)}(c_1)} = \frac{R_{n-1}^{(2)}(c_2)}{G_{n-1}^{(1)}(c_2)} = \cdots = \frac{R_{n-1}^{(n-1)}(c_{n-1})}{G_{n-1}^{(1)}(c_{n-1})} = \frac{R_{n-1}^{(n)}(c_n)}{G_{n-1}^{(n)}(c_n)} 
\end{align*}
$$

where $a < c_n < c_{n-1} < c_{n-2} < \cdots < c_1 < x$. Note $c_n$ is where we need $f^{(n)}$ defined around $a$. Further,

$$
\begin{cases}
G_{n-1}^{(n)} = n! \\
R_{n-1}^{(n)} = f^{(n)}
\end{cases}
$$

$$
\begin{align*}
f &= P_{n-1} + R_{n-1} \\
  &= \left( \sum\limits_{k=0}^{n-1}{ \frac{f^{(k)}(a)}{k!} (x-a)^k} \right) + \frac{R_{n-1}}{G_{n-1}} G_{n-1} \\
  &= \left( \sum\limits_{k=0}^{n-1}{ \frac{f^{(k)}(a)}{k!} (x-a)^k} \right) + \frac{R_{n-1}^{(n)}(c_n)}{G_{n-1}^{(n)}(c_n)} (x-a)^n \\
  &= \left( \sum\limits_{k=0}^{n-1}{ \frac{f^{(k)}(a)}{k!} (x-a)^k} \right) + \frac{f^{(n)}(c_n)}{n!} (x-a)^n \\
\end{align*}
$$

Finally we may derive the desired property, taking advantage of the extra assumption i.e. continuity of $f^{(n)}$ around $a$:

$$
\begin{align*}
f &= \left( \sum\limits_{k=0}^{n-1}{ \frac{f^{(k)}(a)}{k!} (x-a)^k} \right) + \frac{f^{(n)}(c_n)}{n!} (x-a)^n \\
  &= \left( \sum\limits_{k=0}^{n-1}{ \frac{f^{(k)}(a)}{k!} (x-a)^k} \right) + \frac{f^{(n)}(a)}{n!} (x-a)^n + \frac{f^{(n)}(c_n) - f^{(n)}(a)}{n!} (x-a)^n \\
  &= \left( \sum\limits_{k=0}^{n-1}{ \frac{f^{(k)}(a)}{k!} (x-a)^k} \right) + \frac{f^{(n)}(a)}{n!} (x-a)^n + h(x) (x-a)^n \\
  &= \left( \sum\limits_{k=0}^{n}{ \frac{f^{(k)}(a)}{k!} (x-a)^k} \right) + h(x) (x-a)^n \\
\lim\limits_{x \to a} h(x) &= 0
\end{align*}
$$

##### Iteratively Applying L'Hôpital

This version assumes [only](https://en.wikipedia.org/wiki/Taylor%27s_theorem#Proof_for_Taylor's_theorem_in_one_real_variable) $f^{(n)}(a)$ being well-defined: no need to assume $f^{(n)}$ being continuous on some open set containing $a$.

$$
\begin{align*}
\lim\limits_{x \to a} \frac{f(x) - P_n(x)}{(x-a)^n} & \overset{?}{=} 0 \\
\lim\limits_{x \to a} \frac{f(x) - P_n(x)}{(x-a)^n} & \overset{\text{L'Hôpital}}{=} \lim\limits_{x \to a} \frac{f^\prime(x) - P_n^\prime(x)}{n(x-a)^{n-1}} \\
& \overset{\text{L'Hôpital}}{=} \lim\limits_{x \to a} \frac{f^{(2)} - P_n^{(2)}}{n \cdot (n-1) (x-a)^{n-2}} \\
& \overset{\text{L'Hôpital}}{=} \cdots \\
& \overset{\text{L'Hôpital}}{=} \lim\limits_{x \to a} \frac{f^{(n-1)} - P_n^{(n-1)}}{n! \cdot (x-a)} \\
&= \frac{1}{n!} \lim\limits_{x \to a} \frac{\left( f^{(n-1)} - P_n^{(n-1)} \right)}{x-a} \\
&= \frac{1}{n!} \lim\limits_{\varepsilon \to 0} \frac{\left( h = \left( f^{(n-1)} - P_n^{(n-1)} \right) \right)(a+\varepsilon) - \left( h(a) = 0 \right)}{\varepsilon} \\
&= \frac{1}{n!} h^\prime(a) \\
&= 0
\end{align*}
$$

---
title: Sample Post
date: 2013-11-28 09:31 UTC
tags: example, test, mathematical
head: [mathjax]
---

What follows contains an excerpt from D. Knuth's _The Art of Computer Programming_.

READMORE

Algorithm E from Knuth's book, expressed in Ruby:

~~~ ruby
# Given two positive integers m and n,
# find their greatest common divisor.
def algorithm_E(m, n)
  r = m % n
  while (r != 0) do
    m = n
    n = r
    r = m % n
  end
  return n
end
~~~

>Algorithm E may, for example, be formalized […] as follows:
>Let \\(Q\\) <!-- \( \) must be escaped in Markdown. -->
>be the set of all singletons $(n)$, all ordered pairs $(m,n)$,
>and all ordered quadruples $(m,n,r,1)$, $(m,n,r,2)$, and $(m,n,p,3)$,
>where $m$, $n$, and $p$ are positive integers and $r$ is a nonnegative
>integer. Let $I$ be the subset of all pairs $(m,n)$ and let $\Omega$
>be the subset of all singletons $(n)$. Let $f$ be defined as follows:
>
>\\begin{eqnarray}
>f(m,n) &=& (m,n,0,1);\qquad f(n) = (n); \\\\\
>f(m,n,r,1) &=& (m,n,\text{ remainder of }m\div n, 2); \\\\\
>f(m,n,r,2) &=& (n)\quad\text{if}\quad r = 0,\quad (m,n,r,3)\quad\text{otherwise};\\\\\
>f(m,n,p,3) &=& (n,p,p,1).
>\\end{eqnarray}
>
>The correspondence between this notation and Algorithm E is evident.

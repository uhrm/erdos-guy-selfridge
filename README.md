# Verifying the Guy-Selfridge conjecture

For a natural number $N$, let $t(N)$ be the largest number such that $N!$ can be factored into $N$ integer factors, each of which is at least $t(N)$.  [It is known](https://arxiv.org/abs/2503.20170) that $\frac{1}{e} - \frac{O(1)}{\log N} \leq \frac{t(N)}{N} \leq \frac{1}{e} - \frac{c_0+o(1)}{\log N}$,
where $c_0 := \frac{1}{e} \int_0^1 \left \lfloor \frac{1}{x} \right\rfloor \log \left( ex \left \lceil \frac{1}{ex} \right\rceil \right)\ dx = 0.3044\dots,$
answering a question of [Erdős and Graham](https://www.erdosproblems.com/391).  

Here is a graph of the integral defining $c_0$:

![The integral determining $c_0$.](LaTeX/original%20paper/integ.png)

And here is a plot of $t(N)/N$ against some comparators for $N \leq 79$:

![Plot of $t(N)$ and comparators for $N \leq 79$](LaTeX/original%20paper/plot.png)

Here is an extension of that image to $N \leq 200$:

![Plot of $t(N)$ and comparators for $N \leq 200$](src/python/newplot_200.png)

A view of $80 \leq N \leq 599$:

![Plot of $t(N)$ and comparators for $80 \leq N \leq 599$](src/python/newplot_600_all.png)

An enlargement of the previous graph, also including the greedy algorithm lower bound:

![Plot of $t(N)$ and comparators for $80 \leq N \leq 599$](src/python/newplot_600.png)

This repository records the efforts to verify the [Guy-Selfridge conjectures](https://zbmath.org/0918.11013) concerning the sequence $t(N)$:

1. $t(N) \geq \lfloor 2N/7 \rfloor$ for all $N \neq 56$.
2. $t(N) \geq N/3$ for all $N \geq 3 \times 10^5$.  How small can the lower threshold $3 \times 10^5$ be?

(A further conjecture of Guy and Selfridge that $t(N) \leq N/e$ for $N \neq 1,2,4$ [has been solved](https://arxiv.org/abs/2503.20170).) 

Secondary goals are

3.  Extend the values of $t(N)$ reported in the OEIS (which [are listed up to](https://oeis.org/A034258/b034258.txt))  $N \leq 79$, and which can be extended to $N \leq 200$ by inverting [OEIS A034259](https://oeis.org/A034259).
4.  Obtain more accurate values for $c_0$.


## Current status

1. Conjecture 1 has been reduced to Conjecture 2; in particular, it has been verified up to $N \leq 10^{11}$ and for $N \geq 10^{12}$, and for the remaining $N$ it would follow from the corresponding instance of Conjecture 2.
2. Conjecture 2 is known in the range $43632 \leq N \leq 10^{11}$, for $N \geq 10^{12}$, and fails for $N = 43631$.  Thus, contingent on verifying the conjecture for $N > 10^{11}$, the optimal threshold is $43632$.  The smallest $N$ for which the conjecture holds (excluding the small cases $N=1,2,3,4,5,6,9$) is $N=41006$.
3. The OEIS tables have been extended to $N \leq 10000$ by the linear programming method (combined with integer programming to handle a few rare cases where the linear programming bounds are not tight).
4. Non-rigorous numerics suggest that $c_0 \approx 0.30441901087$.  More rigorously, one has $c_0 = 0.304419011 \pm 7 \times 10^{-9}$ (assuming no significant roundoff errors in floating point arithmetic).  In principle, interval arithmetic could give a fully rigorous bound, but this has not yet been attempted.

## Timeline on controlling $t(N)$

| Date | Contributor | Goal | $N$ | Method | Comments |
| --- | --- | --- | --- | --- | --- |
| [Oct 1998](https://www.jstor.org/stable/2588996) | Richard Guy and John Selfridge | 1,3 | $[1,79]$ | Unknown | Exact value computed
| [12 May 2001](https://oeis.org/A034258) | Robert G. Wilson | 1, 3 | $[1,79]$ | Unknown | Exact value computed
| [29 Nov 2001](https://oeis.org/A034259) | Don Reble | 1,  3 | $[1, 200]$ | Unknown | Exact value computed
| [26 Mar 2025](https://arxiv.org/abs/2503.20170v1) | Terence Tao | 1, 2 | Sufficiently large | Modify an approximate factorization | Back of the envelope calculations suggest that this construction works for $N \gtrapprox 10^{11}$
| [27 Mar 2025](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/#comment-687574) | Andrew Sutherland | 1 | $[1,10^5]$ | Greedy | N = [182](https://math.mit.edu/~drew/ES182.txt), [200](https://math.mit.edu/~drew/ES200.txt), [207](https://math.mit.edu/~drew/ES207.txt) treated separately
|  [27 Mar 2025](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/#comment-687574) | Andrew Sutherland | 2 | $[298344, 3 \times 10^5]$ | Greedy | Surplus of 372 at $N=3 \times 10^5$
| [3 Apr 2025](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/#comment-687641) | Matthieu Rosenfeld | 2 | $3 \times 10^5$ | Improved greedy | Surplus of 393
| [3 Apr 2025](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/#comment-687646) | Uhrmar | 2 | $3 \times 10^5$ | Linear program | Surplus of 455; likely optimal
| [4 Apr 2025](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/#comment-687655) | Matthieu Rosenfeld | 2 | $[138075, 5 \times 10^5]$ | Improved greedy
| [5 Apr 2025](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/#comment-687676) | Kevin Ventullo | 2 | $[3 \times 10^5, 10^8$] | Improved greedy 
| [6 Apr 2025](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/#comment-687676) | Kevin Ventullo | 2 | $[8 \times 10^4, 3 \times 10^8$] | Improved greedy | Conjecture 1 is now reduced to Conjecture 2
| [6 Apr 2025](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/#comment-687695) | Matthieu Rosenfeld | 2 | $[8 \times 10^4, 10^9]$ | Improved greedy
| [8 Apr 2025](https://gus-massa.blogspot.com/2025/04/decomposing-factorial-of-300k-as.html) | Gustavo | 2 | $3 \times 10^5$ | Modify an approximate factorization | 
| [9 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/pull/1) | Uhrmar | 3 | $[1,600]$ | Linear programming (or integer programming for $N=155$)| LP bound is off by one at $N=155$.
| [11 Apr 2025](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/comment-page-1/#comment-687728) | Matthieu Rosenfeld | 2 | $[8 \times 10^4, 2 \times 10^{10}]$ | Improved greedy
| [11 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/pull/5) | Boris Alexeev | 2 | $[43632, 80973]$ | Linear programming | 
| [11 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/pull/2#issuecomment-2796186186) | Uhrmar | 2 | $\neg 43631$; $[43632,8 \times 10^4]$ | Linear programming | Provisional limit of Conjecture 2 reached 
| [12 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/pull/8) | Evan Conway | 2 | $\neg[1,15000] \cup [38000,42000]$ $\backslash \{1,2,3,4,5,6,9,41006\}$ | Linear programming | $41006$ is the smallest known $N>9$ where Conjecture 2 holds
| [13 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/pull/13) | Boris Alexeev | 2 | Sufficiently large | Redistributing small factors from standard factorization
| [14 Apr 2025](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/comment-page-1/#comment-687746) | Matthieu Rosenfeld | 2 | $[10^{10}, 10^{11}]$ | Improved greedy
| [14 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/pull/15) | Boris Alexeev | 2 | $\neg 43631$ | Linear programming | Rigorous certificate of Conjecture 2 failure at this point
| [14 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/issues/19) | Evan Conway | 2 | $\neg [10,41005]$ | Linear programming
| [16 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/pull/24#issuecomment-2811388882) | Boris Alexeev | 3 | $[1,10^4] \backslash$ $\{155,765,1528,1618,1619,2574,2935,3265,5122,5680,9633\}$ | Linear programming
| [17 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/pull/25) | Boris Alexeev | 3 | $[1,10^4]$ | Linear and integer programming |  
| [17 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/commit/95e68bd8cf5234d1f722b3c16de5b0dfb37446bc) | Terence Tao | 2 | $N \geq 10^{12}$ | Modified approximate factorization + explicit estimates |  

## Computations of $c_0$

| Date | Contributor | Result | Method | Comments |
| --- | --- | --- | --- | --- | 
| [26 Mar 2025](https://arxiv.org/abs/2503.20170v1) | Terence Tao | $c_0 \approx 0.3044$ | Naive Riemann sum | Non-rigorous
| [11 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/issues/6) | Terence Tao | $c_0 \approx 0.30441901087$ | Exact evaluation of partial integral + heuristic estimate of error | Non-rigorous
| [11 Apr 2025](https://github.com/teorth/erdos-guy-selfridge/issues/6#issuecomment-2797993853) | Evan Conway | $c_0 \in [0.3044190040310339, 0.304419017709828]$| Exact eval. of partial integral + rigorous bound on error | Rigorous (up to rounding errors)

## Data

- [OEIS A034258](https://oeis.org/A034258) - has data on $t(N)$ for $N \leq 79$
- [OEIS A034259](https://oeis.org/A034259) - implicitly has data on $t(N)$ for $N \leq 200$
- [Values of t(N) for N up to 200](https://github.com/teorth/erdos-guy-selfridge/blob/main/Data/t_up_to_200.txt)
- [Greedy algorithm lower bounds on t(N) for N between 80 and 599](https://github.com/teorth/erdos-guy-selfridge/blob/main/Data/tbounds.txt).
- [Examples and linear programming certificates for N up to 600](https://github.com/teorth/erdos-guy-selfridge/tree/main/Data/oeis_results) (explained [here](https://github.com/teorth/erdos-guy-selfridge/pull/1))
- [Values of t(N) for N up to 600](https://github.com/teorth/erdos-guy-selfridge/blob/main/Data/t_up_to_600.txt)
- [Values of t(N) for N up to 10000](https://github.com/teorth/erdos-guy-selfridge/blob/main/Data/a034258-lpsolve.txt) - value at $t(9633)$ is currently only a lower bound, all other values verified to be exact.
- [A factorization verifying t(41006) >= 13669](https://github.com/teorth/erdos-guy-selfridge/blob/main/Data/FC_41006.txt) - the first large positive case of Conjecture 2
- [A factorization verifying t(43632) >= 14545](https://github.com/teorth/erdos-guy-selfridge/blob/main/Data/factorizations/43632-43632-14545.txt) - believed to be the first point where Conjecture 2 becomes true for this and all larger values of $N$
- [Upper and lower bounds for t(N) for randomly sampled N between 10^3 and 10^5](https://github.com/teorth/erdos-guy-selfridge/blob/main/Data/t_large_n_bounds.txt)



## Additional links

- [Instructions for contributors](CONTRIBUTING.md)
- "[Decomposing a factorial into large factors](https://terrytao.wordpress.com/2025/03/26/decomposing-a-factorial-into-large-factors/)", blog post, Terence Tao, 26 March 2025.
- [Decomposing a factorial into large factors](https://arxiv.org/abs/2503.20170), arXiv preprint v2, Terence Tao, 28 March 2025.
- [Notes on criteria for bounding t(N)](https://github.com/teorth/erdos-guy-selfridge/blob/main/LaTeX/notes.pdf)



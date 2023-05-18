---
layout: post
---

*Disclaimer: This page requires a browser that supports [MathML](https://developer.mozilla.org/en-US/docs/Web/MathML#browser_compatibility) and fonts that support basic mathematics symbols in order to render correctly.*

After a few mis-hires, one of my former employers attempted to improve their interview processes by means of introducing a whiteboarded, pseudo-code technical component to the interview. Management came up with a few ideas, ranging from the classic [FizzBuzz](https://en.wikipedia.org/wiki/Fizz_buzz), to implementing *any* sorting algorithm, to producing a function that generates the n-th Fibonnacci number. These suggestions were then brought to a few developers on the team (myself included) to solicit inputs. Near unanimously, FizzBuzz was regarded as "too simple". More surprisingly, sorting was seen as potentially "too difficult"; perhaps the candidate would feel pressured to recall a more complex algorithm to impress the interviewers, only to stumble in the implementation details and appear worse as a result. So the consensus seemed to settle around the Fibonacci numbers. I suggested that in an interview, I'd struggle to solve this problem for much the same reasons the sorting algorithm had been rejected. My coworkes looked at me with confusion. 

Once you've seen the truth, it isn't easily forgotten. It sears a place in the memory, like the after-images of bright light in the eye. These truths might fade slowly from concious thought, but return ablaze with the slightest provocation. I'm sure nearly every student who has gone to grade school has seen a textbook with some spiraled shells adorning the cover, and perhaps a sentence inside the book mentioning some relationship to a mysterious sequence called the Fibonnacci numbers. 

Perhaps shortly after these memories begin, she might start to dreamily recall the numbers, $1, 1, 2, 3, 5, 8, 13, 21 \ldots$, before stating the recurrence relation $F_n = F_{n-1} + F_{n-2}$ (for $n>2$). Perhaps she has become a long distance runner in the years between grade-school and today's interview. She notices that a 5k ($F_5$) is approximately 3 ($F_4$) miles long, and that a half marathon (~13 miles, $F_7$) is 21 km ($F_8$). Coincidence? Someone who has spent enough time developing software might question whether it would be more pragmatic to indroduce a term $F_0 = 0$ to the sequence. A student of mathematics however, will likely recall a late night of linear algebra homework, and begin to mutter strang things about eigenvectors, as the lights in the room mysteriously grow dim. 

Let's make some pragmatic definitions, let $F_k$ refer to the k'th Fibonnaci number, let $F_0 = 0$ (since we're secretly not infinitely opposed to the computer science camp), and let $F_1 = 1.$ We temporarily think back to grade-school. $1 = 1+ 0, 2 = 1+1, 3 = 1+2,$ we pause, getting ahead of ourselves...$144=89+55$. We know the pattern. $F_k = f_{k-1} + f_{k-2}$. Now that we're a bit older, and questionably wiser, we recognize this as a two dimensional recurrance, noting that the ordered pair $(F_1, F_0) = (1, 0)$ can be transformed by a linear mapping into $(2, 1) = (F_2, F_1)$, since we have a recurrence in the form of $T(x, y) = (y, x+y)$ Specifically, we can capture this linear fuction by the matrix $M = \begin{bmatrix}1 & 1 \\ 1 & 0 \end{bmatrix}$ This realization should make us curious. Given a new, unfamiliar matrix, we consider the toolbox of operations we could perform on it, perhaps not too dissimilar to a carpenter, holding a collection of tools hungrily over a fresh piece of wood. 

We compute the eigenvalues, $1/2*(1+\sqrt{5})$ and  $1/2*(1-\sqrt{5})$. If you're really observant here, you'll notice that $s = \phi$, the golden ratio, and $t = -\phi^{-1}$, but it's not relevant quite yet. We compute the corresponding eigenvectors, determining that $u = (\phi, 1)$ and $v = (t, 1)$, and we check that we can in fact get the pair $(F_1, F_0)$ as some linear combination of $u$ and $v.$ 

We push the matricies around, and discover that indeed, $(1, 0) = 1/\sqrt{5} u - 1/\sqrt{5} v.$

$$(F_n, F_n-1) = M^n (1, 0) = M^n (1/\sqrt{5} u - 1/\sqrt{5} v)$$
$$= 1/\sqrt{5} M^n u - 1/\sqrt{5} M^n v$$

but since u, v are eigenvalues, we have $= 1/\sqrt{5} s^n u - 1/\sqrt{5} t^n v$ and we only care about the first coordinate (I suppose $F_{n-1}$ is obsolete in these modern times), thus concluding 

$$F_n =  \frac{1}{\sqrt{5}}(1+\frac{\sqrt{5}}{2})^n  - \frac{1}{\sqrt{5}}(1-\frac{\sqrt{5}}{2})^n.$$

Well, this is surprising. I mean, it's not even clear that $F_n$ takes integer values anymore. but we plug in a few test values, noting that (up to floating point considerations, potentially we'll discuss this in a future article) we only get integral results. 

Overall, I think this is a bit too much math to expect someone to remember off the cuff in an interview, and from my co-worker's horrified expressions, they seemed to agree. It's important to know your audience at all times, but sometimes it's also important to rise above expectations and do the right thing. Choosing to wear the right hat on a given day is an important skill. 

Walking away from this, there's a few questions left dangling, potentially to be explored in subsequent articles. If this were a job, these would be great loose ends to tie up, or propose as follow-on tasking. 

 1. Does this out-perform naive implementations? DP-style implementations?
 2. How badly does floating point mess things up? (I'd guess not much, especially for reasonably small terms, perhaps rounding to nearest integer will always be sufficient. 
 3. What is this eigenvalue, why does it seem familiar. (I.E. why is the golden ratio appearing in my spirals? 

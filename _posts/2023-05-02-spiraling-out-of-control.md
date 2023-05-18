---
layout: post
---

*Disclaimer: This page requires a browser that supports [MathML](https://developer.mozilla.org/en-US/docs/Web/MathML#browser_compatibility) and fonts that support basic mathematics symbols in order to render correctly.*

## I

After a few mis-hires, one of my former employers attempted to improve their interview processes by means of introducing a white-boarded, pseudo-code technical component to the interview. Management came up with a few ideas, ranging from the classic [FizzBuzz](https://en.wikipedia.org/wiki/Fizz_buzz), to implementing *any* sorting algorithm, to producing a function that generates the n'th Fibonacci number. These suggestions were then brought to a few developers on the team (myself included) to solicit inputs. Near unanimously, FizzBuzz was regarded as "too simple". More surprisingly, sorting was seen as potentially "too difficult"; perhaps the candidate would feel pressured to recall a more complex algorithm to impress the interviewers, only to stumble in the implementation details and appear worse as a result. So the consensus seemed to settle around the Fibonacci numbers. I suggested that in an interview, I'd struggle to solve this problem for much the same reasons the sorting algorithm had been rejected. My coworkers looked at me with confusion. 

Once you've seen the truth, it isn't easily forgotten. It sears a place in the memory, like the afterimages of bright light in the eye. These truths might fade slowly from conscious thought, but return ablaze with the slightest provocation. I'm sure nearly every student who has gone to grade school has seen a textbook with some spiraled shells adorning the cover, and perhaps a sentence inside the book mentioning some relationship to a mysterious sequence called the Fibonacci numbers. 

Perhaps shortly after these memories begin, she might start to dreamily recall the numbers, $1, 1, 2, 3, 5, 8, 13, 21 \ldots$. Perhaps she has become a long distance runner in the years between grade-school and today's interview. She notices that a 5k is approximately 3 miles long, and that a half marathon (~13 miles) is 21 km. Coincidence? Someone who has spent enough time developing software might question whether it would be more pragmatic to introduce a term $F_0 = 0$ to the sequence. A student of mathematics however, will likely recall a late night of linear algebra homework, and begin to mutter strange things about eigenvectors, as the lights in the room mysteriously grow dim. 

## II

Let's make some pragmatic definitions, let $F_k$ refer to the k'th Fibonacci number, let $F_0 = 0$ (since we're secretly not infinitely opposed to the computer science camp), and let $F_1 = 1.$ We temporarily think back to grade-school. $1 = 1+ 0, 2 = 1+1, 3 = 1+2,$ we pause, getting ahead of ourselves...$144=89+55$. We know the pattern. $F_k = f_{k-1} + f_{k-2}$ (for $k>2$). Now that we're a bit older, and ostensibly wiser, we recognize this as a two dimensional recurrence, noting that the ordered pair $(F_1, F_0) = (1, 0)$ can be transformed by a linear mapping into $(2, 1) = (F_2, F_1)$, and our recurrence takes the form of $T(x, y) = (x+y, x)$ Specifically, we can describe this linear transformation by the matrix $M = \begin{bmatrix}1 & 1 \\ 1 & 0 \end{bmatrix}$. Going a step further, we confirm that $(1, 1) = M (1, 0)$, that $(2, 1) = M (1, 1)$, and following the pattern, (since matrix multiplication is associative) we observe that $(F_n, F_{n-1}) = M^n (1, 0).$ *(Note: we're not being too careful about the distinction between row and column vectors in our notation. You can safely assume all vectors in this post are column vectors.)* This realization should make us curious. The entries in $M^n$ should be all we need to produce the n'th number in the sequence. Could there perhaps be a formula for $M^n$? We recall that unfortunately, exponentiating general matrices isn't the simplest procedure, so we begin to consider alternative solutions. Is there perhaps some basis with respect to which T is a diagonal matrix? We know that for a diagonal matrix, 
$$A = \begin{bmatrix} a & &  \\  & \ddots & \\ & & b \end{bmatrix}, A^n = \begin{bmatrix} a^n & &  \\  & \ddots & \\ & & b^n \end{bmatrix}.$$
If so, we're in luck, so let's attempt to find such a basis. 

Recalling this basis will be formed by eigenvectors (if such a basis exists), we begin computing eigenvalues, which we will later use to find eigenvectors.

$$Tv = \lambda v$$
$$(x+y, x) = (\lambda x, \lambda y)$$

Thus (by substitution)

$$\lambda y + y = \lambda^2 y$$
$$0 = y(\lambda^2 - \lambda - 1)$$

We're not particularly interested in cases where $y=0$, so we will instead look for the roots of $\lambda^2 - \lambda - 1$, which happen to be $\frac{1+\sqrt{5}}{2}$ and  $\frac{1-\sqrt{5}}{2}$ (our eigenvalues). If you're really observant you'll notice that these are $\phi$ and $-\phi^{-1}$ where $\phi$ is the golden ratio, but it's not relevant quite yet. We compute the corresponding eigenvectors next.

$$(x+y, x) = (\lambda x, \lambda y)$$
And letting $\phi = \lambda$,
$$(x+y, x) = (\phi x, \phi y)$$
$$y = \phi x - \phi y$$
$$y = \frac{\phi^2}{1+\phi}$$
which allows us to conclude $y=1$, and thus $x = \phi$, so our eigenvector $u = (\phi, 1)$ corresponds to the eigenvalue $\phi$. Following an identical process for our second eigenvalue ($-\phi^{-1}$), we have a second eigenvector $v = (-\phi^{-1}, 1)$.

Eigenbasis (i.e. a basis of eigenvectors; showing this does in fact form a basis is beyond the scope of this post)in hand, we should be able to write our first Fibonacci number (or vector in this case) as a linear combination of the eigenbasis. Verily, $(1, 0) = \frac{u}{\sqrt{5}} - \frac{v}{\sqrt{5}}$. 

Therefore,

$$(F_{n}, F_{n-1}) = M^n (1, 0) =  \frac{\phi^n}{\sqrt{5}}u - \frac{(-\phi)^{-n}}{\sqrt{5}}v.$$

We're only in the business of knowing $F_n$, so we can omit the interaction with $F_{n-1}$ in the above formula, finding

$$F_n =  \frac{1}{\sqrt{5}}(\frac{1+\sqrt{5}}{2})^n  - \frac{1}{\sqrt{5}}(\frac{1-\sqrt{5}}{2})^n.$$

## III

Well, this is surprising. I mean, it's not even clear that $F_n$ takes integer values anymore. but we plug in a few test values, noting that (up to floating point considerations, potentially we'll discuss this in a future article) we only get integral results. (Not to mention that the underlying theory is sound, so the only room for error here is in our execution.) 

Overall, I think this is a bit too much math to expect someone to remember off the cuff in an interview, and from my coworker's horrified expressions, they seemed to agree. It's important to know your audience, but sometimes it's also important to rise above expectations and do the right thing. Choosing to wear the right hat on a given day is an important skill, but sometimes people's skills and backgrounds cause them to look at problems in a manner that differs wildly from what we'd expect. 

Walking away from this, there's a few questions left dangling, potentially to be explored in subsequent articles. If this were a job, these would be great loose ends to tie up, or propose as followup tasking. 

 1. Does this outperform naive implementations? DP-style implementations?
 2. How badly does floating point mess things up? (I'd guess not much, especially for reasonably small terms, perhaps rounding to nearest integer will always be sufficient. 
 3. What is this eigenvalue, why does it seem familiar. (I.E. why is the golden ratio appearing in my spirals? 

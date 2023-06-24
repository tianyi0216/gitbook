# GCD Algorithm Proof

```
// Original Algorithm
BINARYGCD(x,y):
    if x = y: # case 1
        return x
    else if x and y are both even: # case 2
        return 2*BINARYGCD(x/2,y/2)
    else if x is even: # case 3
        return BINARYGCD(x/2,y)
    else if y is even: # case 3
        return BINARYGCD(x,y/2)
    else if x > y: # case 4
        return BINARYGCD( (x-y)/2,y )
    else: # case 4
        return BINARYGCD( x, (y-x)/2 )
```

Since both $$x$$ and $$y$$ are integers, we can use proof by strong induction on $$x$$ and $$y$$.

So we prove by strong induction.&#x20;

Base case: if $$x = y = 1$$, then BINARYGCD(1, 1) return 1. So true for base case.

Inductive case: Assume BINARYGCD works for all $$x_0 \leq x$$ and $$y_0 \leq y$$. We now show it works for $$x$$ and $$y$$.

We can divide into 4 cases.

Case 1: if $$x = y$$, then it is trivial that their GCD is themselve.

Case 2: if both $$x$$ and $$y$$ are even, then both can divide by 2. So we can reduce the problem by factor out of 2 from $$x$$ and $$y$$, (2 is a common divisor) and multiply 2 back from the solution of the redduced problem.

Case 3: if one is even the another is odd, then we can divide 2 from the even number without affecting the GCD, since 2 is not a divisor for the odd number.

Case 4: if both is odd. WLOG assume $$x > y$$. Then, we can subtract y from x, let $$z = x - y$$. \*We claim that gcd between $$z$$ and $$y$$ is the same as GCD(x, y). Since $$z$$ is even (odd- odd = even), we can further divide $$z$$ by 2 (case 3). So gcd((x-y)/2 , y) is the same as gcd(x, y).&#x20;

Proof of \*:

Let $$d$$ denote the gcd between $$x, y$$. We know $$d | x$$ and $$d|y$$. So $$x = ad$$ and $$y=bd$$ for some $$a, b \in \mathbb{Z}, a>b$$. So $$x-y =z= (a-b)d, (a-b) \in \mathbb{Z}$$. So $$d|z$$. Since $$z < x$$ and $$d|z$$, gcd between $$z$$ and $$y$$ is $$d.$$

The runtime is $$O(log(x) + log(y))$$ In worst case, it would be just divide 2 for both x and y.

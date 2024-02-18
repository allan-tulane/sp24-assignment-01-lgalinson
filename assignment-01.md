

# CMPS 2200 Assignment 1

**Name: Lakeland Galinson**


In this assignment, you will learn more about asymptotic notation, parallelism, functional languages, and algorithmic cost models. As in the recitation, some of your answer will go here and some will go in `main.py`. You are welcome to edit this `assignment-01.md` file directly, or print and fill in by hand. If you do the latter, please scan to a file `assignment-01.pdf` and push to your github repository. 

1. (2 pts ea) **Asymptotic notation** (12 pts)

  - 1a. Is $2^{n+1} \in O(2^n)$? Why or why not? 

Yes, $2^{n+1} \in O(2^n)$

a function $f(n)$ ($2^{n+1}$) is in $O(g(n))$ ($O(2^n)$) if there is a constant $c > 0$ such that $f(n) \le c \cdot g(n)$.

Since $2^{n+1} = 2 \cdot 2^n$

So if we chose $c=2$,

$2 \cdot 2^n \le 2 \cdot 2^n $

This is true for all $n$, so $2^{n+1} \in O(2^n)$


  - 1b. Is $2^{2^n} \in O(2^n)$? Why or why not?     

No, $2^{2^n} \not\in O(2^n)$ 

This is because $2^{2^n}$ grows significantly faster than $2^n$ and there is no constant c for which $2^{2^n} \le c \cdot 2^n$

Thus, $2^{2^n} \not\in O(2^n)$ 

  - 1c. Is $n^{1.01} \in O(\mathrm{log}^2 n)$?    

No, $n^{1.01} \not\in O(\mathrm{log}^2 n)$

This is because $n^{1.01}$ is a polynomial function, which is always faster than $O(\mathrm{log}^2 n)$, a logarithmic function. no matter how large a constant $c$ you choose, there will be an n large enough that $n^{1.01}$ is larger than $c \cdot \mathrm{log}^2 n$

Thus, $n^{1.01} \not\in O(\mathrm{log}^2 n)$

  - 1d. Is $n^{1.01} \in \Omega(\mathrm{log}^2 n)$?  

Yes, $n^{1.01} \in \Omega(\mathrm{log}^2 n)$

This is because $n^{1.01}$ grows faster than $\mathrm{log}^2 n$. In order for a function to be $\in \Omega(g(n))$, the function has to grow faster or as fast as $g(n)$. In this case, $g(n) = \mathrm{log}^2 n$.

Thus, 
$n^{1.01} \in \Omega(\mathrm{log}^2 n)$

  - 1e. Is $\sqrt{n} \in O((\mathrm{log} n)^3)$?  

No, $\sqrt{n} \not\in O((\mathrm{log} n)^3)$

This is because $\sqrt{n}$ is a square root function, which is always faster than $(\mathrm{log} n)^3$, a cubic logarithmic function. no matter how large a constant $c$ you choose, there will be an n large enough that $\sqrt{n}$ is larger than $c \cdot (\mathrm{log} n)^3$

  - 1f. Is $\sqrt{n} \in \Omega((\mathrm{log} n)^3)$?  

Yes, $\sqrt{n} \in \Omega((\mathrm{log} n)^3)$

This is because $\sqrt{n}$ grows faster than $(\mathrm{log} n)^3$. In order for a function to be $\in \Omega(g(n))$, the function has to grow faster or as fast as $g(n)$. In this case, $g(n) = (\mathrm{log} n)^3$.


2. **SPARC to Python** (12 pts)

Consider the following SPARC code of the Fibonacci sequence, which is the series of numbers where each number is the sum of the two preceding numbers. For example, 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610 ... 
$$
\begin{array}{l}
\mathit{foo}~x =   \\
~~~~\texttt{if}{}~~x \le 1~~\texttt{then}{}\\
~~~~~~~~x\\   
~~~~\texttt{else}\\
~~~~~~~~\texttt{let}{}~~(ra, rb) = (\mathit{foo}~(x-1))~~,~~(\mathit{foo}~(x-2))~~\texttt{in}{}\\  
~~~~~~~~~~~~ra + rb\\  
~~~~~~~~\texttt{end}{}.\\
\end{array}
$$ 

  - 2a. (6 pts) Translate this to Python code -- fill in the `def foo` method in `main.py`  

  - 2b. (6 pts) What does this function do, in your own words?  

The function foo(x) finds the Fibbonacci number at index `x`.
The function checks if `x` is one or zero (base cases). If it is greater than one, the function calls itself to find the two pervious numbers in the sequence and then returns the sum of the two numbers.

3. **Parallelism and recursion** (26 pts)

Consider the following function:  

```python
def longest_run(myarray, key)
   """
    Input:
      `myarray`: a list of ints
      `key`: an int
    Return:
      the longest continuous sequence of `key` in `myarray`
   """
```
E.g., `longest_run([2,12,12,8,12,12,12,0,12,1], 12) == 3`  
 
  - 3a. (7 pts) First, implement an iterative, sequential version of `longest_run` in `main.py`.  

  - 3b. (4 pts) What is the Work and Span of this implementation?  

. The *longest_run* function consists of a single loop that iterates over all elements in the input list only once. 

. During each iteration, the operations performed are constant time operations, including comparisons, arithmetic operations, and variable assignments

. Therefore, if the input list has $n$ elements, the function performs a constant amount of work for each element, leading to a total work of $O(n)$.


  - 3c. (7 pts) Next, implement a `longest_run_recursive`, a recursive, divide and conquer implementation. This is analogous to our implementation of `sum_list_recursive`. To do so, you will need to think about how to combine partial solutions from each recursive call. Make use of the provided class `Result`.   

  - 3d. (4 pts) What is the Work and Span of this sequential algorithm?  

**Work:**
Given a list of size $n$, the recursion tree will have a height of $log(n)$, where each level splits the list and then combines the results from the two halves. 

At each level, the total work done across all nodes is 
$O(n)$ because each element is involved in a constant amount of work for comparison and combining results. Therefore, the total work done by the algorithm is the sum of work done at each level or:

 $W(n) = O(nlogn)$

 **Span:**
 The span is governed by the depth of the recursion tree.

At each level of recursion, the list is divided in half, leading to a recursion tree of depth $log(n)$. Each recursive call is dependent on the completion of the previous calls in its path (need the results from both halves to combine them), leading to a span that is proportional to the depth of the recursion tree. Span:

$S(n) = O(logn)$

  - 3e. (4 pts) Assume that we parallelize in a similar way we did with `sum_list_recursive`. That is, each recursive call spawns a new thread. What is the Work and Span of this algorithm?  

**Work** will remain the same because the total amount of computation does not change when we parrallelize. Each element in the array is still processed a fixed number of times as the array is divided and the results are combined.

**Span:** The Span now depends on the depth of the recursion tree rather than the work at each level. Each recursive division effectively halves the problem size, and since both halves can be processed in parallel, the Span is dictated by the number of divisions needed to reduce the problem to its base case, which is $S(n) = O(logn)$, the depth of the tree.





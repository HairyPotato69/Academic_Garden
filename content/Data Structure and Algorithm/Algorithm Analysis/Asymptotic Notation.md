---
title: Asymptotic Notation
draft: false
tags:
  - Notes
  - Algorithm-Analysis
description:
---
# Algorithm Analysis
How do we measure the time complexity for multiple algorithms objectively? When we run the same algorithm on different machines, the time taken would differ due to the variance in specifications.<br>
But, let's start with *why*? 

**Reasons**
1. Determine the complexity of an algorithm in terms of input size, N
2. Abstract the efficiency of an algorithm regardless of the machine that it runs on
3. Examine the basic computer steps of the code

To examine whether an algorithm is efficient, the performance of the algorithm is observed in 3 scenarios:
1. Worst-case
2. Average-case
3. Best-case

*Does the .5 seconds matter?* <br>
Yes and no. In theory, the $0.5$ seconds is irrelevant as it would be diminished by the $1000$ seconds that came before it. However, in real-life, the $0.5$ seconds can mean life or death, or whether you get the thing you coveted the most. Regardless, since algorithm analysis is theoretical, the $0.5$ seconds is irrelevant.  

Take $n^2 + n$ for example. When the value of n is $4$, $n$ is still relevant; however, when the value of n scales to extremely large, say, one thousand, $n$ is diminished by $n^2$ and is no longer relevant. Because of this, in algorithm analysis, the *constants* and any lower order terms will be ignored. 

1. Constants are ignored
	- $5n -> O(n)$
2. Certain terms dominate others
	- $O(1) < O(logn)<O(n)<O(nlogn)<O(n^2)<O(2^n)<O(n!)$
# Asymptotic Notations
## Big O notation, $O$
*Formula based definition*
$$
\begin{align}
g(n) \in f(n) \\ 
\exists C \cdot \exists n_0 \cdot \forall n > n_0\\ 
g(n) \leq C\cdot f(n)\;
\end{align}
$$
*What does this mean?*<br>
There exist a constant, $c$, and $x_0$ such that $g(x)$ is $\leq$ $f(x)$

Big Oh notation measures the worst case scenario in an algorithm. 
Examples of worst-case scenario would be:
1. The data structure is completely unsorted.
2. The item to be located is at the end of the array.
3. The pivot value chosen is the largest or smallest in the data structure.
4. The value to be located is absent.

*A formula based example*

$f(n) = 4n^2+16n+2$
$\text{Is }f(n) \in O(n^4) \quad \text{?} \qquad \text{side note: this is not tight enough}$

$4n^2+16n+2 \leq (1)\cdot n^4$?
Yes. 

*Assuming C is 1*

| n   | $4n^2+16n+2$ | $n^4$ | $\leq$  |
| --- | ------------ | ----- | ------- |
| 1   | 22           | 1     | `False` |
| 2   | 50           | 16    | `False` |
| 3   | 86           | 54    | `False` |
| 4   | 130          | 256   | `True`  |

Given that C is 1, $g(n)$ will be $\leq f(x)$ when $n$ exceeds 3. So, $f(n) \in O(n^4)$ is `True`.
## Omega notation, $\omega$
*Formula based definition*
$$
\begin{align}
g(n) \in O(f(n)) \\ 
\exists C \cdot \exists n_0 \cdot \forall n > n_0\\ 
g(n) \geq C\cdot f(n) \\
\end{align}
$$
*What does this mean?*

There exist a constant, $c$, and $x_0$ such that $g(x)$ is $\geq$ $f(x)$

*What's the difference with the one above?*

$\omega$ notation is used to represents the best case scenario in an algorithm.

Examples of best-case scenario is:
1. The item to be located, deleted, or changed is the first item in the data structure.
2. The data structure is already arranged in ascending or descending order.

*A formula based example*

$f(n) = 4n^2+16n+2$

$\text{Is }f(n) = \omega(n^2) ?$

$4n^2+16n+2 \geq (1)\cdot n^2$?

Yes. 

| n   | $4n^2+16n+2$ | $n^2$ | $\geq$ |
| --- | ------------ | ----- | ------ |
| 1   | 22           | 1     | `True` |
| 2   | 50           | 4     | `True` |
| 3   | 86           | 9     | `True` |
| 4   | 130          | 16    | `True` |

Given that C is 1, $f(n)$ will be $\leq g(x)$ with any n value. So, $f(n) = \omega(n^2)$ is `True`.

$f(n) = 4n^2+16n+2$

$\text{Is }f(n) \in \omega(n^3) ?$

$4n^2+16n+2 \geq (C)\cdot n^3$?

This will always be false. Cubic power will always overpower square power. 

So, $f(n) \notin \omega(n^3)$
## Theta notation, $\theta$
*Formula based definition*
$$
\begin{align}
g(n) \in \theta(f(n)) \\ 
\exists n_0 \cdot \exists C_1, C_2 \cdot \forall n>n_0\\ 
C_1\times f(n) \leq g(n) \leq C_2 \times f(n) \\
\text{It is basically, } \\
g(n) \in O(f(n)) \\
g(n) \in \omega(f(n))\\
\end{align}
$$
*What does this mean?*

There exist a constant, $c$, and $x_0$ such that $g(x)$ is between $O(f(n))$ and $\omega(f(n))$. In other words, it is the average case. 

It can also be seen as when Big O notation and $\omega$ notation is equivalent.

*Example*

Assuming $f(n) = 4n^2 + 16n + 2$

Is $f(n) \in \theta(n^2)$

In order for this to be true, $f(n)$ has to be $\in O(n^2)$ and $\in\omega(n^2)$. This also means that $g(n)$ has to be $\leq C \cdot n^2$ and $\geq C \cdot n^2$. 

*How do we prove this?*

$f(n) \in \omega(n^2)$

Assuming C is 1,

| n   | $4n^2+16n+2$ | $n^2$ | $\geq$ |
| --- | ------------ | ----- | ------ |
| 1   | 22           | 1     | `True` |
| 2   | 50           | 4     | `True` |
| 3   | 86           | 9     | `True` |
| 4   | 130          | 16    | `True` |

$f(n)\in O(n^2)$

Assuming C is 1,

| n   | $4n^2+16n+2$ | $n^2$ | $\leq$  |
| --- | ------------ | ----- | ------- |
| 1   | 22           | 1     | `False` |
| 2   | 50           | 4     | `False` |
| 3   | 86           | 9     | `False` |
| 4   | 130          | 16    | `False` |

$4n^2 + 16n + 2 \leq (n^2)$ will never be true with any value of C lesser than 5.

Assuming C is 5,

| n   | $4n^2+16n+2$ | $5n^2$ | $\leq$  |
| --- | ------------ | ------ | ------- |
| 1   | 22           | 5      | `False` |
| 2   | 50           | 20     | `False` |
| 3   | 86           | 45     | `False` |
| 4   | 130          | 80     | `False` |
| 5   | 182          | 125    | `False` |
| .   | .            | .      | .       |
| .   | .            | .      | .       |
| 17  | 1430         | 1445   | `True`  |

$C = 5$ and $n_0 = 17$

$4n^2 + 16n + 2 \leq (n^2)$ is true with any value C greater than 5 and $n_0 = 17$.  

So, $4n^2 + 16n + 2 \in O(n^2)$ is True.
## So, what does any of this mean?
![[content/Data Structure and Algorithm/Algorithm Analysis/Images/graph.png|500]]

This means that at some point (*a value*),  $4n^2 + 16n + 2$ will be lesser than $5n^2$ until infinity. When we say some function, $T(n)$, in this case, $4n^2 + 16n + 2$, as the value of $n$ grows to infinity, $4n^2$ will take up majority of the value. $16n+2$ will become irrelevant to the equation. $4n^2$ will dominate the term. 

If we said the function $\in$ $O(n^2)$, it is not wrong, but the function is also $\in O(n^3)$ or $O(n^4)$ and so on. However, we only want the tightest formula to properly describe an algorithm. Out of all the possible time complexity, we want the smallest one that best fits the equation. In this case, $O(n^2)$. 

*But how are we sure that it is indeed the tightest?*
We show it by finding the $\omega$. If they're both true, it becomes $\theta$. 

*Snippet I: reading length*
```python
x:int = len(cat)
```
The worst case and the best case when reading this string are $O(1)$ are $\omega(1)$ respectively. Since, they're both equal, the average case is $\theta(1)$.

Average cases encompasses how long the algorithm would run most of the time. 

# Runtimes

>[!FAQ] The question is
>As the size of the input increases towards infinity, how does the runtime grow?
>For example:
> - Traversing an array from 1 to 100
> - Traversing a string 
> 	- *cat*
> 	- O(n)

## Linear time
*Example: Traversing through a string*

When you decide to traverse through a string, say, *cat*, from start to finish, the time it would take would be length of the string. In this case, it would be 3. 

*Snippet A: Traversing a string*
```python
cat:str = "Cat"
for i in range(len(n)):
	print(i)
```

This algorithm is said to run at linear time, $O(n)$.
As the number of characters in the string increases, the time taken to iterate through the string increases proportionally. If the length of the string is 5, it would take O(5) time and if it is 6, it would then take O(6) time.

*Snippet B: A mathematical example*
```python
y:int = 15 + (15*20) # O(1)
for x in range(n): # O(N)
	print(f'{x}')
```
The time taken to calculate the value of y is $O(1)$ and `print(f'{x}')` will run $O(n)$ times. 

*Why does `print(f'{x}')` run for $n$ times? Shouldn't it be $O(1)$?*

The time complexity for `print(f'{x}')` is $O(1)$; however, since it is inside a `for` loop it would run as long as the loop.  

The total time is the $O(1) * n$, but since higher order terms dominate, the time complexity turns into $O(n)$.

## Constant time, $O(1)$
*Example: Storing the length of the string in a variable*

What if linear time isn't fast enough? *It already is very good, but let's assume otherwise in this example.*

What the user can do is to store the length of the string in a variable.

*Snippet C: Storing length of cat*
```python
word:str = "cat"
length:int = len(str)
for i in range(length):
	print(f'{word[i]}')
```

All the user have to do now is to check the integer value in the variable. The runtime would be just *1*. So no matter how many characters the string has, the runtime will still be $O(1)$. It does not matter if the size of the inputs changes, the runtime is still constant time. 

*A mathematical example*
$$
f(n)=5+(15*20) = O(1)
$$
Since the product is a constant, it will be reduced to $O(1)$ regardless of its value

*Snippet D : Another mathematical example*
```python
x:int = 5 + (15*20); #O(1)
y:int = 15-2; #O(1)
print(f'{x + y}') # O(1)
```
The total time is $3*O(1)$; however, *constants are ignored,* so, the actual time complexity would be $O(1)$

## Logarithmic algorithms
*Example: Binary search*
>[!WARNING] 
>Insert Binary Tree

*Snippet E: Iterative method*
```python
def BinarySearch(arr:list[int], key:int, left:int, right:int)->bool:
	while(left<=right):
		middle:int = left + (right-left) // 2
		if arr[middle] == key:
			return True
		elif (arr[middle] > key):
			right = middle-1
		else:
			left = middle+1
	return false
```

*Snippet F: Recursive method*
```python
def BinarySearch(arr:list[int], key:int, left:int, right:int) ->bool:
	if (left <= right):
		middle:int = left + (right-left) // 2
		if arr[middle] == key:
			return True
		elif arr[middle] > key:
			return BinarySearch(arr, key, left, middle-1)
		else:
			return BinarySearch(arr, key, middle+1, right)
	return 0
```

Binary search starts in the middle of a **sorted list** and decide if the value is larger or smaller than the target value. It then breaks the list into smaller lists and repeats the process until the value is found. Because of this, the size of the array is being divided by 2 in each iteration/recursion. This means the time complexity of binary search is $\log_2 n$. 

Other examples of this is searching in a Binary Search Tree or AVL tree.

>[!WARNING]
>N-ary trees do not have this time complexity as the number of children varies in each subtree present in the tree.

## Other Runtimes
$O(N^2)$ 
- one of the slowest runtime 
- is found in bubble sort, in its average or worst case scenario. Selection sort also has $O(n^2)$ time complexity in each of its scenario. Quick sort has $O(n^2)$ only in its worst case scenario - choosing the largest or smallest value as its pivot. 

*Snippet G: Quadratic time complexity*
```python
for x in range(n): # O(n)
	for y in range(n): # O(n)
		print(f'{x * y}') # O(1)
```
The inner `for` loop will run for `n` times and the `print(f'{x*y}')` will also run for `n` times. Thus, the time complexity is $O(n) \times O(n) =$ $O(n^2)$. However, IF the range of the inner loop is `m`, the time complexity will be $O(n\times m)$ 

*Snippet H: Ignoring time*

```python
def Foo()->None:
	y:int = 15 + (15*20) # O(1)
	for x in range(n): # O(N)
		print(f'{x}')
	for x in range(n): # O(N^2)
		for y in range(n): 
			print(f'{x * y}') 
```
*What is the time complexity of this function?*

# Solving Asymptotic Notations
## Proving statements
### Question I
Prove $200n^2 + 7n = O(n^2)$
$\exists C  = 201 \cdot \exists n_0 = 7 \cdot \forall n > n_0 \cdot 200n^2+7n \leq cn^2$
Prove
$$
\begin{align}
201n^2 < cn^2 \\
200n^2 + n^2 < cn^2 \\
200n^2 + n < cn^2 \\
200n^2 + 7n < cn^2
\end{align}
$$
$\exists C  = 207 \cdot \exists n_0 = 1 \cdot \forall n > n_0 \cdot 200n^2+7n \leq cn^2$

**Rough work**
$$
\begin{align}
200n^2 + 7n < cn^2 \\
200n^2 - cn^2 < -7n \\
n^2(200-c) < -7n \\
n(200 - c) < -7 \\
n < \frac{-7}{(200-c)}
\end{align}
$$
let $c = 207$ and $n_0$ is now 1
$$
\begin{align}
n \leq 1 \\
1 \leq n \\
n \leq n^2 \\
7n \leq 7n^2 \\
207n \leq 207n^2 \\
200n + 7n \leq 207n^2 \\
200^2 + 7n \leq cn^2
\end{align}
$$
### Question II
Prove $2n = O(n^{1.2})$

$\exists C  = 2 \cdot \exists n_0 = 1 \cdot \forall n > n_0 \cdot 2n \leq cn^{1.2}$
$$
\begin{align}
n\geq 1 \\
1 \leq n \\
n \leq n^2 \\
2n \leq 2n^2 \\
2n \leq 2n^{1.2} \\
2n \leq cn^{1.2}
\end{align}
$$
### Question III
Prove $\forall c \cdot \exists n_0 \cdot \forall n>n_0 \cdot 2^{3n} < c(n!)$

$\forall c \cdot \exists n_0 = \max(\frac{8^8}{7!c}, 8^8)\cdot \forall n>n_0 \cdot 2^{3n} < c(n!)$
$$ 
\begin{align}
\text{take } n &> \frac{8^8}{(7!)(c)} \\
& cn (7!) > 8^8 \\
&8^8 < cn(7!) \\
&8^8(8^{n-8}) < cn(7!)(8^{n-8}) \\
&8^n < cn(7!)(8)(9)(10)...(n-1) \\
&8^n < cn!
\end{align}
$$
### Question IV
Prove $\forall c \cdot \exists n_0 \cdot \forall n > n_0 \cdot n^{10,000} < cn!$

$\forall c \cdot \exists n_0  = \max(\lceil \frac{1}{2}\rceil, 20,001) + 1\cdot \forall n > n_0 \cdot n^{10000} < cn!$

Since $n>\lceil \frac{1}{c}\rceil +1$
$$
\begin{align}
n &>\frac{1}{c} \\
& cn > 1 \text{ and } k(n-k+1) > n \text{ for } k = 2,3,4,...,n-1 \\
&\text{Since } n > 20,001; \quad 2(n-1) \geq n, 3(n-2) \geq n,..., 10,001(n-10,000) \\
& \text{Therefore, } \\
& n^{10,000} < (cn)(2(n-1))(3(n-2))...(10,000(n-9999))(10,001(n-10,000))\\
& n^{10,000} < (1)(2)(3)...(10,000)(10,001)(n-10,000)...(n-2)(n-1)(n) \\
& n^{10,000} < c(1)(2)(3)...(10,000)(10,001)[10,002...(n-10,001)]...(n-10,000)\\
& \qquad \quad \;\;\;(n-2)(n-1)(n) \\
& n^{10,000} < cn!
\end{align}
$$
## Negations
Prove $2^{2n} \neq O(2^n)$, using the definition of Big-Oh.
Definition of Big-Oh
$$
\exists C \cdot \exists n_0 \cdot \forall c > n_0 \cdot 2^{2n} \leq c2^n
$$
Negation of Big-Oh
$$
\begin{align}
\neg[\exists C \cdot \exists n_0 \cdot \forall n > n_0 \cdot 2^{2n}\leq c2^n] \\
\forall C \cdot \forall n_0 \cdot \exists n = \max(\lceil \lg c\rceil,n_0) \cdot 2^{2n} > c2^n \\
\end{align}
$$
**Prove**
$$
\begin{align}
2^{2n} > c2^n \\
(2^n)^2 > c2^n \\
2^n > c \\
n \log 2 > \log c \\
n > \log c
\end{align}
$$
---
layout: post
title: General methods to calculate sum  
header-includes:
    - \usepackage{amsmath}
tags: [concrete_mathematics,sum]
comments: true
---
In the last post, I have introduced the notion of sums, include its notations, how to manipulate sums, and sums with multiple indices. In this post, the second post in a 4-post series relating to sum, I will show you some general methods to find the closed form of a sum. This post is based on chapter 2 of the book *Concrete Mathematics* by Donald Knuth. 
## 1. Induction
Induction is one of the simplest way to find the closed form of a sum. Actually, we have to guess the closed form and then use induction to prove that our guess is correct. Consider the example  
$$
\begin{align}
S_n = 1^3+2^3+...+n^3
\end{align}
$$  
First, let's see if we can find the closed form of this sum by trying with some small values of $$n$$.  
$$
S_1=1 \\
S_2=1^3+2^3=9=3^2 \\
S_3=1^3+2^3+3^3=36=6^2 \\
S_4=1^3+2^3+3^3+4^3=100=10^2 \\
S_5=1^3+2^3+3^3+4^3+5^3=225=15^2
$$  
So a reasonable guess may be  
$$
\begin{align}
S_n=(1+2+..+n)^2=\frac{n^2(n+1)^2}{4}
\end{align}
$$  
Now, let's use induction to prove that $$S_n=\frac{n^2(n+1)^2}{4}$$  
First, consider the basic step with $$n=1$$, we have $$S_n=1=\frac{1^22^2}{4}$$.  
For inductive step, assume for the sake of induction that $$S_k=\frac{k^2(k+1)^2}{4}$$, we will prove $$S_{n+1}=\frac{(k+1)^2(k+2)^2}{4}$$.  
Indeed, we have,  
$$
\begin{align}
S_{k+1} &= S_k+(k+1)^3 \\
&= \frac{k^2(k+1)^2}{4}+(k+1)^3 \\
&= (k+1)^2(\frac{k^2}{4}+(k+1)) \\
&= \frac{(k+1)^2(k+2)^2}{4} \square \\
\end{align}
$$  

## 2. Perturb the sum
There is an example of the perturbation method in the last post. Here, we will consider another example.  
$$
S_n = \sum_{k=0}^{n}(-1)^{n-k}
$$  
First, applying *commutative law*, we can rewrite $$S_n$$ as $$\sum_{k=0}^{n}(-1)^{k}$$. Expressing $$S_{n+1}$$ in two ways, we have,    
$$
\begin{align}
S_{n+1} &= S_n + (-1)^{n+1} \\ 
&= 1 + \sum_{k=1}^{n+1}(-1)^{k} \\
&= 1 + \sum_{k+1=1}^{n+1}(-1)^{k+1} \\
&= 1 + -\sum_{k=0}^{n}(-1)^k \\
&= 1 - S_n
\end{align}
$$  
Thus, $$S_n = \frac{1-(-1)^{n+1}}{2}$$. This formula will make a lot of sense if it is expressed in two separate cases when $$n$$ is odd and $$n$$ is even.
$$
S_n = \begin{cases}
1 &\text{n is even} \\
0 &\text{n is odd}
\end{cases}
$$  
Let's apply this result to another sum $$T_n=\sum_{k=0}^{n}(-1)^{n-k}k$$. Take the similar path as before, we will apply the commutative law first to make the sum more approachable.  
$$
\begin{align}
T_n &= \sum_{k=0}^n(-1)^{n-k}k \\
&= \sum_{k=0}^n(-1)^k(n-k) \\
&= n\sum_{k=0}^n(-1)^k - \sum_{k=0}^{n}(-1)^kk \\
\end{align}
$$  
The first sum is equal to $$n\frac{1-(-1)^{n+1}}{2}$$ using the previous formula. The second sum can be solved using the perturbation method.  
$$
\begin{align}
G_{n+1} &= \sum_{k=0}^{n+1}(-1)^kk \\ &= G_n+(n+1)(-1)^{n+1} \\ &= \sum_{k=1}^{n+1}(-1)^kk \\ &= \sum_{k=0}^{n}(-1)^{k+1}(k+1) \\ &= -\sum_{k=0}^{n}(-1)^kk-S_n \\ &= -G_n-S_n
\end{align}
$$  
Thus, 
$$
G_n = \begin{cases}
\frac{n}{2} &\text{n is even} \\
-\frac{n+1}{2} &\text{n is odd}
\end{cases}
$$  
Finally, we can infer that  
$$
T_n = \begin{cases}
\frac{n}{2} &\text{n is even} \\
\frac{n+1}{2} &\text{n is odd}
\end{cases}
$$  
An exercise for the reader, solve the sum $$U_n=\sum_{n=0}^n(-1)^{n-k}k^2$$.

## 3. Replace sums by integral
Consider the following sum $$S_n=\sum_{k=0}^nk^2$$. In calculus, $$\int$$ is interpreted as the area under the curve. This area is calculated as the limit of the sum of thin rectangles that touch the curve. On the other hand, sum of multiple terms can be interpreted as the total area of the rectangles that have one side whose length is equal to the term and the other side has length equal to 1 (as illustrated in the following figure).  
<figure>
  <img src="/img/sum_integral.png" alt="sum_integral"/>
  <figcaption style="text-align: center">Relation between sum and integral. Picture excerpted from *Concrete mathematics* book</figcaption>
</figure>  
Now, we will find the error between the sum of rectangles and the area under the curve. It is the sum of the areas of all the wedge-shaped error terms.  
$$
\begin{align}
S_n-\int_0^nx^2dx &= \sum_{k=1}^n(k^2-\int_{k-1}^kx^2dx)\\
&=\sum_{k=1}^n(k^2-\frac{k^3-(k-1)^3}{2}) \\
&=\sum_{k=1}^n(k-\frac{1}{3})\\
&=\frac{n(n+1)}{2}-\frac{n}{3}\\
\end{align}
$$  
Thus, $$S_n=\frac{2n^3+3n^2+n}{6}=\frac{n(n+1)(2n+1)}{6}$$.

## 4. Expand and contract
In many cases, it is helpful to transform the sum into something that seems to be more convoluted but actually is easier to solve. For example, consider the sum in the last section $$S_n=\sum_{k=1}^n k^2$$. This sum can be rewritten as   
$$
\begin{align}
S_n&=\sum_{1 \le j \le k \le n}k\\
&=\sum_{1 \le j \le n}\sum_{j \le k \le n} k\\
&=\sum_{1 \le j \le n}\frac{(n-j+1)(n+j)}{2}\\
&=\sum_{1 \le j \le n}\frac{n^2+n+j-j^2}{2}\\
&=\frac{n^3}{2}+\frac{n^2}{2}+\frac{n(n+1)}{4}-\frac{S_n}{2}
\end{align}
$$  
From this we can find the closed form of $$S_n$$.  
Now, we will solve a more difficult example $$T_n=\sum_{k=1}{n}k^3$$.  
$$
\begin{align}
T_n+S_n&=\sum_{k=1}^{n}(k^3+k^2)\\
&=\sum_{k=1}^nk^2(k+1)\\
&=2\sum_{1 \le j \le k \le n} jk
\end{align}
$$  
Using the fact that $$\sum_{1 \le j \le k \le n}a_ja_k=\frac{1}{2}((\sum_{k=1}^na_k)^2+\sum_{k=1}^na_k^2)$$, we have  
$$
\begin{align}
2\sum_{1 \le j \le k \le n} jk = (\sum_{k=1}^nk)^2+S_n
\end{align}
$$  
Hence, $$T_n = (\sum_{k=1}^nk)^2$$.

## 4. Use finite calculus
Stay tuned because this will be introduced in the next post.

## Exercises
1. Express $$S_n=\sum_{i=0}^ni^2x^i$$ as a closed-form function of n when $$x \neq 1$$.  
**Solution**  
We will use perturbation method to solve this problem. We have
$$
\begin{align}
S_{n+1}&=S_n+(n+1)^2x^{n+1}\\
&=\sum_{i=1}^{n+1}i^2x^i\\
&=\sum_{i=0}^n(i+1)^2x^{i+1}\\
&=x\sum_{i=0}^n(i^2+2i+1)x^i\\
&=xS_n+2x\sum_{i=0}^nix^i+x\frac{1-x^{n+1}}{1-x}\\
\end{align}
$$  
Now, our remaining job is to find the closed form of $$T_{n}=\sum_{i=0}^nix^i$$. Similarly, we will find the closed form of $$T_n$$ using the perturbation method.  
$$
\begin{align}
T_{n+1}&=T_n+(n+1)x^{n+1}\\
&=\sum_{i=1}^{n+1}ix^i\\
&=\sum_{i=0}^n(i+1)x^{i+1}\\
&=x\sum_{i=0}^n(i+1)x^i\\
&=xT_n+x\frac{1-x^{n+1}}{1-x}\\
\end{align}
$$  
From this, we get the closed form of $$T_n=x\frac{1-x^{n+1}}{(1-x)^2}-\frac{(n+1)x^{n+1}}{1-x}$$. After finding the closed form of $$T_n$$, we get the closed form of $$S_n=\frac{2x}{1-x}T_n+x\frac{1-x^{n+1}}{(1-x)^2}$$.

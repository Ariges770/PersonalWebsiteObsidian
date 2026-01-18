---
draft: false
author: Ari Gestetner
aliases:
tags:
img: Blog/Projects/Packware/attachments/Shipping.png
desc: This is where I document my progress on my work for finding the best shipping prices for Packware
title: Shipping
dateCreated: 28-12-2025
lastModified: 18-01-2026
---

# Shipping
## Q1
If we consider the amount of water added to the larger bucket $v$ as time in an arrival process then all we need to do is substitute $v=t$. Thus the interarrival times is the amount of water added on each draw and the process is counting how many times we add water to the larger bucket.

### (a)
Using this we can find $E[X_{v}] = m(v)$ where $X_{v}$ is the number of draws we performed to draw up to $v=1$ volume. However, since we also need to consider the final draw which means we must find $\mathbb{E}[X_{v}+1]=\mathbb{E}[X_{v}]+1$ by linearity.

Now we can find $E[X_{v}] = m(v) = F(v)+\int_{0}^{v}m(v-s)f(s)ds$ where $v\in[0,1]$ 

Thus we get $m(v)=v+\int_{0}^{v}m(v-s)ds$ since $F(v)=v, v\in[0,1]$ is the CDF of the uniform distribution (same for $f(s)=1$).

Now let $u=v-s \implies du=-ds$

Thus we get

$$
\begin{align*}
m(v)  & = v+\int_{0}^{v}m(v-s)ds  \\
& =v-\int_{v}^{0}m(u)du \\
\implies m(v) &  = v+\int_{0}^{v}m(u)du \\
\implies m'(v) & =1+m(v)+m(0) \\
 & =1+m(v) & \text{Since }m(0)=0 \\
\implies m'(v)-m(v) & =1 \\
\implies \frac{d}{dv}\left( e^{\int_{}^{}-1dv}m(v) \right) & =e^{-v} & \text{Using integrated factor} \\
e^{-v}m(v) & =\int_{}^{}e^{-v}dv \\
 & =-e^{-v}+C \\
m(v) & =-1+\frac{C}{e^{-v}} & \text{Since }m(0)=0, C=1 \\
\therefore m(v) & =e^{v}-1 & \text{For }v\in[0,1]
\end{align*}
$$
Which means $\mathbb{E}[X_{1}+1] = e^{1}-1+1=e$

### (b)
To find $\mathbb{E}[X_{2}+1]=m(2)+1$ we must use the the solution for when $v=1$. Ultimately, we must find 
$$
\begin{align*}
m(v) & =F(v)+\int_{0}^{v}m(v-s)f(s)ds & \text{for } v\in[1,2] \\
\text{since } & f(v) =0\geq 1 \text{ and }F(v)=1, \forall v\geq 1 \\
m(v) & =1+\int_{0}^{1}m(v-s)ds  \\
 & =1+\int_{v}^{v-1}-m(u)du \\
 & =1+\int_{v-1}^{v}m(u)du \\
m'(u) & =m(v)-m(v-1) \\
\text{since } & v-1\in[0,1] \text{ then }m(v-1)=e^{v-1}-1 \\
 & =m(v)-(e^{v}-1) \\
m'(v)-m(v) & =1-e^{v-1} \\
 & \text{ Using integrated factors} \\
\frac{d}{dv}(e^{-v}m(v)) & = e^{-v}-e^{-1} \\
e^{-v}m(v) & =-e^{-v}-ve^{-1}+C \\
m(v) & =-1-ve^{v-1}+Ce^{v} \\
\text{Since } & m(1)=e-1 \\
m(v) & =\frac{e+1}{e}e^{v}-1-ve^{v-1}, v\in[1,2]
\end{align*}
$$
Thus, $m(2)=\frac{e+1}{e}e^{2}-1-ve^{1}=e^{2}-e-1$.
Therefore, $\mathbb{E}[X_{2}+1]=m(2)+1=e^{2}-e$

## Q2
### Classes
All the states form a single recurrence class since every state communicates with state $m+1=6$. Thus $C_{1}=\left\{ 1,2,3,4,5,6 \right\}$ and $C_{1}$ is a recurrent class

### Periodicity
$r_{6,6}(1)=0$ (there are no self loops)
$r_{6,6}(2)>0$ (since state $6$ communicates with all its neighbours)
$r_{6,6}(3)>0$ (if $n\in[1,5]$ is a neighbour state, then we can follow the path $6\to n\to n+1(\text{mod } 5) \to 6$ with positive probability)

However, since $\texttt{gcd}(2,3)=1$ then the class is aperiodic

### Steady state probabilities
Let's consider the the solution to the equations
$$
\mathbf{\pi}=\mathbf{\pi}\begin{bmatrix}
0 & \frac{1}{3} & 0 & 0 & \frac{1}{3} & \frac{1}{3} \\
\frac{1}{3} & 0 & \frac{1}{3} & 0 & 0 & \frac{1}{3} \\
0 & \frac{1}{3} & 0 & \frac{1}{3} & 0 & \frac{1}{3} \\
0 & 0 & \frac{1}{3} & 0 & \frac{1}{3} & \frac{1}{3} \\
\frac{1}{3} & 0 & 0 & \frac{1}{3} & 0 & \frac{1}{3} \\
\frac{1}{5} & \frac{1}{5} & \frac{1}{5} & \frac{1}{5} & \frac{1}{5} & 0
\end{bmatrix}, \sum_{j=1}^{m}\pi _{j}=1
$$
where $\mathbf{\pi}=\left( \pi_{1},\dots \pi_{6} \right)$ 

Using symmetry we can see that $\pi_{1}=\pi_{2}=\pi_{3}=\pi_{4}=\pi_{5}=x$ and $5x+\pi_{6}=1$.
Thus we can easily solve the system that $\mathbf{\pi}=\left(\frac{3}{20}, \frac{3}{20}, \frac{3}{20}, \frac{3}{20}, \frac{3}{20}, \frac{1}{4} \right)$
## Q3
### (a)
#### Transition rates
The transition rates of of $q_{ij}$ are as follows
##### For $i\in[1,m]$ 
The transition rates from any of these states is $\lambda$ and since there is only a single transition from these states they have transition rate $\lambda$
$$
q_{ij}=\begin{cases}
\lambda & \text{if }j=m+1 \\
0 & \text{otherwise}\end{cases}
$$
##### For $i=m+1$
$$
q_{ij}=\begin{cases}
0 & \text{if }j=m+1 \\
\frac{\lambda}{m} & \text{otherwise} 
\end{cases}
$$

Thus we have
$$
Q=\begin{pmatrix}
0 & 0 & \dots & 0 & \lambda \\
0 & 0 & \dots & 0 & \lambda \\
\vdots & \vdots & \ddots & \vdots & \vdots \\
0 & 0 & \dots & 0 & \lambda \\
\frac{\lambda}{m} & \frac{\lambda}{m} & \dots & \frac{\lambda}{m} & 0
\end{pmatrix}
$$

And the rates out of each state is $\lambda$
#### Embedded Chain Transition Matrix
$$
P=\begin{pmatrix}
0 & 0 & \dots & 0 & 1 \\
0 & 0 & \dots & 0 & 1 \\
\vdots & \vdots & \ddots & \vdots & \vdots \\
0 & 0 & \dots & 0 & 1 \\
\frac{1}{m} & \frac{1}{m} & \dots & \frac{1}{m} & 0
\end{pmatrix}
$$

### (b)

### (c)
Let 
$$
A =\begin{pmatrix}
-\lambda & 0 & \dots & 0 & \lambda \\
0 & -\lambda & \dots & 0 & \lambda \\
\vdots & \vdots & \ddots & \vdots & \vdots \\
0 & 0 & \dots & -\lambda & \lambda \\
\frac{\lambda}{m} & \frac{\lambda}{m} & \dots & \frac{\lambda}{m} & -\lambda
\end{pmatrix}
$$
Then the backwards equations are 
$$
P'(t)=AP(t)
$$
Therefore, to solve 

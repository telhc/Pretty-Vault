---
aliases:
  - Transformers
tags:
  - MachineLearning🤖
---
# Attention Is All You Need
Consider length $N$ vector of encodings in $M$ dimensions, ie. $\mathbf{e}_i = \begin{bmatrix}e_{i1}\dots e_{iM}\end{bmatrix}$
$$E_{N\times M} = \begin{bmatrix}\mathbf{e}_1\\\vdots\\\mathbf{e}_N\end{bmatrix}$$
$E$ undergoes 3 linear transformations to form $Q_{N\times d_q}, K_{N\times d_k}, V_{N\times d_v}$, the Query, Key, and Value vector matrices
Notably, head size $d_q=d_k=d_v$


> [!important] Key Formula
> $$\operatorname{Self-Attention}(Q,K,V)_{N\times d_v} = \operatorname{softmax}\left(\frac{Q\cdot K^T}{\sqrt{d_k}}\right)V$$

Denoting $H = \left[\frac{Q\cdot K^T}{\sqrt{d_k}}\right]_{N\times N}$  for explanation
- ⭐ dividing by $\sqrt{d_k}$ for variance preservation to always equal $1$, otherwise variance will always equal head size $d_k$, otherwise softmax will converge to one-hot

$H$ undergoes a [[Softmax]] that ==normalizes ROWS== to sum to $1$
![[Softmax#Softmax Formula]]



> [!example] 
> - If 1 asked how important 2 is (ie. $Q_{1\cdot}\cdot K_{2\cdot}^T = H_{1,2}$)
> - $H_{1,2}$ embodies 2's answer to 1
> - When everyone has answered 1, softmax normalizes everyone's answers. (ie. first row of $H$)
> - Now every row of $\operatorname{softmax}(H)$ has a maximum (soft)
> - Suppose the 1st row's softmax is the 2nd element (ie. 1 pays most attention to 2)
> - Each row of $H$ will choose the most important row of $V$ (ie. $\operatorname{softmax}(H)\cdot V$)
> - So $V_{2\cdot}$, the value vector of 2 will be chosen
> 
> Note: the term "chosen" should be treated loosely, as softmax is still a normalised distribution

___
> [!NOTE] References
> https://arxiv.org/abs/1706.03762
> [Review by Yannic Kilcher](https://www.youtube.com/watch?v=iDulhoQ2pro)
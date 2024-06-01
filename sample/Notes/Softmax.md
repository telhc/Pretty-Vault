#Math📚
# Softmax Formula
$\sigma: \mathbb{R}^K \rightarrow (0,1)^K$
$$\sigma(\mathbf{z})_i = \frac{e^{z_i}}{\sum^K_{j=1}e^{z_j}}$$
where $i=1,\dots,K, \mathbf{z}=\begin{bmatrix}z_1,\dots,z_K\end{bmatrix}\in\mathbb{R}^K$

# Derivative
$$\frac{\partial[\sigma(\mathbf{a})]_i}{\partial a_j} = \frac{\partial}{\partial a_j}\frac{e^{a_i}}{\sum^K_{k=1}e^{a_k}} = \sigma_i(1_{i=j} - \sigma_j)$$
### Proof
By Quotient Rule on $f(x) = \frac{g(x)}{h(x)}$  where $g_i = e^{a_i}, h_i = \sum^K_{k=1}e^{a_k} = \Sigma$
Note
$$\frac{\partial}{\partial a_j}h_i = e^{a_j}$$
and
$$\frac{\partial}{\partial a_j}g_i = \begin{cases} e^{a_i} & i=j \\ 0 & i\neq j \end{cases}$$
Therefore
$$\begin{align*}
\frac{\partial}{\partial a_j}\frac{e^{a_j}}{\sum^K_{k=1}e^{a_k}} &= \frac{g'h - h'g}{h^2}\\
&= \frac{1_{i=j}e^{a_i} \cdot \Sigma - e^{a_j} \cdot e^{a_i}}{\Sigma^2}\\
&= \frac{e^{a_i}}{\Sigma}\frac{1_{i=j}\Sigma - e^{a_j}}{\Sigma}\\
&= \sigma_i(1_{i=j} - \sigma_j)
\end{align*}$$

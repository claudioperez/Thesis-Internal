


## 0) Unknowns and maps

At each integration point $x_i$ (weight $w_i$):

- Basic force vector: $\mathbf{q}\in\mathbb{R}^{n_b}$
- Section deformation vector: $\mathbf{e}_i \in \mathbb{R}^{n_s}$
- Force interpolation: $\mathbf{B}_i := \mathbf{B}(x_i)\in\mathbb{R}^{n_s\times n_b}$
- Interpolated (target) section resultants:
  $$
  \mathbf{s}^h_i(\mathbf{q}) = \mathbf{B}_i\,\mathbf{q} + \mathbf{s}^{p}_i
  $$
  (take $\mathbf{s}^p_i=\mathbf{0}$ if you ignore element loads)
- Constitutive (resisting) section resultants:
  $$
  \mathbf{s}_i(\mathbf{e}_i)
  $$
- Section tangent stiffness:
  $$
  \mathbf{k}_{s,i} := \frac{\partial \mathbf{s}_i}{\partial \mathbf{e}_i}\Big|_{\text{current iterate}}
  $$
- Section tangent flexibility:
  $$
  \mathbf{f}_{s,i} := \mathbf{k}_{s,i}^{-1}
  $$
  (assume invertible for the derivation)

Also define the basic deformation vector (given from the global solve) $\mathbf{v}\in\mathbb{R}^{n_b}$.



## 1) Strong residual statement (the coupled nonlinear equations)

We solve for $\mathbf{q}$ and $\{\mathbf{e}_i\}$ such that:

### (A) Compatibility (exact kinematic constraint)
$$
\mathbf{r}_v(\{\mathbf{e}_i\}) \;:=\; \mathbf{v} \;-\; \sum_{i=1}^{n_{IP}} w_i\,\mathbf{B}_i^{T}\mathbf{e}_i \;=\;\mathbf{0}
\tag{1}
$$

### (B) Section force consistency at every integration point
I’ll write it in the “FF-sign” form (target minus resisting):

$$
\mathbf{r}_{s,i}(\mathbf{q},\mathbf{e}_i)\;:=\;\mathbf{s}^h_i(\mathbf{q}) - \mathbf{s}_i(\mathbf{e}_i)\;=\;\mathbf{0}
\tag{2}
$$

That’s the *strong* residual system: (1) + (2) for all $i$.



## 2) Newton linearization of the residual system

Let the current iterate be $(\mathbf{q},\{\mathbf{e}_i\})$. We seek corrections $(\delta\mathbf{q},\{\delta\mathbf{e}_i\})$ such that the linearized residual vanishes.

### 2.1 Linearize compatibility residual (1)

$$
\mathbf{r}_v(\{\mathbf{e}_i+\delta\mathbf{e}_i\})
\approx
\mathbf{r}_v(\{\mathbf{e}_i\})
-
\sum_i w_i\,\mathbf{B}_i^{T}\delta\mathbf{e}_i
$$

Newton condition: $\mathbf{r}_v + \delta\mathbf{r}_v = \mathbf{0}$, so:

$$
\sum_i w_i\,\mathbf{B}_i^{T}\delta\mathbf{e}_i
=
\mathbf{r}_v(\{\mathbf{e}_i\})
=
\mathbf{v}-\sum_i w_i\,\mathbf{B}_i^T\mathbf{e}_i
\tag{3}
$$

### 2.2 Linearize section residual (2) at each IP

First compute Jacobians:

- $\dfrac{\partial \mathbf{s}^h_i}{\partial \mathbf{q}}=\mathbf{B}_i$
- $\dfrac{\partial \mathbf{s}_i}{\partial \mathbf{e}_i}=\mathbf{k}_{s,i}$

So linearization:

$$
\mathbf{r}_{s,i}(\mathbf{q}+\delta\mathbf{q},\mathbf{e}_i+\delta\mathbf{e}_i)
\approx
\mathbf{r}_{s,i}(\mathbf{q},\mathbf{e}_i)
+
\mathbf{B}_i\,\delta\mathbf{q}
-
\mathbf{k}_{s,i}\,\delta\mathbf{e}_i
$$

Newton condition $\mathbf{r}_{s,i}+\delta\mathbf{r}_{s,i}=\mathbf{0}$ gives:

$$
\mathbf{B}_i\,\delta\mathbf{q} - \mathbf{k}_{s,i}\,\delta\mathbf{e}_i
=
-\mathbf{r}_{s,i}(\mathbf{q},\mathbf{e}_i)
=
-\big(\mathbf{s}^h_i(\mathbf{q})-\mathbf{s}_i(\mathbf{e}_i)\big)
\tag{4}
$$

Solve (4) for $\delta\mathbf{e}_i$:

$$
\mathbf{k}_{s,i}\,\delta\mathbf{e}_i
=
\mathbf{B}_i\,\delta\mathbf{q}
+
\big(\mathbf{s}^h_i(\mathbf{q})-\mathbf{s}_i(\mathbf{e}_i)\big)
$$

$$
\boxed{
\delta\mathbf{e}_i
=
\mathbf{f}_{s,i}\,\mathbf{B}_i\,\delta\mathbf{q}
+
\mathbf{f}_{s,i}\,\big(\mathbf{s}^h_i(\mathbf{q})-\mathbf{s}_i(\mathbf{e}_i)\big)
}
\tag{5}
$$

This is the equation you called out.

Now we can answer your “what is what?” questions precisely:

- **What is $\Delta \mathbf{s}$?**  
  In (5), the term driven by $\delta\mathbf{q}$ is:
  $$
  \Delta\mathbf{s}_i := \mathbf{B}_i\,\delta\mathbf{q}
  $$
  i.e., the *increment in interpolated/target section forces caused by the basic-force correction*.

- **What is $ \mathbf{r}(x)$ (or $\mathbf{r}_i$) exactly?**  
  It is the *Newton deformation correction induced by the current section force residual*, i.e.
  $$
  \boxed{
  \mathbf{r}_i
  :=
  \mathbf{f}_{s,i}\,\big(\mathbf{s}^h_i(\mathbf{q})-\mathbf{s}_i(\mathbf{e}_i)\big)
  }
  \tag{6}
  $$
  No mysticism: it is literally the solution of the *linearized* section equation (4) when $\delta\mathbf{q}=0$.  
  Put differently: it’s the deformation increment that would (to first order) remove the force mismatch at the section.

So if you want the *exact* algebraic identity:
$$
\delta\mathbf{e}_i = \mathbf{f}_{s,i}\,\Delta\mathbf{s}_i + \mathbf{r}_i
$$
with $\Delta\mathbf{s}_i=\mathbf{B}_i\delta\mathbf{q}$, $\mathbf{r}_i$ as in (6).

That’s not “pulled from thin air”; it is (5) obtained by Newton linearization of the **strong residual** (2).


## 3) Eliminate $\delta\mathbf{e}_i$ to get the FF force correction $\delta\mathbf{q}$

Substitute (5) into the linearized compatibility equation (3):

Left-hand side of (3):
$$
\sum_i w_i\,\mathbf{B}_i^{T}\delta\mathbf{e}_i
=
\sum_i w_i\,\mathbf{B}_i^{T}
\Big(
\mathbf{f}_{s,i}\mathbf{B}_i\delta\mathbf{q}
+
\mathbf{f}_{s,i}(\mathbf{s}^h_i-\mathbf{s}_i)
\Big)
$$

Group terms:

$$
\Big(\sum_i w_i\,\mathbf{B}_i^{T}\mathbf{f}_{s,i}\mathbf{B}_i\Big)\delta\mathbf{q}
+
\sum_i w_i\,\mathbf{B}_i^{T}\mathbf{f}_{s,i}(\mathbf{s}^h_i-\mathbf{s}_i)
=
\mathbf{r}_v
\tag{7}
$$

Define the **element tangent flexibility**
$$
\boxed{
\mathbf{F} := \sum_i w_i\,\mathbf{B}_i^{T}\mathbf{f}_{s,i}\mathbf{B}_i
}
\tag{8}
$$

Define the **integrated residual deformation vector**
$$
\boxed{
\mathbf{v}_r := \sum_i w_i\,\mathbf{B}_i^{T}\mathbf{f}_{s,i}(\mathbf{s}^h_i-\mathbf{s}_i)
}
\tag{9}
$$

Then (7) becomes the Newton system reduced to $\delta\mathbf{q}$:

$$
\boxed{
\mathbf{F}\,\delta\mathbf{q} + \mathbf{v}_r = \mathbf{r}_v
}
\tag{10}
$$

So the fully general Newton correction is:
$$
\boxed{
\delta\mathbf{q} = \mathbf{F}^{-1}\Big(\mathbf{r}_v - \mathbf{v}_r\Big)
}
\tag{11}
$$


## 4) The “pure FF” update you asked for

You specifically asked to justify the FF inner-loop update of the form

$$
\delta\mathbf{q} = \mathbf{F}^{-1}\int \mathbf{B}^T\mathbf{f}_s(\mathbf{s}^h-\mathbf{s}(\mathbf{e}))\,dx
$$

From (11), that corresponds to the case where the right-hand side $\mathbf{r}_v$ is taken as zero during the **inner force-correction loop** (because the imposed $\mathbf{v}$ has already been enforced/frozen at that stage).

Setting $\mathbf{r}_v=\mathbf{0}$ in (10):

$$
\mathbf{F}\,\delta\mathbf{q} + \mathbf{v}_r = \mathbf{0}
\quad\Rightarrow\quad
\boxed{
\delta\mathbf{q} = -\mathbf{F}^{-1}\mathbf{v}_r
}
\tag{12}
$$

Expanding $\mathbf{v}_r$ from (9):

$$
\boxed{
\delta\mathbf{q}
=
-\Big(\int_0^L \mathbf{B}^T\mathbf{f}_s\mathbf{B}\,dx\Big)^{-1}
\Big(\int_0^L \mathbf{B}^T\mathbf{f}_s(\mathbf{s}^h-\mathbf{s}(\mathbf{e}))\,dx\Big)
}
\tag{13}
$$

That is exactly the FF update (up to sign convention).

**Sign note:**  
If you instead define the section residual as $\tilde{\mathbf{r}}_{s,i} := \mathbf{s}_i(\mathbf{e}_i)-\mathbf{s}^h_i$ (swap the order), then $\mathbf{v}_r$ flips sign and the update appears without the minus. Your MATLAB code uses `DDq = -f\vr`, i.e. it is consistent with (13) under the residual definition (2).


## 5) Direct correspondence to your FF code lines (so there’s no ambiguity)

At an IP, your code computes:

- $\mathbf{s}^h_i = \mathbf{B}_i\mathbf{q}$  (`s = b*q`)
- $\mathbf{s}_i = \mathbf{s}(\mathbf{e}_i)$  (`sr = SecState.s`)
- $\mathbf{s}^h_i - \mathbf{s}_i$  (`su = s - sr`)
- $\mathbf{r}_i = \mathbf{f}_{s,i}(\mathbf{s}^h_i-\mathbf{s}_i)$  (`er = ks\su`)
- $\mathbf{v}_r = \sum w_i \mathbf{B}_i^T \mathbf{r}_i$  (`vr += b'*er*wIP(i)`)
- $\mathbf{F}=\sum w_i \mathbf{B}_i^T\mathbf{f}_{s,i}\mathbf{B}_i$  (`f += b'*(ks\b)*wIP(i)`)

Then
```matlab
DDq = -f\vr
```
is exactly (12)/(13).


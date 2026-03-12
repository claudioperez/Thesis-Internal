
$$
\newcommand{\FrameBasis}{\mathbf{i}}
\newcommand{\WarpSV}{\varphi}
\newcommand{\WarpFA}{\psi}
\newcommand{\Twist}{\varkappa}
\newcommand{\PlanePosition}{\rho}
\newcommand{\Jv}{J_v}
\newcommand{\Ja}{J_a}
\newcommand{\Jw}{J_w}
$$

### Equilibrium residual: why the correction lives in $\operatorname{span}\{\nabla\WarpSV,\nabla\WarpFA\}$ (and why a free scalar appears)

Start *only* from your kinematics (eq. (26)) and the $z$-equilibrium equation.

#### 1) What equilibrium tests, and what your field feeds into it

From (26), the only pieces that enter the **$z$-equilibrium** are

- shear strain vector on $A$:

  $$
  \gamma
    = \Twist\,(\FrameBasis\times\PlanePosition)
    + \alpha\,\nabla \WarpSV
    + (\Twist-\alpha)\,\bar\eta\big(\nabla\WarpSV + c_{FA}\nabla\WarpFA\big),
    \tag{1}
  $$

- warping normal strain:

  $$\varepsilon_{zz}=\alpha'\,\WarpSV.
  \tag{2}
  $$

With isotropic linear elasticity on the section,

$$\tau = G\,\gamma,\qquad \sigma_{zz}=E\,\varepsilon_{zz}=E\,\alpha'\WarpSV.
\tag{3}
$$

The $z$-component of equilibrium is

$$\partial_x\tau_{xz}+\partial_y\tau_{yz}+\partial_z\sigma_{zz}=0 \quad\text{in }A,
\qquad \tau\cdot n=0\ \text{on }\partial A.
\tag{4}
$$

Testing (4) with any $v\in H^1(A)$ and integrating by parts in $x,y$ (boundary term drops by $\tau\cdot n=0$) gives the **weak sectional equilibrium**

$$\boxed{\int_A G\,\gamma\cdot\nabla v\,dA \;=\; -\int_A \partial_z(E\,\alpha'\WarpSV)\,v\,dA
\qquad\forall v.}
\tag{5}
$$

Since $E$ and $\WarpSV$ depend only on $(x,y)$, $\partial_z(E\alpha'\WarpSV)=E\,\alpha''\,\WarpSV$. Thus the right side is the functional

$$-\alpha''\int_A E\,\WarpSV\,v\,dA.
\tag{6}
$$

So the equilibrium condition is: **the mapping $v\mapsto\int_A G\,\gamma\cdot\nabla v$** must reproduce the mapping $v\mapsto-\alpha''\int_A E\WarpSV v$.

#### 2) The residual has *two* independent functional components

Define $\mathbf g:=\FrameBasis\times\PlanePosition$. Consider first the *unenhanced* shear part

$$\gamma_0 := \Twist\,\mathbf g + \alpha\,\nabla\WarpSV.
\tag{7}
$$

Write

$$\gamma_0 = \Twist(\mathbf g+\nabla\WarpSV) + (\alpha-\Twist)\nabla\WarpSV.
\tag{8}
$$

Now use only the defining Saint–Venant property of $\WarpSV$: it is chosen so that

$$\boxed{\int_A G\,(\mathbf g+\nabla\WarpSV)\cdot\nabla v\,dA = 0\qquad\forall v.}
\tag{9}
$$

Insert (8) into the left side of (5) and apply (9):

$$\int_A G\,\gamma_0\cdot\nabla v
= (\alpha-\Twist)\int_A G\,\nabla\WarpSV\cdot\nabla v.
\tag{10}
$$

Therefore, with $\gamma=\gamma_0$, (5) becomes

$$
\boxed{(\alpha-\Twist)\underbrace{\int_A G\,\nabla\WarpSV\cdot\nabla v}_{=:L_1(v)}
\;+\;\alpha''\underbrace{\int_A E\,\WarpSV\,v}_{=:L_2(v)}
\;=\;0\qquad\forall v.}
\tag{11}
$$

This is the structural content of “torsion‑violation”: the residual is a linear combination of two **a priori independent** continuous linear functionals on $V:=H^1(A)/\mathbb R$:

$$L_1(v)=\int_A G\,\nabla\WarpSV\cdot\nabla v,\qquad
L_2(v)=\int_A E\,\WarpSV\,v.
\tag{12}
$$


#### 4) Why **two gradients**, and why they appear as a **linear combination**

To cancel (11) by adding a *compatible* correction shear field $\delta\gamma=\nabla\psi$, you require

$$
\int_A G\,\nabla\psi\cdot\nabla v
= -(\alpha-\Twist)L_1(v)-\alpha''L_2(v)\quad\forall v.
\tag{15}
$$

Now observe:

- $L_1(\cdot)$ is represented by $\WarpSV$: $L_1(v)=\int_A G\nabla\WarpSV\cdot\nabla v$.
- $L_2(\cdot)$ is represented (in the same operator) by $\WarpFA$ through $\int_A G\nabla\WarpFA\cdot\nabla v = \int_A E\WarpSV v$.

Therefore the unique $\psi\in V$ that satisfies (15) is

$$\psi = -(\alpha-\Twist)\WarpSV - \alpha''\WarpFA \quad(\text{mod constants}),
\tag{16}
$$

and thus

$$
\boxed{\delta\gamma
= -(\alpha-\Twist)\nabla\WarpSV - \alpha''\,\nabla\WarpFA.}
\tag{17}
$$

Thus the residual is a linear combination of two independent functionals $(L_1,L_2)$; the compatible representers of those functionals are $(\nabla\WarpSV,\nabla\WarpFA)$; hence the correcting field must be their linear combination.

#### 5) Why your form has a “free” $c_{FA}$

If you keep (17), there is **no free parameter**: the coefficients are $(\alpha-\Twist)$ and $\alpha''$, fixed by the 1D fields.

Your (26) instead factors the correction as

$$(\Twist-\alpha)\,\bar\eta\,\big(\nabla\WarpSV+c_{FA}\nabla\WarpFA\big).
\tag{18}
$$

This is (17) with two additional constraints imposed simultaneously:

1. **single amplitude** tied to $(\Twist-\alpha)$ (so the correction vanishes when $\Twist=\alpha$), and
2. **localization/orthogonality** via the bubble $\bar\eta$.

Once you collapse the two independent scalars $(\alpha-\Twist)$ and $\alpha''$ into one amplitude, the only way to still represent the 2D residual family (11) is to encode the missing ratio in a scalar:

$$
c_{FA}\ \text{is (up to sign) the effective ratio } \alpha''/(\Twist-\alpha)
\tag{19}
$$

If that ratio is not fixed pointwise by the 1D discretization (or is replaced by an averaged/condensed value), it appears as a “free” constant.

So: **the free parameter is not mandated by equilibrium; it is mandated by the additional modeling choice to factor the correction through $(\Twist-\alpha)\bar\eta$** rather than allowing two independent amplitudes multiplying $\nabla\WarpSV$ and $\nabla\WarpFA$.


**Bottom line:**

- **The “free” $c_{FA}$** is not an equilibrium necessity; it is the bookkeeping of collapsing two scalar amplitudes into one by factoring through $(\Twist-\alpha)\bar\eta$.


**Bridge from eq:torsion-violation to eq:def-enhan-strain.** Decompose the kinematic shear as

$$\hat{\boldsymbol{\gamma}} = \alpha\bigl(\nabla\omega + \mathbf{e}_3\!\times\!\mathbf{r}\bigr) + (\theta'-\alpha)\,\mathbf{e}_3\!\times\!\mathbf{r}.$$

The first term is the SV shear and is cross-sectionally equilibrated (divergence-free in $\Omega$, traction-free on $\partial\Omega$). The second is not: it produces the boundary traction

$$G(\theta'-\alpha)\,(\mathbf{e}_3\!\times\!\mathbf{r})\cdot\mathbf{n}\quad\text{[eq:torsion-violation]}.$$

To cancel this with a gradient field $\nabla\chi$ while preserving the divergence condition, require

$$G(\nabla\chi + \mathbf{e}_3\!\times\!\mathbf{r})\cdot\mathbf{n} = 0\;\text{on }\partial\Omega,\qquad \nabla\!\cdot\!\bigl[G(\nabla\chi + \mathbf{e}_3\!\times\!\mathbf{r})\bigr]=0\;\text{in }\Omega.$$

This is the SV warping BVP, so $\chi = \omega$ (unique up to a constant). Adding $(\theta'\!-\!\alpha)\nabla\omega$ to the kinematic strain converts the shear to $\theta'(\nabla\omega + \mathbf{e}_3\!\times\!\mathbf{r})$—the equilibrated SV form—as visible in your commented-out line 4.

The function $\phi\;(\WarpFA)$ enters as an additional enrichment. It is defined by the flexural-analogy BVP:

$$\nabla\!\cdot\!(G\nabla\phi) + E\,\omega = 0\;\text{in }\Omega,\qquad G\,\tfrac{\partial\phi}{\partial n}=0\;\text{on }\partial\Omega.$$

This field has zero boundary traction (so it does not disturb the fix from $\nabla\omega$) but nonzero divergence $-E\omega$, which gives the enhanced strain the capacity to represent secondary warping shear (the shear flow pattern that balances axial stress gradients $E\alpha''\omega$ from bimoment variation). The combined form, modulated by the axial shape $\bar{\eta}$, is

$$\tilde{\varepsilon} = (\theta'\!-\!\alpha)\,\bar{\eta}\bigl(\nabla\omega + c\,\nabla\phi\bigr)\quad\text{[eq:def-enhan-strain]}.$$

---

**Homogeneous sections:** Yes, the argument holds verbatim. The SV warping satisfies $\nabla^2\omega=0$; the FA warping satisfies $\nabla^2\phi = -(E/G)\,\omega$ with homogeneous Neumann BC. Both problems are well-posed, and $\phi$ is nontrivial whenever $\omega\not\equiv 0$ (i.e., any non-circular section).

**Inhomogeneous sections (variable $E,G$, isotropic):** Also holds. The SV warping now satisfies $\nabla\!\cdot\!(G(\nabla\omega+\mathbf{e}_3\!\times\!\mathbf{r}))=0$ with $G(\nabla\omega+\mathbf{e}_3\!\times\!\mathbf{r})\cdot\mathbf{n}=0$, and the FA warping satisfies $\nabla\!\cdot\!(G\nabla\phi)+E\omega=0$ with $G\,\partial\phi/\partial n=0$. The traction violation remains $G(\theta'\!-\!\alpha)(\mathbf{e}_3\!\times\!\mathbf{r})\cdot\mathbf{n}$ because the SV Neumann condition has the same form regardless of whether $G$ varies. One point worth noting: the kinematic strain now also has a divergence violation $(\theta'\!-\!\alpha)\,\nabla G\cdot(\mathbf{e}_3\!\times\!\mathbf{r})$ in the interior, but the $\nabla\omega$ enhancement cancels this simultaneously (since $\nabla\!\cdot\!(G\nabla\omega) = -\nabla G\cdot(\mathbf{e}_3\!\times\!\mathbf{r})$ by the SV equation). So the derivation goes through identically.

**Uniqueness.** Among gradient-form enhancements $(\theta'\!-\!\alpha)\nabla\chi$: the field $\nabla\omega$ is the unique (modulo constants) one that restores both the traction-free and divergence-free conditions. Any other gradient $\nabla\psi$ preserving both conditions satisfies $\nabla\!\cdot\!(G\nabla\psi)=0$ with $G\,\partial\psi/\partial n=0$—a homogeneous elliptic Neumann problem—forcing $\psi=\text{const}$. The only nontrivial addition is a gradient whose Neumann data vanish but whose divergence is nonzero, which is exactly what the FA problem supplies. So $\nabla\omega + c\,\nabla\phi$ is the most general gradient-based enhancement: $\nabla\omega$ is uniquely determined by equilibrium, $\nabla\phi$ is uniquely determined by the FA source, and $c$ is a free amplitude resolved by the variational (EAS) formulation.
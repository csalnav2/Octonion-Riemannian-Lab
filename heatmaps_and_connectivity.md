# Reading the 8 × 8 heatmaps and connectivity plot

Octonion–Riemann Lab · v5.27 documentation

The repeating heatmap regions follow the observation map's fixed structure. The connectivity plot compares sampled states across representations. It does not draw connections between visible and hidden coordinate axes.

## 1. What one heatmap entry means

The unit source has eight real coefficients, with seven independent tangent directions. The lab uses a fixed orthogonal split

\[
x\leftrightarrow(a,b,c)\in\mathbb R^4\oplus\mathbb R^3\oplus\mathbb R,
\qquad \|a\|^2+\|b\|^2+c^2=1.
\]

Its paired observation is

\[
F(x)=\bigl(H(a/\|a\|),b/\|b\|\bigr)
      =(n_4,n_3)\in S^2\times S^2\subset\mathbb R^6.
\]

The subscripts identify the source-block sizes; both observations lie on two-dimensional spheres. The Hopf map removes a common complex phase. [1]

For the derivative and displayed sensitivity matrix,

\[
J=DF\in\mathbb R^{6\times8},\qquad M=\frac14J^\mathsf TJ,
\qquad M_{ij}=\frac14\frac{\partial F}{\partial x_i}\cdot
                         \frac{\partial F}{\partial x_j}.
\]

A diagonal entry measures sensitivity along one source axis. An off-diagonal entry measures alignment of two output sensitivities. It is not a statistical correlation coefficient. Zero means orthogonal output sensitivities under the chosen product metric, not statistically independent source variables.

The quadratic form

\[
\delta x^\mathsf T M\delta x=\frac14\|J\delta x\|^2
\]

is the pullback of the chosen output metric. The quarter is a metric-scale convention, not a retention percentage. Unlike a nondegenerate Riemannian metric, this form vanishes along hidden directions. Metric lengths and coordinate transformations provide the geometric background. [2]

## 2. Why the active regions stay in place

Define

\[
r_4=\|a\|,\quad q=a/r_4,\quad
r_3=\|b\|,\quad n=b/r_3,\quad
u=(-q_1,q_0,-q_3,q_2).
\]

When both blocks are nonzero, direct differentiation gives

\[
M_{\rm split}=
\begin{pmatrix}
r_4^{-2}(I_4-qq^\mathsf T-uu^\mathsf T)&0&0\\
0&(4r_3^2)^{-1}(I_3-nn^\mathsf T)&0\\
0&0&0
\end{pmatrix}.
\]

The blue branch depends on the four-block and the red branch on the three-block. Their sensitivities occupy separate blocks. The omitted coordinate has a zero row and column in this split frame. Normalization removes block-radius sensitivity; the Hopf map additionally removes the phase direction \(u\).

Orientations and amplitudes change the values inside these fixed regions. Small block amplitudes can amplify derivatives through the inverse-square factors. Brightness concentration alone is not a physical hotspot.

For the default slice and unrotated complement, 21 of the 64 entries are generically nonzero. This includes the structural identities \(M_{01}=M_{23}=0\) and their symmetric counterparts. Special states can have additional zeros. A rotated complementary observation can fill its original four-coordinate block while leaving its coupling to the selected quaternion block zero.

If the split is \(y=Rx\), then \(M_x=R^\mathsf T M_yR\). A different coordinate frame can redistribute the pattern. The matrix indices are fixed axes, not the evolving eigenvectors.

## 3. What is hidden, and what is orthogonal?

Let \(B\in\mathbb R^{8\times7}\) be an orthonormal tangent basis and \(V_r\) the retained right singular vectors of \(JB\). The lab constructs

\[
T=I_8-xx^\mathsf T,\qquad
O=BV_rV_r^\mathsf TB^\mathsf T,\qquad N=T-O.
\]

On the regular paired-map domain,

\[
\operatorname{rank}O=4,\quad\operatorname{rank}N=3,
\qquad ON=0,\qquad JN=0.
\]

The radial norm direction belongs to neither tangent subspace. The eight plotted axes are not eight independently observable modes; an individual axis can have both visible and hidden components.

Although \(O\) is block diagonal in the split frame, \(N\) generally is not. Its cross-block entries are \(-x_i x_j\), expressed in that frame, because the shared unit-norm constraint enters through \(T\). These are geometric projection coefficients, not evidence of learned information transfer. Orthogonality here is constructed locally; it does not prove preservation of every relationship after mapping.

## 4. What the topology plot actually compares

The plot constructs three separate graphs from up to 41 matching recent samples: source states on \(S^7\), paired observations on \(S^2\times S^2\), and quaternionic observations on \(S^4\). Edges connect sample indices when

\[
d_{ij}\leq\varepsilon,\qquad
d^{\rm source}_{ij}=\frac{\|x_i-x_j\|}{2},\quad
d^{\rm pair}_{ij}=\frac{\|F(x_i)-F(x_j)\|}{2\sqrt2},\quad
d^{S^4}_{ij}=\frac{\|H_{\mathbb H}(x_i)-H_{\mathbb H}(x_j)\|}{2}.
\]

The vertical axis is the number of connected components, \(\beta_0=\dim H_0\); the horizontal axis is the distance threshold. The integer staircase records component mergers. This is zero-dimensional persistent connectivity, a limited part of persistent homology. [3]

Different curves reveal differences in sampled clustering and merger scales. Speed, sampling density, window membership and distance normalization can also change them. No graph here connects visible axes directly to hidden axes. The calculation does not establish loop preservation, Hopf linking, or global topology changes. Smooth matrix landscapes are displays over discrete indices, not physical surfaces with measured hills or holes.

For comparison between observation maps, the separate quantity

\[
\eta=\frac{\operatorname{tr}(N_{\rm pair}O_{S^4})}{3}
\]

measures local subspace overlap. Predicting hidden targets from visible histories requires the separate held-out prediction experiment and its baselines. Neither similar connectivity curves nor nonzero overlap establishes that predictive relationship.

## Audit scope and practical use

These implementation statements were checked against the v5.26 analytic derivative, route split, tangent-projector and graph routines retained by this revision. At saved default times 0, 15 and 30 source seconds, the block expression agreed with the stored matrices within \(9\times10^{-16}\). This is an implementation check, not physical validation. Coordinates are dimensionless and time is in declared source seconds.

Inspect matrix entries with their coordinate labels, compare ranks and null residuals, then use connectivity curves to identify sample windows worth investigating. Judge predictive claims from untouched trajectories and fair baselines.

## References

These sources support the mathematical background; they do not independently validate this lab's implementation or establish a physical application.

1. David W. Lyons, *An Elementary Introduction to the Hopf Fibration*, Mathematics Magazine 76(2), 87–98 (2003). [Article PDF](https://nilesjohnson.net/hopf-articles/Lyons_Elem-intro-Hopf-fibration.pdf).
2. David Tong, *General Relativity*, Chapter 3: Introducing Riemannian Geometry (2019), especially metric inner products and transformation law (3.123). [Author's notes](https://www.damtp.cam.ac.uk/user/tong/gr/grhtml/S3.html).
3. Robert Ghrist, *Barcodes: The Persistent Topology of Data*, Bulletin of the American Mathematical Society 45(1), 61–75 (2008). [Publisher article](https://doi.org/10.1090/S0273-0979-07-01191-3).

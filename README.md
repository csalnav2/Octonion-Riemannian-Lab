# Octonion–Riemann Lab

A synthetic geometry and representation-diagnostics lab for asking which coordinates and relationships survive a chosen observation of an octonion. Version **5.26** includes synchronized growing sphere paths, moving Hopf-fiber families, a shared Riemann sphere, an evolving geometric terrain, relationship matrices, reconstruction baselines, and SPSA comparisons.

The motivation is exploratory: could these complementary geometric views help formulate useful hypotheses about a physical system? The current synthetic demonstrations do not establish a new physical law or lossless compression of arbitrary eight-coordinate data.

## Documentation and media update

This package refreshes the posts, mathematical explanation and shareable animations for **v5.26**. The scientific application and its matching Colab notebook are unchanged. Start with [the X/Instagram drafts](docs/octonion_social_posts.md), [the mathematical follow-up](docs/octonion_math_post.md), and [the media guide](media/README.md). Numbered literature references appear after each post.

The main focus is the **octonion experiment**. The earlier MEAO spinor/Clifford work motivated the concern with coordinate relationships. Its full coefficient encoding can be invertible; the harder information problem here is the noninjective octonion observation, where different source states can give identical sphere measurements. This is a comparison of information-preservation tasks, not a universal ranking of implementation difficulty. The package contains the octonion lab and does not merge the MEAO field solver.

## What the current prediction result supports

The earlier coupled PCA/ridge-DMD configuration increased visible and hidden test errors by approximately 22.1% and 2.2% compared with each branch's own predictor. The newer supervised visible-history ridge experiment is a separate method with stricter input access.

| Hidden-projector prediction on eight new synthetic test trajectories | MSE |
|---|---:|
| Visible-history ridge | 0.0286737463 |
| Single-visible-snapshot ridge | 0.0284449133 |
| Constant training-mean baseline | 0.0422955656 |

The history model has **32.2% lower MSE than the mean baseline**, but about **0.8% higher MSE than the snapshot model**. There is predictable target structure within this synthetic family; an additional benefit from history has not been demonstrated. These percentages are predictive-error comparisons, not information-retention fractions or hidden-state recovery rates.

Complete saved numerical examples and protocol metadata are in [examples/benchmarks](examples/benchmarks/README.md). Their hidden labels are evaluation/training targets, never visible-only inference inputs. These experiments use one fixed synthetic driver family with independent initial states; they do not establish a physical mechanism or validate an application to a real system.

## Visible history to hidden targets

The optional visible-history test predicts hidden projector entries or hidden tangent velocity from the six observed sphere coordinates. The predictor is trained using archived hidden labels, then deployed using visible history alone. Exported coefficients and `vh_predict_next(model, observation_history)` make that access boundary explicit.

Defaults use 24 training, eight validation and eight test trajectories with independent initial octonions and the same declared synthetic driver. Histories never cross trajectories. Train-only normalization and fixed ridge prevent held-out fitting. Compare delay ridge with a snapshot model, training mean and frozen initial visible estimate; hidden persistence is separately labeled as requiring a true hidden seed at each forecast origin. Uncertainty resamples whole test trajectories.

Dynamic error plots and fixed first-test-case heatmaps share the source clock. A phase-twin control demonstrates identical visible histories with different hidden targets under unrestricted trajectories; it is not an impossibility proof within the chosen driver family. Positive skill describes predictive structure, not physical causality, full phase recovery or information-retention percentage. Existing PINN/DMD and source metrics remain unchanged. See section 21 of [the geometry guide](docs/octonion_geometry_guide.md).

## PINN with time-varying boundary values

A separate scalar diffusion benchmark uses a selected spherical latitude band with fixed edges and time-varying Dirichlet data from the blue/red observable sphere signals. A small sine neural network trains all weights against the PDE after a linear residual initialization. Hard initial and boundary constraints are part of its ansatz. Reference interior values never supply training labels.

The independent conservative BDF solver uses nested 65/129-node grids, and a nonconstant analytic P₂ eigenmode provides an exact verification case. The dashboard reports field error, independent residual, grid-refinement difference, sampled extrema and actual optimization status. Smooth heatmaps, profiles and error traces use the shared replay. Training is manual and runs as a reconnectable, cancellable local job; no provider key or GPU is required.

All boundary times are known during this solve. It is a chosen model experiment, not future forecasting, validated octonion physics, or a method to restore hidden information. Existing source/DMD/SPSA and retention calculations are unchanged. SciPy is declared in requirements. See section 20 of [the geometry guide](docs/octonion_geometry_guide.md) for equations, units and primary references.

## Visible and hidden PCA–DMD

The separate model comparison applies train-only PCA via SVD and affine ridge DMD to visible and hidden direction projectors, or their components of source motion. A coupled model and cross-only prediction tests assess whether the other branch improves forecasts on later samples. The original X8 PCA/DMD pipeline remains available.

Training, validation and test use a fixed 60/20/20 chronological split. Centering and one pooled RMS scale are fitted on training data only. All comparisons include persistence and training-mean baselines; zero-denominator skill and undefined inputs are reported explicitly. Smooth synchronized plots distinguish reconstruction, one-step prediction and open-loop rollout. Numerical JSON retains model parameters and original errors.

The inputs are calculated from the archived source. Predictive association does not establish causal coupling or hidden-state recovery from sphere measurements. Projector matrices avoid arbitrary SVD-basis sign flips; unconstrained forecasts can still fail projector identities. See section 19 of [the geometry guide](docs/octonion_geometry_guide.md).

## Observable and hidden directions

The new paired heatmaps and matrix landscapes follow the same SLERP source clock. Choose the sphere-pair or quaternionic map, and inspect the complete hidden subspace, the blue common-phase direction, or its amplitude complement. Matrices exclude the radial norm direction and use a shared fixed signed scale. Raw Jacobian magnitudes remain unchanged.

A bounded local audit compares source-motion partitions, cross-map subspace overlap and rolling finite-cloud H₀ connectivity on matched samples. Export the full numerical evidence as JSON. Constant-series correlations remain undefined. No physical coupling, hidden-phase recovery or global topology preservation is asserted. H₀ counts remain discrete; color easing affects presentation only. The existing global topology status and movie scenes retain their earlier scope.

See section 18 of [the geometry guide](docs/octonion_geometry_guide.md) for equations, assumptions and numbered primary references. Existing retention controls, S⁷ companion, trace-integrated amber bands, replay, chat and SPSA remain available.

## Start in Google Colab

1. Upload `launch_octonion_colab.ipynb` to Google Colab.
2. Run its **first code cell**. It contains the complete Python program, verifies its checksum, installs dependencies, and finishes startup precomputation before requesting credentials.
3. Supply an ngrok token for the external dashboard. OpenAI is optional for chat and voice; geometry works without it. Open the complete newly printed launch link and keep the runtime connected.

The notebook's later cells provide optional numerical assessments, a mathematical/physics-model audit, and an additional diagnostic movie. Video exports replay automatically; the live dashboard uses the shared 20-second replay. Browser frame rate depends on hardware and the number of visible plots.

## Local setup

Python **3.11 or later** is required. From this repository:

```bash
python -m venv .venv
# Linux/macOS:
source .venv/bin/activate
# Windows PowerShell instead: .venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python scripts/verify_bundle.py
python octonion_lab_revised.py --serve --access local --precompute --no-prompt-keys
```

For ngrok access and secure credential prompts:

```bash
python octonion_lab_revised.py --serve --ngrok --prompt-keys --precompute
```

The combined installer is also available:

```bash
python octonion_lab_revised.py --install --serve --ngrok --prompt-keys --precompute
```

For a quick launch without startup movie rendering, replace `--precompute` with `--no-precompute`. Scientific diagnostic caches may still need computation. Output files are written to `octonion_outputs/` by default; `OCTONION_OUTPUT_DIR` can select a different directory. The default server binds to `127.0.0.1`. This is a research application, not a hardened multi-user deployment.

`requirements.txt` reproduces the ranges declared by the source, not a fully pinned environment. Account access to configured AI models must be checked in the running application; repository packaging does not verify access or perform billable API calls. The optional Blender renderer also requires a separately installed Blender executable.

## What the geometry means

- A unit octonion has **eight real coefficients** with one norm constraint, so it lies on **S⁷**. Its seven imaginary basis units are not seven complex-valued coordinates.
- A recorded orthogonal **4 + 3 + 1** split retains the source if all blocks and the observation frame are kept. The additional scalar `c` is a complementary coordinate, not the original real coefficient `x₀`; `x₀` belongs to the quaternion block in the available slices.
- The normalized four-coordinate block lies on **S³**. The complex Hopf map takes it to **S²** and removes a common U(1) phase. The second sphere shows the normalized complementary three-vector. These are **parallel observations** of the same source.
- The visible linked loops are stereographic images of fibers in S³. S³ stereographic projection is invertible away from its pole; the Hopf quotient is the information-losing step. Large exact-projection loops can be a chart-pole effect. Compact display mode deliberately changes the displayed geometry and is labeled accordingly.
- The shared Riemann sphere is **S² ≅ CP¹**. Showing the two paths on one sphere does not encode all missing amplitudes, phase, and complementary scalar.
- The terrain's Christoffel symbols come from its declared metric. They describe its conditional trajectory and transport; they do not restore discarded coordinates. Blue terrain motion follows the observed Hopf route. The red terrain path is separately integrated in that metric and is different from the red complementary sphere path. Height represents a chosen diagnostic field.

The paired surface observation has generic local rank four on S⁷, leaving three hidden local directions. Retaining side information can support exact reconstruction; recovering from the two surface points alone is a different problem. Archive raw measurements when adapting the lab to physics.

## Fixed retention display

The v5.26 retention plot uses a fixed 0–1 axis for scores and losses that are already normalized by their definitions. Linear and zero-preserving log-like spacing remain. Data are not renormalized or clipped; out-of-range values expand the axis and trigger a visible data check. Diagnostic movie retention uses the same bounds. The Jacobian spectra retain their original values and scale; singular values above one can legitimately indicate local stretching.

## Quaternionic Hopf companion

The v5.26 companion uses the complete source S⁷ and the quaternionic Hopf map H(A,B)=(2A B̄, |A|²−|B|²) in S⁴. Fibers in S⁷ are S³; the live view shows source-anchored S² parameter slices under one fixed 3D projection, with all five exact base coordinates in a synchronized graph. Slice motion may occur within a fixed full fiber. Projected crossings are not topology evidence.

Use **Audit this source interval** for algebra, local-rank and reconstruction checks. JSON and CSV retain the source, base, actual source-side fiber quaternion, and patch. Additional side data are needed to reconstruct the source; base-only information loss remains. Existing retention metrics and SPSA retain their original scope. Existing movie exporters keep their existing scenes; the new companion exports numerical evidence.

Read [the updated mathematics](docs/octonion_math_post.md) and [X/Instagram drafts with references after each post](docs/octonion_social_posts.md).

## Stored-phase sensitivity bands

Short amber-yellow highlights follow the blue/shared S² curve and corresponding terrain trace, with the same centerline and thickness as the parent curve. One gentle brightness pulse introduces each band; a persistent color remains. The live controls offer amber-yellow, teal, and violet, with trailing spans of 0.08, 0.15 (default), or 0.25 source seconds. A band's span is a display annotation width, not a measured event duration. Bands end at the qualifying sample, stay within revealed history, and follow the shared replay. Stale configurations and B³ mode hide the overlays. There are no beads or expanding rings.

The red sphere route already carries source octonion information through b/‖b‖. This phase experiment varies the blue four-block while keeping b fixed, so applying the same phase bands to red would mislabel the result. The red terrain path is a separate integrated metric trajectory, distinct from the red complementary sphere path.

The experiment holds the Hopf base point and original ambient precision fixed. Hopf invariance and isotropic precision are null controls. The Fubini–Study reference retains K = 4. The conditional metric has a π-phase ambiguity; its curvature is not a decoder for the complete common phase. Bands are added source-side annotations and do not establish a physical phase coupling.

Nested 8/16 phase samples and temporal midpoint checks assess numerical resolution. They do not add independent measurements or improve retention percentages by themselves. Existing SPSA objectives and scientific arrays remain. Standard route movie exports use the default amber-yellow 0.15-second bands and an audit JSON sidecar; their standalone default metric is explicitly recorded. See [the mathematical guide](docs/octonion_geometry_guide.md) and [revision notes](docs/octonion_revision_notes.md).

## Retention, optimization, and interpretation

There is no single universal information-retention percentage. The lab reports separately:

- raw coordinate reconstruction and squared-norm accounting;
- distance, Gram/inner-product, neighborhood, and temporal relationship losses;
- finite-label information under an explicitly declared noise model;
- chronologically held-out coordinate reconstruction;
- instantaneous rank and model-dependent time-series observability.

SPSA can tune the chosen observation parameters against a declared loss. Improvement on training data is not a guarantee of validation improvement or invertibility. A 99.999% target is a requested score for a specified metric, not proof that 99.999% of all possible octonion information survived.

For geodesic questions, separate path length, intrinsic geodesic curvature, ambient curvature of a rendered path, and curvature of the metric. A geodesic has zero intrinsic geodesic curvature while it may look curved in an embedding. A time-dependent metric can change path length and transport without revealing a new physical force.

## Checks and reproducibility

The fast bundle check uses only the Python standard library. It parses the complete source and notebook cells, verifies the notebook's embedded-source checksum, checks that both source copies match exactly, and checks dependency-range consistency:

```bash
python scripts/verify_bundle.py
```

Run the existing numerical audit and bundled regression suites after dependencies are installed:

```bash
python octonion_lab_revised.py --physics-audit --out octonion_outputs/physics_audit.json
python octonion_lab_revised.py --test
```

These checks assess implemented mathematics and software behavior. They are not validation of an experimental physical model, a live ngrok account, or a paid OpenAI endpoint. Current phase controls and historical verification are distinguished in [revision notes](docs/octonion_revision_notes.md).

## MEAO, Clifford geometry and preservation

The documented full MEAO coefficient encoding takes a two-component complex spinor to an even Clifford element:

$$
\psi=(a+ib,c+id) \longleftrightarrow \Phi=a+b e_{12}+c e_{23}+d e_{31}.
$$

With the declared Clifford basis and retained complex structure, this full, invertible coefficient representation preserves the complex inner product and orthogonality. That algebraic statement does not extend automatically to compressed descriptor summaries or to every physical interpretation of a reduced model. The [math appendix](docs/octonion_math_post.md#h-meao-clifford-representations-and-the-meaning-of-preservation) derives the real and complex inner-product identities explicitly.

A **Borel isomorphism** preserves measurable structure; it does not by itself preserve the usual metric or angles. Clifford geometry instead encodes a specified metric through $uv+vu=2g(u,v)1$. A smooth change of coordinates preserves geometric lengths when the metric transforms with it. The rank-deficient Hopf observations are not invertible chart changes. [Hirata, Standard Borel Spaces](https://isa-afp.org/entries/Standard_Borel_Spaces.html), [Park, Lecture note on Clifford algebra](https://arxiv.org/abs/2205.09509).

For an individual normalized pure qubit, a full Bloch vector determines its density matrix and all Hermitian-observable expectations; the discarded global phase is redundant for that state. Orthogonal state vectors correspond to antipodal Bloch vectors. These facts do not make every synthetic octonion coordinate a quantum observable or retain all spatial phase information of a field. [IBM Quantum, Bloch sphere](https://quantum.cloud.ibm.com/learning/en/courses/general-formulation-of-quantum-information/density-matrices/bloch-sphere).

## Animation clips

![Hopf geometry and trace-integrated yellow phase-sensitivity bands](media/hopf_phase_bands.gif)

The [media directory](media/README.md) contains three square MP4 clips and a compact GIF, with scene explanations and provenance. These are visualizations of synthetic numerical data, rendered using the current dashboard code. Playback compression is declared in the media guide; displayed source seconds are the scientific clock.

The clips distinguish phase-sensitive conditional-metric annotations, local matrix geometry, sampled H₀ connectivity, and held-out prediction. They should not be captioned as direct movies of quantum particles, recovered hidden phase, or experimentally observed physical forces.

## Files

| File | Purpose |
|---|---|
| `octonion_lab_revised.py` | Complete v5.26 application, embedded UI, audits, exports, and CLI |
| `launch_octonion_colab.ipynb` | One-cell Colab launcher with the exact complete application bundled |
| `requirements.txt` | Dependency ranges extracted from this source |
| `docs/octonion_geometry_guide.md` | Detailed map conventions and diagnostic interpretation |
| `docs/octonion_revision_notes.md` | Current revision and clearly labeled historical notes |
| `docs/octonion_social_posts.md` | Updated X/Instagram drafts with numbered references |
| `docs/octonion_math_post.md` | Mathematical follow-up, benchmark details, MEAO/Clifford comparison and references |
| `media/` | MP4/GIF clips and source/interpretation guide |
| `examples/benchmarks/` | Saved synthetic prediction results and access/protocol metadata |
| `scripts/verify_bundle.py` | Offline source/notebook consistency check |
| `scripts/publish_github.sh` | Explicit local publication helper; private by default |

## Publish this prepared repository

Review the files and [security notes](SECURITY.md) first. Install and authenticate the GitHub CLI on your own machine with `gh auth login`. The helper defaults to **private**, requires a clean committed working tree, and does not run automatically:

```bash
git init -b main
git add .
git commit -m "Prepare Octonion Riemann Lab v5.26"
bash scripts/publish_github.sh octonion-riemann-lab
```

The ZIP distribution omits Git internals; `git init` establishes them after extraction. No remote repository has been created by preparing these files. The helper uses the [official GitHub CLI repository-creation command](https://cli.github.com/manual/gh_repo_create).

Use `--public` only after deciding to make the reviewed repository public:

```bash
bash scripts/publish_github.sh octonion-riemann-lab --public
```

No license has been selected yet. Do not assume the project grants redistribution or modification rights merely because a repository is readable. Embedded third-party assets remain subject to their own notices. Choose a project license deliberately before inviting outside contributions.

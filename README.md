## Hybrid: Two Signal Model for Evidence Value (Caliper and Density)

**The problem:** infer evidential value from published p‑values when publication and reporting are selective. Practically, we want a calibrated quantity such as the fraction of studies with a real effect, $\pi$, or a closely related target like expected replication, while also diagnosing how selection operates.

Two influential families of approaches look at different parts of the same elephant. “p‑curve” methods read the shape of significant p‑values—right‑skew should appear when effects are real—while “caliper/bunching” tests look for a discontinuity at the significance threshold (e.g., a jump at $p=\alpha$). Selection models (e.g., Vevea–Hedges) move closer to a unified treatment by estimating a stepwise publication weight function on p‑bins, but in practice the step at $\alpha$ and the interior “stars preference” (a slope favoring ever‑smaller significant p’s) can be conflated, which makes $\pi$ fragile when journals prefer tiny p‑values.

Our contribution is to bring the boundary and interior signals together in a single likelihood/posterior by modeling both the jump and the slope explicitly in the selection function $w(p)$, while fitting a flexible, decreasing “true‑effect” p‑density $g(p)$. Concretely, if a fraction $\pi$ of studies have nonzero effects, the pre‑selection p‑density is

$$
f_{\text{true}}(p\mid \pi,g) = (1-\pi)\cdot 1 + \pi\cdot g(p),\quad p\in(0,1),
$$

and the observed density is

$$
f_{\text{obs}}(p)\ \propto\ w(p)\,f_{\text{true}}(p\mid \pi,g).
$$

We parameterize selection as

$$
\log w(p)=\beta\,\mathbf 1\{p<\alpha\}+\sum_j \gamma_j\,B_j(p)\,\mathbf 1\{p<\alpha\},
$$

where $\beta$ captures the publication‑line jump at $\alpha$ and the nonnegative basis $B_j$ (e.g., I‑splines on $(0,\alpha)$) with coefficients $\gamma_j$ encode a monotone nonincreasing interior slope (“stars” preference). For $g(p)$ we use a low‑rank mixture of Beta densities with $a<1$ (or an equivalent monotone family), which is the natural image of power on the p‑scale. Estimation can be maximum likelihood (with closed‑form weights within bins) or fully Bayesian with weak priors on $\pi,\beta,\gamma$ and mixture weights. Either way, the same fit yields a posterior for $\pi$ (or expected replication) and interpretable posteriors for the jump and the slope.

A few assumptions are needed for identification and calibration, and they are inspectable. We require some observed mass above $\alpha$ (even a small window) to see the jump; we constrain $g$ to be decreasing and $w$ to be nonincreasing with limited degrees of freedom so that left‑tail mass is not entirely explainable by either mechanism alone; and we standardize inputs (two‑sided p’s, one pre‑specified test per study). If within‑study multiplicity or rounding is present, we either pre‑process (one focal test; analyze z‑statistics) or add simple layers (min‑of‑m and rounding) so the selection/jump diagnostics are not artifacts.

In simulations designed to probe the main failure mode—journals preferring “stars”—the explicit jump‑plus‑slope model remained well‑behaved while a p‑only Vevea–Hedges–style step function substantially over‑estimated $\pi$. When selection consisted only of a boundary jump, both approaches recovered $\pi$ similarly (with a small accuracy edge for the jump‑plus‑slope model in our settings). When we added strong stars preference inside $(0,\alpha)$, the explicit decomposition preserved calibration of $\pi$ and recovered the jump and slope separately, whereas the stepwise model blended the two and pushed $\hat{\pi}$ upward. These results are illustrative rather than universal—the exact numbers depend on the simulated envelopes and grids—but they show why separating “jump” from “slope” in $w(p)$, while fitting $g(p)$ for evidential shape, reduces the core confounding that makes $\pi$ unstable under stars selection.

The practical benefit is that inference and diagnostics become one object. From a single fit you obtain (i) a decision‑ready posterior for $\pi$ or expected replication and (ii) clear evidence about how selection operates: a publication line ($\beta$) and any interior stars preference ($\gamma$). Decisions can then be tied to losses—claim evidential value when $P(\pi>\pi^\*)$ exceeds a chosen threshold and prioritize replication when the posterior shows a large $\beta$ or strong interior slope even if $P(\pi>\pi^\*)$ is borderline. The method does not preclude richer meta‑analytic structure (effects and standard errors, moderators, clustering); it provides the selection layer that lets p‑curve and caliper information be combined coherently rather than tested piecemeal.

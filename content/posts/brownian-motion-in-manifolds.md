+++
date = '2026-07-14T13:19:39+01:00'
draft = false
title = 'Brownian motion in Riemannian manifolds'
featured_image = '/images/random-walk.png'
+++

Random walks are the quintessential building blocks of stochastic processes. From Einstein's explanation of Brownian motion to the discrete-time models underpinning modern option pricing, the premise is deceptively simple: at each step, take an independent, identically distributed (IID) jump in a random direction. In Euclidean space \(\mathbb{R}^n\), this is trivial, as all position vectors share the same global tangent space. However, when the state space is a curved manifold—say, the space of covariance matrices, the configuration space of a rigid body, or the parameter space of an interest rate curve—the very notion of "stepping in the same direction" breaks down. To extend the random walk to a curved geometry, we must first understand how to "go straight" on a manifold. This is precisely the role of a Riemannian metric and its associated geodesics.

### Riemannian Metrics and Geodesics

A Riemannian metric equips each tangent space \(T_x X\) with an inner product, allowing us to measure lengths and angles locally. More formally:

{{< def >}}
Let \(X\) be a smooth manifold. A **Riemannian metric** \(g\) on \(X\) is a smooth section 
\(g \in \Gamma(S^2T^*X)\), such that \(g(x) \in S^2T_x^* X\) is a positive definite 
quadratic form on \(T_x X\) for all \(x \in X\).
{{< /def >}}

This metric induces a unique Levi-Civita connection \(\nabla\), which provides a notion of parallel transport. Critically, it also defines the geodesic equation \(\nabla_{\dot{\gamma}} \dot{\gamma} = 0\). Solving this yields the exponential map \(\exp_x: T_x X \to X\), which sends a tangent vector \(v_x\) to the point reached by traversing the unique geodesic starting at \(x\) with initial velocity \(v_x\) for unit time. The existence of these geodesics is guaranteed locally, and globally under completeness:

{{< theorem >}}
Given a Riemannian manifold \((X, g)\) and a point \(x \in X\), for any tangent vector 
\(v_x \in T_x M\), there exists a unique maximal geodesic \(\gamma: I \to X\) such that 
\(\gamma(0) = x\) and \(\dot{\gamma}(0) = v_x\).
{{< /theorem >}}

In fact, under compactness this interval \(I\) is always the whole of \(\mathbb{R}\). This is exactly the content of the following lemma:

{{< lemma >}}
Every compact Riemannian manifold is geodesically complete.
{{< /lemma >}}

{{< proof >}}
This follows directly from the Hopf-Rinow theorem, which states that for a connected Riemannian manifold, metric completeness is equivalent to geodesic completeness. Compactness implies metric completeness. The idea is that the only way a geodesic can fail to be globally-defined is if it "falls off" the manifold, or is allowed to go off "into infinity". Compactness makes sure this can never happen.
{{< /proof >}}

---

### From Fixed Vectors to Isotropic Distributions

At first glance, defining a random walk seems straightforward: pick some deterministic \(v_x \in T_x X\) and travel along \(\exp_x(v_x)\) for one step. But now the problem emerges. Random walks are supposed to have IID steps, yet after one step we land at \(y = \exp_x(v_x)\), and the next step must live in \(T_y X\), a completely different vector space. To compare these tangent spaces, differential geometers use connections and parallel transport. However, parallel transporting a deterministic vector \(v_x\) from \(x\) to \(y\) along different curves yields different results if the manifold has non-zero curvature (holonomy). Therefore, a fixed tangent vector does not provide a well-defined "same direction" on a curved space unless the manifold is flat.

To salvage the IID property, we shift our perspective. Instead of asking for *deterministic* vectors to be transported identically, we ask for the *distribution* of the step to be invariant under parallel transport. Since parallel transport is a linear isometry (it preserves the inner product), any isotropic (rotationally invariant) distribution on \(T_x X\) is automatically mapped to the same isotropic distribution on \(T_y X\), irrespective of the chosen path. The canonical choice is the standard Gaussian measure \(\mathcal{N}(0, g_x^{-1})\) on \(T_x X\), or equivalently, a uniform distribution on the tangent sphere. Consequently, the steps are not IID as vectors, but rather IID as *random directions drawn from the rotationally invariant measure*. As noted by Hsu (2002, Ch. 1), this isotropic geodesic random walk is the natural probabilistic analogue of the Euclidean random walk on a Riemannian manifold.

Formally, the geodesic random walk with step size \(\epsilon > 0\) is a Markov chain \((X_k^{\epsilon})_{k \geq 0}\) defined by:
\[
X_{k+1}^{\epsilon} = \exp_{X_k^{\epsilon}}\left( \epsilon \, V_{k+1} \right),
\]
where \(V_{k+1}\) is a random vector in \(T_{X_k^\epsilon} X\) whose distribution is the standard Gaussian measure (or uniform on the unit sphere). This construction is beautifully intrinsic; it does not require embedding the manifold in a higher-dimensional Euclidean space. The generator of this Markov chain, acting on smooth functions \(f: X \to \mathbb{R}\), is given by:
\[
L_\epsilon f(x) = \frac{1}{\epsilon^2} \mathbb{E}\left[ f(\exp_x(\epsilon V)) - f(x) \right].
\]
A standard Taylor expansion in normal coordinates reveals that as \(\epsilon \to 0\), the generator converges to the Laplace-Beltrami operator \(\frac{1}{2} \Delta\), which is the canonical second-order differential operator on \(X\).

---

### Central Limit Theorem Type Result

In Euclidean space, the classical CLT tells us that a scaled random walk \(S_n / \sqrt{n}\) converges in distribution to a normal (Gaussian) random variable, which is the time-1 marginal of Brownian motion. On a manifold, the analogous statement is that the geodesic random walk, when scaled diffusively, converges to Brownian motion on \(X\). Brownian motion on a Riemannian manifold is the Markov process whose generator is exactly \(\frac{1}{2} \Delta\) (the Laplace-Beltrami operator). This deep result was rigorously established by Stroock and Varadhan (1971) in their seminal work on the support of diffusion processes.

Let us define the continuous-time scaled geodesic random walk. Let \(X^{(n)}_t = X_{\lfloor nt \rfloor}^{1/\sqrt{n}}\), where \(\lfloor nt \rfloor\) denotes the integer part. Essentially, we take \(n\) microscopic steps of size \(1/\sqrt{n}\) over one unit of macroscopic time. The convergence result is as follows:

{{< theorem >}}
Let \((X, g)\) be a compact Riemannian manifold. Let \((X^{(n)}_t)_{t \geq 0}\) be the continuous-time geodesic random walk with step size \(1/\sqrt{n}\). Then, as \(n \to \infty\), the sequence of processes \((X^{(n)}_t)\) converges weakly in the Skorokhod topology to Brownian motion on \(X\). Specifically, for any smooth function \(f\),
\[
\lim_{n \to \infty} \mathbb{E}[ f(X^{(n)}_t) ] = \mathbb{E}[ f(B_t) ],
\]
where \((B_t)\) is the Brownian motion on \(X\) starting from the same initial point, characterised by the heat equation \(\partial_t u = \frac{1}{2} \Delta u\).
{{< /theorem >}}

The proof hinges on the martingale problem formulation. The generator \(L_{1/\sqrt{n}}\) converges to \(\frac{1}{2} \Delta\) uniformly on compact sets, and the compactness of the manifold ensures tightness of the family of laws. For a detailed exposition of this convergence, including the subtle issues regarding the cut locus and the exponential map, we refer the reader to Hsu (2002, Ch. 8) and the classic text by Stroock (2000). This theorem is a cornerstone of stochastic analysis on manifolds, as it justifies the use of Brownian motion as the universal scaling limit of random processes on curved spaces.

---

### Uses in Mathematical Finance

The rigorous framework of random walks on manifolds and their convergence to manifold-valued Brownian motions is not merely an abstract mathematical curiosity; it has profound and increasingly practical applications in mathematical finance. Here, the state variables often live on non-linear, curved spaces due to no-arbitrage constraints, positivity requirements, and degeneracies in volatility.

**1. Modelling Stochastic Covariance and Correlation Matrices**:
In multivariate portfolio risk management, the covariance matrix of asset returns must remain symmetric and positive-definite at all times. The space \(\mathrm{Sym}^+(n)\) of \(n \times n\) positive-definite matrices is a Riemannian manifold (typically endowed with the affine-invariant metric). A random walk on \(\mathrm{Sym}^+(n)\)—and its scaling limit, Brownian motion on this manifold—provides a natural, geometry-aware prior for stochastic volatility models. By discretising the stochastic differential equation (SDE) of a Wishart process or a matrix geometric Brownian motion, one recovers geodesic random walks on \(\mathrm{Sym}^+(n)\). This approach preserves the intrinsic positivity of covariance estimates and avoids the ad-hoc "projection" methods used in Euclidean frameworks (see, e.g., Jørgensen, 1982, on the geometry of the Wishart distribution).

**2. Interest Rate Curve and Term Structure Models**:
The Heath-Jarrow-Morton (HJM) framework models the entire forward rate curve as an infinite-dimensional object. In practice, factor models reduce this to a finite-dimensional parameter space, which is often a curved manifold (e.g., the Nelson-Siegel space, which exhibits hyperbolic geometry). The no-arbitrage condition under an equivalent martingale measure enforces a specific drift restriction that depends on the manifold's connection. By viewing the forward curve as a Brownian motion on a finite-dimensional Riemannian manifold, practitioners can construct arbitrage-free discretisations that do not introduce biases into the price of interest rate derivatives. As Björk and Landén (2002) demonstrate, the geometric structure of the parameter space is crucial for constructing consistent finite-dimensional realisations of HJM models.

**3. Pricing and Heat Kernels**:
The fundamental solution of the heat equation on a manifold is the heat kernel, which represents the transition density of Brownian motion. The geodesic random walk provides an intuitive Monte Carlo scheme for numerically approximating this heat kernel, which in finance corresponds to the transition density of the underlying risk factors. For instance, the pricing of a European option on a stochastic volatility model where the volatility state space is the hyperbolic plane \(\mathbb{H}^2\) requires integrating the payoff against the heat kernel of \(\mathbb{H}^2\). Since closed-form solutions are rarely available, simulating the geodesic random walk of the volatility process (and scaling it appropriately) yields an unbiased, geometrically correct approximation of the option price, respecting the curvature of the state space.

**4. Manifold Learning and Statistical Arbitrage**:
With the rise of machine learning in finance, high-frequency asset returns are increasingly seen as lying on low-dimensional non-linear manifolds embedded in high-dimensional price spaces. Algorithms for detecting statistical arbitrage or co-movement often perform random walks on these learned manifolds to explore the state space efficiently. A random walk that ignores the underlying Riemannian metric (e.g., using Euclidean steps in the embedded space) will oversample low-density regions and introduce a bias. The geodesic random walk, conversely, respects the intrinsic geometry, leading to improved convergence in Markov Chain Monte Carlo (MCMC) procedures for Bayesian portfolio allocation, as highlighted in the geometric MCMC literature (see Girolami & Calderhead, 2011).

In summary, the geodesic random walk provides a robust, geometry-agnostic discretisation scheme for manifold-valued diffusions. Whether calibrating a correlation matrix process or pricing an exotic derivative dependent on a non-linear factor, stochastic analysis on manifolds offers the mathematical tools to ensure that the discrete-time models converge cleanly to their continuous-time, no-arbitrage limits, preserving the intrinsic structure of the financial state space.

---

**References**

- Hsu, E. P. (2002). *Stochastic Analysis on Manifolds*. American Mathematical Society.
- Stroock, D. W., & Varadhan, S. R. S. (1971). On the support of diffusion processes with applications to the strong maximum principle. In *Proceedings of the Sixth Berkeley Symposium on Mathematical Statistics and Probability*.
- Stroock, D. W. (2000). *An Introduction to the Analysis of Paths on a Riemannian Manifold*. American Mathematical Society.
- Björk, T., & Landén, C. (2002). On the construction of finite dimensional realizations for nonlinear forward rate models. *Finance and Stochastics*.
- Jørgensen, M. (1982). *The Geometry of the Multivariate Normal Distribution and the Wishart Distribution*. University of Copenhagen.
- Girolami, M., & Calderhead, B. (2011). Riemann manifold Langevin and Hamiltonian Monte Carlo methods. *Journal of the Royal Statistical Society: Series B*.

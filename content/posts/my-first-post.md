+++
date = '2026-07-14T13:19:39+01:00'
draft = false
title = 'Brownian motion in Riemannian manifolds'
+++

## Random walks on manifolds

A random walk is ...
To do the same on a manifold need a good theory of 'paths in a direction'.
This is exactly what a Riemannian metric gives, by way of geodesics.

{{< def title="Riemannian Metric" >}}
Let \(X\) be a smooth manifold. A **Riemannian metric** \(g\) on \(X\) is a smooth section 
\(g \in \Gamma(S^2T^*X)\), such that \(g(x) \in S^2T_x^* X\) is a positive definite 
quadratic form on \(T_x X\) for all \(x \in X\).
{{< /def >}}

{{< theorem title="Existence of Geodesics" >}}
Given a Riemannian manifold \((X, g)\) and a point \(x \in X\), for any tangent vector 
\(v_x \in T_x M\), there exists a unique maximal geodesic \(\gamma: I \to X\) such that 
\(\gamma(0) = x\) and \(\dot{\gamma}(0) = v_x\).
{{< /theorem >}}

{{< lemma >}}
Every compact Riemannian manifold is geodesically complete.
{{< /lemma >}}

{{< proof >}}
This follows directly from the Hopf-Rinow theorem.
{{< /proof >}}
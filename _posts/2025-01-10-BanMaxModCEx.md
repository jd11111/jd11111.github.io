---
layout: post
title:  "The Maximum Modulus Principle is False for Banach space valued functions"
date:   2025-01-10 10:00:00 +0200
categories:
---

**False Theorem:**
Let $X$ be a complex Banach space, $U \subset \mathbb{C}$ open and connected and $f:U \to X$ holomorphic.
If $\\|\cdot \\| \circ f$ has a global maximum, then $f$ is constant.

**False Proposition:**
In the same situation as above:
If $\\| \cdot \\| \circ f$ is constant, then $f$ is constant.

**Counter example (to both):**
Let $X := (\mathbb{C}^2, \\| \cdot \\|\_\infty)$ (maximum norm).
Let $U = \{ z \in \mathbb{C}: |z|< 1\}$ and define $f:U \to X$ by $f(z) := (1, z)$.
Then $f$ is holomorphic, since both component functions are.
Furthermore for all $z \in \mathbb{C} : \\| f (z) \\|\_\infty = \max \{ |z| , 1\} = 1$.
Therefore $\\| \cdot \\| \circ f$ is constant.
However $f$ is not constant.

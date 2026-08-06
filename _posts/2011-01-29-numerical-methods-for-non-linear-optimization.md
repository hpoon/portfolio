---
layout: post
title: "Numerical Methods for Non-Linear Optimization"
categories:
  - Programming
  - Mathematics
image: assets/images/algorithm.jpg
description: "Exploring Newton's Method and Steepest Descent for solving non-linear optimization problems numerically"
---

This post is recreated from the original at [https://blog.henrypoon.com/blog/2011/01/29/numerical-methods-for-non-linear-optimization/](https://blog.henrypoon.com/blog/2011/01/29/numerical-methods-for-non-linear-optimization/)

In many sciences, the problem of non-linear optimization appears quite often. In single-variable calculus, the idea of optimization involves taking the derivative of the function and equating it to zero. In multivariable calculus, the same idea applies: we set all the partial derivatives to zero and solve the system.

For a function _f(**x**)_ where **x** = [x1, x2, ..., xn]T, we can find maxima or minima by solving:

_∂f/∂x1 = 0_
_∂f/∂x2 = 0_
...
_∂f/∂xn = 0_

Using the gradient vector, this can be expressed as: _∇f(**x**) = **0**_.

However, an analytical solution is not always possible, hence the need for numerical approximation methods.

## Newton's Method

Newton's Method is an iterative approach:

1. Derive equations for the approximating line or plane (depending on dimension)
2. Using the linearized equations, solve the system
3. Generate new equations and repeat

### Step 1: Linear Approximation

For a function _f(**x**)_, we need a linear approximation of the partial derivatives. This requires taking second derivatives.

In 2D: _f(x) ≈ f(x0) + f'(x0)(x – x0)_
In 3D: _f(x, y) ≈ f(x0, y0) + fx(x0, y0)(x – x0) + fy(x0, y0)(y – y0)_
In nD: _f(**x**) ≈ f(**x0**) + ∇f(**x0**)(**x** – **x0**)_

For each partial derivative, we approximate:
- _fx(x, y) ≈ fx(x0, y0) + fxx(x0, y0)(x – x0) + fxy(x0, y0)(y – y0)_
- _fy(x, y) ≈ fy(x0, y0) + fyy(x0, y0)(x – x0) + fyx(x0, y0)(y – y0)_

### Step 2: Solve the Linear System

The resulting system is linear and can be solved analytically using row reduction or other methods. The solution becomes the values for the next iteration.

### Step 3: Iterate

Generate new approximating planes using the solution from step 2 and repeat step 2.

A good initial guess helps. A bad guess can lead to divergence or require many iterations to converge.

## Steepest Descent Method

This method uses first derivatives and follows the direction of maximum or minimum directional derivative.

### Step 1: Find the Direction

The directional derivative is defined as: _Du f = ∇f(**x**) · u_

The maximum directional derivative is parallel to the gradient. For minimum, use the negative gradient.

The unit vector in the direction of the gradient is: **u** = ∇f(**x**)/|∇f(**x**)|

The maximum and minimum directional derivatives are:
- Max Du f = |∇f(**x**)|
- Min Du f = -|∇f(**x**)|

### Step 2: Take Steps

Choose a step size "h". To maximize: _**x**n+1 = **x**n + ux h_ (where ux is the x-component of the unit vector).

Calculate the function value at the new point. Repeat until max/min is reached.

## Limitations

The approximation is generally only as good as the initial guess. A bad guess can lead to a solution that never converges. For example, with a fourth-order polynomial, a local extreme exists. If the initial guess is poor, the solution might diverge to infinity instead of finding the local extreme.

## Sources

1. Calculus by Gilbert Strang
2. Applied Regression Analysis by Norman Draper and Harry Smith

## Homework 4.1: Barenblatt Solutions and the Porous Medium Equation
# Introduction
In this homework, I study the Barenblatt self-similar solutions of the porous medium equation

$$
\partial_t\rho = \Delta(\rho^m), \qquad m>1.
$$

Unlike the ordinary heat equation, the porous medium equation is nonlinear and degenerate when

$$
\rho=0.
$$

This leads to several important properties, including compact support, finite-speed propagation, and a moving free boundary.

The Barenblatt solutions provide explicit examples of these effects.

The main goals of this homework are to:

- derive the self-similar exponents $\alpha$ and $\beta$;

- determine and verify the coefficient $k$ in the Barenblatt profile;

- plot the solution and study its spreading behavior;

- explain finite-speed propagation;

- connect the porous medium equation with Otto calculus and Wasserstein gradient flow;

- use an LLM critically and verify its mathematical claims.

---

# Part I: Self-Similar Ansatz
## Prompt Given to the LLM

```text
Consider the porous medium equation

partial_t rho = Delta(rho^m),    m > 1,

in R^d.

Derive a self-similar solution of the form

rho(t,x) = t^(-alpha) F(|x| / t^beta).

Determine the exponents alpha and beta using scaling and mass conservation.
```

## Self-Similar Form
Assume

$$
\rho(t,x) = t^{-\alpha} F\left( \frac{|x|}{t^\beta} \right).
$$

Let

$$
y = \frac{x}{t^\beta}.
$$

The factor

$$
t^{-\alpha}
$$

controls the height of the profile, while

$$
t^\beta
$$

controls its spatial width.

## Mass Conservation
The total mass is

$$
M(t) = \int_{\mathbb R^d} \rho(t,x)\\,dx.
$$

Substituting the self-similar form gives

$$
M(t) = t^{-\alpha} \int_{\mathbb R^d} F\left( \frac{|x|}{t^\beta} \right) dx.
$$

Using

$$
x=t^\beta y,
$$

we have

$$
dx=t^{d\beta}dy.
$$

Therefore,

$$
M(t) = t^{-\alpha+d\beta} \int_{\mathbb R^d} F(|y|)\\,dy.
$$

For the mass to be independent of time,

$$
-\alpha+d\beta=0.
$$

Thus,

$$
\alpha=d\beta .
$$

## Scaling of the PDE
The time derivative scales as

$$
\partial_t\rho \sim t^{-\alpha-1}.
$$

Also,

$$
\rho^m \sim t^{-m\alpha}.
$$

Each spatial derivative contributes a factor

$$
t^{-\beta},
$$

so

$$
\Delta(\rho^m) \sim t^{-m\alpha-2\beta}.
$$

Since

$$
\partial_t\rho = \Delta(\rho^m),
$$

the powers of $t$ must agree:

$$
-\alpha-1 = -m\alpha-2\beta.
$$

Therefore,

$$
\alpha+1 = m\alpha+2\beta .
$$

Using

$$
\alpha=d\beta,
$$

we obtain

$$
d\beta+1 = md\beta+2\beta.
$$

Hence,

$$
1 = \beta[d(m-1)+2].
$$

Therefore,

$$
\beta = \frac{1} {d(m-1)+2}
$$

and

$$
\alpha = \frac{d} {d(m-1)+2} .
$$

## Numerical Verification
The formulas were tested for several values of $d$ and $m$.

The maximum numerical error in

$$
\alpha=d\beta
$$

was

$$
1.11\times10^{-16},
$$

while the maximum error in

$$
\alpha+1=m\alpha+2\beta
$$

was

$$
0.
$$

Thus the numerical calculation is consistent with the two scaling identities. The derivation above, rather than the floating-point check, is the mathematical justification for the exponents.

---

# Part II: The Barenblatt Profile
The Barenblatt solution has the form

$$
\rho(t,x) = t^{-\alpha} \left( C-k\frac{|x|^2}{t^{2\beta}} \right)_+^{1/(m-1)},
$$

where

$$
(s)_+ = \max\{s,0\}.
$$

## Prompt Given to the LLM

```text
For the porous medium equation

partial_t rho = Delta(rho^m),

consider the Barenblatt profile

rho(t,x) = t^(-alpha) (C - k |x|^2 / t^(2 beta))_+^(1/(m-1)).

Determine the constant k by substituting the profile into the porous medium
equation. Check the coefficient carefully.
```

The LLM predicted

$$
k = \frac{m-1}{2m}\beta.
$$

## Derivation of $k$
Let

$$
\xi = \frac{|x|}{t^\beta}
$$

and write

$$
F(\xi) = (C-k\xi^2)^{1/(m-1)}
$$

inside the support.

The similarity equation becomes

$$
-\alpha F - \beta\xi F' = (F^m)'' + \frac{d-1}{\xi}(F^m)'.
$$

Since

$$
\alpha=d\beta,
$$

the left-hand side is

$$
-\beta \left( dF+\xi F' \right).
$$

Now

$$
F^m = (C-k\xi^2)^{m/(m-1)}.
$$

Differentiating gives

$$
(F^m)' = -2k \frac{m}{m-1} \xi F.
$$

Therefore,

$$
(F^m)'' + \frac{d-1}{\xi}(F^m)' = -2k \frac{m}{m-1} \left( dF+\xi F' \right).
$$

Matching the two sides gives

$$
\beta = 2k\frac{m}{m-1}.
$$

Thus,

$$
k = \frac{m-1}{2m}\beta .
$$

Since

$$
\beta = \frac{1}{d(m-1)+2},
$$

we obtain

$$
k = \frac{m-1} {2m[d(m-1)+2]} .
$$

## Numerical Verification
The coefficient was checked by substituting the profile into the similarity equation for several values of $d$ and $m$.

The maximum absolute residual was

$$
4.44\times10^{-16},
$$

and the maximum relative residual was

$$
4.85\times10^{-16}.
$$

Several plausible incorrect coefficients were also tested.

For

$$
d=2, \qquad m=3,
$$

the correct coefficient gave a relative residual

$$
2.36\times10^{-16},
$$

while incorrect coefficients produced residuals between

$$
0.5
$$

and

$$
0.6667.
$$

Therefore,

$$
k = \frac{m-1}{2m}\beta
$$

is consistent with the similarity equation to numerical precision.

---

# Part III: Plotting the Barenblatt Solution
For the numerical experiment, choose

$$
d=1, \qquad m=2, \qquad C=1.
$$

Then

$$
\alpha = \beta = \frac13
$$

and

$$
k = \frac1{12}.
$$

Therefore,

$$
\rho(t,x) = t^{-1/3} \left( 1- \frac{x^2} {12t^{2/3}} \right)_+ .
$$

The solution was evaluated at

$$
t = 0.25,\ 0.5,\ 1,\ 2,\ 4.
$$

## Barenblatt Profiles
![Barenblatt profiles](hw41_part3_barenblatt_profiles.png)

The plots show that the density becomes wider and lower as time increases.

## Maximum Height
The maximum occurs at

$$
x=0.
$$

Therefore,

$$
\rho(t,0) = t^{-1/3}.
$$

The numerical values are:

| $t$ | Maximum height |
| ---: | ---: |
| $0.25$ | $1.587401$ |
| $0.5$ | $1.259921$ |
| $1$ | $1.000000$ |
| $2$ | $0.793701$ |
| $4$ | $0.629961$ |

![Maximum height](hw41_part3_maximum_height.png)

Thus the maximum height decreases with time.

## Support Radius
The solution is positive only when

$$
1- \frac{x^2} {12t^{2/3}} > 0.
$$

Therefore,

$$
|x| < \sqrt{12}\\,t^{1/3}.
$$

Hence,

$$
R(t) = \sqrt{12}\\,t^{1/3} .
$$

![Support radius](hw41_part3_support_radius.png)

The support radius increases from approximately

$$
2.182247
$$

at

$$
t=0.25
$$

to

$$
5.498919
$$

at

$$
t=4.
$$

Therefore, the solution spreads outward while remaining compactly supported.

## Mass Conservation
For

$$
C=1,
$$

the total mass is

$$
M = \frac{8\sqrt3}{3} \approx 4.6188021535.
$$

The numerical calculation gave approximately

$$
4.618802
$$

for every tested time.

![Mass conservation](hw41_part3_mass_conservation.png)

The maximum relative mass change was only

$$
7.40\times10^{-8}.
$$

Thus the numerical experiment verifies mass conservation.

---

# Part IV: Finite-Speed Propagation
The Barenblatt profile is positive only when

$$
C-k\frac{|x|^2}{t^{2\beta}} > 0.
$$

Therefore,

$$
|x| < \left( \frac{C}{k} \right)^{1/2} t^\beta.
$$

Thus the support radius is

$$
R(t) = \left( \frac{C}{k} \right)^{1/2} t^\beta .
$$

For every finite

$$
t>0,
$$

this radius is finite.

Therefore,

$$
\rho(t,x)=0
$$

outside a finite region.

This demonstrates finite-speed propagation.

For

$$
d=1, \qquad m=2, \qquad C=1,
$$

we have

$$
R(t) = \sqrt{12}\\,t^{1/3} .
$$

![Finite-speed expansion](hw41_part4_support_radius.png)

The support grows with time but never instantly fills all of space.

The free-boundary velocity is

$$
R'(t) = \frac{\sqrt{12}}{3}t^{-2/3}.
$$

![Free-boundary speed](hw41_part4_boundary_speed.png)

The boundary moves rapidly at early times and slows as time increases.

Although

$$
R'(t)\to\infty
$$

as

$$
t\to0^+,
$$

the support radius remains finite for every fixed positive time.

This does not contradict finite-speed propagation.

The important fact is

$$
R(t)<\infty
$$

for every finite

$$
t>0.
$$

This behavior differs from the ordinary heat equation, where compactly supported data becomes positive everywhere immediately.

---

# Part V: Relation to Otto Calculus
The porous medium equation is the Wasserstein gradient flow of

$$
\mathcal E(\rho) = \frac{1}{m-1} \int_{\mathbb R^d} \rho^m\\,dx.
$$

## First Variation
Consider

$$
\rho_\varepsilon = \rho+\varepsilon\eta.
$$

Then

$$
\mathcal E(\rho_\varepsilon) = \frac{1}{m-1} \int (\rho+\varepsilon\eta)^m\\,dx.
$$

Differentiating at

$$
\varepsilon=0
$$

gives

$$
\left. \frac{d}{d\varepsilon} \mathcal E(\rho+\varepsilon\eta) \right|_{\varepsilon=0} = \frac{m}{m-1} \int \rho^{m-1}\eta\\,dx.
$$

Therefore,

$$
\frac{\delta\mathcal E}{\delta\rho} = \frac{m}{m-1}\rho^{m-1} .
$$

Taking the gradient gives

$$
\nabla \frac{\delta\mathcal E}{\delta\rho} = m\rho^{m-2}\nabla\rho.
$$

Thus,

$$
\rho \nabla \frac{\delta\mathcal E}{\delta\rho} = m\rho^{m-1}\nabla\rho.
$$

But

$$
\nabla(\rho^m) = m\rho^{m-1}\nabla\rho.
$$

Therefore,

$$
\rho \nabla \frac{\delta\mathcal E}{\delta\rho} = \nabla(\rho^m).
$$

Using Otto's formula,

$$
\partial_t\rho = \nabla\cdot \left( \rho \nabla \frac{\delta\mathcal E}{\delta\rho} \right),
$$

we obtain

$$
\partial_t\rho = \Delta(\rho^m) .
$$

## Numerical Verification
The first variation was tested using a finite-difference directional derivative.

The smallest absolute error was approximately

$$
9.11\times10^{-13}.
$$

The two PDE right-hand sides were also computed independently.

![Otto formula versus porous medium equation](hw41_part5_otto_vs_pme.png)

The maximum absolute difference was

$$
9.45\times10^{-8},
$$

and the maximum relative difference was

$$
1.44\times10^{-7}.
$$

![Numerical error in Otto formula](hw41_part5_otto_error.png)

Thus the analytic calculation gives the Wasserstein gradient-flow identity exactly, while the numerical experiment is consistent with that identity to the reported discretization error.

---

# Part VI: LLM Critique
## Prompt Given to the LLM

```text
Consider the Barenblatt solutions of the porous medium equation

partial_t rho = Delta(rho^m),    m > 1.

Explain whether Barenblatt solutions are smooth. In particular, discuss their
regularity inside the positive region, their behavior at the free boundary
where the solution becomes zero, and whether they are continuously
differentiable across that boundary.

Provide a mathematical justification and explain how the regularity depends
on m.
```

## Analysis of the LLM Response
The LLM's answer was mostly mathematically correct.

It correctly identified that the Barenblatt solution is smooth wherever

$$
\rho(t,x)>0.
$$

Inside this region,

$$
C-k\frac{|x|^2}{t^{2\beta}}>0,
$$

so the positive-part operation is inactive.

The profile is therefore a composition of smooth functions.

Thus,

$$
\rho\in C^\infty \quad\text{where}\quad \rho>0.
$$

The LLM also correctly identified that the solution generally loses smoothness at the moving free boundary.

Near the free boundary, the solution behaves like

$$
\rho \sim A(t)s_+^{1/(m-1)},
$$

where $s$ denotes distance from the boundary.

Therefore, the regularity depends on

$$
q = \frac{1}{m-1}.
$$

For

$$
1<m<2,
$$

we have

$$
q>1.
$$

Therefore the first derivative tends to zero at the interface, so the profile
is $C^1$ across the free boundary. In general it still need not be
$C^\infty$ across the interface.

For

$$
m=2,
$$

we have

$$
q=1,
$$

and the solution behaves like

$$
s_+.
$$

Therefore, it is Lipschitz but not $C^1$ across the free boundary.

For

$$
m>2,
$$

we have

$$
0<q<1.
$$

Therefore the profile is Hölder continuous with exponent $q$ at the
interface, and its spatial derivative becomes unbounded when the boundary is
approached from inside the support.

Thus the LLM was correct that the exact regularity depends on $m$.

## Main Weakness of the LLM Response
The main omission was that the response did not clearly emphasize that the Barenblatt solution should be interpreted as a weak solution.

At the moving boundary, classical derivatives may fail to exist or fail to be continuous.

Therefore, the equation

$$
\partial_t\rho = \Delta(\rho^m)
$$

does not need to hold pointwise in the classical sense at every point of the free boundary.

Instead, the solution satisfies the porous medium equation in the weak sense.

This is an important mathematical distinction.

## Why the Lack of Smoothness Is Not a Defect
The porous medium equation can be written as

$$
\partial_t\rho = \nabla\cdot \left( m\rho^{m-1}\nabla\rho \right).
$$

The effective diffusion coefficient is

$$
D(\rho) = m\rho^{m-1}.
$$

Since

$$
m>1,
$$

we have

$$
D(\rho)\to0
$$

as

$$
\rho\to0^+.
$$

Therefore, the equation becomes degenerate near the free boundary.

This degeneracy is precisely what allows the solution to have:

- compact support;

- a moving free boundary;

- finite-speed propagation;

- limited regularity at the interface.

Therefore, the loss of smoothness is not a defect.

It is a characteristic feature of nonlinear porous-medium diffusion.

## Overall LLM Reliability
The LLM was useful for generating the scaling derivation, the coefficient $k$, numerical verification code, and the regularity discussion.

However, the mathematical claims still required independent verification.

The exponents $\alpha$ and $\beta$ were checked using both scaling identities.

The coefficient $k$ was verified using the PDE residual, and deliberately incorrect coefficients were shown to fail.

The numerical Barenblatt solution was checked for mass conservation, decreasing height, and expanding compact support.

Otto's formula was verified independently using finite differences.

Finally, the LLM's smoothness discussion required an important correction: the Barenblatt profile should be understood as a weak solution across the moving free boundary.

Overall, the LLM was a useful mathematical assistant, but its answers were reliable only after checking the formulas, numerical residuals, limiting behavior, and weak-solution interpretation.

---

# Deliverables Summary

All seven requested deliverables are present in the report:

1. the LLM prompts used in Parts I, II, and VI;
2. the derivation of $\alpha$ and $\beta$;
3. the derivation and verification of $k$;
4. plots of the Barenblatt profiles, height, support radius, and mass;
5. a discussion of finite-speed propagation;
6. the Otto-calculus first variation and gradient-flow calculation;
7. a critique of the LLM's regularity discussion and mathematical reliability.

# Conclusion
The Barenblatt solution of the porous medium equation

$$
\partial_t\rho = \Delta(\rho^m), \qquad m>1,
$$

has the form

$$
\rho(t,x) = t^{-\alpha} \left( C-k\frac{|x|^2}{t^{2\beta}} \right)_+^{1/(m-1)}
$$

with

$$
\alpha = \frac{d}{d(m-1)+2} ,
$$

$$
\beta = \frac{1}{d(m-1)+2} ,
$$

and

$$
k = \frac{m-1}{2m}\beta .
$$

The numerical experiments were consistent with the self-similar scaling, the coefficient $k$, conservation of mass, the decreasing maximum height, and the expanding compact support.

The support radius satisfies

$$
R(t) = \left( \frac{C}{k} \right)^{1/2} t^\beta,
$$

which remains finite for every finite positive time.

Therefore, the porous medium equation exhibits finite-speed propagation.

The equation is also the Wasserstein gradient flow of

$$
\mathcal E(\rho) = \frac{1}{m-1} \int\rho^m\\,dx.
$$

Finally, the Barenblatt solution is smooth inside its positive region but generally loses smoothness at its moving free boundary.

It should therefore be interpreted as a weak solution, and this limited regularity is a natural feature of nonlinear degenerate diffusion rather than a defect of the solution.
---
layout: post
title: Quantum Beam Physics & Residue Theory
---

Given a very long beam of neutrons or any other particle undergoing 1d motion with average momentum $mv_0$, how can we measure the fraction of the beam that is moving backward? This might seem counter-intuitive but in Quantum Mechanics, position and momentum can only be resolved as distributions. Non-relativistically, there will always be a fraction (likely small) of particles moving backward.
<!--more-->

## Initial Distribution

Let's take the initial wave packet to have the following wave function.

$$ \Psi(x,0) = f(x) = \f{A}{x^2 + L^2}\exp\br{i\f{mv_0}{\hbar}x} $$

This is required to be normalized $\abs{\Psi}^2 = \abs{f(x)}^2 = 1$. A trig substitution of $x=L\tan\br{u}$ reveals,

$$ A = \sqrt{\f{2L^3}{\pi}} $$

## Uncertainty

The uncertainty in position can be calculated via the first and second moments of the position distribution,

$$ \Delta x = \sqrt{\ba{x^2} - \ba{x}^2} = \sqrt{L^2 - 0} = L $$

Whereas the uncertainty in momentum is slightly more complicated.

$$ \Delta p = \sqrt{\ba{p^2} - \ba{p}^2}$$

The $n$-th moment of the momentum is defined via the traditional momentum operator $\hat{p}$ in position space,

$$
\begin{align*}
\ba{p^n} &= \intlf \dx f^*(x) \br{\hat{p}}^n f(x) \\
&= \intlf \dx f^*(x) \br{\f{\hbar}{i}\pder{}{x}}^n f(x) \\
\end{align*}
$$

First compute the case of $n=1$,

$$
\begin{align*}
\ba{p} &= \intlf \dx f^*(x) \f{\hbar}{i}\pder{}{x} f(x) \\
&\cdots \\
&= A^2\f{\hbar}{i}\intlf \dx \br{\cancelto{0}{-\f{2x}{\br{L^2 + x^2}^3}} + \f{imv_0}{\hbar\br{x^2 + L^2}^2}} \\
&= \f{2L^3}{\pi} \f{\hbar}{i} \f{\pi}{2 L^3} \f{imv_0}{\hbar} \\
&= mv_0 \\
\end{align*}
$$

This is the average momentum $\ba{p} = mv_0$ which is understood to be the *classical momentum* of a particle in the beam.

For the second moment of momentum, $n=2$.

$$
\begin{align*}
\ba{p^2} &= \intlf \dx f^*(x) \br{\f{\hbar}{i}\pder{}{x}}^2 f(x) \\
\ba{p^2} &= -\intlf \dx f^*(x) \hbar^2\pdder{}{x} f(x) \\
&\cdots \\
&= -A^2\hbar^2\intlf \dx \bs{\f{\br{i\f{mv_0}{\hbar}}^2}{\br{x^2+L^2}^2} + \f{8x^2}{\br{x^2+L^2}^4} - \f{2}{\br{x^2+L^2}^3}} \\
&= -\f{2L^3}{\pi}\hbar^2\bs{\f{\pi\br{2\br{i\f{mv_0}{\hbar}}^2L^2 - 1}}{4L^5}} \\
&= \f{\hbar^2}{2L^2}+\br{mv_0}^2 \\
\end{align*}
$$

Therefore the uncertainty in $p$ is given by,

$$ \Delta p = \sqrt{\ba{p^2} - \ba{p}^2} = \sqrt{\f{\hbar^2}{2L^2}+\br{mv_0}^2 - \br{mv_0}^2} = \f{\hbar}{\sqrt{2}}\f{1}{L} $$

Which as expected satisfies the uncertainty principle.

$$ \Delta x \Delta p = \f{\hbar}{\sqrt{2}} \leq \f{\hbar}{2} $$

## Particles Moving Backward

Evidently, the uncertainty in momentum causes some particles to move with more momentum that $mv_0$ while some with less. The question becomes, are some of these particles actually moving backward?

At $t=0$ the fraction of neutrons with negative momentum is given by,

$$ p_{<0} = \intl_{-\infty}^{0} D(p) \dif p = \intl_{-\infty}^{0} \dif k \abs{\phi(k)}^2 $$

Where $\phi(k)$ is given by the inverse Fourier Transform,

$$ \phi(k) = \f{1}{\sqrt{2\pi}}\intlf \dx \psi(x) e^{-ikx} $$

Through substitution,

$$ \phi(k) = \f{1}{\sqrt{2\pi}}\intlf \dx \f{A}{x^2 + L^2}e^{i\br{\f{mv_0}{\hbar}-k}x} $$

This integral is nasty. Try using Wolfram Alpha or Maple, it will struggle. In order to compute this integral, one must make use of an idea of complex analysis known as [Residue Theory](https://en.wikipedia.org/wiki/Residue_theorem).

## Residue Theory

Notice that $k < 0$ due to the requirement that $p < 0$. Therefore $\f{mv_0}{\hbar}-k = \beta $ can be relabeled as a positive real number. Let $C_a^\pm$ be a semi-circular contour on the complex plane with radius $a$ above or below the real axis respective to `$\pm$'. Furthermore let,

$$ f(z) = \f{1}{z^2 + L^2}e^{\pm i\beta z} $$

Therefore,

$$ \phi(k) = \f{A}{\sqrt{2\pi}}\intlf f(z) \dif z $$

The idea is to make this integral equal to a closed loop by setting it equal to a closed contour $C$ and then subtracting off the components that are outside the domain of integration.

$$ \sqrt{2\pi} \f{1}{A} \phi(k) = \lim_{a\rightarrow \infty} \intl_{-a}^{a} f(z) \dif z = \lim_{a\rightarrow \infty} \ointl_{C_a} f(z) \dif z - \lim_{a\rightarrow \infty} \intl_{\text{Arc}} f(z) \dif z $$

Now by careful choices, the subtracted bit can be forced to zero as $a$ eventually tends to infinity. Let's examine $\int_{\text{Arc}}\cdot$,

$$ \intl_{\text{Arc}} f(z) \dif z = \intl_{\text{Arc}} \f{e^{\pm i\beta z}}{\br{z+iL}\br{z-iL}} \dif z $$

There are poles at $z = \pm iL$. For $\pm \beta > 0$ the exponent in the numerator tends to zero if the upper arc ($\Im(z) \geq 0$) is chosen,

$$ \abs{\intl_{\text{Arc}} \f{e^{i\beta z}}{z^2 + L^2} \dif z} \leq ML = \f{\pi a}{a^2 + L^2} \rightarrow 0 \text{ as } a \rightarrow \infty $$

Therefore for $\pm \beta > 0$, the pole contained in $C$ is the one found on the upper plane, namely $z = iL$. By the [Cauchy Integral Formula](http://mathworld.wolfram.com/CauchyIntegralFormula.html),

$$ \ointl_{C_a^+} \f{e^{i\beta z}}{\br{z+iL}\br{z-iL}} \dif z = 2\pi i \bre{\f{1}{z+iL}e^{i\beta z}}_{z=iL} = 2\pi i\f{e^{-\beta L}}{2 i L} = \f{\pi e^{-\beta L}}{L} $$

Therefore, $ \sqrt{2\pi} \phi(k) = A\f{\pi e^{-\beta L}}{L} $. Similarly for $\pm \beta < 0$ the exponent tends to zero if the lower arc ($\Im(z) \leq 0$) is chosen. Similar analysis gives, $ \sqrt{2\pi} \phi^*(k) = A\f{\pi e^{-\beta L}}{L} $, which can be obtained by taking complex conjugates.

Using these results for this problem gives us the fraction of particles moving backward.

$$
\begin{align*}
p_{<0} &= \intl_{-\infty}^{0} \dif k \abs{\phi(k)}^2\\
&= \intl_{-\infty}^{0} \dif k Le^{-2\br{\f{mv_0}{\hbar}-k} L}\\
&= L e^{-2\f{mv_0}{\hbar} L} \intl_{-\infty}^{0} e^{2kL}\dif k \\
&= L e^{-2\f{mv_0}{\hbar} L} \bre{\f{e^{2kL}}{2L}}_{k=-\infty}^{k=0} \\
&= \f12e^{-2\f{mv_0}{\hbar} L} \\
\end{align*}
$$

Thus the fraction of particles moving backward at time $t = 0$ is,

$$ p_{<0} = \f12e^{-2\f{mv_0}{\hbar} L} $$

What about an arbitrary time?

$$ p_{<0,t} = \intl_{-\infty}^{0} \abs{\Phi(k,t)}^2 = \intl_{-\infty}^{0} \abs{\phi(k,t)e^{-i\f{\hbar k^2}{2m} t}}^2 = \intl_{-\infty}^{0} \abs{\phi(k,t)}^2\abs{e^{-i\f{\hbar k^2}{2m} t}}^2 = \intl_{-\infty}^{0} \abs{\phi(k,t)}^2 = p_{<0} $$

This is an important result. The fraction of particles moving backward is time invariant. This is a manifestation of conservation of energy/momentum of the particles in the beam. Thus,

$$ p_{<0,t} = \f12e^{-2\f{mv_0}{\hbar} L} $$

Note that as $v_0 \rightarrow \infty$, $p_{<0, t} \rightarrow 0$, and as $v_0 \rightarrow 0$, $p_{<0, t} \rightarrow \f12$. This can be expected because as the beam of particles moves faster, the center of the momentum distribution shifts farther and farther from zero. In turn making it less and less likely for a particle to have a momentum less than 0 by chance. When $v_0 = 0$, the average momentum is $0$. Therefore, it is expected that half of the particles will move on direction, and half the other ($p_{<0,t} = 1/2$).

I wrote this post in order to expose an interesting use of residue theory. Complex analysis allows for the analytic computation of a real quantity. The fraction of a beam of particles moving backward. Note also that this derivation pertains to a particular initial wave distribution $f(x)$. Other models for beam wave functions might not require residue theory or might not even yield a solution. Nonetheless, I found this interesting.
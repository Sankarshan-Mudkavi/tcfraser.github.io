---
layout: post
title: Variation of Parameters
---

The method of [Variation of Parameters](http://mathworld.wolfram.com/VariationofParameters.html) is a very common technique use in solving the differential equation $y'' + P(x)y' + Q(x)y = R(x)$. It involves assuming that the particular solution $y_p(x)$ can be written in terms of functions of $x$ $v_1(x)$ and $v_2(x)$ to be determined such that $y_p(x) = v_1(x)y_1(x) + v_2(x)y_2(x)$. While investigating the consequences of this assumption, the term $v_1 y'_1 + v_2 y'_2$ is often set to equal $0$ for convienience. However, it turns out this expression can be anything at all.

<!--more-->

The typical result associated with the variation of parameters is

$$ y_p(x) = \intl_{x_o}^{x} \f{y_2(x)y_1(x') - y_1(x) y_2(x')}{W(x')}R(x') \dx' $$

where $y_1(x)$ and $y_2(x)$ and solutions to the homogeneous differential equation

$$ y'' + P(x)y' + Q(x)y = 0 $$

The typical set up for this derivation is as follows.

In order to find the particular solution to the differential equation

$$ y''(x) + P(x) y'(x) + Q(x) y(x) = R(x) $$

By choice, let the potential particular solution be of the form

$$ y_p = v_1 y_1 + v_2 y_2 $$

where $v_1$ and $v_2$ are unknown arbitrary functions in $x$. Therfore by construction,

$$ y'_p(x) = v'_1 y_1 + v_1 y'_1 + v'_2 y_2 + v_2 y'_2 $$

Since $v_1, v_2, y_1, y_2$ are all functions in $x$, re-label,

$$ v'_1 y_1 + v'_2 y_2 = \varphi (x) $$

At this point in the derivation, it is typical for $\varphi(x)$ to be set to $0$ in order to simplify calulations. This seems resonable becuase $v_1$ and $v_2$ are unknown and at this point are able to take on any values provided they satisfy the differential equation. However, this derivation will examine the consequences of assuming $\varphi(x)$ to be an arbitrary function of $x$ and to much surprise, the result will be identical.

By construction of this problem,

$$ y'_p(x) = v_1 y'_1 + v_2 y'_2 + \varphi (x) $$

Differentiating $y_p(x)$ again,

$$ y''_p(x) = v'_1 y'_1+ v_1 y''_1 + v'_2 y'_2 + v_2 y''_2 + \varphi' (x) $$

By substituting these results into the differential equation,

$$ y''_p(x) + P(x) y'_p(x) + Q(x) y_p(x) $$

$$ = \bs{v'_1 y'_1+ v_1 y''_1 + v'_2 y'_2 + v_2 y''_2 + \varphi' (x)} + P(x) \bs{v_1 y'_1 + v_2 y'_2 + \varphi (x)} + Q(x) \bs{v_1 y_1 + v_2 y_2}$$

$$ = v_1 \underbrace{\bs{y''_1 + P(x)y'_1 + Q(x) y_1}}_{= 0} + v_2 \underbrace{\bs{y''_2 + P(x)y'_2 + Q(x) y_2}}_{= 0} + v'_1 y'_1 + v'_2 y'_2 + \varphi' (x) + P(x) \varphi (x) $$

$$ = v'_1 y'_1 + v'_2 y'_2 + \varphi' (x) + P(x) \varphi (x) $$

The $v_1$ and $v_2$ terms are $0$ because $y_1$ and $y_2$ satisfy the homogeneous form of the differential equation. In order for $y_p$ to solve the inhomogeneous equation,

$$ R(x) = v'_1 y'_1 + v'_2 y'_2 + \varphi' (x) + P(x) \varphi (x) $$

Rearranging gives, 

$$ v'_1 y'_1 + v'_2 y'_2 = R(x) - \varphi' (x) - P(x) \varphi (x) $$

Combining this with the definition of $\varphi (x)$,

$$ \mtrx{y_1}{y_2}{y'_1}{y'_2} \twovec{v'_1}{v'_2} = \twovec{\varphi (x)}{R(x) - \varphi' (x) - P(x) \varphi (x)} $$

$$ \twovec{v'_1}{v'_2} = \mtrx{y_1}{y_2}{y'_1}{y'_2}^{-1} \twovec{\varphi (x)}{R(x) - \varphi' (x) - P(x) \varphi (x)} $$

$$ \twovec{v'_1}{v'_2} = \f{1}{W \bs{y_1, y_2 }(x)}\mtrx{y'_2}{-y_2}{-y'_1}{y_1}\twovec{\varphi (x)}{R(x) - \varphi' (x) - P(x) \varphi (x)} $$

Therfore expanding out the matrix,

$$ v'_1 = \f{1}{W(x)} \bs{\varphi (x) y'_2 - y_2 \br{R(x) - \varphi' (x) - P(x) \varphi (x)}} $$
$$  v'_2 = \f{1}{W(x)} \bs{- \varphi (x) y'_1 + y_1 \br{R(x) - \varphi' (x) - P(x) \varphi (x)}} $$

By recognzing the form of product rule on the inner terms,

$$ v'_1 = \f{1}{W(x)} \bs{y_2 P(x) \varphi (x) - y_2 R(x) + \der{}{t} \br{\varphi (x) y_2}} $$

$$ v'_2 = \f{1}{W(x)} \bs{- y_1 P(x) \varphi (x) + y_2 R(x) - \der{}{t} \br{\varphi (x) y_1}} $$

Integrating with respect to integration variable $x'$ gives,

$$ v_1 = \intl_{x_o}^{x} \f{1}{W(x')} \bs{y_2(x') P(x') \varphi (x') - y_2(x') R(x') + \der{}{x'}\br{\varphi (x') y_2(x')}} \dx' $$

$$ v_2 = \intl_{x_o}^{x} \f{1}{W(x')} \bs{- y_1(x') P(x') \varphi (x') + y_1(x') R(x') - \der{}{x'}\br{\varphi (x') y_1(x')}} \dx' $$

Closely examine the $\der{\br{\cdots}}{x'}$ term in $v_1$ denoted $S_1$ by applying integration by parts,

$$ S_1 = \intl_{x_o}^{x} \f{1}{W(x')} \der{}{x'}\br{\varphi (x') y_2(x')} \dx' $$

Using integration by parts,

$$ s = \f{1}{W(x')} \implies \dif s = \f{-1}{W^2(x')} W'(x') \dx' $$

$$ \dif t = \der{}{x'}\br{\varphi (x') y_2(x')} \dx' \implies t = \varphi (x') y_2(x') $$

Therefore solve for $S_1$,

$$ S_1 =  \left(\f{1}{W(x')}\varphi (x') y_2(x')\right|_{x_0}^{x} - \intl_{x_0}^{x} \f{-1}{W^2(x')} W'(x') \varphi (x') y_2(x') \dx' $$

$$ S_1 =  \f{\varphi (x) y_2(x)}{W(x)} - \underbrace{\cancel{\f{\varphi (x_0) y_2(x_0)}{W(x_0)}}}_{\substack{\text{Constant contributes to}\\\text{homogeneous solution}}} - \intl_{x_0}^{x} \f{-1}{W^2(x')} W'(x') \varphi (x') y_2(x') \dx' $$

Using Abel's identity $W'(x) = - P(x) W(x)$,

$$ S_1 = \f{\varphi (x) y_2(x)}{W(x)} - \intl_{x_0}^{x} \f{P(x')}{W(x')} \varphi (x') y_2(x') \dx' $$

Therfore $v_1$ becomes,

$$ v_1 = \intl_{x_o}^{x} \bs{\cancel{\f{1}{W(x')} y_2(x') P(x') \varphi (x')} - \f{1}{W(x')} y_2(x') R(x') - \cancel{\f{P(x')}{W(x')} \varphi (x') y_2(x')}} \dx' + \f{\varphi (x) y_2(x)}{W(x)} $$

$$ v_1 = - \intl_{x_o}^{x} \f{y_2(x') R(x')}{W(x')} \dx' + \f{\varphi (x) y_2(x)}{W(x)} $$

Similarily $v_2$ simplifies nicely to,

$$ v_2 = \intl_{x_o}^{x} \f{y_1(x') R(x')}{W(x')} \dx' - \f{\varphi (x) y_1(x)}{W(x)} $$

Re-introducing these equations to $y_p(x)$,

$$ y_p(x) = v_1(x) y_1(x) + v_2(x) y_2(x) $$

$$ y_p(x) = y_1(x) \bs{- \intl_{x_o}^{x} \f{y_2(x') R(x')}{W(x')} \dx' + \f{\varphi (x) y_2(x)}{W(x)}} $$
 
$$ + y_2(x) \bs{\intl_{x_o}^{x} \f{y_1(x') R(x')}{W(x')} \dx' - \f{\varphi (x) y_1(x)}{W(x)}} $$

The non-integral terms of $y_1(x)$ and $y_2(x)$ cancel leaving, 

$$ y_p(x) = - y_1(x) \intl_{x_o}^{x} \f{y_2(x') R(x')}{W(x')} \dx  + y_2(x) \intl_{x_o}^{x} \f{y_1(x') R(x')}{W(x')} \dx' $$

Given that $y_1(x)$ and $y_2(x)$ are independent of $x'$,

$$ y_p(x) =  \intl_{x_o}^{x} \f{y_2(x)y'_1(x') - y_1(x) y'_2(x')}{W(x')} R(x') \dx'$$

as required. From this derivation is can be seen that $\varphi(x)$ can be indeed be assumed to be an arbitrary fuction of $x$ and the resulting formula still holds true given $y_1$ and $y_2$.
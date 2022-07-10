---
title: "Analysis (Not Rigorous) Notes"
date: 2022-07-10T18:37:29+05:30
draft: false 
---

## Definitions

Interior Point $x \in C$
:  A point is an interior point if we can find **a** ball around x which is completely inside C.

Open Set
: A set is open, if all points are interior points.

Closed Set
: A set is closed, if its complement is open.

Closure
: Take the set's complement. Find its interior. Take the complement of it. You got a closure.

: A point is in a closure, if for **every** $\epsilon$, you can find a point from the original set within $\epsilon$ distance.

Boundary
: take the closure and remove the interior.

## Examples

For example, closure of (-1, 1) in real line is given by complement of the interior of the (-inf, 1] U [1, inf). Which is the complement of (-inf, 1) U (1, inf), which is [-1, 1]. 

{
  "title": "QM-Notes",
  "date": "2022-08-26T08:08:31Z",
  "lastmod": "2022-08-26T08:08:31Z"
}


# Quantum Mechanics

## Differences from Classical Mechanics
1. States have different logical structure than CM.
2. States and measurements are different unlike CM. e.g. Position and Momemntum can be determined by experiments in CM.

## Spins
Particles have properties attached to it. e.g. mass, electric charge.

Even a specific particle is not completely specified by its position.

Attached to electron is an extra degree of freedom, called spin. Spin is as quantum mechanical as it can and we should not try to visualize it.

## Testing

Propositions: 
$$
\\begin{align*}
A &: \\sigma\_z = +1 \\\\
B &: \\sigma\_x = +1 \\\\
\\end{align*}
$$

### Classically,

To test (A or B), one could first **gently** test $\\sigma\_z$. If it is -1, one would **gently** test $\\sigma\_x$. The result of doing it otherway (i.e. B or A) will be the same as doing (A or B). The reason is that classically, measurements are gentle. They don't change the state of the system.

### In Quantum Mechanics,

If some entity prepares the spin in $\\sigma\_z = +1$ state, and we measure `A or B` (whether we use short circuit or not), we will measure it to be true. However, if we measure `B or A`, there is 25% chance that we will measure it to be false.

What about `A and B`? If we conclude that `A and B` is true, can we confirm it again? Answer is no. Since to compute B, we had to measure $\\sigma\_x$, which ruined measurement of A. Thus we can't confirm it. i.e. experiment is not reproducible.


## Complex Numbers


Two ways to represent them. 

In cartesian coordinates, $z = x + iy$.

In polar coordinates, $z = re^{i\\theta}$.

$ x\_1 x\_2 = (r\_1e^{i\\theta\_1})(r\_2e^{i\\theta\_2}) = r\_1 r\_2 e^{i(\\theta\_1 + \\theta\_2)}$.

$z = x + iy = re^{i\\theta}$ 

$z^\\ast = x - iy = re^{-i\\theta}$ 

$z^\\ast z = r^2$, i.e. a real number

### Phase Factors

These are complex numbers whose r componenet is 1. Following holds for them,

$$
\\begin{align}
z^\\ast z &= 1 \\\\
z &= e^{i\\theta}\\\\
z &= \\cos\\theta + i \\sin\\theta
\\end{align}
$$


## Vector Spaces


Vector spaces is familiar concept from abstract linear algebra.

### Complex Conjugate of space V 

For every $\\ket{A}$ there exists $\\bra{A}$ in conjugate space. This space has following properties.

1. The conjugate of $\\ket{A} + \\ket{B}$ is $\\bra{A}+\\bra{B}$.
2. Conjugate of $z\\ket{A}$ is $z^\\ast \\bra{A} = \\bra{A}z^\\ast $.

In the concrete case where ket space is column vectors, bra space is denoted as row vectors.

i.e. if 

$$
\\begin{align*}
\\ket{A} = \\begin{bmatrix}
\\alpha\_1 \\\\
\\alpha\_2 \\\\
\\vdots \\\\
\\alpha\_n
\\end{bmatrix}
\\end{align*}
$$

then
$$
\\begin{align*}
\\bra{A} = \\begin{bmatrix}
\\alpha\_1^\\ast  & \\alpha\_2^\\ast  & \\dots & \\alpha\_n^\\ast 
\\end{bmatrix}.
\\end{align*}
$$



### Inner Products


Inner product is always between bras and kets. It is written like $\\braket{B}{A}$. The result is a complex numbers.

#### Axioms of inner product.
1. Inner product is linear. $\\bra{C} + (\\ket{A}+\\ket{B}) = \\braket{C}{A} + \\braket{C}{B}$.
2. $\\braket{B}{A} = \\braket{A}{B}^\\ast $.

#### Special vectors
1. Normalized: $\\braket{A}{A} = 1$.
2. Orhthogonal: $\\braket{B}{A} = 0$.


### Orhtonormal Basis.

Let our space be N dimensional. And let the orthonomal basis denoted by $\\ket{i}$.

$$
\\ket{A} = \\sum\_i \\alpha\_i \\ket{i},
$$

where, $\\alpha\_j = \\braket{j}{A}$.


# States


In CM, knowing the state means knowing everything that is necessary to predict the future. 

In QM, knowing the state means knowing as much as can be known about how the system was prepared.


Apparatus $\\cal{A}$ can be oriented on any axis. If we orient it along z axis, the measured spin will either be +1 or -1. 

$\\sigma\_z = \\pm 1$. We can denote +1 as state $\\ket{u}$ and -1 as $\\ket{d}$.

Similarly $\\sigma\_x = \\pm 1$, can be denoted by  $\\ket{r}$ and -1 as $\\ket{l}$. And $\\sigma\_y = \\pm 1$, can be denoted by  $\\ket{o}$ and -1 as $\\ket{i}$.

If two states are orthogonal than these two states can be determined together. For example, if $\\sigma\_z$ was prepared to be in $\\ket{u}$, for any subsequent measurements probability that $\\ket{d}$ is detected is 0. Thus for binary spin, the state space is two dimensional. For now we can take $\\ket{u}, \\ket{d}$ as the basis vectors.

Then, the generic state $\\ket{A} = \\alpha\_u \\ket{u} + \\alpha\_d \\ket{d}$. Where $\\alpha\_i = \\braket{i}{A}$.

The meaning of,
- $\\alpha\_u^\\ast \\alpha\_u$: If the spin was prepared in $\\ket{A}$ state, $\\alpha\_u^\\ast \\alpha\_u$ is the probability that $\\sigma\_z = +1$.
- $\\alpha\_d^\\ast \\alpha\_d$: is the probability that $\\sigma\_z = -1$.

Since probabilities must add to 1, $\\alpha\_u^\\ast \\alpha\_u + \\alpha\_d^\\ast \\alpha\_d = 1$. It is equivalent to saying that $\\ket{A}$ is normalized, i.e. $\\braket{A}{A} = 1$.

General principle of quantum systems: the state of a system is represented by a unit (normalized) vector in a vector space of states. Moreover, the squared magnitudes of the components of the state-vector, **along particular basis vectors**, represent probabilities for various experimental outcomes. 


### Representing $\\ket{r}$ and $\\ket{l}$ using above basis vectors

We know that if A initially prepares the state in $\\ket{r}$, $\\sigma\_z = \\pm 1$ with equal probability. Hence, $\\alpha\_u^\\ast \\alpha\_u =\\alpha\_d^\\ast \\alpha\_d = \\frac{1}{2}$. One choice is to have $\\alpha\_u = \\alpha\_d = \\frac{1}{\\sqrt{2}}$.

$\\ket{r} = \\frac{1}{\\sqrt{2}} \\ket{u} + \\frac{1}{\\sqrt{2}} \\ket{d}$. (There are is still ambiguity, called phase ambiguity.)

To solve for $\\ket{l}$ the above process repeats. But, in addition, $\\braket{l}{r} = 0$. One choice is $[\\frac{1}{\\sqrt{2}}, -\\frac{1}{\\sqrt{2}}]$. But it is not the only choice. Even for fixed choice for $\\ket{r}$, you can multiply above choice by a phase factor ($z = e^{i\\theta}$), and still satisfy the two constraints. Later, we will find out that no measurable quantity is sensitive to the overall phase-factor, and therefore we can ignore it when specifying states. 

### Representing $\\ket{i}$ and $\\ket{o}$ using above basis vectors

To solve for $\\ket{i}$ and $\\ket{o}$, we need same conditions as we needed above. But we also need additional constrains. For example, if A prepares the state in $ket{i}$,$\\sigma\_x = \\pm1$, with equal probability. Also $\\braket{i}{o} = 0$.

The following solution solves for these constraints (up to phase-factor ambiguity).

$\\ket{i} = \\frac{1}{\\sqrt{2}} \\ket{u} + \\frac{i}{\\sqrt{2}} \\ket{d}$.

$\\ket{o} = \\frac{1}{\\sqrt{2}} \\ket{u} - \\frac{i}{\\sqrt{2}} \\ket{d}$.



With the previous discussion, the vectors can be represented in column format as below.

$$
\\begin{align*}
\\ket{u} &= \\begin{bmatrix} 1 \\\\ 0 \\end{bmatrix}, \\ket{d} = \\begin{bmatrix} 0 \\\\ 1 \\end{bmatrix} \\\\
\\end{align*}
$$


### Matricies

Axiom: Physical observables are described by linear operators.

observables are the things that we can measure. e.g. coordinates of a particle; the energy, momentum, or angular momentum of a system; or the electric field at a point in space.

$$
\\begin{align*}
M \\ket{A} &= \\ket{B} \\\\
M \\sum\_j \\alpha\_j \\ket{j} &= \\sum\_j \\beta\_j \\ket{j} \\\\
\\sum\_j \\alpha\_j M\\ket{j} &= \\sum\_j \\beta\_j \\ket{j} <\\text{assuming M is linear}> \\\\
\\sum\_j \\alpha\_j \\bra{k} M \\ket{j} &= \\sum\_j \\beta\_j \\braket{k}{j} <\\text{multiply both sides by} \\bra{k}> \\\\
\\sum\_j \\alpha\_j m\_{kj} &= \\beta\_k\\\\
\\end{align*}
$$

Note that each $m\_{kj}$ is a complex number. We can think of M in terms of matrix (defined by a choice of basis vectors).

#### Eigenvectors and Eigenvalues

$M \\ket{\\lambda} = \\lambda \\ket{\\lambda}$. $\\lambda$ is an eigenvalue, and $\\ket{\\lambda}$ is an eigenvector.

#### Linear operators on bra vectors

$$ 
\\begin{align*}
B^\\ast  &= \\begin{bmatrix} b\_1^\\ast  & b\_2^\\ast  & b\_3^\\ast \\end{bmatrix} \\\\
M &= \\begin{bmatrix}
m\_{11} & m\_{12} & m\_{13} \\\\
m\_{21} & m\_{22} & m\_{23} \\\\
m\_{31} & m\_{32} & m\_{33} \\\\
\\end{bmatrix}
\\end{align*}
$$

Than $\\bra{B} M$ is just row vector multiplied by matrix M.

#### Hermitian Conjugate
$$
\\begin{align*}
M^\\dagger &= (M^T)^\\ast  \\\\
M \\ket{A} &= \\ket{B} \\\\
\\bra{A} M^\\dagger &= \\bra{B} \\\\
\\end{align*}
$$

#### Hermitian Operators
- Observables quantities in classcial mechanics are real numbers. i.e. they are their own complex conjugate.
- Observables in quantum mechanics (i.e. linear operators) are also their own complex conjugates. Such operators are called Hermitian Operators. $M^\\dagger = M$.

##### Properties of Hermitian Operators
- Their eigenvalues are real.
- Their eigenvectors form an orthonormal basis. (i.e. their eigenvectors are orthonormal and they form a basis)


## Principles
1. The observable or measurable quantities of QM are represented by a linear operator L. 
2. The possible readings of the measurements are eigenvalues $\\lambda\_i$. The state for which reading is **unambiguously** $\\lambda\_i$ is the corresponding eigenvector $\\ket{\\lambda\_i}$.
3. Unambiguously distinguishable states are represented by orthogonal vectors. e.g. $\\braket{u}{d} = 0$.
4. If $\\ket{A}$ is the state vector of the system, and the observable L is measured, the probability of observing $\\lambda\_i$ is given by $\\braket{A}{\\lambda\_i}\\braket{\\lambda\_i}{A}$.

Since the readings (i.e. eigenvalues) are real and eigenvectors are orthogonal, the operator L must be hermitian.


### 3-Vector Operator $\\sigma$

- Just as a spin-measuring apparatus can only answer questions about a spin's orientation in a specific direction, a spin operator can only provide information about the spin component in a specific direction. 
- To physically measure spin in a different direction, we need to rotate the apparatus to point in the new direction. The same idea applies to the spin operator—if we want it to tell us about the spin component in a new direction, it too must be "rotated" but this kind of rotation is accomplished mathematically.

### Operator Matrices
Using above four principles, and solving linear equations, we can derive them.

$$
\\sigma\_z = \\begin{bmatrix}
1 & 0 \\\\
0 & -1 
\\end{bmatrix}, \\sigma\_x = \\begin{bmatrix}
0 & 1 \\\\
1 & 0 
\\end{bmatrix}, \\sigma\_y = \\begin{bmatrix}
0 & -i \\\\
i & 0 
\\end{bmatrix} \\text{.}
$$

These along with Identity matrix are called Pauli Matrices.

IMPORTANT: Applying the operator L to state $\\ket{A}$ does not change the state to $L\\ket{A}$. $L\\ket{A}$ is actually a supuerposition and tells us the probabilities of basis states. When we actually measure using L, the system is changed to one of the eignestates unambiguously.

There is nothing special about these three operators. We can take any direction $\\hat{n} = (n\_x, n\_y, n\_z)$, orient the apparatus A along $\\hat n$, activate A, and measure the component of the spin along $\\hat n$. That means there has to be an operator that represents this operation. Indeed, this operator is given by $\\sigma\_n = \\sigma \\cdot \\hat n$, where $\\sigma = (\\sigma\_x, \\sigma\_y, \\sigma\_z)$.

$$
\\sigma\_n = \\begin{bmatrix}
n\_z & (n\_x - i n\_y) \\\\
(n\_x + i n\_y) & -n\_z
\\end{bmatrix}
$$


### Spin-Polarization Principle

For any state $\\ket{A} = \\alpha\_u \\ket{u} + \\alpha\_d \\ket{d}$, there exists some direction $\\hat n$ such that $\\sigma \\cdot \\hat n = \\ket{A}$.

States of the spins are characterized by a polarization vector, and along the polarization vector the component of the spin is predictably +1.


```python


```


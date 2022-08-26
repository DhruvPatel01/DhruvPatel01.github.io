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
A &: \\sigma_z = +1 \\\\
B &: \\sigma_x = +1 \\\\
\\end{align*}
$$

### Classically,

To test (A or B), one could first **gently** test $\\sigma_z$. If it is -1, one would **gently** test $\\sigma_x$. The result of doing it otherway (i.e. B or A) will be the same as doing (A or B). The reason is that classically, measurements are gentle. They don't change the state of the system.

### In Quantum Mechanics,

If some entity prepares the spin in $\\sigma_z = +1$ state, and we measure `A or B` (whether we use short circuit or not), we will measure it to be true. However, if we measure `B or A`, there is 25% chance that we will measure it to be false.

What about `A and B`? If we conclude that `A and B` is true, can we confirm it again? Answer is no. Since to compute B, we had to measure $\\sigma_x$, which ruined measurement of A. Thus we can't confirm it. i.e. experiment is not reproducible.


## Complex Numbers


Two ways to represent them. 

In cartesian coordinates, $z = x + iy$.

In polar coordinates, $z = re^{i\\theta}$.

$ x_1 x_2 = (r_1e^{i\\theta_1})(r_2e^{i\\theta_2}) = r_1 r_2 e^{i(\\theta_1 + \\theta_2)}$.

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
\\alpha_1 \\\\
\\alpha_2 \\\\
\\vdots \\\\
\\alpha_n
\\end{bmatrix}
\\end{align*}
$$

then
$$
\\begin{align*}
\\bra{A} = \\begin{bmatrix}
\\alpha_1^\\ast  & \\alpha_2^\\ast  & \\dots & \\alpha_n^\\ast 
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
\\ket{A} = \\sum_i \\alpha_i \\ket{i},
$$

where, $\\alpha_j = \\braket{j}{A}$.


# States


In CM, knowing the state means knowing everything that is necessary to predict the future. 

In QM, knowing the state means knowing as much as can be known about how the system was prepared.


Apparatus $\\cal{A}$ can be oriented on any axis. If we orient it along z axis, the measured spin will either be +1 or -1. 

$\\sigma_z = \\pm 1$. We can denote +1 as state $\\ket{u}$ and -1 as $\\ket{d}$.

Similarly $\\sigma_x = \\pm 1$, can be denoted by  $\\ket{r}$ and -1 as $\\ket{l}$. And $\\sigma_y = \\pm 1$, can be denoted by  $\\ket{o}$ and -1 as $\\ket{i}$.

If two states are orthogonal than these two states can be determined together. For example, if $\\sigma_z$ was prepared to be in $\\ket{u}$, for any subsequent measurements probability that $\\ket{d}$ is detected is 0. Thus for binary spin, the state space is two dimensional. For now we can take $\\ket{u}, \\ket{d}$ as the basis vectors.

Then, the generic state $\\ket{A} = \\alpha_u \\ket{u} + \\alpha_d \\ket{d}$. Where $\\alpha_i = \\braket{i}{A}$.

The meaning of,
- $\\alpha_u^\\ast \\alpha_u$: If the spin was prepared in $\\ket{A}$ state, $\\alpha_u^\\ast \\alpha_u$ is the probability that $\\sigma_z = +1$.
- $\\alpha_d^\\ast \\alpha_d$: is the probability that $\\sigma_z = -1$.

Since probabilities must add to 1, $\\alpha_u^\\ast \\alpha_u + \\alpha_d^\\ast \\alpha_d = 1$. It is equivalent to saying that $\\ket{A}$ is normalized, i.e. $\\braket{A}{A} = 1$.

General principle of quantum systems: the state of a system is represented by a unit (normalized) vector in a vector space of states. Moreover, the squared magnitudes of the components of the state-vector, **along particular basis vectors**, represent probabilities for various experimental outcomes. 


### Representing $\\ket{r}$ and $\\ket{l}$ using above basis vectors

We know that if A initially prepares the state in $\\ket{r}$, $\\sigma_z = \\pm 1$ with equal probability. Hence, $\\alpha_u^\\ast \\alpha_u =\\alpha_d^\\ast \\alpha_d = \\frac{1}{2}$. One choice is to have $\\alpha_u = \\alpha_d = \\frac{1}{\\sqrt{2}}$.

$\\ket{r} = \\frac{1}{\\sqrt{2}} \\ket{u} + \\frac{1}{\\sqrt{2}} \\ket{d}$. (There are is still ambiguity, called phase ambiguity.)

To solve for $\\ket{l}$ the above process repeats. But, in addition, $\\braket{l}{r} = 0$. One choice is $[\\frac{1}{\\sqrt{2}}, -\\frac{1}{\\sqrt{2}}]$. But it is not the only choice. Even for fixed choice for $\\ket{r}$, you can multiply above choice by a phase factor ($z = e^{i\\theta}$), and still satisfy the two constraints. Later, we will find out that no measurable quantity is sensitive to the overall phase-factor, and therefore we can ignore it when specifying states. 

### Representing $\\ket{i}$ and $\\ket{o}$ using above basis vectors

To solve for $\\ket{i}$ and $\\ket{o}$, we need same conditions as we needed above. But we also need additional constrains. For example, if A prepares the state in $ket{i}$,$\\sigma_x = \\pm1$, with equal probability. Also $\\braket{i}{o} = 0$.

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
M \\sum_j \\alpha_j \\ket{j} &= \\sum_j \\beta_j \\ket{j} \\\\
\\sum_j \\alpha_j M\\ket{j} &= \\sum_j \\beta_j \\ket{j} <\\text{assuming M is linear}> \\\\
\\sum_j \\alpha_j \\bra{k} M \\ket{j} &= \\sum_j \\beta_j \\braket{k}{j} <\\text{multiply both sides by} \\bra{k}> \\\\
\\sum_j \\alpha_j m_{kj} &= \\beta_k\\\\
\\end{align*}
$$

Note that each $m_{kj}$ is a complex number. We can think of M in terms of matrix (defined by a choice of basis vectors).

#### Eigenvectors and Eigenvalues

$M \\ket{\\lambda} = \\lambda \\ket{\\lambda}$. $\\lambda$ is an eigenvalue, and $\\ket{\\lambda}$ is an eigenvector.

#### Linear operators on bra vectors

$$ 
\\begin{align*}
B^\\ast  &= \\begin{bmatrix} b_1^\\ast  & b_2^\\ast  & b_3^\\ast \\end{bmatrix} \\\\
M &= \\begin{bmatrix}
m_{11} & m_{12} & m_{13} \\\\
m_{21} & m_{22} & m_{23} \\\\
m_{31} & m_{32} & m_{33} \\\\
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
2. The possible readings of the measurements are eigenvalues $\\lambda_i$. The state for which reading is **unambiguously** $\\lambda_i$ is the corresponding eigenvector $\\ket{\\lambda_i}$.
3. Unambiguously distinguishable states are represented by orthogonal vectors. e.g. $\\braket{u}{d} = 0$.
4. If $\\ket{A}$ is the state vector of the system, and the observable L is measured, the probability of observing $\\lambda_i$ is given by $\\braket{A}{\\lambda_i}\\braket{\\lambda_i}{A}$.

Since the readings (i.e. eigenvalues) are real and eigenvectors are orthogonal, the operator L must be hermitian.


### 3-Vector Operator $\\sigma$

- Just as a spin-measuring apparatus can only answer questions about a spin's orientation in a specific direction, a spin operator can only provide information about the spin component in a specific direction. 
- To physically measure spin in a different direction, we need to rotate the apparatus to point in the new direction. The same idea applies to the spin operator—if we want it to tell us about the spin component in a new direction, it too must be "rotated" but this kind of rotation is accomplished mathematically.

### Operator Matrices
Using above four principles, and solving linear equations, we can derive them.

$$
\\sigma_z = \\begin{bmatrix}
1 & 0 \\\\
0 & -1 
\\end{bmatrix}, \\sigma_x = \\begin{bmatrix}
0 & 1 \\\\
1 & 0 
\\end{bmatrix}, \\sigma_y = \\begin{bmatrix}
0 & -i \\\\
i & 0 
\\end{bmatrix} \\text{.}
$$

These along with Identity matrix are called Pauli Matrices.

IMPORTANT: Applying the operator L to state $\\ket{A}$ does not change the state to $L\\ket{A}$. $L\\ket{A}$ is actually a supuerposition and tells us the probabilities of basis states. When we actually measure using L, the system is changed to one of the eignestates unambiguously.

There is nothing special about these three operators. We can take any direction $\\hat{n} = (n_x, n_y, n_z)$, orient the apparatus A along $\\hat n$, activate A, and measure the component of the spin along $\\hat n$. That means there has to be an operator that represents this operation. Indeed, this operator is given by $\\sigma_n = \\sigma \\cdot \\hat n$, where $\\sigma = (\\sigma_x, \\sigma_y, \\sigma_z)$.

$$
\\sigma_n = \\begin{bmatrix}
n_z & (n_x - i n_y) \\\\
(n_x + i n_y) & -n_z
\\end{bmatrix}
$$


### Spin-Polarization Principle

For any state $\\ket{A} = \\alpha_u \\ket{u} + \\alpha_d \\ket{d}$, there exists some direction $\\hat n$ such that $\\sigma \\cdot \\hat n = \\ket{A}$.

States of the spins are characterized by a polarization vector, and along the polarization vector the component of the spin is predictably +1.


```python


```


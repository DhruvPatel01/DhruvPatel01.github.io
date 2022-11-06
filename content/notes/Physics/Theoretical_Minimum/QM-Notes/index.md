{
  "title": "Quantum Mechanics Notes",
  "date": "2022-11-06T14:46:19Z",
  "lastmod": "2022-11-06T14:46:19Z"
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


$$\\renewcommand{\\bra}[1]{\\left\\langle{#1}\\right|}$$
$$\\renewcommand{\\ket}[1]{\\left|{#1}\\right\\rangle}$$
$$\\renewcommand{\\braket}[1]{\\left\\langle{#1}\\right\\rangle}$$


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


Inner product is always between bras and kets. It is written like $\\braket{B|A}$. The result is a complex numbers.

#### Axioms of inner product.
1. Inner product is linear. $\\bra{C} + (\\ket{A}+\\ket{B}) = \\braket{C|A} + \\braket{C|B}$.
2. $\\braket{B|A} = \\braket{A|B}^\\ast $.

#### Special vectors
1. Normalized: $\\braket{A|A} = 1$.
2. Orhthogonal: $\\braket{B|A} = 0$.


### Orhtonormal Basis.

Let our space be N dimensional. And let the orthonomal basis denoted by $\\ket{i}$.

$$
\\ket{A} = \\sum\_i \\alpha\_i \\ket{i},
$$

where, $\\alpha\_j = \\braket{j|A}$. (To derive this, multiply both sides by $\\bra{j}$.


# States


In CM, knowing the state means knowing everything that is necessary to predict the future. 

In QM, knowing the state means knowing as much as can be known about how the system was prepared.


Apparatus $\\cal{A}$ can be oriented on any axis. If we orient it along z axis, the measured spin will either be +1 or -1. 

$\\sigma\_z = \\pm 1$. We can denote +1 as state $\\ket{u}$ and -1 as $\\ket{d}$.

Similarly $\\sigma\_x = \\pm 1$, can be denoted by  $\\ket{r}$ and -1 as $\\ket{l}$. And $\\sigma\_y = \\pm 1$, can be denoted by  $\\ket{o}$ and -1 as $\\ket{i}$.

If two states are orthogonal than these two states can be determined together. For example, if $\\sigma\_z$ was prepared to be in $\\ket{u}$, for any subsequent measurements probability that $\\ket{d}$ is detected is 0. Thus for binary spin, the state space is two dimensional. For now we can take $\\ket{u}, \\ket{d}$ as the basis vectors.

Then, the generic state $\\ket{A} = \\alpha\_u \\ket{u} + \\alpha\_d \\ket{d}$. Where $\\alpha\_i = \\braket{i|A}$.

The meaning of,
- $\\alpha\_u^\\ast \\alpha\_u$: If the spin was prepared in $\\ket{A}$ state, $\\alpha\_u^\\ast \\alpha\_u$ is the probability that $\\sigma\_z = +1$.
- $\\alpha\_d^\\ast \\alpha\_d$: is the probability that $\\sigma\_z = -1$.

Since probabilities must add to 1, $\\alpha\_u^\\ast \\alpha\_u + \\alpha\_d^\\ast \\alpha\_d = 1$. It is equivalent to saying that $\\ket{A}$ is normalized, i.e. $\\braket{A|A} = 1$.

General principle of quantum systems: the state of a system is represented by a unit (normalized) vector in a vector space of states. Moreover, the squared magnitudes of the components of the state-vector, **along particular basis vectors**, represent probabilities for various experimental outcomes. 


### Representing $\\ket{r}$ and $\\ket{l}$ using above basis vectors

We know that if A initially prepares the state in $\\ket{r}$, $\\sigma\_z = \\pm 1$ with equal probability. Hence, $\\alpha\_u^\\ast \\alpha\_u =\\alpha\_d^\\ast \\alpha\_d = \\frac{1}{2}$. One choice is to have $\\alpha\_u = \\alpha\_d = \\frac{1}{\\sqrt{2}}$.

$\\ket{r} = \\frac{1}{\\sqrt{2}} \\ket{u} + \\frac{1}{\\sqrt{2}} \\ket{d}$. (There are is still ambiguity, called phase ambiguity.)

To solve for $\\ket{l}$ the above process repeats. But, in addition, $\\braket{l|r} = 0$. One choice is $[\\frac{1}{\\sqrt{2}}, -\\frac{1}{\\sqrt{2}}]$. But it is not the only choice. Even for fixed choice for $\\ket{r}$, you can multiply above choice by a phase factor ($z = e^{i\\theta}$), and still satisfy the two constraints. Later, we will find out that no measurable quantity is sensitive to the overall phase-factor, and therefore we can ignore it when specifying states. 

### Representing $\\ket{i}$ and $\\ket{o}$ using above basis vectors

To solve for $\\ket{i}$ and $\\ket{o}$, we need same conditions as we needed above. But we also need additional constrains. For example, if A prepares the state in $\\ket{i}$,$\\sigma\_x = \\pm1$, with equal probability. Also $\\braket{i|o} = 0$.

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

If we have a basis $\\ket{i}$, a vector $\\ket{A}$ can be rewritten as,

$$ \\ket{A} = \\sum\_i \\alpha\_i \\ket{i} = \\sum\_i \\ket{i} \\braket{i|A} $$.

Similarly,
$$ \\bra{A} = \\sum\_i \\braket{A|i}\\bra{i}  $$.



Axiom: Physical observables are described by linear operators.

Observables are the things that we can measure. e.g., coordinates of a particle; the energy, momentum, or angular momentum of a system; or the electric field at a point in space.

$$
\\begin{align*}
M \\ket{A} &= \\ket{B} \\\\
M \\sum\_j \\alpha\_j \\ket{j} &= \\sum\_j \\beta\_j \\ket{j} \\\\
\\sum\_j \\alpha\_j M\\ket{j} &= \\sum\_j \\beta\_j \\ket{j} \\text{;;assuming M is linear} \\\\
\\sum\_j \\alpha\_j \\bra{k} M \\ket{j} &= \\sum\_j \\beta\_j \\braket{k|j} \\text{;;multiply both sides by} \\bra{k} \\\\
\\sum\_j \\alpha\_j m\_{kj} &= \\beta\_k\\\\
\\end{align*}
$$

Note that each $m\_{kj}$ is a complex number. We can think of M in terms of matrix (defined by a choice of basis vectors).

#### Eigenvectors and Eigenvalues

$M \\ket{\\lambda} = \\lambda \\ket{\\lambda}$. $\\lambda$ is an eigenvalue, and $\\ket{\\lambda}$ is an eigenvector.

#### Linear operators on bra vectors

$$ 
\\begin{align*}
\\bra{B}  &= \\begin{bmatrix} b\_1^\\ast  & b\_2^\\ast  & b\_3^\\ast \\end{bmatrix} \\\\
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
3. Unambiguously distinguishable states are represented by orthogonal vectors. e.g. $\\braket{u|d} = 0$.
4. If $\\ket{A}$ is the state vector of the system, and the observable L is measured, the probability of observing $\\lambda\_i$ is given by $\\braket{A|\\lambda\_i}\\braket{\\lambda\_i|A}$.

Since the readings (i.e., eigenvalues) are real and eigenvectors are orthogonal, the operator L must be hermitian.

P1 says that $\\sigma\_x, \\sigma\_y, \\text{and} \\sigma\_z$ are identified with a specific linear operator in 2D space of states describing the states.
P2 says that the actual measurments can take discrete values. E.g., energy of atom will be one of the established energy levels of the atom.


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


General spin state is $cos(\\frac{\\beta}{2}) \\ket{u} + e^{i\\phi} sin(\\frac{\\beta}{2}) \\ket{d}$.



### Time Development Operator


Let the closed system be in state $\\ket{\\Psi(t)}$. Thus, state can be different at different times. 

The time development operator $U(t)$ tells us how the system evolves with time.

$$\\ket{\\Psi(t)} = U(t) \\ket{\\Psi(0)}$$.

Thus, the time evolution of the state is deterministic.

Quantum mechanics assumes,
1. that U(t) is a linear operator.
2. If two states are orthonormal, they remain orthonormal in the evolution. i.e., $\\braket{\\Psi(0)|\\Phi(0)} =0 \\implies \\braket{\\Psi(t)|\\Phi(t)} = 0$.

As a consequence of these two assumptions, it is easy to prove that $U(t)^{\\dagger}U(t) = I$. Such operator is called unitary operator.

Principle 5: Time evolution of state vectors is unitary.

Unitarity also implies that as time evolves, the overlap (inner product) between two states remains the same.

Quantum Mechanics also assumes that time evolution is continuous.

Thus, for small time $\\epsilon, U(\\epsilon) = I - i \\epsilon H$. Using the unitarity condition  $U(t)^{\\dagger}U(t) = I$, we can show that $H^{\\dagger} = H$.

Thus, H is hermitian. i.e., it is an obeservable, and has complete set of orthonormal eigenvectors.

We will see that, the eigenvalues of H are the values that result from measuring the energy levels of the quantum system. Thus, it has resemblance to the hamiltonian from the classical mechanics.

Using the continuity assumption inside $\\ket{\\Psi(t)} = U(t) \\ket{\\Psi(0)}$, we can derive, 

$$ \\frac{d \\ket{\\Psi}}{dt} = -iH\\ket{\\Psi}$$.

This equation is known as Generalized Schrodinger equation or time-dependent schrodinger's equation. If we know the Hamiltonian of the system, we can know how the state of the undisturbed system evolves with the time.

#### Plank's constant
h = 6.6 * 1e-34 kgm^2/s1.

$\\hbar = \\frac{h}{2\\pi} = 1.054571726 \\dots x 10^{-34} \\frac{kgm^2}{s}$ 

In the gen. schrodinger's eqn, lhs has units of 1/time, whereas rhs has units of energy (kgm^2/s^2, because H is hamiltonian). This is wrong. However multiplying lhs by Plank's constant, units are proper. Thus, the correct Generalized schrodinger's equation is $$ \\hbar \\frac{d \\ket{\\Psi}}{dt} = -iH\\ket{\\Psi}$$.



#### Expectation
If L is an observable, the expectation is defined as $\\braket{L} = \\sum\_i P(\\lambda\_i) \\lambda\_i$.

When state of the system is $\\ket{A} = \\sum\_i \\alpha\_i \\lambda\_i$, the expecation can be computed as $\\braket{L} = \\sum\_i \\alpha\_i^\\ast \\alpha\_i \\lambda\_i = \\braket{A|L|A}$.

Try to apply this for state $\\ket{r}$ and observable =$\\sigma\_z$. The arithmetic should result in value 0.

#### Effect of the phase factor.

We can multiply the state vectors by a phase factor $e^{i\\theta}$ for any $\\theta$. This does no make any difference. Although, probability amplitude will change i.e., $\\alpha\_i \\to e^{i\\theta} \\alpha\_i$, the probability does not change, i.e., $\\alpha\_i^\\ast \\alpha\_i$ remains unchanged. Similarly, the expectation of the observable does not change.


#### Change in the expectation

$\\frac{d \\braket{\\Psi(t)|L|\\Psi(t)}}{dt} = \\braket{\\dot\\Psi(t)|L|\\Psi(t)} + \\braket{\\Psi(t)|L|\\dot\\Psi(t)}$. Using generalized schrodinger's equations, 

$\\frac{d \\braket{\\Psi(t)|L|\\Psi(t)}}{dt} = \\frac{i}{\\hbar} \\braket{\\Psi(t)|HL - LH|\\Psi(t)}$.

Linear operators don't commute, so HL != LH.

**Commutator**: Given two operators L, and M, LM - ML is called the commutator of L with M, and is denoted by [L, M]. Note that [L, M] = -[M, L].

Thus, $\\frac{d}{dt} \\braket{L} = \\frac{-i}{\\hbar} \\braket{[L, H]}$.

It is easy to prove that $i[L, H]$ is also Hermitian. Thus, a valid observable.

This has resemblance to classical mechanics. $\\dot{F} = \\{F, H\\}$.


### Conservation in quantum mechanics

To say that an observable Q is conserved is to say that expected value $\\braket{Q}$ does not change with time. A stronger condition is that any moment $\\braket{Q^m}$ does not change with time.

$\\braket{Q}$ does not change ammounts to $[Q, H] = 0$. That is Q commutes with H. Using the properties of commutator, it is easy to prove that $[Q^m, H] = 0$ for any $m \\ge 1$.

It turns out that if $[Q, H] = 0$ then for **any** function of Q, $[f(Q), H] = 0$.

H is also conserved, as $[H, H] = 0$. H is defined to be the energy of the quantum system.


### Solving Schrodinger's equation

Time dependent Schrodinger's equation is $ \\hbar \\frac{d \\ket{\\Psi}}{dt} = -iH\\ket{\\Psi}$. 

Since H represents enrgy, the oberservable values of energy are eigenvalues of H. Call them $\\ket{E\_j}$ and $E\_j$.

$$
    H \\ket{E\_j} = E\_j \\ket{E\_j}
$$

These are call time-independent schrodinger's equations.

We can write $\\ket{\\Psi{(t)}} = \\sum\_j \\alpha\_j(t) \\ket{E\_j}$.

Thus, $\\ket{\\dot\\Psi{(t)}} = \\sum\_j \\dot\\alpha\_j(t) \\ket{E\_j}$.

Using time-dependent Schrodinger's equation, we can solve for $\\dot\\alpha\_j(t)$. It has the form $\\dot\\alpha\_j(t) = -\\frac{i}{\\hbar}E\_j \\alpha\_j(t)$. Which has the solution $\\alpha\_j(t) = \\alpha\_j(0) e^{\\frac{-i}{\\hbar} E\_j t}$.

But, $\\alpha\_j(0) = \\braket{E\_j|\\Psi(0)}$.

So, $\\Psi(t) = \\sum\_j \\ket{E\_j}\\braket{E\_j|\\Psi(0)} e^{-\\frac{i}{\\hbar}E\_j t}$.

#### General Recipe

1. Get the H somehow.
2. Find the $\\ket{E\_j}$ and $E\_j$.
3. Prepare the system in initial state $\\Psi(0)$.
4. Use above solution to find the state at any later time.
5. If you have some other operator L, you can "predict" the outcome of measuring future state using the eigenvectors of L. i.e., the probability the outcome of measuring L is $\\lambda\_i$ is precisely $|\\braket{\\lambda\_i|\\Psi(t)}|^2$.


## Complex systems

There are systems for which there are more than two observables, and they all can be measured simultaneously. Single spin is **not** such system. Though there are three observables $\\sigma\_{\\{x,y,z\\}}$. Only one of them can be observed at a time.

Particle moving in three dimensions, all three dimensions x, y, and z can be measured simultaneously.

Other such system is a system of two particles. Let's denote these two observables as L and M.
If we measure both spins, we leave the system in a state which is simultaneously eigenvector of both L and M. Let the eigenvectors of L be denoted as $\\lambda\_i$ and same for M with $\\mu\_a$.

In order to have simultaneous eigenvectors $\\ket{\\lambda, \\mu}$, L and M must commute with each other. i.e., $LM \\ket{\\lambda, \\mu} = ML\\ket{\\lambda, \\mu}$. i.e., $[L, M]\\ket{\\lambda, \\mu} = 0$. Since this statement is true of any basis eigenvector $\\ket{\\lambda, \\mu}$, we know that $[L, M] = 0$.

Thus, if we have complete basis of simultaneous eigenvectors, the observables commute. Converse is also true. If observables commute, they have a complete basis of simultaneous eigenvectors. This statement is true for any number of observables in the system, and not just two.





Suppose, we have a basis of states $\\ket{a,b,c, \\dots}$ for some complex system. 

$$\\ket{\\Psi} = \\sum\_{a,b,c,\\dots} \\psi{(a,b,c, \\dots)} \\ket{a,b,c, \\dots}$$

Where, $\\psi{(a,b,c, \\dots)} = \\braket{a,b,c, \\dots|\\Psi}$. This $\\psi$ is called a wave function.

$P(a,b,c, \\dots) = \\psi^\\ast{(a,b,c, \\dots)} \\psi{(a,b,c, \\dots)}$. This is the probability of observing the value $a,b,c,\\dots$ of commuting observables $A,B,C,\\dots$.


If a state is an eigenvector of operator A, which does not commute with B, then it will not be an eigenvector for B. Thus, if A and B don't commute, there will be uncertainity in either A or B if not both.



### Quantifying Uncertainty

The system is in state $\\ket\\Psi$. We want to observe some A. A can be thought as a random variable. The possible outcomes are eigenvalues of A, with predefined probabilities. Thus $\\braket{A}$ is well defined, and is the expected value of A. We can also find the variance of A! This quantifies the uncertainty of A. 

First define $\\bar{A} = A - \\braket{A}I$. This is also an Hermitian operator, so has real eigenvalues. If $a$ is an eigenvalue of A, $\\bar{a} = a - \\braket{A}$ is an eigenvalue of $\\bar{A}$.

Thus the variance, denoted as $(\\Delta A)^2 = \\sum\_a \\bar{a}^2 P(a)$.

A little bit of algebra shows that this is equivalent to $\\braket{\\bar{A}^2} = \\braket{\\Psi|\\bar{A}^2|\\Psi}$.


### Uncertainty Principle

From triangle inequality $|x| + |y| \\ge |x+y|$, one can derive $2|x||y| \\ge |\\braket{x|y} + \\braket{y|x}|$. (Hint: Square both sides, and expand).

Putting, $x = A\\ket\\Psi$ and $y = iB\\ket\\Psi$, we get $\\Delta{A} \\Delta{B} \\ge \\frac{1}{2} | \\braket{\\Psi|[A, B]|\\Psi}$. (Hint: Though formula is true in general, it is easy to derive by assuming that $\\braket{A} = \\braket{B} = 0$, in which case $(\\Delta{A})^2 = \\braket{A^2}$.




## Composite System

Atom is made of nucleons and electrons, each is a quantum system of it's own. We want to study composite system.

For the moment we assume there are two systems, A and B (a.k.a. Alices's sytem and Bob's sytem, respectively).
A has states from staet space $S\_A$, which has dimensionality of $N\_A$. Same for system B. 

The combined system has statespace $S = S\_A \\otimes S\_B$, which has dimensionality $N\_A N\_B$. $\\otimes$ is a tensor product. The states of S are denoted as $\\ket{ab}$, where $a \\in S\_A$ and $b \\in S\_B$.

If an operator M acts on the states of the composite system, M has $N\_A N\_B$ rows and colums. The entry $M\_{a'b', ab}$ is given by $\\braket{a'b'|M|ab}$. The basis vectors $\\ket{ab}$ are taken to be orthonormal. $\\braket{ab|a'b'} = [a = a', b = b']$.

Thus, any state in the composite system is written as $\\ket\\Psi = \\sum\_{a,b} \\psi(a, b) \\ket{ab}$.


### Two Spin System

Let's have four state vectors $\\ket{uu}, \\ket{ud}, \\ket{du}, \\ket{dd}$.


#### Product State
A product state is the result of completely independent preparations of two spins, each with its' own apparatus to prepare a spin. 

Suppose spin A is prepared in $\\alpha\_u \\ket{u} + \\alpha\_d \\ket{d}$ and B is prepared in $\\beta\_u \\ket{u} + \\beta\_d \\ket{d}$ Where $\\alpha^\\ast\_u \\alpha\_u + \\alpha^\\ast\_d \\alpha\_d = \\beta^\\ast\_u \\beta\_u + \\beta^\\ast\_d \\beta\_d = 1$. In such case we need 4 real parameters to define the state (2 for each spin).

Thus, the combined product state is written as $\\{\\alpha\_u \\ket{u} + \\alpha\_d \\ket{d} \\} \\otimes \\{ \\beta\_u \\ket{u} + \\beta\_d \\ket{d} \\}$. This can be expanded, to rewrite in the basis vectors of the combined system, as $\\alpha\_u \\beta\_u \\ket{uu} + \\alpha\_u \\beta\_d \\ket{ud} + \\alpha\_d \\beta\_u \\ket{du} + \\alpha\_d \\beta\_d \\ket{dd}$. 

The main feature of a product state is that each subsystem behaves independently of the other.


#### General Tensor product space.
The general space is written as $\\psi\_{uu} \\ket{uu} + \\psi\_{ud} \\ket{ud} + \\psi\_{du} \\ket{du} + \\psi\_{dd} \\ket{dd}$. Unlike product space, we need 6 real parameters (8(to define complex numbers) - 1 (normalization) - 1(phase factor)).

Thus, there has to be some states which can not be written as product state. Singlet, and triplets are such states. 

Singlet: $\\ket{sing} = \\frac{1}{\\sqrt{2}} (\\ket{ud} - \\ket{du})$.

Triplets:
1. $T\_1 = \\frac{1}{\\sqrt{2}} (\\ket{ud} + \\ket{du})$.
2. $T\_2 = \\frac{1}{\\sqrt{2}} (\\ket{uu} + \\ket{dd})$.
3. $T\_3 = \\frac{1}{\\sqrt{2}} (\\ket{uu} - \\ket{dd})$.


It is easy to prove that these states can't be written as product states. (Hint: for product state you have to show that $\\alpha\_x \\beta\_y = c$, but this will be impossible as some other requirement $\\alpha\_x \\beta\_w = 0$  or $\\alpha\_z \\beta\_y = 0$ will be violated.)

These states are maximally entangled.


### Observables in combined system.

The observables in the case of single sping system, still apply in the combined system. They just modify their half. 

E.g. if $\\sigma\_x$ is observable of spin A, $\\sigma\_x \\ket{ud} = \\ket{dd}$.

Note that $\\sigma\_x$ for single spin system and $\\sigma\_x$ for combined systems are different operators. This is easy to see in the matrix forms. The two matrices are different. 

In the case of single spin system (or product state), there is a direction where the measurement is guaranteed to be +1. Thus, $\\braket{\\vec{\\sigma} \\cdot \\vec{n}} = \\braket{\\Psi|\\vec{\\sigma} \\cdot \\vec{n}|\\Psi} = 1$, for that particular $\\vec{n}$. Thus we know that none of the $\\braket{\\sigma\_x}, \\braket{\\sigma\_y}, \\braket{\\sigma\_z}$ can be zero(which would lead to contradiction). 

On the other hand, if you compute $\\braket{\\sigma\_x}$ for $\\ket{sing}$, you will find it to be zero. In fact, for singlet state, $\\braket{\\sigma\_x} = \\braket{\\sigma\_y} = \\braket{\\sigma\_z} = 0$. Since the components are zero on expectation, we are equaly likely to get +1 and -1 for any measurement. Thus, although the state is known, we don't know the outcome.


---

The operators that act on the two separate factors commute with one another.

The operator $\\tau\_z \\sigma\_z$, is a product of two oprators. Little math tells us that $\\ket{sing}$ is an eigenvector for $\\tau\_z \\sigma\_z$. $\\tau\_z \\sigma\_z \\ket{sing} = -\\ket{sing}$. This means that the product of observations is always -1. Thus both measurements always have opposite signs. In fact, $\\ket{sing}$ is also an eigenvector for operators $\\tau\_x \\sigma\_x$ and $\\tau\_y \\sigma\_y$, with eigenvalue -1.

On the other hand if you try to compute $\\braket{\\tau\_x \\sigma\_y}$, you will find that to be 0.

For the triplets:



|                            | $\\ket{sing}$ | $\\ket{T\_1}$ | $\\ket{T\_2}$ | $\\ket{T\_3}$ |
|----------------------------|--------------|-------------|-------------|-------------|
| $\\braket{\\sigma\_z \\tau\_z}$ | -1         | -1        | +1        | +1        |
| $\\braket{\\sigma\_x \\tau\_x}$ | -1         | +1        | +1        | -1        |
| $\\braket{\\sigma\_y \\tau\_y}$ | -1         | +1        | -1        | +1        |

Thus, singlet and triplets are eigenvalues for the product operators.

--- 

$\\vec{\\sigma} \\cdot \\vec{\\tau}$ is an observable that can not be measured by measuring two spins by individual apparatuses. How can we measure such thing? Some atoms have spins. When two of these atoms are close to each other (e.g., in a lattice), in some situations their Hamiltonian is proportional to $\\vec{\\sigma} \\cdot \\vec{\\tau}$.

The four vectors above are eigenvectors for $\\vec{\\sigma} \\cdot \\vec{\\tau}$. The singlet has eigenvalue -3 and each triplet has eigenvalue +1.


Comment: Generating singlet state is easy. Two spins prefer to be anti-aligned. Now bring these two spins together, they will radiate a photon and result in this state, as this state has low energy.

For product state it is easy to prove $\\braket{AB} = \\braket{A} \\braket{B}$. Thus, we can see that $\\braket{\\sigma\_w \\tau\_w}$ can not be product states. Because for them $\\braket{\\sigma\_w} = 0$.


```python


```


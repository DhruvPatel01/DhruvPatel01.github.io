{
  "date": "2023-05-23",
  "summary": "My book summary for the book by  Ernest Nagel and James Newman.",
  "tags": [
    "math",
    "logic",
    "theory"
  ],
  "title": "Gödel's Proof: Book Notes",
  "lastmod": "2023-05-23T04:04:41Z"
}


Following is my summary of the book Gödel's Proof by Nagel and Newman. While reading the book I realized that the topic under the discussion is quite complex and the book does not go over every minute details. Thus, the notes below may contain inconsistencies, as they reflect my understanding, which is incomplete. 

--------------------


Eulid's axiom: 
Given line, and a point outside it, only one parallel line can be drawn.

Can this be derived from other Euclidean axioms? 

In the 19th century, through the works of Gauss, Bolyai, Lobachevsky, and Riemann, it was proved that was impossible. This proved that proof can be given of the _impossibility of proving_ certain proposition in a given system.


Soundness: logically incompatible statements can not be simultaneously be true.

Sometimes the postulates/axioms themselves are not "true". e.g., non-euclidean geometry. In such cases it is imperative to ascertain if the assumed axioms are consistent.

Elliptical Geometry has an axiom that says that given point outside of the line, no parallel line to it can be drawn. If we list down all the theorems derived so far and manually check, what is the guarantee that our grand children won't derive a theorem that contradicts one of these?




In classical set theory, Burtrand Russell's normal set (set that doesn't contain itself as a member) proves a statement that is both true and false. Thus that system is not consistent.


## Example of a consistent system


### axioms

Vocabulary
- letters like p, q, r: they can be replaced by any sentence
- ~, .(and), |(or), ⇒(if then else) 

Formulas
- These are familiar rules. Like `p .` is not a valid formula. But, `p.q` is.

Transformation Rules

one can derive new formulas by
- uniformly substituting letters by other formulas.
- If we are given two formulas, `S` and `S => T`, then `T` is also a formula.

Axioms
1. `(p | p) => p`
2. `p => (p | q)`
3. `p|q => q|p`
4. `(p => q) =>((r|p) => (r|q))`

Theorems: All the formulas that can be derived using the above axioms and transformations. 

What we want to show is that, it is "absolutely"(as opposed to relatively) impossible to derive two statements `S` and `~S` from these axioms. 

One can prove that the formula `p => (~p => q)` is a theorem. 

If it was possible to derive both `S` and `~S`, we can substitute `S` in the above theorem to get `S => (~S => q)`. The second transformation rule then can be applied to get `~S => q`. But, again, by the same transformation we get `q`.

Thus, if the system were inconsistent, any formula can be derived. Conversely, if we prove that there is a formula that cannot be derived from the stated axioms, we have proved that the system is consistent.

For the proof that such a formula exists, we use tautology. Tautology is a formula which is always true. Now, all the axioms are tautologies. The book's appendix shows that if either of the two transformations is applied to the tautology, the resulting formula is also a tautology.

Look at the formula `p | q`. Is it a tautology? No, because if both `~p` and `~q` are true, the formula is false. Tautology means always true. 

So, we showed a formula which is not a tautology. If this were a theorem, it would have been a tautology. So, it isn't a theorem. Thus, there is a formula which isn't a theorem. Thus, the system is consistent.

It also turns out that the system is complete. i.e., every tautology can be derived from these axioms.

Note: This system is not sufficient even to develop elementary arithmatic.


#### Correspondence Lemma:

PM (Principia Mathematica) gave each symbol a meaning (e.g., `+` is addition). However, the formal system does not require us to give a meaning to the symbols. The theorems are derived from axioms by following the rules of the system.



However, Godel proved that
- there is an infinite class of theorems, which interpreted with the "intendend" meaning, are arithmatical truths.
- there are infinite recursive primitive truths, which when encoded using symbols with "intended" meanings are indeed theorems

Recursive Primitive Truths: correct additions like "2 plus 2 is 4". Or "17 is 7th prime". 


Then, there is a mapping from an expression in the calculus to a unique number.
Conversely, given any number, it is easy to see if it makes symbols of the calculus, or expression or a sequence of expressions. 




Godel also showed that statements (in meta-mathematics) about the calculus can also be mapped to expressed with the symbols of the calculus itself.

The fundamental idea is to convert the typographical relationship between the expression to the arithmetical relationship between Gödel numbers. 

E.g., `~(0 = 0)`. Consider the  meta-mathematical statement, *The first symbol of the expression is ~*.

The Gödel number associated with the expression is`a = 2^s(!) * 3^s('(') * 5^s(0) * 7^s(=) * 11^s(')')`.

Suppose that the associated number with `!` is 7 (there are only few such preliminary symbols). Then, the "expression" `2^7 is a factor of a, and 2^8 is not a factor of a` can be expressed with the symbols of calculus, and hence by a Gödel number.

By the way, `x is a factor of y` is a primitive recursive truth. Thus, by correspondence lemma, is a theorem in PM.



Another meta-mathematical statement is `the sequence of formulas having Godel number x is a proof (in PM) of the formula with Godel number z`. There is a mathematical relationship between x and z, denote it by `dem(x, z)`. Godel showed that this relation `dem(x, z)` is a primitive recursive relation. Thus, there, the formula in the PM `Dem(x, z)` is actually a theorem. 

<details> <summary>Example</summary>
Notaion: s[5] = sssss

the meta-mathematical statement `x is prime (or pr(x))` can be written as a formula `~ (E y) (E z) (s[x]0 = s[y]0 * s[z]0`. Now since `is prime`, or `is not prime` is a primitive recursive, there is a theorem in PM for the formula `~ ~ (E y) (E z) (s[9]0 = s[y]0 * s[z]0`
</details>

Also, `~Dem(y, z)` is a theorem.

Take the formula `(E x) (x = sy)`. This formula has a Godel number m. We can replace y with the concrete number m and get the new formula `(E x) (x = ss[m]0)`. This formula states nothing new, but `m has a successor`. Meta-mathematically, this is a Godel number obtained from the formula for Godel number m by substituting 17 with m. This function of replacing a variable within the formula by the Godel number of the formula itself is a primitive recursive function.  Denote the new Godel number by `sub (x, 17, x)`.

Since the algorithm is primitive recursive, the formula `z = sub(x, 17, x)` is a theorem. This formula is denoted as `Sub (x, 17, x)`. 


## Gödel's proof


Gödel showed 
1. How to construct a formula G for the meta-mathematical statement "The formula G is not demonstrable". This formula's Gödel number is denoted as g.
2. G is demonstrable iff ~G is demonstrable. Thus, if PM is consistent, neither G nor ~G can be demonstrated. Such formulas where neither G nor ~G can be proved (under the assumption that PM is consistent) are called formally undecidable. 
3. Though G is not formally demonstrable, it is nevertheless true.
4. Since G is true and formally undecidable, PM is incomplete. Godel showed PM is essentially incomplete. That is, even if you augment PM with some axioms, the new resulting system still would be incomplete.
5. Gödel showed how to construct `A` ("PM is consistent"), and `A => G` is formally demonstrable. But A is not demonstrable. 



Notaion: `n := x`. n is a godel number that represents a formula or a sequence of forumlas.

### 1: Construction of G

- `Dem(x, z)` was showed to exist earlier.
- The new formula `(E x) Dem(x, z)` tells us that z is demonstrable.
- The formula `~(E x) Dem(x, z)` tells us that z is not demonstrable.
- Consider the formula `n := ~(E x) Dem(x, Sub(y, 17, y))` This formula tells meta-mathematically that a formula with `Sub(y, 17, y)` is not provable in PM. However, this formula is not definite, as it uses a variable y.
- Consider the formula `g := ~(E x) Dem(x, Sub(n, 17, n))`. This formula tells meta-mathematically that `Sub(n, 17, n)` is not demonstrable. g represents a definite formula, as it doesn't have any variables.
- But, `sub(n, 17, n)` is precisely g. That is how g was constructed.
- Thus, G tells that G is not demonstrable in PM.

    "In a word, the PM formula G can be construedas asserting of itself that it is not a theorem of PM."


### 2: If PM is consistent, neither G nor ~G can be derived.

- Gödel showed that if G can be demonstrated, ~G can be demonstrated.
    - Proof goes like this. If G is demonstrable, let k denote the proof.
    - i.e., `Dem (k, Sub(n, 17, n))` is a theorem.
    - By the inference rules of PM, `(E x) Dem(x, Sub(n, 17, n))` is a theorem.
    - But, that is precisely ~G. QED.
- Gödel also showed that if ~G is demonstrable, then PM is $\\omega$-consistent.
- Rosser later proved that if ~G is demonstrable, then G is demonsrable.
- Thus, if PM were to be consistent, neither G nor ~G must be demonsrable. Thus, G is formally undemonsrable. 


### Digression: In an inconsistent system every statement is provable.

This is a little bit of revision from above.

- Since the system is inconsistent, there is some P such that both P and ~P are true (as per the system).
- Since `P` is true `P or Q` is true.
- Since `P or Q` is true and `~P` is true, i.e., `P` is false, Q must be true.

Thus, we just proved that arbitrary statement Q is true. Because of this, the previous point and the next points do not consider about what happens if the system is inconsistent. 

There is another implication. If there is at least one formula which is not demonstrable, the system is consistent.


### 3: G is true statement.
Certainly, either G or ~G must be true. It can be shown by the meta-mathematical reasoning that G is true. 

 G says that "There is no proof of G in the PM".
~G says that "There is a proof of G in the PM".

We(Gödel) in 2nd point proved that G does not have a proof in PM. Thus, G is a true statement. 

Note: We have not used axioms or the rules of the inference in this proof. We used meta-mathematical reasoning. 

Note: Gödel also showed in 2nd point that ~G does not have a proof in the system, but this part seems irrelevant. 


### 4: PM is incomplete

Under the hypothesis that PM is consistent, using pt2 and pt3, we see that PM is incomplete. 


### 5 Consistency => Incompletness is demonstrable.

Based on the digression above, the statement "PM is consistent" is equivalent to the statement that "There is a formula of PM that is not demonstrable inside PM". This meta-mathematical statement can be written as a formula in PM `(E y) ~ (E x) Dem(x, y)`. Call this formula A. The antecedent therefore is in place.

The consequent clause too is easy. The system is incomplete means there is a true-but-not-demonstrable formula X, "X is not a theorem of PM". G is such formula. So, the consequent clause "G is not a theorem of PM" can be encoded. We already know the encoding, it is G itself. 

The statement "If PM is consistent,then it is incomplete" is represented in PM by `(E y) ~ (E x) Dem(x, y) => ~(E x) Dem(x, Sub(n, 17, n))`. This forumala (abbreviated as `A => G`) is demonstrable (not proved in the book).

If we can proove A in the PM, by the rule of detachment `(A and A => B) => B`, G is proveable. But, unless PM is inconsistent, G is formally undemonstrable. 

Thus, if PM is consistent, the consistency of it can not be proved by PM itself. One should note that, this does not consider meta-mathematical proof that can not be mirrored by the PM. That is a fair game. Only that a reasoning that can be mirrored in PM, can not show that PM is consistent. 


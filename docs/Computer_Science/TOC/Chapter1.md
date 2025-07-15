---
statistics: True
comments: true
---

# Chapter 1

## 离散知识的回顾

### Set

- A set is a collection of objects
- Objects in a set are called **elements** or **members** of the set.
- a $\in$ A if a is an element of A; a $\notin$ A, otherwise.

- A set is **empty** if it contains no element.
- A set is a **singleton** if it contains only one element.
- A set is **finite** if it contains finite number of elements.
- A set is **infinite** if it contains infinite number of elements.

---

### Subsets

- A is a **subset** of B if each element of A is also an element of B.

$$A \subseteq B$$

We also say that B is a **superset** of A.

- A is a **proper subset** of B if $A \subseteq B$ and $A \neq B$.

$$ A \subset B$$

We also say that B is a **proper superset** of A.

---

### Set Operations

- **Union**: $A \cup B = \{x : x \in A \lor x \in B\}$
- **Intersection**: $A \cap B = \{x : x \in A \land x \in B\}$
- **Complement**: $\overline{A} = \{x : x \notin A\}$
- **Power Set**: $2^A = \{S : S \subseteq A\}$

---

### Sequences

- A sequence is a list of objects in some order.

$$(1,2) \neq (2,1)$$

- A finite sequence is also called a **tuple**. A sequence of k elements is called a **k-tuple**.
- A 2-tuple is also called an **ordered pair**.

---

### Cartesian Product

- The **Cartesian product** of two sets A and B is

$$A \times B = \{(a,b) : a \in A \land b \in B\}$$

- The **Cartesian production** of k sets $A_1, A_2, \ldots, A_k$ is

$$A_1 \times A_2 \times \ldots \times A_k = \{(a_1, a_2, \ldots, a_k) : a_i \in A_i\}$$

---

### Relations

- A relation on k sets $A_1, A_2, \ldots, A_k$ is a subset of $A_1 \times A_2 \times \ldots \times A_k$.
- A binary relation R on $A \times A$ is

    (a) **reflexive**: if (a,a) $\in R$ for every $a \in A$

    (b) **symmetric**: if (b,a) $\in R$ whenever (a,b) $\in R$

    (c) **transitive**: if (a,c) $\in R$ whenever (a,b) $\in R$ and (b,c) $\in R$

- A binary relation R on $A \times A$ is an **equivalence relation** if it is reflexive, symmetric, and transitive.

---

### Functions

- A function $f : A \rightarrow B$ assigns each $a \in A$ a **unique** $f(a) \in B$.
- f(a) is the **image** of a.
- A is called the **domain** of f.
- **Range** of f is the set of all images, denoted as f(A).
- Let $f : A \rightarrow B$ be a function.
- f is **one-to-one(injective)** if for any $a \neq a'$ , $f(a) \neq f(a')$.
- f is **onto(surjective)** if f(A) = B.
- f is **bijective** if it is both one-to-one and onto.

---


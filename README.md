# Formal Semantics of Programming Languages

A report on the theoretical foundations that define what programs *mean* — beyond syntax and execution.

-----

## Overview

Programming languages are often treated as practical tools. This report argues they are better understood as formal systems, where three components work together to fully specify program behavior:

- **Operational Semantics** — how programs execute, step by step
- **Scope Rules & Parameter Passing** — how names are resolved and how procedure calls connect caller and callee state
- **Type Systems** — which programs are statically guaranteed to be safe

Each layer answers a different question. Together, they explain why superficially similar programs can behave differently across languages, and why language design choices have non-obvious consequences.

-----

## Contents

### 1. Operational Semantics

Programs are given meaning through inference rules that describe legal computation steps. A state is modeled as a mapping from locations to values. Complex constructs reduce to the behavior of their parts — a compositional structure essential for both implementation and formal reasoning.

This is the conceptual foundation of program logics such as **Hoare logic** (Hoare, 1969), where correctness is stated as a relationship between preconditions, program fragments, and postconditions.

### 2. Scope Rules and Parameter Passing

Operational semantics alone do not fix how variable names are resolved. That depends on scope rules and parameter passing:

**Static (lexical) scope** — bindings are determined by the textual structure of the program. A name always refers to the nearest enclosing declaration, regardless of call history.

**Dynamic scope** — bindings are resolved at runtime using the most recent entry on the call stack. The same expression may denote different variables depending on which procedures were called to reach that point.

**Parameter passing mechanisms:**

- *Call-by-value* — the callee receives a copy; updates do not propagate back
- *Call-by-reference* — the callee receives an alias; assignments affect the caller’s state
- *Call-by-name* — the argument expression is re-evaluated in the caller’s context at each use

These are not implementation details. They determine which state updates occur and which variables are affected — they are part of meaning (Reynolds, 1972).

### 3. Type Systems and Type Safety

Types are *static semantics*: constraints on program structure that can be checked without execution. A well-typed program carries a proof that certain classes of runtime errors cannot occur.

Type soundness is formalized via two properties (Wright & Felleisen, 1994):

- **Progress** — a well-typed term is either a value or can take a step
- **Preservation** — taking a step does not change the type

Together these establish that well-typed programs never get stuck in an ill-typed state.

-----

## Key Argument

Semantics explain why the same construct can mean different things in different languages. Changing scope rules can redirect a name to a different binding. Changing parameter passing can turn a harmless-looking call into a state mutation. Changing the type system can move an error from runtime to compile time — or vice versa.

Formal semantics make these differences precise, inspectable, and provable.

-----

## References

- Hoare, C. A. R. (1969). An axiomatic basis for computer programming. *Communications of the ACM*, 12(10), 576–580.
- Reynolds, J. C. (1972). Definitional interpreters for higher-order programming languages. *Proceedings of the ACM Annual Conference*.
- Wright, A. K., & Felleisen, M. (1994). A syntactic approach to type soundness. *Information and Computation*, 115(1), 38–94.

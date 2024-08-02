---
title: Boolean Satisfiability
date: 2024-06-26 13:00
categories: [Software Development, Boolean Logic]
tags: [haskell, sat solver, boolean logic]     # TAG names should always be lowercase
math: true
comments: false
---

### **Introduction**

The aim of this project is to implement a SAT solver in Haskell which uses conflict driven clause learning.
The solver is based on [MiniSAT](https://minisat.se/MiniSat).

### **Preliminaries**

This section covers basic boolean logic.
For readers familiar with boolean logic up to conjunctive normal forms, skip to the next section.
Consider formal variables $ x_1, ..., x_n $ taking values in $ \lbrace \texttt{False}, \texttt{True} \rbrace$.
We build up variables into expressions using the following operators,

- $ \vee $ known as $ \texttt{or} $,
- $ \wedge $ known as $ \texttt{and} $,
- $ \neg $ known as $ \texttt{not} $.

Boolean expressions can are either formal variables, or of the following form

$$\text{expr}_1 \vee \text{expr}_2 \qquad \text{expr}_3 \wedge \text{expr}_4 \qquad \neg \text{expr}_5$$

To evaluate boolean expressions, we only need to know how the operators act on $ \{ \texttt{False}, \texttt{True} \} $, which is as follows,

Or:

| Input | Output |
| :---: | :---: |
| $\texttt{False} \vee \texttt{False}$ | $\texttt{False}$ |
| $\texttt{False} \vee \texttt{True}$ | $\texttt{True}$ |
| $\texttt{True} \vee \texttt{False}$ | $\texttt{True}$ |
| $\texttt{Ture} \vee \texttt{True}$ | $\texttt{True}$ |

And:

| Input | Output |
| :---: | :---: |
| $\texttt{False} \wedge \texttt{Fasle}$ | $\texttt{False}$ |
| $\texttt{False} \wedge \texttt{True}$ | $\texttt{False}$ |
| $\texttt{True} \wedge \texttt{False}$ | $\texttt{False}$ |
| $\texttt{True} \wedge \texttt{True}$ | $\texttt{True}$ |

Not:

| Input | Output |
| :---: | :---: |
| $\neg \texttt{Fasle}$ | $\texttt{True}$ |
| $\neg \texttt{True}$ | $\texttt{False}$ |

Expression can be evaluated by simplifying the component expressions down to a single value and then applying the tables above, for example

$$(\texttt{False} \vee \texttt{True}) \wedge (\neg \texttt{False})$$

$$\rightarrow \qquad (\texttt{False} \vee \texttt{True}) \wedge \texttt{True}$$

$$\rightarrow \qquad\texttt{True} \wedge \texttt{True}$$

$$\rightarrow \qquad\texttt{True}$$

We can now describe the Boolean Satisfiability Problem as follows

> Given a boolean expression consisting of formal variables $ x_1, ..., x_n $, does there exist an assignment of the variables to $ \texttt{True} $ or $ \texttt{False} $ such that the expression evaluates to $ \texttt{True} $. If such an assignment exists, the expression is called satisfiable.

The first thing to note is the existential quantifier, we care about the existence of an assignment which satisfies the expression.
Secondly, if our expression has $ n $-variables, we have $ 2^n $ possible assignments.
This makes a brute force approach very slow, and in general it is not known if an efficient algorithm for solving boolean satisfiability exists.
This is known as the P vs NP problem, and boolean satisfiability is [NP-complete](https://en.wikipedia.org/wiki/NP-completeness).
Hope is not lost though, we can do better than brute force in some cases.

Before we get to solving satisfiability problems, we want to simplify the types of expressions we solve.
Expressions of the form $x_1 \vee ... \vee x_n$ are known as `Clauses`.
Expressions which are made of the conjunction of clauses (clauses joined by $ \wedge $) are said to be in `Conjunctive Normal Form`.

### **Initial State**

We now describe the process of solving boolean satisfiability problems.
Our solver will only accept expressions in conjunctive normal form.
Any boolean expression can be converted to [Conjunctive Normal Form](https://en.wikipedia.org/wiki/Conjunctive_normal_form), so this restriction does not reduce the ability of the solver.
Observe the conjunctive normal form gives a few implications about a solution.
We have an assignment which satisfies the expression if and only if the assignment satisfies each clause of the expression.
Furthermore, if a variable only occurs in one type, i.e. $ x $ or $ \neg x $, then we can assign $ x $ the value which makes it True without any other knowledge.
Finally, if we have clauses $ x $ and $ \neg x $ then the expression is not satisfiable.

### **Backtracking Search**

The simplest approach to searching is backtracking.

1. Begin with all variables unassigned
2. Assign a variable at random, to a value which has not been assigned previously
3. If the resulting expression is not satisfiable, back track undoing the previous assignment
4. Otherwise go back to 2 until all variables have been assigned

This approach is slightly better than the brute force approach of try all $ 2^n $ combinations, since we trim the search space when we find an partial assignment of variables which does not satisfy the expression.
We will improve this search algorithm with back jumping.

### **Unit Propagation**

A `unit clause` is a clause which contains a single variable.
Previously we noted that we have an assignment if and only if the assignment satisfies each clause of the expression.
Consequently, suppose we have a partial assignment of the expression and a clause has become a unit clause.
Then we can deduce the assignment of this variable, the one which makes the clause $ \texttt{True} $.
Otherwise, the assignment would not be satisfiable.

This allows us to speed up the search process.
Each time a variable is assigned, we check for any unit clauses.
For each clause, we propagate the assignment for the variable, reducing the search space and checking for any new unit clauses.

### **Conflict Driven Clause Learning**

The backtracking search algorithm implicitly finds out information about which variable assignments cause conflicts, but does not make use of this information as it backtracks immediately after detecting conflict.
Conflict Driven Clause Learning (CDCL) is a method of learning from conflicts.
We illustrate this with a concrete example.

Suppose we have the following expression in CNF,

$$ (x_1 \vee x_2 \vee x_3) \wedge (\neg x_1 \vee x_2) \wedge (x_2 \vee x_3) $$

and in the search process we assign $ x_2 = \texttt{True} $ and $ x_3 = \texttt{True} $.
Then simplifying the expression we have,

$$ x_1 \wedge \neg x_1 $$

which is a conflict.
The two clauses which caused the conflict are the ones containing $ x_1 $ and $ \neg x_1 $, namely

$$ x_1 \vee x_2 \vee x_3 \qquad \neg x_1 \vee x_2 $$

In order to avoid this confict, we want atleast one of $ x_2, x_3, x_2 $ to be true (where the second $ x_2 $ is from the second clause).
As an expression we have

$$ \neg x_2 \vee \neg x_3 $$

This is the learnt clause, which we add to the expression.

CDCL allows information from conflicts to be threaded through the solving process, at the cost of increasing the number of expressions.
More advanced SAT solvers use heuristics to decide when to reduce the number of learnt expressions.
For this simple SAT solver we just keep all learnt clauses.

### **Backjumping**

Backjumping is an optimisation to the search procedure introduced by [GRASP](https://www.cs.cmu.edu/~emc/15-820A/reading/grasp_iccad96.pdf).
If we consider the search space as a binary tree, backtracking simply traversed backwards one level up the tree and continued down another branch.
Backjumping backtracks up multiple levels of this search tree, further reducing the search space.

Backtracking/jumping occurs on conflict.
When a conflict occurs, we produce a conflict clause.
Variable assigments are then undone until one literal in the learn clause is unbound, at which point the search continues.

### **Future Work**

MiniSAT includes a notion of variable activity, which is used to choose the next variable to assign.
Currently our SAT solver does not implement this feature.
MiniSAT gives fine control over the starting procedure of the solver, allowing some pre-conditions to be set.

---
up:
  - "[[Recursion]]"
tags:
  - atomic
created: 2025-11-18 21:30
---
> The evolved process looks like a tree, where the branches split at each level.

In general, the number of steps will be proportional to the number of nodes in the tree, while the space will be proportional to the maximum depth of the tree.

This is why tree recursion can be exponentially expensive in time but only linearly expensive in space.

# See also 
- [[Linear Recursion is a chain of deferred operations]] — the contrast: linear recursion is a single path (one branch), tree recursion fans out; both share the expansion/contraction shape but at different scales 
- [[A ball can be covered by N balls of radius epsilon*r]] — iterative halving is tree recursion applied to metric spaces: each level branches into $2^D$ subproblems, depth is $\log_2(1/\epsilon)$, exactly the tree recursion complexity model 
- [[Doubling Dimension D - a ball or radius r can be covered by smaller balls]] — the branching factor $2^D$ in iterative halving is the tree recursion branching factor; D is what determines whether the tree is tractable
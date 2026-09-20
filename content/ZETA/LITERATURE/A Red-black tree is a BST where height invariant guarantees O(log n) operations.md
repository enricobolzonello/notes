---
up:
tags:
  - atomic
created: 2026-05-12 12:23
---
A red-black tree (**rbtree**) is a binary search tree in which each node has also a *color*, which can be red or black. 
It needs to have the following properties:
- each node is either red or black
- all leaves are black and NIL
- if a node is red, then both child are black
- each path between a node and a descendent leaf contains the same number of black nodes
- root is always black (as a convention)
- height is at most $2 \cdot log_2(n+1)$

![[Red-black_tree_example.svg]]

When a node are inserted that change the height invariant, the tree is rearranged using the current coloring scheme. Once the tree is rearranged, it is repainted.

The height property is what allows to calculate its asymptotic complexity and performance. 

| Operation   | Complexity         |
| ----------- | ------------------ |
| Insertion   | $O(\log_2 n)$      |
| Recolouring | $O(\log_2 n)$      |
| Deletion    | $O(\log_2 n)$      |
| Searching   | $O(\log_2 n)$      |
| Traversal   | $O(n)$ (amortized) |

# See also
- [[h(x) = g(f(x)) — Composing Functions With ∘ and Its Reverse]] — a BST lookup is iterated function composition: at each node, the comparison function maps the search key to the left or right subtree; the height bound guarantees at most 2·log₂(n+1) compositions
- [[Tree Recursion branches at each level]] — insertion and deletion traverse a root-to-leaf path; the height bound is the maximum depth, directly determining the $O(log n)$ complexity
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] — red-black trees have poor cache behaviour: each node lookup follows a pointer to an arbitrary memory location; this is the same random access problem as hash maps, just O(log n) jumps instead of O(1)
- [[SSTables enable sparse indexes, simple merges and block compression]] — red-black trees maintain sorted order like SSTables; `std::BTreeMap` in Rust uses a B-tree (generalization of BST) for better cache behaviour than a red-black tree precisely because of the random access problem

# References
- https://brilliant.org/wiki/red-black-tree/
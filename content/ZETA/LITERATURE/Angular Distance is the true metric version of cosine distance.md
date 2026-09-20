---
up:
  - "[[Cosine Similarity is the cosine of the angle between two vectors]]"
tags:
  - atomic
created: 2024-12-20 19:24
---
> [!DEFINITION]
> Angular distance or angular separation is the measure of the angle between the orientation of two straight lines, rays, or vectors in three-dimensional space, or the central angle subtended by the radii through two points on a sphere.
> — https://en.wikipedia.org/wiki/Angular_distance

Since it is the angle between two vectors it can be derived from the [[Cosine Similarity is the cosine of the angle between two vectors]].

When the vectors may be positive or negative:
$$
d_{ang} = \frac{\arccos (d_{cos})}{\pi}
$$
if the vector elements are always positive:
$$
d_{ang} = \frac{2\arccos (d_{cos})}{\pi}
$$

# See also
- [[Cosine Similarity is the cosine of the angle between two vectors]] - angular distance is the metric-compliant conversion of cosine distance (i.e. it does not violate the triangle inequality)
- [[SimHash - h(x) = sign(wᵀx)]] - the factor $\theta$ in SimHash's collision probability is exactly the numerator of angular distance
- [[Clustering is the task of grouping a set of objects]] - clustering algorithms that require a true metric (i.e. [[k-center]]) need angular distance rather than cosine for correctness guarantees
- [[A Hash Function Must Be Deterministic, Uniform, and Fast — FNV-1a Is One Example]] - angular distance is what LSH schemes for cosine similarity are actually preserving, in fact SimHash maps nearby vectors in angular space to the same bucket

Summary of **Dimensionality Reduction (DR)**  literature review, highlighting critical pain points, algorithmic weaknesses, and potential directions for future research.

### Three Main Goals:
- Find a way to make a new (hopefully better) algorithm
- Find a way to obtain better metrics that can (hopefully) find a good balance between both local and global structure of a manifold
- Test either/both of these on interesting financial datasets

---

## 1. The Fundamental Trade-Off: Local vs. Global Structure Preservation of a Manifold

A core issue between balancing local and global manifold preservation.

- **Local Structure:** **t-SNE** &  **UMAP** capture details in the clusters, but often result in distorted global geometry.

- **Global Structure:**  **PCA** and **metric MDS (mMDS)** preserve large-scale relationships but lose local fidelity at the more local relationships.

- **Hybrid Approach:** Combining local and global objectives (e.g., **SQuaD-MDS** + **FIt-SNE**) can yield embeddings that maintain both overall topology and local neighborhood quality.

---

## 2. Theoretical/Optimization Weaknesses

Nonlinear Dimenstionality Reduction methods suffer from both theoretical and numerical limitations.

#### A. Objective Function Flaws
- Sparse spectral methods (e.g., **LLE**, **Laplacian Eigenmaps**, **HLLE**, **LTSA**) can produce "trivial solutions" (all embeddings collapse to zero).  
- Naïve constraints (e.g., ‖y‖² = 1) can be “cheated,” resulting in "degenerate" embeddings.

> **Potential Area to Explore:** Design cost functions whose resultant minimum is "non-trivial". Check this out in more depth: [Knowledge Learning-Based Dimensionality Reduction for Solving Large-Scale Sparse Multiobjective Optimization Problems](https://ieeexplore.ieee.org/abstract/document/10969804)

#### B. Numerical Instability
- Spectral methods (those that rely on eigen-decomposition of some matrix) rely on finding very small non-zero eigenvalues, which are numerically unstable and difficult for modern eigensolvers to separate from zero.

#### C. Distance Retention Bias
Convex Dimensionality Reduction methods inherently favor large pairwise distances, forgetting about the small distances critical for local geometry.

---

## 3. Scalability and Computational Constraints (From the Internet)

Traditional Dimensionality Reduction algorithms struggle to scale with modern datasets.

| Method | Time Complexity | Memory Complexity | Notes |
|--------|----------------|------------------|-------|
| **SMACOF (mMDS)** | O(N²) per iteration | O(N²) | Infeasible for large data |
| **Isomap / KPCA** | O(N³) | O(N²) | Requires full pairwise matrix |
| **SQuaD-MDS** | O(N) per SGD step | O(N) | Scalable with data partitioning |
| **UMAP / FIt-SNE** | ~O(N log N) | Efficient | Competitive for >100k samples |
AND OTHER TECHNIQUES!
## 4. Robustness to Real-World Data

A major performance gap exists between synthetic benchmarks and real-world datasets.

- **Performance Gap:**  
  Methods optimized for clean synthetic manifolds (the Swiss roll example) often fail on noisy or complex data, while **PCA** and **autoencoders** often perform competitively on real datasets. Where they are used in a dataset before it is handed off to t-SNE.

- **Curse of Intrinsic Dimensionality:**  
  Local methods require exponentially more data as intrinsic dimension (d) increases, making them unsuitable for complex, high-d data.

- **Noise and Outliers:**  
  Nonlinear DR is highly sensitive to discontinuities, that results in clusters of data that although provide important local structure, result in distances of global structure that are unable to be interpreted as they do not show actual "distance" in terms of relationships.     
  Suggestions of using **Mixtures of t-distributed Subspaces (MoTS)** offer improved robustness by heavier-tailed distributions.

---

## 5. Non-Parametric Nature and Generalization Limits

Most nonlinear Dimensionality Reduction methods are **non-parametric**, meaning they lack a direct mapping from high- to low-dimensional space.

- **Out-of-Sample Problem:**  
  New data points require non-parametric extension, introducing estimation errors.

- **Parametric Alternatives:**  
  **PCA** and **Autoencoders** provide explicit mappings, enabling efficient and accurate embedding of unseen data.

> **Potential Direction:** Deep, parametric models (multilayer autoencoders?).

---

## 6. Current Literature Review Conclusions

Dimensionality reduction challenges:
- Balancing **local vs. global** preservation  
- Overcoming **theoretical and numerical instability**  
- Achieving "**scalability**" for large-scale data  
- Ensuring **robustness** to noise and real-world complexity  
- Enabling **generalizable parametric embeddings**

### The Path Forward
Progress probably will go in the direction of **hybrid, deep-learning-inspired approaches** that unify:
- Physics-inspired Approach: [A Survey on Design-Space Dimensionality Reduction Methods for Shape Optimization](https://link.springer.com/article/10.1007/s11831-025-10349-x)
- Local and global objectives  
- Robust optimization  
- Scalable computation  
- Parametric mappings for generalization  

Next Steps for me:
- Test out the important metrics
- Further research on the Computation/Scalability Potential of these algorithms
- Look for more "inspiring approaches"
- Focus on obtaining some dataset that this can be tested on, one with random noise from financial markets

© 2025 — Sebastian Perilla: Dimensionality Reduction Literature Review Research :)

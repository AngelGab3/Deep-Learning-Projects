Add Self-Organizing Maps (SOM) notebook

Implements a Kohonen SOM from scratch (square and hexagonal grids)
on a 240-star dataset (temperature, luminosity, radius, magnitude),
recovering the Hertzsprung-Russell diagram in an unsupervised way.

Includes:
- U-Matrix, component planes, hit map, and quality metrics (QE/TE)
- Two-level clustering (SOM + K-Means)
- Hyperparameter grid search over grid size and iterations
- Theoretical background on SOM vs. K-Means, GNG, GTM, UMAP

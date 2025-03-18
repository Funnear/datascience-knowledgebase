# Principal Component Analysis

TODO: basics

## Principal Component Analysis (PCA) helps in reducing multicollinearity among features in a dataset.

### How PCA Reduces Multicollinearity:
1. Transforms Correlated Variables into Uncorrelated Principal Components
- PCA creates a new set of orthogonal (uncorrelated) components by performing an eigen decomposition of the covariance matrix (or singular value decomposition on the data matrix).
- These principal components (PCs) are linear combinations of the original variables, ensuring that they are uncorrelated.

2. Selects the Most Important Components
- If the original dataset has highly correlated variables, PCA compresses the variance into fewer dimensions.
- By choosing only the top k principal components (those with the highest variance), we effectively remove redundant information caused by multicollinearity.

3. Improves Regression Models
- In linear regression, multicollinearity causes instability in coefficient estimates, making them sensitive to small data changes.
- By replacing the original variables with the uncorrelated PCs, PCA helps stabilize regression models, reducing the impact of collinearity.

### Limitations of PCA for Multicollinearity
- PCA transforms the data, so the original interpretability of features is lost.
- It does not necessarily remove multicollinearity in the original dataset, but rather replaces correlated variables with uncorrelated components.
- If interpretability is crucial, other methods like Variance Inflation Factor (VIF) analysis, Lasso regression, or removing redundant features might be preferred.


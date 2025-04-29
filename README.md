# Stroke Prediction using Support Vector Machines

### Support Vector Machines: Theory and Kernels

Support Vector Machines (SVMs) are powerful supervised learning models that find an optimal separating hyperplane between classes with maximum margin. For linearly separable data, the ideal decision boundary is a hyperplane that maximizes the distance to the nearest data points of each class (the support vectors). But in practice, data is usually not perfectly separable, so SVMs use a "soft" margin implementation that allows some misclassifications while still trying to keep the margin as wide as possible. These kind of margins have an optimization problem that can be expressed as minimizing a specific objective function. 

One important feature of SVMs is that the decision boundary is determined by a subset of training points (the support vectors) and can be defined in terms of dot products between data points. Another is that the kernel function defines the feature space in which the SVM finds the optimal hyperplane. For instance, a linear kernel uses the original features (no transformation), whereas polynomial or RBF kernels allow non-linear separation by mapping to a higher dimensional feature space. SVMs with non-linear kernels can capture complex patterns in the data without requiring new features.

Specifics of the three kernels:
1. **Linear kernel**: This results in a standard linear SVM where the decision boundary is a flat hyperplane. A linear kernel is effective if the relationship between features and the target is approximately linear.
2. **Radial kernel**: The radial kernel maps points into an infinite-dimensional space and can fit very complex boundaries​. The gamma parameter controls the radius of influence of each training point, i.e., a low gamma means a point’s influence is spread out (smooth decision boundary) and a high gamma means each point has a very localized effect, giving a highly "wiggly" boundary​. The radial kernel is usually a default kernel when a non-linear relationship is suspected.
3. **Polynomial kernel**: This introduces polynomial combinations of features up to a specific degree. For example, a quadratic (degree 2) kernel can model pairwise feature interactions​. Higher degree makes the decision boundary more complex (risking overfitting).

Hyperparameter tuning is also important when using SVMs. Certain tunable parameters include:
1. **C (Regularization)**: Controls margin width vs. training error trade-off. Needs to be chosen to prevent overfitting (too high C) or underfitting (too low C).
2. **Kernel parameters**: For the radial kernel, the gamma parameter must be set appropriately (if gamma is too large, the model can overfit by creating very tight boundaries around points; if too small, the model underfits by becoming almost linear). For polynomial kernels, the polynomial degree must be chosen along with gamma. A higher degree increases model complexity and can lead to overfitting. These parameters are usually determined via cross-validation.

**Practical Considerations**:
Before training an SVM, it is very important to scale or normalize features because the SVM objective function and kernels are sensitive to the scale of input features​. If one feature has a much larger numeric range than others, it can dominate the dot product or distance calculation, thus distorting the kernel values and the resulting model​. So in this project, I applied standardization to the variables so that all features contribute equally to the kernel computation. Another consideration is class imbalance: if one class heavily outweighs the other (like the stroke class I used), a normal SVM will bias toward predicting the majority class. To address this, I set class_weight='balanced' in the SVC function, which automatically weights the classes​. I used this to ensure the model pays sufficient attention to the positive stroke cases. 













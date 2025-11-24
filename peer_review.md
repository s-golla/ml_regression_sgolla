# Peer Review: Kiruthikaa's Regression Analysis Project

**Reviewed Notebook:** [regression_ml_kiruthikaa.ipynb](https://github.com/Kiruthikaa2512/ml_regression_kiruthikaa/blob/main/regression_ml_kiruthikaa.ipynb)

**Reviewer:** Saratchandra Golla

### 1. Clarity & Organization

**Positive:**
The notebook is well-structured with clear, numbered headings (Sections 1 through 6) that follow the project guidelines. The use of separate Markdown cells for explanations and code cells for execution makes the document easy to read and follow sequentially.

**Constructive Feedback:**
To enhance professional presentation and reproducibility, consider using the Scikit-Learn `Pipeline` and `ColumnTransformer` instead of performing categorical encoding and scaling manually outside the model fitting process. This integrates all preprocessing steps directly into the model training pipeline.

### 2. Feature Selection & Justification

**Positive:**
The author correctly selected all six available features, which is appropriate for this dataset as all variables (`age`, `bmi`, `smoker`, etc.) are strong predictors of the target. The use of the correlation matrix is good justification for confirming the importance of numerical features.

**Constructive Feedback:**
The approach to categorical data preprocessing should be refined. Using **`LabelEncoder`** for the binary features (`sex`, `smoker`) is generally discouraged because it assigns arbitrary numerical values (0 and 1) that the model might interpret as an ordinal rank. The recommended best practice is to use **One-Hot Encoding (OHE)** for all nominal categorical variables, as it prevents the introduction of artificial ordering.

### 3. Model Performance & Comparisons

**Positive:**
All three required linear models (Linear Regression, Ridge, and Lasso) were implemented and evaluated using the correct metrics ($R^2$, MAE, MSE, RMSE). The comparison table is clear and summarizes the models' results effectively.

**Constructive Feedback:**
The models achieved similar, modest performance ($R^2 \approx 0.75$). This performance plateau indicates the primary limitation of the model is not multicollinearity (which Ridge addresses) but likely **non-linearity** and missing **interaction effects** (e.g., the compounding cost of *age* for a *smoker*). I suggest replacing or adding a **Polynomial Regression** model (degree 2 or 3) to the comparison. This addition is often crucial for the insurance dataset and would likely increase the $R^2$ significantly, providing a much stronger final result.

### 4. Reflection Quality

**Positive:**
The notebook includes reflections after each major section, demonstrating adherence to all assignment requirements. The author correctly identifies that the models perform "average" and that there's potential for better performance.

**Constructive Feedback:**
The reflections could be more deeply tied to machine learning theory and diagnostic tools. For instance, after observing the plateau in performance, the reflection should specifically mention potential violations of linear assumptions (like **heteroscedasticity** or non-linearity) as the reason for the average $R^2$. Including and interpreting a **Residual Plot** for the baseline model would provide the visual evidence needed to justify the need for Polynomial features.
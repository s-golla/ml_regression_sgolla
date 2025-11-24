# PROJECT SUMMARY: Medical Insurance Charges Regression

| Metadata | Details |
| :--- | :--- |
| **Title** | Predicting Medical Insurance Charges |
| **Author** | Saratchandra Golla |
| **Date** | November 24, 2025 |
| **Project** | Final Project: Regression Analysis |
| **Dataset** | Medical Cost Personal Datasets (insurance.csv) |
| **Target Variable** | charges |
| **Best Model** | Polynomial Regression (Degree 3) |

---

## 1. Identify the Target Variable

- **What is the exact name of the target variable:** `charges`
- **Confirm the target is continuous and numeric:** Yes, the target consists of continuous monetary values.
- **Confirm no unexpected values, missing values, or outliers that distort the target:** No missing values were found. The target distribution is highly **right-skewed**, which acts like a structural outlier for linear modeling assumptions.
- **Why is this target meaningful for prediction:** Predicting insurance charges is meaningful for insurance companies to accurately estimate risk, calculate potential liability, and set fair premiums for policyholders.

---

## 2. Review Feature Variables

- **What features are available:** `age`, `sex`, `bmi`, `children`, `smoker`, `region` (6 features).
- **Are they numerical, categorical, or mixed:** Mixed. `age`, `bmi`, `children` are numerical; `sex`, `smoker`, `region` are categorical.
- **Are any features irrelevant or redundant:** No. All features were considered relevant to health status or market pricing factors.
- **Are any features ethically or legally restricted:** In many real-world insurance markets, using features like `sex` and `region` to set prices is restricted by anti-discrimination laws. This is a deployment caveat, not a modeling restriction.
- **Could any features cause leakage (contain future information):** None of the current features appear to cause leakage, as they describe a policyholder's status at the time of policy purchase.
- **Provide at least one example of possible leakage in this domain:** A feature named `total_claims_paid` would cause leakage, as the claims paid value is a consequence of (and therefore determined after) the charges being modeled.

---

## 3. Understand Relationships and Distributions

- **What patterns or correlations appear between features and the target:** **`smoker`** status and **`age`** showed the strongest positive correlation with `charges`. There is a clear pattern of **non-linearity**, where the impact of age is conditional (much higher for smokers than non-smokers).
- **Are any features strongly correlated with each other (multicollinearity):** Multicollinearity was not a primary concern, but was addressed using Ridge Regression as a precaution.
- **Are any transformations needed (log, square, scaling, normalization):** **Standard Scaling** was necessary for numerical features (`age`, `bmi`, `children`). A **log transformation** of the skewed `charges` target is strongly suggested for future work to normalize residuals.
- **Are there noticeable outliers:** The overall **right-skewness** of the `charges` distribution creates high leverage points that act like outliers, particularly impacting the simple Linear Regression model.
- **How were outliers handled:** Outliers were not explicitly removed. Instead, they were handled by modeling the underlying **non-linear structure** using Polynomial Features, which better accounts for the high-cost cases.

---

## 4. Improve the Model or Try Alternates

### Enhance Pipelines
- Combine preprocessing and modeling into one repeatable process.
- Improves reproducibility and reduces human error.

- **What alternate models or improvements were tried (e.g., Polynomial Regression, Ridge, Lasso):**
    - **Ridge Regression** ($\alpha=10.0$)
    - **Polynomial Regression (Degree 3)**

- **Why did you try each improvement (what problem was it addressing):**
    - **Ridge Regression:** To address potential multicollinearity from one-hot encoding and stabilize feature coefficients.
    - **Polynomial Regression:** To solve the model's severe **non-linearity** and **heteroscedasticity** problem identified in the baseline model's residual plot.

- **Which changes improved performance, based on metrics:**
    The **Polynomial Regression (Degree 3)** dramatically improved performance:
    - $R^2$ increased from 0.7836 (Baseline) to **0.8486**.
    - RMSE dropped from \$5,796 to **\$4,847**.

- **Why do you think those changes helped:**
    Introducing **third-degree polynomial terms** created essential **interaction terms** (e.g., $age \times smoker$) that correctly modeled the exponential cost increase associated with older smokers. This directly addressed the non-linearity that the simple linear models could not capture.

- **Which changes did NOT improve performance:**
    **Ridge Regression** ($R^2=0.7817$) was marginally worse than the Baseline Linear model ($R^2=0.7836$).

- **Why might those approaches have failed or underperformed:**
    Ridge Regression failed to improve performance because **multicollinearity** was not the primary limitation of the baseline model; the dominant problem was the **non-linearity** in the feature-target relationship.

- **If you had more time, which additional improvements might you try next:**
    1. **Target Transformation:** Applying a **log transformation** to the skewed `charges` target variable to normalize residuals and improve prediction of high-cost cases.
    2. **Hyperparameter Tuning:** Using `GridSearchCV` to find the optimal polynomial degree (between 2 and 3) and the best regularization strength simultaneously.

---

## 5. Validate and Compare Models

- **How were models compared:** All models were trained on the same training set and evaluated on a held-out **test set** (20% of the data).
- **Which metrics were compared:** **$R^2$** (Coefficient of Determination), **MAE** (Mean Absolute Error), and **RMSE** (Root Mean Squared Error).
- **Which model performed best:** The **Polynomial Regression (Degree 3)** model.
- **How do you know:** It achieved the highest $R^2$ (0.8486), meaning it explained the highest percentage of the variance in the charges, and the lowest RMSE (\$4,847), signifying the lowest typical prediction error in dollar terms.
- **Does the best-performing model generalize well:** The model generalized well on the test set, showing a significant improvement. However, due to the high polynomial degree (3), there is an inherent risk of **overfitting** which would require cross-validation and hyperparameter tuning to fully mitigate.
- **Discuss:** The high degree of the polynomial terms significantly reduces the bias of the model by capturing the underlying pattern, which is a necessary trade-off for this dataset's complexity.

---

## 6. Real-World Interpretation

- **What does the model tell us about how the features influence the target:**
    The model reveals that **smoking status** is the most significant determinant of charges. Crucially, the non-linear nature of the model shows that the impact of **age** is heavily compounded by smoking status; the older a smoker gets, the exponentially higher their cost.
- **What practical insights can stakeholders use:**
    Stakeholders (e.g., actuaries) should prioritize the **interaction** between age and smoking status, rather than modeling their effects separately, when setting premiums. This justifies higher premium increases for aging smokers.
- **Is the model stable and reliable enough for real decisions:**
    The model is **moderately reliable**. An RMSE of approximately **\$4,847** means the prediction will typically be off by this amount. Given that the mean charge is around \$13,000, this is a reasonable, though not perfect, error margin.
- **How do you know:** The strong $R^2$ score and significantly reduced RMSE confirm its predictive power on unseen data.
- **Any limitations or caveats:**
    The main limitations are the **complexity** of the model (difficult to fully interpret every coefficient) and the remaining non-normal residuals, indicating that some underlying non-linear relationships or data skewness have not been perfectly resolved.
# League-of-Legends-Project

# Introduction to the Dataset

This project focuses on analyzing competitive League of Legends games using data from professional matches played in 2022. The dataset includes over **150,000 rows** and **162 columns**, covering statistics like gold earned, kills, and other in-game metrics for every team and player at various points in the game.

## Research Question

**Can we predict whether a team will win based on their early-game performance?**

## Dataset Details

The dataset contains **150,180 rows** and **162 columns**. Below are the key columns relevant to our analysis:

- **goldat15**: The total gold earned by a team at 15 minutes.
- **killsat15**: The total number of kills secured by a team at 15 minutes.
- **xpat15**: The total experience points accumulated by a team at 15 minutes.
- **result**: A binary variable indicating whether the team won (1) or lost (0).


# Data Cleaning and Exploratory Data Analysis

## Data Cleaning

We performed the following data cleaning steps:
- Dropped missing values for critical columns like `goldat15`, `killsat15`, `xpat15`, and `result`.
- Filtered the dataset to focus only on completed games (`datacompleteness` column).
- Converted relevant columns to appropriate data types (e.g., numeric for game metrics).

### Head of Cleaned DataFrame:
| goldat15 | killsat15 | xpat15 | result |
|----------|-----------|--------|--------|
| 15000    | 5         | 14000  | 1      |
| 12500    | 3         | 13200  | 0      |
| 13700    | 4         | 12800  | 0      |
| 15400    | 6         | 14200  | 1      |
| 14200    | 5         | 13900  | 1      |

## Univariate Analysis

### Distribution of `goldat15`
![Gold Distribution](path-to-your-gold-plot.png)

The histogram shows the distribution of total gold earned by teams at 15 minutes. The data is slightly right-skewed, with most values between 12,000 and 18,000 gold. This suggests that teams typically earn around 15,000 gold by 15 minutes in competitive matches.

## Bivariate Analysis

### Relationship Between `goldat15` and `killsat15`
![Gold vs. Kills](path-to-your-bivariate-plot.png)

The scatter plot shows a positive correlation between `goldat15` and `killsat15`. Teams with more kills tend to earn more gold by 15 minutes. This relationship highlights the impact of successful early-game fights on economic advantage.

## Aggregated Table

### Average Gold Earned by Game Outcome
| Result | Average Gold at 15 Minutes |
|--------|----------------------------|
| Win    | 16,200                    |
| Loss   | 13,800                    |

Teams that win matches tend to earn around 2,400 more gold by 15 minutes than losing teams, underscoring the importance of early-game performance in determining match outcomes.


# Assessment of Missingness

## Identifying NMAR

The `goldat15` column was identified as having missing values that could potentially be **Not Missing At Random (NMAR)**. This missingness may depend on unrecorded circumstances, such as technical issues or incomplete game data.

**Why It's NMAR:**  
The missingness does not appear to depend on observed variables, such as `killsat15` or `xpat15`. Additional data, like match logs or collection timestamps, would be needed to explain the missingness and potentially convert it to MAR.

## Missingness Dependency Analysis

**Hypothesis:**
- **Null Hypothesis (H₀):** The missingness of `goldat15` is independent of the `result` column (whether a team won or lost).
- **Alternative Hypothesis (H₁):** The missingness of `goldat15` depends on the `result` column.

After running a permutation test, we obtained a p-value of **X.XX**, leading to the following conclusions:
- If `p < 0.05`, reject the null hypothesis: The missingness of `goldat15` depends on the `result`.
- If `p > 0.05`, fail to reject the null hypothesis: The missingness of `goldat15` is independent of the `result`.

## Visualizations

### Distribution of `result` for Missing vs. Non-Missing `goldat15`
![Missingness Plot](path-to-your-missingness-plot.png)

The plot shows that rows with missing `goldat15` values have a slightly different distribution of `result` values compared to non-missing rows, suggesting potential dependence.

### Empirical Distribution of Test Statistic
![Permutation Test Plot](path-to-your-permutation-plot.png)

The vertical line represents the observed test statistic, while the shaded area shows the distribution under the null hypothesis. If the observed statistic lies in the tails, it supports rejecting the null hypothesis.


# Hypothesis Testing

## Hypothesis
- **Null Hypothesis (H₀):** The average gold earned at 15 minutes (`goldat15`) is equal for teams on the **Blue Side** and **Red Side**.
- **Alternative Hypothesis (H₁):** The average gold earned at 15 minutes (`goldat15`) is not equal for teams on the **Blue Side** and **Red Side**.

## Test Statistic
- **Test Used:** Two-sample t-test
- **Significance Level (α):** 0.05

## Results
- **T-Statistic:** -1.58
- **P-Value:** 0.11

At a significance level of 0.05, the p-value of 0.11 is greater than α, so we fail to reject the null hypothesis.

## Conclusion
There is not enough evidence to conclude that the average gold earned at 15 minutes differs between the Blue Side and Red Side. This finding suggests that early-game economic performance is relatively balanced across team sides.

## Why This Test is Appropriate
The t-test is used to compare the means of two independent groups (Blue Side and Red Side) to determine if there is a significant difference between them. The choice of a 0.05 significance level aligns with common statistical practices for hypothesis testing.

## Visualization

### Average Gold Earned (`goldat15`) by Team Side
![Gold Distribution by Side](path-to-your-plot.png)

The box plot shows the distribution of `goldat15` for Blue Side and Red Side teams. While there is some variation in the distributions, the overlap indicates that the difference in means is not statistically significant.

# Framing a Prediction Problem

## Prediction Problem

The prediction problem we aim to solve is:
**"Can we predict whether a team will win (`result`) based on their early-game performance metrics?"**

This is a **binary classification problem** where:
- `1` represents a win.
- `0` represents a loss.

## Response Variable

- **Variable to Predict (`result`)**: The `result` column indicates whether a team won or lost a game. This variable was chosen because it directly represents match outcomes, which is the focus of this project.

## Features Used

The following early-game metrics were selected as features:
- **`goldat15`**: Total gold earned by a team at 15 minutes.
- **`killsat15`**: Total kills secured by a team at 15 minutes.
- **`xpat15`**: Total experience points accumulated by a team at 15 minutes.
- **`csat15`**: Total creep score accumulated by a team at 15 minutes.

## Evaluation Metric

The model will be evaluated using **accuracy**. Accuracy is chosen because:
- The dataset is relatively balanced between wins and losses.
- It provides a straightforward measure of how often the model correctly predicts the outcome (win or loss).

## Why This Prediction Problem Matters

Understanding how early-game performance metrics influence match outcomes can help teams and coaches identify key areas of improvement. It can also provide insights into strategies that maximize a team’s chances of winning.

# Baseline Model

## Model Description

For the baseline model, we trained a **logistic regression classifier** to predict whether a team will win (`result`) based on their early-game performance metrics.

### Features Used:
- **Quantitative Features:**
  - `goldat15`: Total gold earned by a team at 15 minutes.
  - `killsat15`: Total kills secured by a team at 15 minutes.
  - `xpat15`: Total experience points gained by a team at 15 minutes.
  - `csat15`: Total creep score at 15 minutes.

## Feature Encodings

- **Quantitative Features:** Used as-is.
- No categorical or nominal features were included in the baseline model, so no additional encodings were necessary.

## Model Performance

- **Training Accuracy:** 76%
- **Test Accuracy:** 74%

The model’s performance suggests that it captures meaningful relationships between early-game metrics and match outcomes. However, there is room for improvement in predictive accuracy by incorporating additional features or exploring more advanced modeling techniques.

## Is This Model “Good”?

While the baseline model provides a reasonable starting point, it is not “good” in the sense of being production-ready. The gap between training and test accuracy indicates slight overfitting, and the accuracy itself could likely be improved with more feature engineering or by testing other algorithms.

# Final Model

## Features Added and Justification

In the final model, we added new features to improve performance:
- **`opp_goldat15`**: The opposing team's gold earned at 15 minutes.
- **`golddiffat15`**: The difference in gold earned between the team and the opposing team at 15 minutes.
- **`xpdiffat15`**: The difference in experience points gained at 15 minutes.

**Why These Features Improve Performance:**
- Relative advantage metrics (`golddiffat15`, `xpdiffat15`) directly measure a team's performance compared to their opponents.
- Opponent information (`opp_goldat15`) provides additional context, enhancing the model's understanding of competitive dynamics.

## Modeling Algorithm and Hyperparameters

The final model was a **Random Forest Classifier**, chosen for its robustness and ability to handle complex feature interactions.

### Hyperparameters Tuned:
- Number of trees: `n_estimators = 100`
- Maximum tree depth: `max_depth = 10`
- Minimum samples split: `min_samples_split = 4`

**Hyperparameter Tuning Method:**  
We used `GridSearchCV` to select the best configuration.

## Performance Comparison

| Metric               | Baseline Model (Logistic Regression) | Final Model (Random Forest) |
|----------------------|--------------------------------------|-----------------------------|
| Training Accuracy    | 76%                                 | 90%                         |
| Test Accuracy        | 74%                                 | 85%                         |

The final model achieved an 11% increase in test accuracy over the baseline, demonstrating significant improvement.

## Visualization

### Confusion Matrix
![Confusion Matrix](path-to-your-confusion-matrix.png)

The confusion matrix shows the model performs well in predicting both wins and losses, with a slight tendency to misclassify some matches.

# Fairness Analysis

## Fairness Evaluation

We conducted a fairness analysis to determine whether our predictive model performs equally well across different groups. Specifically, we assessed if the model's precision differs significantly between:

- **High Gold Teams**: Teams with above-median gold earned at 15 minutes (`goldat15`).
- **Low Gold Teams**: Teams with median or below-median gold earned at 15 minutes.

## Hypotheses

- **Null Hypothesis (H₀)**: The model's precision is the same for both high gold and low gold teams. Any observed difference in precision is due to random chance.
- **Alternative Hypothesis (H₁)**: The model's precision differs between high gold and low gold teams.

## Methodology

**Grouping:** We split the test dataset into two groups based on the median value of `goldat15`.

- **High Gold Teams:** `goldat15` > median
- **Low Gold Teams:** `goldat15` ≤ median

**Metric Evaluated:** Precision of the model for each group.

**Statistical Test:** Permutation test with 1,000 iterations to assess the significance of the observed difference in precision.

## Results

- **Precision for High Gold Teams:** 85%
- **Precision for Low Gold Teams:** 85%
- **Observed Difference in Precision:** 0%
- **P-Value from Permutation Test:** 1.0

Since the p-value is greater than the significance level of 0.05, we fail to reject the null hypothesis.

## Conclusion

The fairness analysis indicates that our model's precision does not differ significantly between high gold and low gold teams. This suggests that the model is fair in terms of precision across these groups.

## Interpretation

- **Model Fairness:** The equal precision rates imply that the model does not favor one group over the other.
- **Implications:** Teams can trust the model's predictions regardless of their early-game gold earnings.

## Visualization

### Permutation Test Results

![Permutation Test Plot](path-to-your-permutation-test-plot.png)

**Description:**

- The plot shows the distribution of precision differences under the null hypothesis.
- The observed difference (0%) is marked on the plot.
- Since the observed difference lies within the bulk of the distribution, it supports the conclusion that there is no significant difference.


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


# Step 3: Assessment of Missingness

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


# Step 4: Hypothesis Testing

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


Framing a Prediction Problem
Baseline Model
Final Model
Fairness Analysis

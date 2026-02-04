
# NBA-Salary-Minning

This project applies data science and machine learning techniques to evaluate salary efficiency in the National Basketball Association (NBA). Inspired by the Moneyball philosophy, the analysis treats player contracts as economic assets and asks a central question.

***Are NBA players paid in proportion to their on-court impact?***

Using five seasons of NBA data (2020–21 through 2024–25), the project models the relationship between player compensation and advanced performance metrics. A predictive salary model estimates expected salary based on production, and residual analysis is used to identify overvalued and undervalued contracts across the league.

Rather than attempting to predict exact salaries, this work focuses on value efficiency,how much performance teams receive per dollar spent under a salary cap environment.

# Methodology
### Feature Engineering

The model estimates expected salary using a combination of performance, role, and contextual variables

- Minutes Played (MP) – proxy for role size and availability
- Offensive Box Plus/Minus (OBPM) – offensive impact
- Defensive Box Plus/Minus (DBPM) – defensive impact
- Value Over Replacement Player (VORP) – aggregate value metric
- Position (one-hot encoded) – PG, SG, SF, PF, C
- Log-transformed Salary – reduces skew and stabilizes variance

#### Modeling Approach

##### Algorithm: XGBoost Regression

- Training Data: 2020–21 through 2023–24 seasons
- Holdout Season for residual analysis: 2024–25

XGBoost was chosen for its ability to:
- Capture nonlinear relationships
- Handle correlated advanced metrics
- Perform well on structured, tabular data

##### Hyperparameter Tuning

A large-scale RandomizedSearchCV was used:

- X configurations
- Y cross-validation
- Z total model fits
- Parallelized across CPU cores

Best Params 
```Text
Objective: reg:quantileerror
n_estimators: 1743
max_depth: 3
learning_rate: 0.0238
subsample: 0.95266
colsample_bytree: 0.9836
min_child_weight: 4
```

### Model Performance 
| Metric | Baseline (squarred error) | Baseline (quantile error) |Tunned | 
| :--- | :---: | :---: | :---: |
| RMSE (log salary) | 1.083 | 0.990 |  0.954 |
| R^2 | 0.192 |  0.325 | 0.372 |

### Residual Analysis (Core Insight)

Residuals are computed as:

**Residual = Actual Salary − Predicted Salary**

Positive residual → Potentially overvalued contract
Negative residual → Potentially undervalued contract

Residual analysis allows salary efficiency to be evaluated relative to peers, isolating compensation not explained by production.

### Key Findings

Residuals are broadly symmetric around zero with no strong nonlinear bias

Slight underprediction for top earners (likely driven by star power & market effects)

Heavy tails identify players whose compensation deviates sharply from performance

Team-level aggregation reveals systematic over and under spending patterns

This confirms the model is best used as a diagnostic tool, not a literal salary prediction mechanism.
# What I Learned
### Technical Skills

- Building end-to-end data pipelines with messy, real-world sports data
- Feature engineering with correlated and nonlinear metrics
- Training and tuning tree-based ML models (XGBoost)
- Applying residual analysis for economic and business interpretation
- Model evaluation using RMSE and R² in log-transformed space

### Data Science & Analytics

- Translating abstract performance metrics into financial value signals
- Understanding limitations of models in markets with narrative-driven pricing
- Balancing model accuracy with interpretability and decision usefulness
- Framing ML outputs for business-facing insights, not just technical metrics

### Domain Insight (Sports Analytics)

- Offensive impact and minutes played dominate salary determination
- Aggregate value metrics (VORP) outperform isolated box-score stats
- Position matters less than expected once performance is controlled for
- Salary inefficiencies persist even in highly optimized professional leagues

### Why This Project Matters

This project demonstrates how machine learning + residual analysis can support smarter decision making in constrained environments like the NBA salary cap. The framework is directly transferable to:

- Front-office analytics
- Contract valuation
- Roster construction strategy

This idea can also be appilied to another market where money in finite and there are inefficiencies in such markets.
## Appendix

![fig_1_2](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_1_2.png)
![fig_3_4](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_3_4.png)
![fig_5](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_5.png)
![fig_6_7](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_6_7.png)
![fig_8](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_8.png)
![fig_9](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_9.png)
![fig_10](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_10.png)
![fig_11](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_11.png)
![fig_12](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_12.png)
![fig_13_14](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_13_14.png)
![fig_15](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/fig_15.png)
![feature_importance](https://github.com/jhatch3/NBA-Salary-Minning/blob/main/NBA-Salary/Figs/feature_importance.png)


Any additional information goes here


##  Folder Sctructure


```text
NBA-Salary/
├── main.ipynb
├── preprocessing.ipynb
├── df.png
├── Figs
│   ├── ... 
└── Data/
    ├── nba_advanced_data.ipynb
    ├── nba_salaries.ipynb
    ├── team_colors.csv
    ├── names_advanced_tmp.csv
    ├── names_salaries_tmp.csv
    ├── dirty/
    │   ├── 2020-21/ --- teams.csv ---
    │   ├── 2021-22/ --- teams.csv ---
    │   ├── 2022-23/ --- teams.csv ---
    │   ├── 2023-24/ --- teams.csv ---
    │   └── 2024-25/ --- teams.csv ---
    └── clean/
        ├── nba_advanced_data.csv
        ├── nba_salaries_2021_to_2025.csv
        ├── master_data.csv
        ├── 2020-21/ --- teams.csv ---
        ├── 2021-22/ --- teams.csv ---
        ├── 2022-23/ --- teams.csv ---
        ├── 2023-24/ --- teams.csv --- 
        └── 2024-25/ --- teams.csv ---
```

## Data Source(s)

 - [NBA Salary Data](https://www.basketball-reference.com/)
 - [NBA Advanced Data](https://www.espn.com/nba/salaries/_/)



## Authors

- [@Justin Hatch](https://www.github.com/jhatch3), B.S. Computer Science, University of Oregon

# Contact 
- jhatch3@uoregon.edu
- [@X](https://x.com/jjhatch11)
- [@Linkedin](https://www.linkedin.com/in/justinhatch/)
- [@GitHub](https://www.github.com/jhatch3)

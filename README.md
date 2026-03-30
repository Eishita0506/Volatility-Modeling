# Overview
This project focuses on modeling and forecasting financial market volatility using classical time-series approaches—ARCH, GARCH, and EWMA. The goal is to understand how different models capture volatility clustering and persistence, and to benchmark their effectiveness in short-horizon forecasting.The empirical analysis highlights clear differences in how ARCH, GARCH, and EWMA models capture the dynamics of financial market volatility, particularly in terms of shock responsiveness, persistence, and forecasting accuracy.
## Objective
- Model time varying volatility in financial returns of JP Morgan
- Compare ARCH, GARCH, EWMA
- Forecast short-term volatility (5-day horizon)
- Evaluate
## ARCH Model
ARCH (Auto-regressive Conditional Heteroskedastic) model captures volatility clustering by modeling current variance as a function of past squared shocks, allowing volatility to change over time. It is not used in industry as better models exist
Limitations:
- Does not capture long term memory effiently
- Has no memory of past volatility
## GARCH Model
GARCH (Generalized Auto-regressive Conditional Heteroskedastic) Model is an improved version and industry standard for volatility modelling. It uses past shocks as well as past volatility to capture persistence with fewer parameters or lags. It is used along with advanced model as a standard model to gain accurate volatility modelling
Limitations:
- Inability to model asymmetry, fat tails, regime shifts, and forward-looking market expectations, making them insufficient on their own for modern financial modeling.
Used by:
- Hedge funds
- Quant funds
- Risk modeling teams
When chosen:
- Medium-frequency strategies
- Volatility forecasting
- Stress testing
## EWMA Model
EWMA (Exponential Moving Average) Model is a simple model that gives more weightage to recent observation and less weightage to older observations. It uses past shocks as well as past volatility for modelling.
Used by:
- Banks (Basel frameworks)
- Asset managers
- Risk engines (daily VaR)
When chosen:
- When volatility is very high and GARCH model fails
- Need real-time updates
- Large portfolios
- Regulatory reporting
## Results
### ARCH Model​
- Predicted Volatility: 1.5631
- Actual Volatility: 1.6919
### GARCH Model
- Predicted Volatility: 1.6210
- Actual Volatility: 1.6919
- Key parameters:
- 𝛼1=0.0165
- 𝛽1=0.9737
### EWMA Model
- Predicted Volatility: 1.5269
- Actual Volatility: 1.6919
- λ = 0.94
# Key Insights
### 1. Volatility Persistence and Model Performance
- A key observation from the GARCH(1,1) estimation is the high persistence of volatility, with 
𝛼+𝛽≈0.99
- This indicates that shocks to volatility decay slowly over time, consistent with well-documented stylized facts in financial markets. This persistence explains the superior performance of the GARCH model relative to ARCH and EWMA. By incorporating both past shocks and past variance, GARCH effectively captures the long memory structure of volatility. In contrast, the ARCH model, which relies solely on lagged squared shocks, fails to account for this persistence, leading to comparatively weaker forecasts.
### 2. Trade-off Between Reactivity and Stability
The comparison between ARCH and EWMA reveals an important trade-off:
- ARCH is highly reactive to recent shocks but lacks smoothing, making it sensitive to noise.
- EWMA, with a fixed decay parameter (λ=0.94), provides smoother estimates but may underreact during periods of rapidly changing volatility regimes. The empirical results show that EWMA tends to underestimate realized volatility, particularly during elevated volatility periods. This reflects its inflexibility in adapting to regime shifts, as the decay structure is fixed rather than learned from data.
### 3.Implications for Forecasting Accuracy
All three models exhibit some degree of underestimation relative to realized volatility. This is not unexpected, as:
- These models are backward-looking, relying solely on historical returns.
- They do not incorporate forward-looking market expectations, such as implied volatility from options markets.
- They assume relatively simple distributional structures (e.g., conditional normality), which fail to capture fat tails and extreme events.
- Among the models, GARCH demonstrates the closest alignment with realized volatility, suggesting that capturing persistence is more critical than immediate responsiveness for short-horizon forecasting.
### 4. Structural Limitations and Market Realities
Despite their effectiveness, all three models share common limitations:
- Absence of asymmetry: They do not account for the leverage effect, where negative returns have a larger impact on volatility than positive returns.
- Inability to capture regime shifts: Sudden transitions (e.g., financial crises) are not well modeled.
- Lack of microstructure information: High-frequency dynamics, order flow, and liquidity effects are ignored.
- These limitations suggest that while classical models are useful for baseline estimation, they are insufficient for capturing the full complexity of modern financial markets.
#### 5. Industry Relevance and Model Selection
From an applied perspective, the results align with industry practices:
- EWMA is widely used in risk management due to its computational efficiency and stability.
- GARCH is preferred for volatility forecasting and scenario analysis, given its ability to model persistence.
- ARCH is largely of theoretical importance and rarely used in isolation.
In practice, institutions often employ hybrid frameworks, combining:
- Time-series volatility models (e.g., GARCH)
- Market-implied measures (e.g., implied volatility)
- Machine learning models for nonlinear pattern recognition
# Conclusion
While GARCH provides the most accurate volatility forecasts among the models considered, the broader implication is that effective volatility modeling in modern financial markets requires integrating persistence-based models with forward-looking and data-driven approaches.

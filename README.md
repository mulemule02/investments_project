# International Portfolio Diversification Project

## Overview

This project analyzes the benefits of international diversification and dynamic trading strategies for US investors through systematic portfolio construction and performance evaluation. The analysis combines international stock market indices with currency exposures to evaluate various trading strategies including momentum, reversal, carry, and dollar strategies.

## Team Members

- **MULEWICZ Jagoda Janina** (396439)
- **BRIOT Paul Constantin** (346444)
- **PATULARU Andrei Eugeniu** (388746)
- **NAHOUL Victor** (339407)

*EPFL, Lausanne, Switzerland*


## Data Sources

### Stock Market Data
- **Source**: WRDS Monthly World Indices
- **Period**: April 2002 - December 2024
- **Countries**: Australia, France, Germany, Japan, Switzerland, United Kingdom, USA (CRSP)
- **Risk-free Rate**: 1-month T-Bill from CRSP

### Currency Data
- **Source**: Federal Reserve Economic Data (FRED)
- **Currencies**: AUD, EUR, JPY, CHF, GBP vs USD
- **Additional**: 3-month interbank rates for each country

## Investment Strategies Implemented

### 1. International Diversification Strategy (DIV)
- **Equal Weight Portfolio**: Equal allocation across all indices
- **Risk-Parity Portfolio**: Inverse volatility weighting based on 60-month rolling windows
- **Mean-Variance Portfolio**: Optimal allocation using expected returns and covariance matrix
- **Currency Hedging**: Analysis of hedged vs unhedged international exposure

### 2. Equity Index Momentum Strategy (MOM)
- **Signal**: 11-month lagged cumulative returns (months t-12 to t-1)
- **Construction**: Long-short portfolio based on cross-sectional momentum rankings
- **Performance**: Long leg: 8.1% annual return, Short leg: -9.9% annual return

### 3. Equity Index Long-Term Reversal Strategy (REV)
- **Signal**: 5-year lagged returns (months t-60 to t-12)
- **Construction**: Long countries with weak long-term performance, short strong performers
- **Logic**: Mean reversion in international equity markets

### 4. Currency Carry Strategy (CARRY)
- **Signal**: Interest rate differentials (foreign rate - USD rate)
- **Construction**: Long high-carry currencies, short low-carry currencies
- **Mechanism**: Exploit persistent interest rate differentials

### 5. Currency Dollar Strategy (DOLLAR)
- **Construction**: Short equal-weighted basket of all foreign currencies vs USD
- **Purpose**: Capture broad USD strength/weakness trends

### 6. Optimal Fund Strategy (STRAT)
- **Combination**: Risk-parity weighting of MOM, REV, CARRY, and DOLLAR strategies
- **Optimization**: Mean-variance optimal allocation between DIV and STRAT overlay
- **Target**: 15% annualized volatility

## Key Findings

### Performance Summary
| Strategy | Annual Return | Volatility | Sharpe Ratio |
|----------|---------------|------------|--------------|
| DIV (Risk-Parity, Hedged) | 5.40% | 12.71% | 0.306 |
| MOM (Total) | -1.78% | 7.93% | -0.224 |
| REV (Total) | -0.54% | 7.30% | -0.074 |
| CARRY | 0.98% | 13.35% | -0.039 |
| DOLLAR | -0.41% | 9.13% | -0.210 |
| Optimized Fund | 11.12% | 13.78% | 0.654 |

### Key Insights

1. **International Diversification Benefits**: Currency-hedged risk-parity portfolios provide superior risk-adjusted returns compared to unhedged strategies.

2. **Strategy Independence**: Low correlations between strategies (MOM, REV, CARRY, DOLLAR) and the DIV benchmark suggest potential diversification benefits.

3. **Factor Exposure**: Fama-French 5-factor analysis reveals primary exposure to market risk (β = 0.603) with limited exposure to size, value, profitability, or investment factors.

4. **Market Efficiency**: No significant alpha generation (p = 0.717), consistent with the Efficient Market Hypothesis and CAPM predictions.


### Data Access Requirements
- WRDS account for stock market data
- FRED API key for currency and interest rate data


### Currency Hedging
Currency-hedged returns neutralize exchange rate risk:
```
X^EU_{t+1} = (S_{t+1}/S_t)(1 + r^EU_t) - (1 + r^US_t)
F^FR,US_t = R^FR_t - X^EU_t
```

### Rolling Window Optimization
- **Window Size**: 60 months for all rolling estimates
- **Rebalancing**: Monthly based on updated parameter estimates
- **Volatility Targeting**: 15% annualized volatility for fund strategies

### Statistical Testing
All strategy returns tested for statistical significance using t-statistics and p-values at 5% significance level.

## Risk Management

### Volatility Targeting
All fund strategies maintain constant 15% annualized volatility through dynamic scaling:
```
scale_t = 0.15 / (√12 × σ_monthly,t)
```

### Position Limits
Strategy weights clipped within [-1, +1] range to prevent extreme leverage during high estimation error periods.

## Limitations and Considerations

1. **Survivorship Bias**: Analysis limited to major developed markets with complete data
2. **Transaction Costs**: Not explicitly modeled in strategy returns
3. **Parameter Stability**: Rolling window estimates may be noisy during volatile periods
4. **Currency Regime Changes**: Fixed exchange rate periods may affect currency strategy performance

## Academic Context

This project demonstrates practical applications of:
- International portfolio theory
- Factor investing and anomaly strategies
- Currency carry trade mechanics
- Mean-variance optimization with constraints
- Performance attribution using factor models

## References

- Fama, E.F., & French, K.R. (2015). A five-factor asset pricing model
- Lustig, H., Roussanov, N., & Verdelhan, A. (2011). Common risk factors in currency markets
- Jegadeesh, N., & Titman, S. (1993). Returns to buying winners and selling losers

---

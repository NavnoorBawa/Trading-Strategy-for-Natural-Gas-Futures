# Multi-Factor Trading Strategy for Natural Gas Futures

## Overview

I've developed a comprehensive quantitative framework for trading natural gas futures contracts, leveraging multiple datasets to extract predictive features and generate trading signals. The strategy employs a composite signal approach that weighs technical, fundamental, seasonal, and market positioning factors to identify high-conviction trading opportunities.

## Data Integration

My implementation integrates five primary datasets:

- **Price data**: Front-month (NG1) and second-month (NG2) natural gas futures
- **Inventory data**: Weekly natural gas storage figures in BCF
- **Weather data**: Heating Degree Days (HDD) and Cooling Degree Days (CDD) metrics
- **Market positioning data**: CFTC Commitment of Traders reports focusing on Managed Money positions
- **Derived seasonal indicators**: Historical monthly performance patterns

A key challenge addressed in the code is the standardization of date formats across various data sources, implemented through a custom date normalization function.

## Feature Engineering

The strategy employs both standard technical features and cross-dataset composite features:

### Standard Technical Features
- Price momentum and moving average crossovers
- RSI (Relative Strength Index)
- Bollinger Bands and percentile-based positioning
- Spread dynamics between front and second-month contracts

### Cross-Dataset Composite Features
- **Weather-Adjusted Inventory**: Normalizing inventory figures by total degree days to account for weather-driven demand variations
- **Managed Money/Price Ratio**: Identifying when speculative positioning becomes extreme relative to price levels
- **Historical Seasonal Performance**: Integrating monthly historical returns rather than using static seasonal rules

## Signal Generation Methodology

The signal generation module creates a weighted composite score integrating:

- Technical components (40% weight): MA crossovers, price momentum, spread dynamics
- Fundamental components (30% weight): Inventory changes, weather-driven demand metrics
- Positioning components (20% weight): Changes in speculative positioning from CFTC data
- Seasonal components (10% weight): Historical monthly performance patterns

## Risk Management Framework

I've implemented several risk management features:

- **Volatility-Based Position Sizing**: Dynamically adjusts position size based on recent volatility relative to historical norms
- **Signal Strength-Based Scaling**: Increases/decreases position size proportionally to signal conviction
- **Adaptive Exit Thresholds**: Modifies exit parameters based on volatility regime
- **Maximum Position Size Cap**: Limits maximum exposure to 25% of capital

## Backtesting Framework

The backtesting engine includes:

- Transaction-level position tracking
- P&L calculation with comprehensive trade analytics
- Equity curve generation and drawdown analysis
- Performance metrics calculation (Sharpe ratio, win rate, average return per trade)

## Performance Characteristics

Initial backtesting results demonstrate:

- Effective risk control with maximum drawdown of 2.48%
- A 44.44% win rate indicating potential for optimization
- Sharpe ratio heavily dependent on parameter tuning
- Strong filtering capabilities resulting in selective high-conviction trade signals

## Usage Instructions

To run the strategy:

```python
# Initialize the enhanced strategy
strategy = EnhancedNaturalGasStrategy()

# Load data
strategy.load_data(
    price_file='Natural_Gas_Data prices.csv',
    inventory_file='inventory.csv',
    hdd_file='HDD.csv',
    cdd_file='CDD.csv',
    positioning_file='Natural_Gas_Data positioning.csv'
)

# Merge datasets and engineer features
strategy.merge_datasets()
strategy.engineer_features()

# Backtest with custom parameters
strategy.backtest_strategy(
    initial_capital=100000, 
    position_size_pct=0.1, 
    use_enhanced_signal=True
)

# Visualize results
strategy.visualize_results()
```

## Future Development

I'm currently exploring several enhancements:

1. Incorporating additional weather forecast data to improve forward-looking signal components
2. Implementing regime-switching logic based on volatility and trend characteristics
3. Adding a machine learning layer to optimize feature weights
4. Expanding to a multi-timeframe approach to improve entry/exit timing

## Repository Information

Full implementation: [https://github.com/NavnoorBawa/Trading-Strategy-for-Natural-Gas-Futures](https://github.com/NavnoorBawa/Trading-Strategy-for-Natural-Gas-Futures)

For discussions or collaboration opportunities, please contact me via GitHub or LinkedIn.

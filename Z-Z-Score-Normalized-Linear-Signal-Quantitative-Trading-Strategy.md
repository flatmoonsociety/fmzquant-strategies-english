
> Name

Linear signal quantitative trading strategy based on Z-score normalization-Z-Score-Normalized-Linear-Signal-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/193a08cfaaf674f1ccb.png)

[trans]
#### Overview
This strategy is a quantitative trading system based on linear signals and Z-score normalization. It constructs standardized trading signals by combining exogenous variables such as RSI with price data, and uses thresholds to trigger transactions. This strategy is suitable for intraday and high-frequency trading scenarios and has strong adaptability and configurability.
#### Strategy Principle
The core principles of the strategy include the following key steps:
1. Linear signal construction: Use configurable weights (signal_alpha) to linearly combine the RSI indicator and price data to form an initial signal.
2. Z-score standardization: Based on the set lookback period (lookback_period), calculate the mean and standard deviation of the linear signal, and normalize the signal into Z-score form.
3. Threshold trigger mechanism: When the Z score is lower than the negative threshold, a long position is opened, and when it is higher than the positive threshold, a short position is opened. The threshold is controlled by the risk adjustment factor (risk_adjustment_factor).
4. Risk management: Set a stop-profit and stop-loss for each transaction, and flexibly adjust the risk-return ratio through percentage parameters.
#### Strategic Advantages
1. Signal standardization: Z-score transformation makes the signal have good statistical properties and facilitates the setting of universal thresholds.
2. Strong flexibility: signal_alpha can be adjusted to balance the influence of exogenous variables and prices.
3. Controllable risk: A complete stop-profit and stop-loss mechanism that can be flexibly configured according to market characteristics.
4. Good adaptability: suitable for multiple time periods and can be extended to other trading varieties with high liquidity.
#### Strategy Risk
1. Parameter sensitivity: Strategy performance is relatively sensitive to parameter selection and requires full backtest verification.
2. Dependence on market environment: Frequent transactions may occur in volatile markets with weak trends.
3. Signal lag: The lag caused by moving average calculation may affect the timing of entry.
4. Liquidity risk: High-frequency trading may face slippage losses when liquidity is insufficient.
#### Strategy optimization direction
1. Dynamic parameter adjustment: Introduce an adaptive mechanism to dynamically adjust the threshold and stop loss position according to market volatility.
2. Multiple signal confirmation: Add other technical indicators as filtering conditions to improve signal reliability.
3. Position management optimization: Design a dynamic position management system based on volatility and signal strength.
4. Transaction cost control: Optimize the logic of opening and closing positions to reduce cost losses caused by frequent transactions.
#### Summary
This is a quantitative trading strategy with clear structure and rigorous logic. Through linear combination and standardization processing, a robust trading signal system is constructed. The strategy has strong configurability and perfect risk management, but attention needs to be paid to parameter optimization and market adaptability. Through the suggested optimization direction, the stability and profitability of the strategy can be further improved. ||
#### Overview
This strategy is a quantitative trading system based on linear signals and Z-score normalization. It constructs standardized trading signals by combining exogenous variables like RSI with price data and triggers trades using thresholds. The strategy is suitable for intraday and high-frequency trading scenarios, offering strong adaptability and configurability.

#### Strategy Principle
The core principles include several key steps:
1. Linear Signal Construction: Uses configurable weights (signal_alpha) to linearly combine RSI indicator with price data to form initial signals.
2. Z-Score Normalization: Calculates mean and standard deviation of linear signals based on a lookback period, normalizing signals into Z-scores.
3. Threshold Trigger Mechanism: Opens long positions when Z-score falls below negative threshold and short positions when above positive threshold, controlled by risk_adjustment_factor.
4. Risk Management: Sets stop-loss and take-profit levels for each trade, with flexible risk-reward ratio adjustment through percentage parameters.

#### Strategy Advantages
1. Signal Standardization: Z-score transformation provides good statistical properties, facilitating universal threshold settings.
2. High Flexibility: Can balance influence of exogenous variables and price through signal_alpha adjustment.
3. Controlled Risk: Complete stop-loss and take-profit mechanism, configurable based on market characteristics.
4. Good Adaptability: Applicable to multiple timeframes, expandable to other highly liquid trading instruments.

#### Strategy Risks
1. Parameter Sensitivity: Strategy performance is sensitive to parameter selection, requiring thorough backtesting.
2. Market Environment Dependency: May generate frequent trades in range-bound markets with weak trends.
3. Signal Lag: Moving average calculations can introduce lag affecting entry timing.
4. Liquidity Risk: High-frequency trading may face slippage losses during low liquidity periods.

#### Strategy Optimization Directions
1. Dynamic Parameter Adjustment: Introduce adaptive mechanisms to dynamically adjust thresholds and stop-loss positions based on market volatility.
2. Multiple Signal Confirmation: Add other technical indicators as filtering conditions to improve signal reliability.
3. Position Management Optimization: Design dynamic position management system based on volatility and signal strength.
4. Transaction Cost Control: Optimize entry and exit logic to reduce costs from frequent trading.

#### Summary
This is a well-structured and logically rigorous quantitative trading strategy. It builds a robust trading signal system through linear combination and standardization processing. The strategy offers strong configurability and comprehensive risk management but requires attention to parameter optimization and market adaptability. Through the suggested optimization directions, the strategy's stability and profitability can be further enhanced.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-29 00:00:00
end: 2025-01-05 00:00:00
period: 15m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Linear Signal-Based Strategy", shorttitle = "LSB_V1", overlay=true)

// Inputs
lookback_period = input.int(14, title="Lookback Period for Moving Averages")
signal_alpha = input.float(0.5, title="Signal Weight Alpha (Exogenous Variable)")
take_profit_percent = input.float(0.02, title="Take Profit (%)")
stop_loss_percent = input.float(0.01, title="Stop Loss (%)")
risk_adjustment_factor = input.float(1.5, title="Risk Adjustment Factor")

// Fetch Exogenous Variable (Example: RSI as a Proxy)
rsi_value = ta.rsi(close, lookback_period)

// Linear Signal Calculation
linear_signal = signal_alpha * rsi_value + (1 - signal_alpha) * close

// Z-Score Normalization for Signal
mean_signal = ta.sma(linear_signal, lookback_period)
stddev_signal = ta.stdev(linear_signal, lookback_period)
z_score_signal = (linear_signal - mean_signal) / stddev_signal

// Entry Conditions
long_condition = z_score_signal < -risk_adjustment_factor
short_condition = z_score_signal > risk_adjustment_factor

// Risk Management
long_take_profit = close * (1 + take_profit_percent)
long_stop_loss = close * (1 - stop_loss_percent)
short_take_profit = close * (1 - take_profit_percent)
short_stop_loss = close * (1 + stop_loss_percent)

// Execute Trades
if (long_condition)
    strategy.entry("Long", strategy.long, qty=1)
    strategy.exit("Exit Long", "Long", stop=long_stop_loss, limit=long_take_profit)

if (short_condition)
    strategy.entry("Short", strategy.short, qty=1)
    strategy.exit("Exit Short", "Short", stop=short_stop_loss, limit=short_take_profit)



```

> Detail

https://www.fmz.com/strategy/477593

> Last Modified

2025-01-06 16:14:07

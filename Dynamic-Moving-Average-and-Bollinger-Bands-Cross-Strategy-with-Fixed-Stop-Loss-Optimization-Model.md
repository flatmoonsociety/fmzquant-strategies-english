
> Name

Dynamic-Moving-Average-and-Bollinger-Bands-Cross-Strategy-with-Fixed-Stop-Loss-Optimization-Model
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/a7039f06de5ae4a67c.png)

[trans]
#### Overview
This strategy is a trend following trading system that combines moving averages (MA) and Bollinger Bands. The strategy identifies market trends by analyzing the relationship between price and the 200-period moving average and the Bollinger Bands, while integrating a fixed percentage stop loss mechanism to control risk. The strategy adopts a position management of 2.86%, which matches the leverage of 35 times and reflects the prudent fund management concept.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Use the 200-period moving average as the main trend indicator.
2. Combine the upper and lower tracks of the 20-period Bollinger Bands as the fluctuation interval judgment
3. Open a long position when the following conditions are met:
   - Price is above the 200 EMA
   - The middle track of the Bollinger Bands is above the 200 moving average
   - Price crosses the lower Bollinger Bands track from bottom to top
4. Open a short position when the following conditions are met:
   - Price is below the 200 EMA
   - The middle track of the Bollinger Bands is below the 200 moving average
   - Price crosses the Bollinger Band track from top to bottom
5. Use a fixed stop loss percentage of 3% for risk control
6. Close long positions when the price touches the upper band of Bollinger Bands, and close short positions when the price touches the lower band.
#### Strategic Advantages
1. Strong trend following ability
- Effectively identify long-term trends through the 200 EMA
- Bollinger Bands assist in judging short- and medium-term trend changes
2. Improved risk control
- Fixed stop loss mechanism effectively controls the risk of each transaction
- Dynamic take-profit design improves profit opportunities
3. Flexible parameter optimization
- The moving average period and Bollinger Band parameters can be adjusted according to market characteristics
- Stop loss ratio can be adjusted according to risk tolerance
4. High degree of systematization
- Clear trading signals, no subjective judgment factors
- Suitable for automated trade execution
#### Strategy Risk
1. Risk of market shock
- False breakthrough signals may appear frequently in the sideways market.
- It is recommended to trade only when the trend is clear
2. Slippage risk
- May face greater slippage during periods of severe volatility
- It is recommended to set up reasonable slippage protection
3. Systemic risk
- Market emergencies may cause stop loss to become invalid
- It is recommended to cooperate with other risk control measures
4. Risks of parameter optimization
- Over-optimization may lead to overfitting
- It is recommended to conduct backtest verification in different time periods
#### Strategy optimization direction
1. Dynamic stop loss optimization
- Introduce ATR indicator to dynamically adjust stop loss distance
- Adjust stop loss percentage based on market fluctuations
2. Optimization of entry signals
- Added volume confirmation indicator
- Added trend strength filter
3. Optimization of warehouse management
- Implement dynamic position management
- Adjust leverage based on market fluctuations
4. Optimize trading timing
- Added market sentiment indicator
- Add time filter
#### Summary
This strategy builds a complete trading system by combining classic technical indicators, which has better trend capturing capabilities and risk control effects. The core advantages of the strategy lie in its high degree of systematization, strong parameter adjustability, and effective risk control through a fixed stop-loss mechanism. Although the performance may be poor in volatile markets, the stability and profitability of the strategy can be further improved through the implementation of optimized directions. It is recommended that traders pay attention to the selection of market environment when using real trading, and adjust parameter settings according to their own risk tolerance. ||
#### Overview
This strategy is a trend-following trading system that combines Moving Average (MA) and Bollinger Bands indicators. It identifies market trends by analyzing price relationships with the 200-period moving average and Bollinger Bands position, while incorporating a fixed percentage stop-loss mechanism for risk control. The strategy employs a 2.86% position management, compatible with 35x leverage, demonstrating prudent fund management principles.

#### Strategy Principles
The core logic of the strategy is based on the following key elements:
1. Uses 200-period moving average as the primary trend indicator
2. Combines 20-period Bollinger Bands' upper and lower channels for volatility range assessment
3. Opens long positions when:
   - Price is above the 200 MA
   - Bollinger Bands middle band is above 200 MA
   - Price crosses above the lower Bollinger Band
4. Opens short positions when:
   - Price is below the 200 MA
   - Bollinger Bands middle band is below 200 MA
   - Price crosses below the upper Bollinger Band
5. Implements 3% fixed stop-loss percentage for risk control
6. Closes long positions at upper Bollinger Band, shorts at lower band

#### Strategy Advantages
1. Strong Trend Following Capability
- Effectively identifies long-term trends using 200 MA
- Bollinger Bands assist in detecting medium-short term trend changes
2. Comprehensive Risk Control
- Fixed stop-loss mechanism effectively controls per-trade risk
- Dynamic take-profit design enhances profit opportunities
3. Flexible Parameter Optimization
- MA period and Bollinger Bands parameters adjustable to market characteristics
- Stop-loss percentage adjustable to risk tolerance
4. High Systematization
- Clear trading signals without subjective judgment
- Suitable for automated trading execution

#### Strategy Risks
1. Sideways Market Risk
- False breakout signals may occur frequently in ranging markets
- Recommended to trade only in clear trending markets
2. Slippage Risk
- Significant slippage possible during volatile periods
- Recommend setting reasonable slippage protection
3. Systematic Risk
- Market events may cause stop-loss failure
- Recommend combining with other risk control measures
4. Parameter Optimization Risk
- Over-optimization may lead to overfitting
- Recommend backtesting across different timeframes

#### Strategy Optimization Directions
1. Dynamic Stop-Loss Optimization
- Introduce ATR indicator for dynamic stop-loss adjustment
- Adjust stop-loss percentage based on market volatility
2. Entry Signal Optimization
- Add volume confirmation indicators
- Implement trend strength filters
3. Position Management Optimization
- Implement dynamic position sizing
- Adjust leverage based on market volatility
4. Trading Timing Optimization
- Add market sentiment indicators
- Implement time filters

#### Summary
This strategy builds a complete trading system by combining classic technical indicators, demonstrating good trend capture ability and risk control effects. The core advantages lie in its high systematization and parameter adjustability, while achieving effective risk control through fixed stop-loss mechanisms. Although performance may be suboptimal in ranging markets, implementing the suggested optimizations can further enhance strategy stability and profitability. Traders are advised to consider market conditions when implementing live trading and adjust parameters according to their risk tolerance.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-26 00:00:00
end: 2024-12-25 08:00:00
period: 3h
basePeriod: 3h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


//@version=5
strategy("MA 200 and Bollinger Bands Strategy", overlay=true) // 2.86% for 35x leverage

// inputs
ma_length = input(200, title="MA Length")
bb_length = input(20, title="Bollinger Bands Length")
bb_mult = input(2.0, title="Bollinger Bands Multiplier")

// calculations
ma_200 = ta.sma(close, ma_length)
bb_basis = ta.sma(close, bb_length)
bb_upper = bb_basis + (ta.stdev(close, bb_length) * bb_mult)
bb_lower = bb_basis - (ta.stdev(close, bb_length) * bb_mult)

// plot indicators
plot(ma_200, color=color.blue, title="200 MA")
plot(bb_upper, color=color.red, title="Bollinger Upper Band")
plot(bb_basis, color=color.gray, title="Bollinger Basis")
plot(bb_lower, color=color.green, title="Bollinger Lower Band")

// strategy logic
long_condition = close > ma_200 and bb_basis > ma_200 and ta.crossover(close, bb_lower)
short_condition = close < ma_200 and bb_basis < ma_200 and ta.crossunder(close, bb_upper)

// fixed stop loss percentage
fixed_stop_loss_percent = 3.0 / 100.0

if (long_condition)
    strategy.entry("Long", strategy.long)
    strategy.exit("Stop Long", "Long", stop=strategy.position_avg_price * (1 - fixed_stop_loss_percent))

if (short_condition)
    strategy.entry("Short", strategy.short)
    strategy.exit("Stop Short", "Short", stop=strategy.position_avg_price * (1 + fixed_stop_loss_percent))

// take profit conditions
close_long_condition = close >= bb_upper
close_short_condition = close <= bb_lower

if (close_long_condition)
    strategy.close("Long")

if (close_short_condition)
    strategy.close("Short")




```

> Detail

https://www.fmz.com/strategy/476259

> Last Modified

2024-12-27 14:57:38

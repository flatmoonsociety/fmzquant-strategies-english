
> Name

Dynamic-Volatility-Adjusted-Dual-Moving-Average-Crossover-System-with-RSI-ATR-Composite-Filter based on dynamic volatility adjustment
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d933ad313ea6450ac8d0.png)
![IMG](https://www.fmz.com/upload/asset/2d832437766cdd85d5739.png)




[trans]
#### Strategy Overview
This strategy is a compound trading system that combines double moving average crossover, RSI overbought and oversold, and ATR volatility filtering. The system uses short-term and long-term moving averages to generate trading signals, filters the market status through the RSI indicator, uses the ATR indicator to determine volatility, and combines percentage stop loss and risk-return ratio for position management and risk control. This strategy has strong adaptability and can flexibly adjust parameters according to the market environment.
#### Strategy Principle
The core logic of the strategy is based on the following aspects:
1. Signal generation: Use the intersection of the 9-day and 21-day simple moving averages to capture trend changes. When the short-term moving average crosses the long-term moving average, a long signal is generated, and when it crosses below the long-term moving average, a short signal is generated.
2. Conditional filtering: Filter overbought and oversold conditions through the RSI indicator to avoid entering the market under extreme market conditions. At the same time, use the ATR indicator to ensure that market volatility meets the trading conditions.
3. Risk management: Use a percentage stop loss based on the account's net value, and determine the stop loss position by setting the risk-return ratio to achieve reasonable returns while hedging risks.
#### Strategic Advantages
1. The system is highly adaptable: by enabling/disabling RSI and ATR filters, the strategy can be flexibly adjusted according to different market environments.
2. Improved risk control: Use percentage stop loss and dynamic position management to effectively control the risk exposure of each transaction.
3. High signal reliability: Through multiple filtering mechanisms, the impact of false signals is reduced and the success rate of transactions is improved.
4. Strong parameter adjustability: All parameters can be optimized and adjusted according to specific market characteristics.
#### Strategy Risk
1. Risk of volatile market: In a volatile market, moving average crossovers may produce frequent false signals.
2. Lagging risk: The moving average has a certain lag and may miss the best entry opportunity.
3. Risks of parameter optimization: Over-optimizing parameters may lead to over-fitting of the strategy and affect real performance.
4. Market environment dependence: Strategies perform better in markets with obvious trends, but may not perform well in other market environments.
#### Strategy optimization direction
1. Dynamic parameter adjustment: The moving average period and RSI threshold can be automatically adjusted according to market volatility.
2. Add trend strength filtering: Introduce indicators such as DMI or ADX to evaluate trend strength.
3. Optimize the stop loss method: You can consider using trailing stop loss or dynamic stop loss based on ATR.
4. Improve position management: introduce a dynamic position management system based on volatility.
#### Summary
This strategy builds a relatively complete trading system by combining multiple technical indicators. The strategy performs well in trending markets and has good risk control capabilities. By setting parameters appropriately and adding necessary filtering conditions, strategies can be adapted to different market environments. It is recommended to conduct sufficient backtesting and parameter optimization before using it in real market.
||

#### Strategy Overview
This strategy is a composite trading system combining dual moving average crossover, RSI overbought/oversold, and ATR volatility filtering. The system generates trading signals using short-term and long-term moving averages, filters market conditions through RSI indicators, assesses volatility using ATR, and implements position management and risk control through percentage-based stop-loss and risk-reward ratios. The strategy demonstrates strong adaptability and can flexibly adjust parameters based on market conditions.

#### Strategy Principles
The core logic of the strategy is based on the following aspects:
1. Signal Generation: Captures trend changes using crossovers of 9-day and 21-day simple moving averages. Long signals are generated when the short-term MA crosses above the long-term MA, and short signals when it crosses below.
2. Condition Filtering: Filters overbought/oversold conditions using RSI indicator to avoid entering trades in extreme market conditions. Uses ATR indicator to ensure market volatility meets trading criteria.
3. Risk Management: Employs percentage-based stop-loss relative to account equity, determines take-profit levels through risk-reward ratios to achieve reasonable returns while hedging risks.

#### Strategy Advantages
1. Strong System Adaptability: Strategy can flexibly adjust to different market environments through enabling/disabling RSI and ATR filters.
2. Comprehensive Risk Control: Effectively controls risk exposure per trade through percentage-based stop-loss and dynamic position management.
3. High Signal Reliability: Reduces impact of false signals through multiple filtering mechanisms, improving trade success rate.
4. Strong Parameter Adjustability: All parameters can be optimized and adjusted according to specific market characteristics.

#### Strategy Risks
1. Ranging Market Risk: Moving average crossovers may generate frequent false signals in sideways markets.
2. Lag Risk: Moving averages have inherent lag, potentially missing optimal entry points.
3. Parameter Optimization Risk: Over-optimization may lead to strategy overfitting, affecting live trading performance.
4. Market Environment Dependency: Strategy performs better in trending markets but may underperform in other market conditions.

#### Strategy Optimization Directions
1. Dynamic Parameter Adjustment: Automatically adjust MA periods and RSI thresholds based on market volatility.
2. Add Trend Strength Filtering: Introduce DMI or ADX indicators to evaluate trend strength.
3. Optimize Stop-Loss Methods: Consider implementing trailing stops or ATR-based dynamic stop-losses.
4. Improve Position Management: Introduce volatility-based dynamic position sizing system.

#### Summary
The strategy constructs a relatively complete trading system by combining multiple technical indicators. It performs excellently in trending markets and demonstrates good risk control capabilities. Through proper parameter settings and necessary filtering conditions, the strategy can adapt to different market environments. Thorough backtesting and parameter optimization are recommended before live implementation.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-01-21 00:00:00
end: 2025-02-20 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

//@version=5
strategy("Simplified MA Crossover Strategy with Disable Options", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// Inputs
shortLength = input.int(9, title="Short MA Length", minval=1)
longLength = input.int(21, title="Long MA Length", minval=1)

// RSI Filter
enableRSI = input.bool(true, title="Enable RSI Filter")
rsiLength = input.int(14, title="RSI Length", minval=1)
rsiOverbought = input.int(70, title="RSI Overbought Level", minval=50, maxval=100)
rsiOversold = input.int(30, title="RSI Oversold Level", minval=0, maxval=50)

// ATR Filter
enableATR = input.bool(true, title="Enable ATR Filter")
atrLength = input.int(14, title="ATR Length", minval=1)
minATR = input.float(0.005, title="Minimum ATR Threshold", minval=0)

// Risk Management
stopLossPerc = input.float(0.5, title="Stop Loss (%)", minval=0.1) / 100
riskRewardRatio = input.float(2, title="Risk-Reward Ratio", minval=1)
riskPercentage = input.float(2, title="Risk Percentage", minval=0.1) / 100

// Indicators
shortMA = ta.sma(close, shortLength)
longMA = ta.sma(close, longLength)
rsi = ta.rsi(close, rsiLength)
atr = ta.atr(atrLength)

// Conditions
longCondition = ta.crossover(shortMA, longMA)
shortCondition = ta.crossunder(shortMA, longMA)

// Apply RSI Filter (if enabled)
if (enableRSI)
    longCondition := longCondition and rsi < rsiOverbought
    shortCondition := shortCondition and rsi > rsiOversold

// Apply ATR Filter (if enabled)
if (enableATR)
    longCondition := longCondition and atr > minATR
    shortCondition := shortCondition and atr > minATR

// Risk Management
positionSize = strategy.equity * riskPercentage / (stopLossPerc * close)
takeProfitLevel = strategy.position_avg_price * (1 + stopLossPerc * riskRewardRatio)
stopLossLevel = strategy.position_avg_price * (1 - stopLossPerc)

// Execute Trades
if (longCondition)
    strategy.entry("Long", strategy.long, qty=positionSize)
    strategy.exit("Take Profit/Stop Loss", "Long", limit=takeProfitLevel, stop=stopLossLevel)

if (shortCondition)
    strategy.entry("Short", strategy.short, qty=positionSize)
    strategy.exit("Take Profit/Stop Loss", "Short", limit=strategy.position_avg_price * (1 - stopLossPerc * riskRewardRatio), stop=strategy.position_avg_price * (1 + stopLossPerc))

// Plotting
plot(shortMA, color=color.blue, title="Short MA")
plot(longMA, color=color.red, title="Long MA")
hline(rsiOverbought, "Overbought", color=color.red)
hline(rsiOversold, "Oversold", color=color.green)
plot(atr, color=color.orange, title="ATR")
plotshape(series=longCondition, title="Long Entry", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=shortCondition, title="Short Entry", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")
```

> Detail

https://www.fmz.com/strategy/483082

> Last Modified

2025-02-21 11:58:43

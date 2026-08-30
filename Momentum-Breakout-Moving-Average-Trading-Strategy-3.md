
> Name

Momentum-Breakout-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1300f35054c557636f9.png)
[trans]

## Overview
This strategy comprehensively uses three indicators: Relative Strength Index (RSI), Super Trendline (SuperTrend) and Average True Range (ATR) to construct a comprehensive and practical quantitative trading strategy.
## Strategy Principle
### Relative Strength Index (RSI)
RSI is a powerful oscillator that measures the speed and strength of price changes to determine whether the market is overbought or oversold. When the RSI is below the oversold zone, it is an oversold signal, and conversely, when it is above the overbought zone, it is an overbought signal.
### Super Trend Line (SuperTrend)
SuperTrend is a trend following indicator that can be used to identify the current trend direction. When the price is above the SuperTrend line, it indicates an uptrend; when the price is below the SuperTrend line, it indicates a downtrend.
### Average true range (ATR)
ATR is used to measure market volatility and risk levels. The higher the ATR, the more intense the market is, and vice versa. This strategy uses ATR to set stop loss levels and profit-loss ratios.
## Strategy operation mechanism
**Bull signal:** When the fast RSI is lower than the slow RSI and the price is higher than the SuperTrend line, go long;
**Short signal:** When the fast RSI is higher than the slow RSI and the price is lower than the SuperTrend line, go short;
**Stop loss exit:** When holding a long order, if the fast RSI is higher than the slow RSI or the price is lower than the SuperTrend line, stop the loss and exit the long order; when holding a short order, if the fast RSI is lower than the slow RSI or the price is higher than the SuperTrend line, stop the loss and exit the short order.
## Strategic Advantages
1. Trend tracking: SuperTrend can clearly identify the trend direction;
2. Momentum confirmation: RSI ensures that trades are in line with current market sentiment;
3. Fluctuation adaptive: Stop loss based on ATR can be dynamically adjusted to adapt to market changes.
## Risks and Countermeasures
1. Trend mismatch risk: When there is a probability that SuperTrend does not match the actual trend direction, losses will occur. The error rate can be reduced through parameter optimization.
2. Risk of stop loss being triggered: If the stop loss is too close, it may be broken. The stop loss distance should be set reasonably.
3. Risk of improper parameters: Improper setting of RSI parameters will affect the selection of trading timing. Sufficient parameters should be determined through sufficient backtesting.
## Optimization suggestions
1. Combine with other indicators to filter signals and improve system stability;
2. Optimize the RSI parameter combination based on the maximum retracement;
3. Use heuristic algorithms to search for optimal SuperTrend parameters.
## Summarize
This strategy integrates trend, momentum and volatility indicators to build a quantitative trading strategy with clear trading signals, flexible parameter settings and in place risk control. Through continuous testing and optimization, it is expected to obtain stable excess returns.
||


## Overview

This strategy integrates Relative Strength Index (RSI), SuperTrend indicator and Average True Range (ATR) to construct a comprehensive and practical quantitative trading strategy.  

## Strategy Logic  

### Relative Strength Index (RSI)

RSI is a powerful oscillating indicator that judges if the market is overbought or oversold by measuring the velocity and magnitude of price movements. RSI below oversold region indicates oversold signal, while RSI above overbought region is overbought signal.

### SuperTrend Indicator   

SuperTrend is a trend following indicator that helps identify current trend direction. Price above SuperTrend line indicates an uptrend while price below SuperTrend line an downtrend.  

### Average True Range (ATR)  

ATR measures the degree of market volatility and risk level. Higher ATR represents higher market volatility while lower means relatively calm. This strategy leverages ATR to set stop loss and profit target.

## Strategy Execution Logic  

**Long Signal:** When fast RSI crosses below slow RSI while price is above SuperTrend line to go long.  

**Short Signal:** When fast RSI crosses above slow RSI while price is below SuperTrend line to go short.   

**Exit Rule:** If holding long position, exit when fast RSI crosses above slow RSI OR price falls below SuperTrend line. If holding short position, exit when fast RSI crosses below slow RSI OR price rises above SuperTrend line.

## Advantages  

1. Trend Following: SuperTrend identifies trend clearly. 

2. Momentum Confirmation: RSI ensures trades align with market sentiment.   

3. Volatility Adaptive: ATR-driven stop loss adapts to varying market conditions.  

## Risks & Solutions   

1. Trend Misalignment Risk: Probability of conflicts between SuperTrend and actual trend direction resulting losses. Parameter optimization helps to improve accuracy.  

2. Premature Stop Loss Risk: Stop loss too close may get hit unintentionally. Reasonable stop distance should be set.  

3. Parameter Risk: Improper RSI parameters setting affects timing of entries and exits. Careful backtests required to determine proper parameters.  

## Enhancement Recommendations    

1. Add other technical indicators to filter signals improving system stability.  

2. Optimize RSI parameters based on maximum drawdown constraints.  

3. Leverage heuristic algorithms to search optimal SuperTrend parameters.  

## Conclusion  

This strategy integrates trend, momentum and volatility indicators constructing a quantitative model with clear signals, flexible parameter tuning, and sound risk control. With continuous testing and enhancement, it is promising to achieve steady above-average returns over the long run.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|RSI Length 1|
|v_input_2|21|RSI Length 2|
|v_input_3|1.5|SuperTrend Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-27 00:00:00
end: 2023-12-03 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("RSI, SuperTrend, and ATR Strategy", overlay=true)

// Define input parameters
rsiLength1 = input(14, title="RSI Length 1")
rsiLength2 = input(21, title="RSI Length 2")
supertrendMultiplier = input(1.5, title="SuperTrend Multiplier")

// Calculate indicators
rsi1 = ta.rsi(close, rsiLength1)
rsi2 = ta.rsi(close, rsiLength2)
supertrend = ta.atr(14) * supertrendMultiplier

// Define trading conditions
rsiLongCondition = rsi1 > rsi2
rsiShortCondition = rsi1 < rsi2
supertrendLongCondition = close > supertrend
supertrendShortCondition = close < supertrend

// Execute trades
if (rsiLongCondition and supertrendLongCondition)
    strategy.entry("Long", strategy.long)

if (rsiShortCondition and supertrendShortCondition)
    strategy.entry("Short", strategy.short)

if (strategy.position_size > 0 and (rsiShortCondition or supertrendShortCondition))
    strategy.close("Long")

if (strategy.position_size < 0 and (rsiLongCondition or supertrendLongCondition))
    strategy.close("Short")

// Plot indicators on the chart
plot(rsi1, color=color.orange, title="RSI 1")
plot(rsi2, color=color.yellow, title="RSI 2")
plot(supertrend, color=color.blue, title="SuperTrend")

```

> Detail

https://www.fmz.com/strategy/434187

> Last Modified

2023-12-04 15:57:06

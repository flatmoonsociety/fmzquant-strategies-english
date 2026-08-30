
> Name

Multi-Take-Profit-and-Stop-Loss-WaveTrend-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1b3c8e682e89ddc59c3.png)

[trans]

## Overview
This strategy is LazyBear's original wave trend strategy, adding a second stop loss, multiple take profit prices, and a high time frame EMA filter. It uses wave trend indicators to generate trading signals, and then combines EMA filtering and stop-loss and take-profit management to realize automated trend tracking transactions.
## Strategy Principle
The core indicator of this strategy is the WaveTrend indicator, which consists of three parts:
1. AP: average price = (highest price + lowest price + closing price)/3
2. ESA:AP’s n1 period EMA
3. The n1-period EMA of the absolute value of CI: (AP-ESA)/(0.015×AP-ESA’s n1-period EMA)
4. TCI: CI’s n2 EMA, that is, wave trendline 1 (WT1)
5. WT2: 4-period SMA of WT1
When WT1 crosses above WT2 and produces a golden cross, go long; when WT1 crosses below WT2 and produces a dead cross, close the position.
In addition, the strategy also introduces high time frame EMA as a filter. Only when the price is higher than the EMA, you can go long, and when it is lower than the EMA, you can go short, thereby filtering out some false signals.
## Strategic Advantages
1. Use wave trend indicators to automatically track trends and avoid human judgment errors.
2. Add a second stop loss to effectively control single losses
3. Multiple take-profit prices to lock in profits to the greatest extent
4. EMA filter, filter out false signals and improve winning rate
## Strategy Risk and Optimization
1. Failure to filter trend reversal may cause losses
2. Improper parameter settings may lead to too frequent transactions
3. Can test different parameter combinations and optimize parameters
4. Consider combining other indicators to determine trend reversal
## Summarize
This strategy comprehensively considers multiple dimensions such as trend tracking, risk control, and profit maximization. It automatically captures trends through wave trend indicators and cooperates with EMA filters to improve trading efficiency. It controls risks while grasping trends. It is an efficient and stable trend following strategy. Through further parameter optimization and adding reversal judgment, the applicability of this strategy can be further expanded.
||
## Overview

This strategy is based on the original WaveTrend strategy from LazyBear, with additional features like secondary stop loss, multiple take profit levels and high timeframe EMA filter. It uses WaveTrend indicator to generate trading signals, combined with EMA filter and stop loss/take profit management for automated trend following trading.

## Strategy Logic

The core indicator of this strategy is WaveTrend, consisting of three components:

1. AP: Average Price = (Highest + Lowest + Close) / 3

2. ESA: n1-period EMA of AP  

3. CI: (AP - ESA) / (0.015 * n1-period EMA of absolute value of (AP - ESA))

4. TCI: n2-period EMA of CI, also called WaveTrend Line 1 (WT1)

5. WT2: 4-period SMA of WT1

A long position is opened when WT1 crosses above WT2 (golden cross), and is closed when WT1 crosses below WT2 (death cross).

Additionally, a high timeframe EMA filter is implemented to avoid false signals, so that long trades are only taken when price is above EMA and short trades below EMA. 

## Advantages

1. Automatically follow trends using WaveTrend without manual judgment  

2. Secondary stop loss effectively limits single trade loss

3. Multiple take profit levels maximize profit capture

4. EMA filter improves win rate by avoiding false signals

## Risks and Improvements   

1. Fails to detect trend reversal, might cause losses

2. Poor parameter tuning leads to over-trading

3. Different parameter sets can be tested for optimization

4. Consider additional indicators for reversal detection

## Conclusion

This strategy comprehensively incorporates trend following, risk control and profit maximization through WaveTrend's automatic trend detection, EMA filter to improve efficiency and stop loss/take profit management to balance trend trading and risk control. It is an efficient and steady trend following system. Further parameter optimization and reversal mechanisms can enhance the strategy's applicability.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Channel Length|
|v_input_2|21|Average Length|
|v_input_3|60|Over Bought Level 1|
|v_input_4|53|Over Bought Level 2|
|v_input_5|-60|Over Sold Level 1|
|v_input_6|-53|Over Sold Level 2|
|v_input_7|false|Use EMA Filter|
|v_input_8|50|EMA Length|
|v_input_9|60|EMA Time Frame|
|v_input_10|0|Trade Mode: Both|Short Only|Long Only|
|v_input_11|false|Use Secondary Stop Loss|
|v_input_12|5|Stop Loss Percentage (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-31 00:00:00
end: 2023-11-30 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © undacovacobra

//@version=4
strategy("WaveTrend Strategy [LazyBear] with Secondary Stop Loss", overlay=true)

// Input parameters
n1 = input(10, "Channel Length")
n2 = input(21, "Average Length")
obLevel1 = input(60, "Over Bought Level 1")
obLevel2 = input(53, "Over Bought Level 2")
osLevel1 = input(-60, "Over Sold Level 1")
osLevel2 = input(-53, "Over Sold Level 2")
useEmaFilter = input(false, "Use EMA Filter")
emaLength = input(50, "EMA Length")
emaTimeFrame = input("60", "EMA Time Frame")
tradeMode = input("Both", "Trade Mode", options=["Long Only", "Short Only", "Both"])
useSecondarySL = input(false, "Use Secondary Stop Loss")
slPercentage = input(5.0, "Stop Loss Percentage (%)")

// WaveTrend Indicator Calculations
ap = hlc3 
esa = ema(ap, n1)
d = ema(abs(ap - esa), n1)
ci = (ap - esa) / (0.015 * d)
tci = ema(ci, n2)
wt1 = tci
wt2 = sma(wt1, 4)

// EMA Calculation with Selected Time Frame
getEma(timeFrame) =>
    security(syminfo.tickerid, timeFrame, ema(close, emaLength))

emaFilter = getEma(emaTimeFrame)

// Secondary Stop Loss Calculation
longStopPrice = strategy.position_avg_price * (1 - slPercentage / 100)
shortStopPrice = strategy.position_avg_price * (1 + slPercentage / 100)

// Long Entry and Exit Conditions with EMA Filter and Trade Mode
longEntry = crossover(wt1, wt2) and wt2 < osLevel1 and (not useEmaFilter or close > emaFilter) and (tradeMode == "Long Only" or tradeMode == "Both")
if (longEntry)
    strategy.entry("Long", strategy.long)
longExit = crossunder(wt1, wt2) and wt2 > obLevel1
if (longExit)
    strategy.close("Long")
if (useSecondarySL and strategy.position_size > 0 and low < longStopPrice)
    strategy.close("Long", comment="SL Hit")

// Short Entry and Exit Conditions with EMA Filter and Trade Mode
shortEntry = crossunder(wt1, wt2) and wt2 > obLevel1 and (not useEmaFilter or close < emaFilter) and (tradeMode == "Short Only" or tradeMode == "Both")
if (shortEntry)
    strategy.entry("Short", strategy.short)
shortExit = crossover(wt1, wt2) and wt2 < osLevel1
if (shortExit)
    strategy.close("Short")
if (useSecondarySL and strategy.position_size < 0 and high > shortStopPrice)
    strategy.close("Short", comment="SL Hit")

// Plotting
plot(0, color=color.gray)
plot(obLevel1, color=color.red)
plot(osLevel1, color=color.green)
plot(obLevel2, color=color.red, style=plot.style_cross)
plot(osLevel2, color=color.green, style=plot.style_cross)
plot(wt1, color=color.green)
plot(wt2, color=color.red, style=plot.style_cross)
plot(wt1-wt2, color=color.blue, style=plot.style_area, transp=80)
plot(emaFilter, color=color.blue)


```

> Detail

https://www.fmz.com/strategy/433966

> Last Modified

2023-12-01 18:09:12

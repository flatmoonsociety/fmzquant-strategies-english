
> Name

Momentum-Moving-Average-Crossover-Quant-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/a4553a4d75f4e66627.png)
 [trans]
## Overview
This strategy combines two key technical indicators, moving average and trading volume, and designs entry and exit rules for long and short positions to form a complete quantitative trading strategy.
## Strategy Principle
### Key indicators
1. Moving averages: fast moving average (blue line) and slow moving average (red line).
2. Trading volume: 24-hour trading volume (purple) and 7-day average trading volume (orange line).
### Strategy conditions
**Long position entry conditions:**
1. The fast moving average crosses the slow moving average
2. 24-hour trading volume is less than 50% of the 7-day average trading volume
**Short position entry conditions:**
The fast moving average crosses below the slow moving average
### Entry and Exit
**Long position entry:** Go long when long position entry conditions are met
**Short position entry:** Go short when the conditions for short position entry are met.
**Take Profit and Stop Loss:**
Display the take-profit and stop-loss levels after going long
## Advantage Analysis
1. Combine price indicators and trading volume indicators to avoid false breakthroughs
2. Clear entry and exit rules
3. Have a stop-profit and stop-loss mechanism to control risks
## Risk Analysis
1. Double moving average strategy is prone to frequent transactions
2. The quality of transaction volume data cannot be guaranteed.
3. Parameter optimization has the risk of over-optimization
**Improvement method:**
1. Appropriately adjust moving average parameters to reduce trading frequency
2. Combine more data sources to verify quantitative signals
3. Strict backtest verification to prevent over-optimization
## Optimization direction
1. Add other indicators to filter signals
2. Dynamically adjust take profit and stop loss levels
3. Multi-time frame analysis to improve stability
## Summarize
This strategy integrates moving average indicators and trading volume indicators, and designs a complete quantitative trading strategy through a double confirmation mechanism. It has the advantages of clear entry conditions, stop-profit and stop-loss, and simple operation. At the same time, it is also necessary to prevent frequent trading problems with the double moving average strategy, pay attention to the quality of transaction volume data, and prevent parameter over-optimization. The NEXT step performs multi-index optimization, dynamic stop-profit and stop-loss, and multi-time frame analysis.
||

## Overview

This strategy combines the moving average and trading volume indicators to design the long and short entry and exit rules, forming a complete quantitative trading strategy.

## Strategy Principle  

### Key Indicators

1. Moving Averages: Fast MA (Blue Line) and Slow MA (Red Line) 
2. Volume: 24-hour Volume (Purple) and 7-day Average Volume (Orange)

### Strategy Conditions  

**Long Entry Conditions:**

1. Fast MA crosses above Slow MA
2. 24-hour Volume below 50% of 7-day Average Volume

**Short Entry Conditions:**

Fast MA crosses below Slow MA

### Entries and Exits

**Long Entry:** Go long when long conditions are met

**Short Entry:** Go short when short conditions are met  

**Take Profit and Stop Loss:**
Displayed take profit and stop loss levels for long position

## Advantage Analysis

1. Combining price and volume avoid false breakout 
2. Clear entry and exit rules
3. Take profit and stop loss to control risk

## Risk Analysis  

1. Frequent trading with moving average strategy
2. Unreliable volume data quality
3. Overoptimization in parameter tuning  

**Improvements:**

1. Adjust MA parameters to reduce trading frequency
2. Verify signals with more data sources  
3. Strict backtesting to prevent overoptimization

## Optimization Directions

1. Add other indicators to filter signals
2. Dynamic take profit and stop loss  
3. Multiple timeframe analysis to improve stability  

## Summary

This strategy integrates MA and volume indicators to design a complete quant strategy with clear entry conditions, take profit/stop loss, easy to operate. Need to prevent frequent trading issue, monitor volume data quality and overoptimization. NEXT steps are multivariate optimization, dynamic TP/SL and multiple timeframe analysis.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Fast MA Length|
|v_input_2|21|Slow MA Length|
|v_input_3|50|Volume Percentage Threshold|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-25 00:00:00
end: 2024-01-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("MA and Volume Strategy", overlay=true)

// Input parameters
fastLength = input(9, title="Fast MA Length")
slowLength = input(21, title="Slow MA Length")
volumePercentageThreshold = input(50, title="Volume Percentage Threshold")

// Calculate moving averages
fastMA = ta.sma(close, fastLength)
slowMA = ta.sma(close, slowLength)

// Calculate 24-hour volume and weekly volume average
dailyVolume = request.security(syminfo.tickerid, "D", volume)
weeklyVolumeAvg = ta.sma(request.security(syminfo.tickerid, "W", volume), 7)

// Strategy conditions
longCondition = ta.crossover(fastMA, slowMA) and dailyVolume < (weeklyVolumeAvg * volumePercentageThreshold / 100)
shortCondition = ta.crossunder(fastMA, slowMA)

// Set take profit and stop loss levels
takeProfitLong = close * 1.50
stopLossLong = close * 0.90

// Strategy orders
strategy.entry("Long", strategy.long, when=longCondition)
strategy.entry("Short", strategy.short, when=shortCondition)

// Plot moving averages
plot(fastMA, color=color.blue, title="Fast MA")
plot(slowMA, color=color.red, title="Slow MA")

// Plot 24-hour volume and weekly volume average
plot(dailyVolume, color=color.purple, title="24-Hour Volume", transp=0)
plot(weeklyVolumeAvg, color=color.orange, title="Weekly Volume Average")

// Plot entry signals
plotshape(series=longCondition, title="Buy Signal", color=color.green, style=shape.triangleup, size=size.small)
plotshape(series=shortCondition, title="Sell Signal", color=color.red, style=shape.triangledown, size=size.small)

// Plot take profit and stop loss levels only when a valid trade is active
plotshape(series=longCondition, title="Take Profit Long", color=color.green, style=shape.triangleup, size=size.small)
plotshape(series=longCondition, title="Stop Loss Long", color=color.red, style=shape.triangledown, size=size.small)

```

> Detail

https://www.fmz.com/strategy/440063

> Last Modified

2024-01-26 11:39:26

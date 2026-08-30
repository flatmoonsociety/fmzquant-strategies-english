
> Name

Based on the breakout regression strategyThe-Breakout-Regression-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/6727ef820f88c51f18.png)
[trans]

### Overview
This strategy is a systematic approach designed to profit from the volatility of the crude oil futures market. It measures the average range of candles. If the fast moving average is above the slow moving average, it means the candle is larger; if the slow moving average is above the fast moving average, it means the candle is smaller.
Based on this principle, identify potential long entry points and short entry points. The position is only maintained for a certain number of candles, this parameter is controlled by the "Exit after bars" input.
### Strategy Principles
1. Calculate the highest closing price of the last 9 K lines as a breakthrough judgment criterion
2. Calculate the lowest closing price of the last 50 K lines as a breakthrough judgment criterion
3. Calculate the comparison of the average amplitude of the last 5 K lines and the 20 K lines to determine whether the K line pattern is gradually expanding or shrinking.
4. Identify long-term and short-term breakthrough signals: when the closing price is equal to the highest closing price and the K-line gradually shrinks, go long; when the closing price is equal to the lowest closing price and the K-line gradually shrinks, go short
5. Fixed root K line closing and exiting after a breakthrough: parameters can be adjusted to change the closing interval
### Advantage Analysis
1. Regression strategy, judging the market direction by comparing it with historical extreme values
2. Combined with volatility judgment, false breakthroughs can be avoided
3. Fixed root K line to leave the market, which can lock in a certain profit and avoid retracement.
### Risk Analysis
1. Historical extreme values change with changes in market structure, and signal failure may occur.
2. False breakthroughs lead to hold-up
3. If the exit interval parameters are inappropriate, you may lose greater profits or increase losses.
### Optimization direction
1. Extreme value parameters can be optimized through market statistics
2. Volatility indicators can be added to evaluate the true probability of breakthrough
3. The number of exit roots can be optimized through strategy backtest results
### Summarize
This strategy uses breakthroughs and regressions to determine short-term trends and is a volatility strategy. By optimizing parameter settings and adding volatility indicator determination, the probability of false breakthroughs can be reduced and profitability improved. At the same time, the quick exit mechanism of the fixed K-line can lock in a certain profit and effectively control risks. This strategy can be used as an auxiliary tool for short-term operations, and can also be used to obtain longer-period operating signals through parameter adjustment.
||

### Overview

This is a systematic approach designed to capitalize on the volatility of crude oil futures markets. It measures the average range of candlesticks. If the fast moving average is above the slow one, it means the candles are bigger. If the slow moving average is above the fast one, it means the candles are smaller.

According to this principle, it identifies potential long and short entry points. The position is only held for a fixed number of candles, controlled by the "Exit after bars" input.  

### Strategy Logic  

1. Calculate the highest close price of the most recent 9 bars, as the breakout benchmark
2. Calculate the lowest close price of the most recent 50 bars, as the breakout benchmark
3. Compare the average volatility of the most recent 5 and 20 bars to judge if the candlestick pattern is expanding or contracting
4. Identify long and short signals: when close equals the highest close and candles contracting, go long; when close equals the lowest close and candles contracting, go short
5. Close position after a fixed number of bars following breakout: adjustable parameter  

### Advantage Analysis   

1. Regression strategy, judge direction by comparing with historical extremes 
2. Combine with volatility, avoid false breakouts
3. Fixed number of bars for exit locks in some profit and avoids drawdown  

### Risk Analysis

1. Historical extremes change with market structure changes, signals may fail
2. False breakouts cause being trapped
3. Improper exit interval may lose greater profit or increase loss  

### Optimization  

1. Extremes parameters can be optimized through market statistics
2. Add volatility metrics to evaluate true breakout probability  
3. Optimize number of exit bars through backtest result  

### Summary  

This strategy utilizes breakout and regression to determine short-term trends, belonging to volatility strategies. By optimizing parameters and adding volatility metrics to determine false breakout probability, it can increase profitability. Also the fast exit mechanism locks in some profit and controls risk effectively. It can serve as an auxiliary tool for short-term trading, and can also generate longer-term trading signals through parameter tuning.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Highest Close lookback|
|v_input_2|50|Lowest Close lookback|
|v_input_3|10|Exit after bars|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-01 00:00:00
end: 2024-02-29 23:59:59
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Celestial_Logic

//@version=5
strategy("Crudeoil Breakout strategy", overlay = true, initial_capital = 20000, default_qty_type = strategy.fixed, default_qty_value = 1)


highestCloseLookback = input(9 , title = 'Highest Close lookback')
lowestCloseLookback  = input(50, title = 'Lowest Close lookback'  ) 

exitAfter = input(10, title = 'Exit after bars')

hc = ta.highest(close,highestCloseLookback)
lc = ta.lowest(close,lowestCloseLookback)

rangeFilter = (ta.sma( (high - low), 5 ) > ta.sma((high-low), 20) ) // Candles getting bigger.

longCondition  = (close == hc ) and not rangeFilter
shortCondition = (close == lc ) and not rangeFilter
if  longCondition
    strategy.entry(id = 'long', direction = strategy.long) 
if shortCondition
    strategy.entry(id = 'short', direction = strategy.short)



var int longsince = 0 
var int shortsince = 0 

if strategy.position_size > 0 
    longsince += 1
else
    longsince := 0

if strategy.position_size < 0 
    shortsince += 1 
else 
    shortsince := 0

if longsince >= exitAfter 
    strategy.close(id = 'long', comment = 'long close')
if shortsince >= exitAfter
    strategy.close(id = 'short', comment = 'short close')


```

> Detail

https://www.fmz.com/strategy/443239

> Last Modified

2024-03-01 11:58:56


> Name

Moving-Average-System-Trading-Strategy Moving-Average-System-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/ca2fd81ada0cb3f5786c4fc24a7c40342c96cdd4006e1e086face4093996c1ce.png)

[trans]

## Overview
This article discusses a trading strategy based on a simple moving average. This strategy uses a moving average of length 17 to compare with the closing price, going long when the closing price crosses above the moving average and short when it crosses below.
## Strategy Principle
### Moving average calculation
This strategy calculates moving averages using the following parameters:
- MA source: Default is the average of OHLC (OHCL4)
- MA type: Default is Simple Moving Average (SMA)
- MA length: default is 17
Based on these parameters, the getMAType() function will be called to calculate the 17-period closing price SMA.
### Trading signal generation
Then compare the closing price to that moving average:
- Closing price > Moving average: Long position signal
- Closing price < moving average: short position signal
When the closing price crosses above the moving average, a long signal is generated; when the closing price crosses below the moving average, a short signal is generated.
### Transaction Execution
During the backtesting period, long positions are opened when a long signal is encountered, and short positions are opened when a short signal is encountered.
## Advantage Analysis
The biggest advantage of this strategy is that the idea is very simple and clear. It is just an indicator that determines trend changes through changes in its direction. The strategy is easy to understand and implement, and is suitable for novices to learn.
In addition, the moving average is a trend-following indicator that can effectively track trend changes and avoid being disturbed by short-term noise in the market.
Through parameter adjustment, it can adapt to different cycles and different varieties.
## Risk Analysis
First of all, this strategy is only based on one indicator, and the judgment standard is relatively single, which may produce more false signals.
Moreover, this strategy is a trend following system and cannot work properly in consolidated and volatile markets.
In addition, if stop loss and stop profit are not set, there is a risk of loss expansion.
The solution is to combine other indicators, optimize parameter combinations, and reduce error signals. Set stop-loss and take-profit, control risks, and optimize drawdowns.
## Optimization direction
The following aspects can be used as ideas for strategy optimization:
1. Adjust the moving average parameters and optimize the number of periods. For example, change it to 30 cycles or 50 cycles, etc.
2. Try different types of moving averages, such as EMA, VIDYA, etc. They differ in their sensitivity to price changes.
3. Add other indicator combinations. For example, combined with MACD, it can judge the strength. Or combined with RSI to reduce false signals.
4. Add a stop loss mechanism. Set a trailing stop loss of a fixed percentage or ATR value. Control single losses.
5. Add a profit-taking mechanism. Set a target profit percentage. Maximize profits.
These optimizations can make the strategy performance more stable and avoid excessive retracement.
## Summarize
This article analyzes a simple trading strategy based on a 17-period moving average. The strategy signal source is simple, easy to understand and implement, and is a typical trend tracking system. Through an in-depth interpretation of the strategy, its advantages and risks are analyzed, and optimization ideas in multiple dimensions are given. I believe that through continuous optimization and enrichment, this strategy can gradually evolve and achieve stable returns in real markets.
||

## Overview

This article discusses a trading strategy based on a simple moving average. The strategy compares the closing price with a 17-period moving average, going long when the closing price crosses above the moving average and going short when it crosses below.  

## Strategy Logic

### Moving Average Calculation

The strategy uses the following parameters to calculate the moving average:

- MA Source: Default to average of OHLC (OHLC4) 
- MA Type: Default to Simple Moving Average (SMA)
- MA Length: Default to 17

Based on these parameters, the getMAType() function is called to calculate the 17-period SMA of closing prices.

### Trading Signal Generation 

Then compare the relationship between the closing price and the moving average:

- Close > Moving Average: Long signal
- Close < Moving Average: Short signal

When the closing price crosses above the moving average from below, a long signal is generated. When it crosses below from above, a short signal is generated.

### Trade Execution

During the backtest period, open long positions when long signals appear and open short positions when short signals appear.

## Advantage Analysis

The biggest advantage of this strategy is that the logic is very simple and clear. With just one indicator, it judges the trend reversal based on the direction change of the indicator. The strategy is easy to understand and implement, suitable for beginners to learn.

In addition, moving averages belong to trend-following indicators, which can effectively track trend changes and avoid interference from short-term market noise.

By adjusting parameters, it can adapt to different cycles and different products.

## Risk Analysis

Firstly, this strategy relies solely on one indicator, so the judgment criteria are relatively single, which may generate more false signals. 

Also, as a trend following system, it does not work well in range-bound and sideways markets.

Besides, without stop loss or take profit, there is a risk of expanding losses.

The solutions are to incorporate other indicators, optimize parameter combinations to reduce false signals. Add stop loss and take profit to control risks and optimize drawdowns.

## Optimization Directions 

Here are some ideas for optimizing the strategy:

1. Adjust moving average parameters, optimize period numbers, e.g. change to 30-period or 50-period.

2. Try different types of moving averages, like EMA, VIDYA etc. They have varying sensitivity to price changes.

3. Add other indicators in combination, e.g. MACD to judge strength; RSI to reduce false signals. 

4. Add stop loss mechanisms. Set fixed percentage or ATR-based trailing stop loss to control single-trade loss amount.

5. Add take profit mechanisms. Set target profit percentage to maximize profits.

These optimizations can make the strategy performance more stable and avoid excessive drawdowns. 

## Summary

This article analyzes a simple trading strategy based on a 17-period moving average. The strategy has simple signal sources, easy to understand and implement, belonging to a typical trend following system. Through in-depth interpretation of the strategy, its pros and cons are analyzed, and multiple dimensions of optimization ideas are proposed. It is believed that through continuous optimization and enrichment, this strategy can gradually evolve and achieve stable returns in live trading as well.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2012|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2019|Backtest Stop Year|
|v_input_5|12|Backtest Stop Month|
|v_input_6|31|Backtest Stop Day|
|v_input_7_ohlc4|0|MA Source: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|
|v_input_8|0|MA Type: sma|ema|swma|wma|vwma|rma|
|v_input_9|17|MA Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-05 00:00:00
end: 2024-01-04 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Simple 17 BF ?", overlay=true, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.0)

/////////////// Time Frame ///////////////
testStartYear = input(2012, "Backtest Start Year") 
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay, 0, 0)

testStopYear = input(2019, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay, 0, 0)

testPeriod() => true

///////////// Moving Average /////////////
source = input(title="MA Source", defval=ohlc4)
maType = input(title="MA Type", defval="sma", options=["sma", "ema", "swma", "wma", "vwma", "rma"])
length = input(title="MA Length", defval=17)

///////////// Get MA Function /////////////
getMAType(maType, sourceType, maLen) => 
    res = sma(close, 1)
    
    if maType == "ema"
        res := ema(sourceType, maLen)
    if maType == "sma"
        res := sma(sourceType, maLen)
    if maType == "swma"
        res := swma(sourceType)
    if maType == "wma"
        res := wma(sourceType, maLen)
    if maType == "vwma"
        res := vwma(sourceType, maLen)
    if maType == "rma"
        res := rma(sourceType, maLen)
    res
    
MA = getMAType(maType, source, length)

/////////////// Strategy ///////////////
long = close > MA
short = close < MA

last_long = 0.0
last_short = 0.0
last_long := long ? time : nz(last_long[1])
last_short := short ? time : nz(last_short[1])

long_signal = crossover(last_long, last_short)
short_signal = crossover(last_short, last_long)

/////////////// Execution /////////////// 
if testPeriod()
    strategy.entry("L", strategy.long, when=long_signal)
    strategy.entry("S", strategy.short, when=short_signal)

/////////////// Plotting /////////////// 
p1 = plot(MA, color = long ? color.lime : color.red, linewidth=2)
p2 = plot(close, linewidth=2)
fill(p1, p2, color=strategy.position_size > 0 ? color.lime : strategy.position_size < 0 ? color.red : color.white, transp=80)
```

> Detail

https://www.fmz.com/strategy/437786

> Last Modified

2024-01-05 15:36:00

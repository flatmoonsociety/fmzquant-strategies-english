
> Name

Enhanced-Moving-Average-Convergence-Trend-Strategy
> Author

ChaoZhang

> Strategy Description



[trans]

## Strategy Principle
This strategy is based on the enhanced MACD indicator for trend following. It simultaneously calculates the fast moving average, the slow moving average and the difference between the two, and then moves the average of the difference to generate trading signals.
The specific logic is:
1. Calculate the fast EMA period, such as the 12th
2. Calculate the slow EMA period, such as the 26th
3. Calculate the difference between fast and slow EMA as MACD
4. Perform signal line EMA on MACD, such as 9-day EMA
5. Then use EMA to generate an enhanced signal line on the difference between MACD and the signal line.
6. Go long when the enhanced signal line crosses the zero axis
7. Close long positions when the enhanced signal line crosses the zero axis
This strategy fully explores the trend following characteristics of the MACD indicator, and performs secondary optimization filtering to improve signal quality and pursue the medium and long-term trend.
## Strategic Advantages
- Enhanced MACD noise reduction to improve signal accuracy
- Use fast and slow EMA to determine direction and strength
- Slower parameters focus on mid- to long-term trends
## Strategy Risk
- Careful selection of EMA period parameters is required
- Only going long cannot take advantage of short opportunities
- The signal appears less frequently
## Summarize
This strategy identifies mid- to long-term opportunities by enhancing MACD’s trend following capabilities. But parameter optimization and risk control are particularly important. Appropriate combination of other factors can improve results.

||

## Strategy Logic

This trend following strategy utilizes an enhanced MACD indicator. It calculates fast EMA, slow EMA, their difference, and EMA of that difference to generate signals.

The logic is:  

1. Compute fast EMA period, e.g. 12-day

2. Compute slow EMA period, e.g. 26-day 

3. Subtract fast from slow EMA to get MACD

4. Take EMA of MACD as signal line, e.g. 9-day

5. EMA of MACD minus signal gives enhanced signal 

6. Go long when enhanced signal crosses above zero line

7. Close long when enhanced signal crosses below zero line

The strategy taps into MACD's trend following ability, and optimizes it further for quality mid- to long-term trend signals. 

## Advantages

- Enhanced MACD reduces noise and improves signals

- Fast/slow EMA combo gauges direction and strength

- Slower parameters focus on mid- to long-term trends

## Risks

- Careful optimization of EMA periods needed 

- LONG only unable to use short opportunities

- Less frequent signal occurrence 

## Summary

This strategy leverages enhanced MACD for improved mid- to long-term trend identification. But optimization and risk controls are key. Combining with other factors can improve performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2018|Backtest Start Year|
|v_input_2|4|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2018|Backtest Stop Year|
|v_input_5|12|Backtest Stop Month|
|v_input_6|31|Backtest Stop Day|
|v_input_7|12|fastperiod|
|v_input_8|26|slowperiod|
|v_input_9|9|signalperiod|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-07 00:00:00
end: 2023-09-13 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//study("MACDAS")
// strategy("macdas",shorttitle="macdas",overlay=true,default_qty_value=10000,initial_capital=10000,currency=currency.USD)

// Date range filter
testStartYear = input(2018, "Backtest Start Year")
testStartMonth = input(4, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear, testStartMonth, testStartDay, 0, 0)

testStopYear = input(2018, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear, testStopMonth, testStopDay, 0, 0)

inTimeRange = true


fastperiod = input(12,title="fastperiod",minval=1,maxval=500)
slowperiod = input(26,title="slowperiod",minval=1,maxval=500)
signalperiod = input(9,title="signalperiod",minval=1,maxval=500)
fastMA = ema(close, fastperiod)
slowMA = ema(close, slowperiod)
macd = fastMA - slowMA
signal = ema(macd, signalperiod)
macdAS = macd - signal
signalAS = ema(macdAS, signalperiod)
plot(macdAS, color=blue, linewidth=2)
plot(signalAS, color=red, linewidth=2)
plot(0, color=black)

strategy.entry("LONG", strategy.long, when =inTimeRange and crossover(macdAS,signalAS))
strategy.close("LONG", when= inTimeRange and crossunder(macdAS,signalAS))

plotshape(crossover(macdAS, signalAS) , style = shape.arrowup, text="Long",color=green,size=size.huge)
plotshape(crossover(signalAS,macdAS) , style = shape.arrowdown, text="End Long",color=red,size=size.huge)


```

> Detail

https://www.fmz.com/strategy/426808

> Last Modified

2023-09-14 16:46:53

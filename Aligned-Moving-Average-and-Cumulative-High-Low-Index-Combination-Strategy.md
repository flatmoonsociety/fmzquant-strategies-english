
> Name

Aligned-Moving-Average-and-Cumulative-High-Low-Index-Combination-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14370d8f66999d20eab.png)
[trans]


## Overview
This strategy mainly combines high and low indicators, moving average indicators and super trend indicators to determine market trends and build positions.
## Strategy Principle
1. Use the high and low indicators to determine whether the price has reached a new high or a new low in a certain period recently, and add up the scores. When the score rises, it means the strength of the bulls has increased; when the score falls, it means the strength of the shorts has increased.
2. Use the moving average indicator to determine whether the price is in a ladder-shaped upward trend from bottom to top, or a ladder-shaped downward trend from top to bottom. When the moving average rises in a stepped manner, it means that the strength of the bulls has increased; when the moving average decreases in a stepped form, it means that the strength of the short side has increased.
3. Combine the judgment results of high and low indicators and moving average indicators to determine the market trend; combined with the direction of the super trend indicator, look for opportunities to open positions. Specifically, when both the high and low indicators and the moving average indicators show that the strength of the bulls has increased, and the direction of the super trend indicator is downward, a long position is opened; when both the high and low indicators and the moving average indicator show that the strength of the shorts has increased, and the direction of the super trend indicator is upward, a short position is opened.
## Strategic Advantages
1. The high and low indicators can effectively judge the price trend and power changes, and the moving average indicator can effectively judge the price trend. The combination of the two can more accurately judge the market direction.
2. Combining super trend indicators to build a position can avoid opening a position too early or too late. The Super Trend indicator is effective in identifying price reversal points.
3. Multiple indicators verify each other, which can reduce false signals.
## Strategy Risk
1. If the high and low indicators and moving average indicators send out wrong signals, it may result in opening a position at a loss.
2. If the participation level is not high and the parameters of the super trend indicator are not set properly, it may send out wrong signals.
3. If the trend reverses too quickly and the stop loss is improperly set, it may cause large losses.
4. Risks can be reduced by optimizing indicator parameters and adjusting stop loss points.
## Strategy optimization
1. Different types of moving average indicators can be tested to find the best parameter combination.
2. The parameters of high and low indicators and moving average indicators can be optimized to make signals more stable and reliable.
3. Can be combined with other indicators for verification, such as MACD, KD, etc., to reduce false signals.
4. Can be combined with machine learning algorithms to automatically optimize parameters and signal weights.
5. Can combine sentiment analysis and other factors to determine the market popularity and avoid trading low-popularity products.

## Summarize
This strategy determines the market trend and strength through high and low indicators and moving average indicators, and then combines it with the super trend indicator to filter signals. It builds a position when the long and short forces confront each other and the super trend indicator reverses, achieving low-risk transactions. The advantage of the strategy lies in multi-indicator verification and timely opening of positions, which can effectively control risks. The problem lies in false signals and incorrect trend judgment. It can be improved through parameter optimization, stop loss setting, signal filtering and other methods to make the strategy more robust and reliable.
||
## Overview
This strategy mainly combines the High Low Index, Moving Average Index and Super Trend Index to determine the market trend and open positions.  

## Strategy Logic

1. The High Low Index judges whether the latest price over a certain period has made a new high or new low, and accumulates the score. When the score rises, it represents the strengthening of bullish forces. When the score falls, it represents the strengthening of bearish forces.

2. The Moving Average Index judges whether the price is in an upward ladder-shaped uptrend or a downward ladder-shaped downtrend. When the moving average shows a ladder-shaped rise, it represents the strengthening of bullish forces. When it shows a ladder-shaped decline, it represents the strengthening of bearish forces.

3. Combine the judgments of the High Low Index and the Moving Average Index to determine the market trend, and then find trading opportunities combined with the direction of the Super Trend Index. Specifically, when both the High Low Index and the Moving Average Index show strengthening bullish forces and the direction of the Super Trend Index is downward, open long positions. When both indices show strengthening bearish forces and the direction of the Super Trend Index is upward, open short positions.

## Advantages

1. The High Low Index can effectively judge the price movement and changes in momentum. The Moving Average Index can effectively determine the price trend. The combination of both can more accurately determine the market direction.  

2. Opening positions combined with the Super Trend Index can avoid premature or late opening of positions. The Super Trend Index can effectively identify price reversal points.

3. Multiple indicators verify each other and reduce false signals.

## Risks

1. Incorrect signals from the High Low Index and Moving Average Index may lead to loss-making positions.  

2. Insufficient participation and improper parameter settings of the Super Trend Index may generate incorrect signals.

3. Rapid trend reversals and improper stop loss settings may lead to large losses.

4. Risks can be reduced by optimizing indicator parameters, adjusting stop loss price levels, etc.

## Optimization

1. Test different types of moving average indicators to find the optimal combination of parameters.  

2. Optimize the parameters of the High Low Index and Moving Average Index to make the signals more stable and reliable.

3. Incorporate other indicators for verification, such as MACD, KD, etc., to reduce false signals. 

4. Incorporate machine learning algorithms to automatically optimize parameters and signal weights.

5. Incorporate sentiment analysis to avoid trading less popular products.

## Conclusion

This strategy determines market trends and momentum through the High Low Index and Moving Average Index, and then filters the signals using the Super Trend Index, opening positions when bullish and bearish forces confront each other and the Super Trend Index reverses. Its advantages lie in multiple signal verification and timely opening of positions, which can effectively control risks. Existing problems include false signals and trend misjudgment. Various improvements can be made through parameter optimization, stop loss settings, signal filtering, etc. to make the strategy more robust and reliable.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0|Moving Average Type: sma|ema|hma|rma|vwma|wma|
|v_input_2|true|includePartiallyAligned|
|v_input_3|50|HighLowPeriod|
|v_input_4|10|LookbackPeriod|
|v_input_5|2|supertrendMult|
|v_input_6|10|supertrendLength|
|v_input_7|0|Trade Direction: strategy.direction.long|strategy.direction.all|strategy.direction.short|
|v_input_8|10|backtestYears|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-21 00:00:00
end: 2023-11-20 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © HeWhoMustNotBeNamed

//@version=4
strategy("AlignedMA and Cumulative HighLow Strategy", overlay=true, initial_capital = 1000, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, commission_type = strategy.commission.percent, pyramiding = 1, commission_value = 0.01, calc_on_order_fills = true)

MAType = input(title="Moving Average Type", defval="sma", options=["ema", "sma", "hma", "rma", "vwma", "wma"])
includePartiallyAligned = input(true)
HighLowPeriod = input(50, minval=1,step=1)
LookbackPeriod = input(10, minval=1,step=1)

supertrendMult = input(2, minval=1, maxval=10, step=0.5)
supertrendLength = input(10, minval=1)

tradeDirection = input(title="Trade Direction", defval=strategy.direction.long, options=[strategy.direction.all, strategy.direction.long, strategy.direction.short])
backtestYears = input(10, minval=1, step=1)

f_getMovingAverage(source, MAType, length)=>
    ma = sma(source, length)
    if(MAType == "ema")
        ma := ema(source,length)
    if(MAType == "hma")
        ma := hma(source,length)
    if(MAType == "rma")
        ma := rma(source,length)
    if(MAType == "vwma")
        ma := vwma(source,length)
    if(MAType == "wma")
        ma := wma(source,length)
    ma
    
f_getMaAlignment(MAType, includePartiallyAligned)=>
    ma5 = f_getMovingAverage(close,MAType,5)
    ma10 = f_getMovingAverage(close,MAType,10)
    ma20 = f_getMovingAverage(close,MAType,20)
    ma30 = f_getMovingAverage(close,MAType,30)
    ma50 = f_getMovingAverage(close,MAType,50)
    ma100 = f_getMovingAverage(close,MAType,100)
    ma200 = f_getMovingAverage(close,MAType,200)

    upwardScore = 0
    upwardScore := close > ma5? upwardScore+1:upwardScore
    upwardScore := ma5 > ma10? upwardScore+1:upwardScore
    upwardScore := ma10 > ma20? upwardScore+1:upwardScore
    upwardScore := ma20 > ma30? upwardScore+1:upwardScore
    upwardScore := ma30 > ma50? upwardScore+1:upwardScore
    upwardScore := ma50 > ma100? upwardScore+1:upwardScore
    upwardScore := ma100 > ma200? upwardScore+1:upwardScore
    
    upwards = close > ma5 and ma5 > ma10 and ma10 > ma20 and ma20 > ma30 and ma30 > ma50 and ma50 > ma100 and ma100 > ma200
    downwards = close < ma5 and ma5 < ma10 and ma10 < ma20 and ma20 < ma30 and ma30 < ma50 and ma50 < ma100 and ma100 < ma200
    upwards?1:downwards?-1:includePartiallyAligned ? (upwardScore > 5? 0.5: upwardScore < 2?-0.5:upwardScore>3?0.25:-0.25) : 0

f_getHighLowValue(HighLowPeriod)=>
    currentHigh = highest(high,HighLowPeriod) == high
    currentLow = lowest(low,HighLowPeriod) == low
    currentHigh?1:currentLow?-1:0

inDateRange = time >= timestamp(syminfo.timezone, year(timenow) - backtestYears, 01, 01, 0, 0)

maAlignment = f_getMaAlignment(MAType,includePartiallyAligned)
alignedMaIndex = sum(maAlignment,LookbackPeriod)

maAlignmentDirection = alignedMaIndex > alignedMaIndex[1] ? 1 : alignedMaIndex < alignedMaIndex[1] ? -1 : 0
maAlignmentDirection := maAlignmentDirection == 0? nz(maAlignmentDirection[1],0):maAlignmentDirection

highLowIndex = f_getHighLowValue(HighLowPeriod)
cumulativeHighLowIndex = sum(highLowIndex,LookbackPeriod)

hlDirection = cumulativeHighLowIndex > cumulativeHighLowIndex[1] ? 1 : cumulativeHighLowIndex < cumulativeHighLowIndex[1] ? -1 : 0
hlDirection := hlDirection == 0? nz(hlDirection[1],0):hlDirection

[superTrend, dir] = supertrend(supertrendMult, supertrendLength)

buyEntry = (dir == -1 and maAlignmentDirection == 1 and hlDirection == 1)
sellEntry = (dir == 1 and maAlignmentDirection == -1 and hlDirection == -1)

barColor = buyEntry?color.lime:sellEntry?color.orange:color.gray
barcolor(barColor)

// strategy.risk.allow_entry_in(tradeDirection)
strategy.entry("Buy", strategy.long, when=barColor == color.lime and inDateRange, oca_name="oca_buy")
strategy.close("Buy", when=dir == 1)

strategy.entry("Sell", strategy.short, when=barColor == color.orange and inDateRange, oca_name="oca_sell")
strategy.close("Sell", when=dir == -1)

```

> Detail

https://www.fmz.com/strategy/432793

> Last Modified

2023-11-21 15:19:35

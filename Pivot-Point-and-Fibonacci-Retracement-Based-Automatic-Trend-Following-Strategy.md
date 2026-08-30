
> Name

Pivot-Point-and-Fibonacci-Retracement-Based-Automatic-Trend-Following-Strategy Based on Pivot Points and Fibonacci Retracement
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/79fc000dc22e3f7250f600aae766fd0d3b888195d0f7f4afd837503c94619c37.png)
[trans]

## Overview
This strategy automatically identifies the ABC band of stock prices based on pivot points and Fibonacci retracement ratios, and gives long and short position signals. The strategy uses pivot points to determine stock price bands, then calculates the Fibonacci retracement ratio between the ABC bands, and generates trading signals if certain conditions are met.
## Strategy Principle
1. Calculate a stock’s pivot high and low
2. Determine whether the price is falling from the high point of the previous band or rising from the low point of the previous band.
3. Calculate the Fibonacci retracement ratio between the current band and the previous band
4. If the retracement ratios of the rising band and the falling band are both within an appropriate range, it is determined that an ABC band may be formed.
5. After the ABC band is confirmed, when going long, set the stop loss to point C and the take profit to 1.5 times the fluctuation; when going short, set the stop loss to point A and the take profit to 1.5 times the fluctuation.
## Advantage Analysis
1. Use pivot points to determine key support and resistance areas to improve signal accuracy.
2. Use Fibonacci retracement to identify ABC patterns and automatically capture trend transition points
3. Clear and reasonable stop-profit and stop-loss rules to avoid huge losses
## Risk Analysis
1. Pivot points and Fibonacci retracements do not guarantee accurate judgment of trend transition points every time, and misjudgments may occur.
2. The stop loss at point C and point A may be breached, causing the loss to expand.
3. Parameter optimization is required, such as the range of Fibonacci retracement ratios
## Optimization direction
1. It can be combined with more technical indicators to help determine the ABC pattern and improve signal accuracy.
2. The range of Fibonacci retracement ratio can be optimized to adapt to more market conditions
3. Machine learning methods can be combined to train a model for judging ABC shapes.
## Summary
This strategy determines key support and resistance areas based on pivot points, uses Fibonacci retracement ratios to automatically identify ABC patterns, and provides long and short position trading signals at the turning point of the band. The strategy logic is clear and concise, the stop-profit and stop-loss settings are reasonable, and the risk can be effectively controlled. However, there is also a certain risk of misjudgment, which requires further optimization and improvement to adapt to more market conditions.
||

## Overview
This strategy automatically identifies ABC patterns in stock prices based on pivot points and Fibonacci retracement ratios, and generates long/short signals. It uses pivot points to determine price waves and calculates Fibonacci retracement ratios between ABC waves. If the ratios meet certain criteria, trading signals are generated.

## Strategy Logic  
1. Calculate the stock's pivot high and low points
2. Judge if the price has fallen from the previous high point or risen from the previous low point  
3. Calculate the Fibonacci retracement ratio between the current wave and previous wave
4. If the retracement ratios of both up and down waves are within proper ranges, determine a potential ABC pattern
5. After ABC pattern confirmation, set stop loss at Point C for long, and Point A for short. Set take profit at 1.5 times the price wave range.

## Advantage Analysis
1. Pivot points identify key support/resistance levels to improve signal accuracy 
2. Fibonacci retracements catch trend turning points by identifying ABC patterns
3. Clear profit/loss rules avoid huge losses 

## Risk Analysis  
1. Pivot points and Fibonacci retracements cannot ensure perfect identification of every trend turning point. Misjudgements may occur.
2. Point C and Point A stops can be broken through, leading to larger losses
3. Parameters like Fibonacci retracement ratio ranges need further optimization

## Optimization Directions
1. Incorporate more technical indicators to assist ABC pattern confirmation, improving signal accuracy
2. Optimize Fibonacci retracement ratio ranges to suit more market conditions 
3. Utilize machine learning methods to train ABC pattern recognition models

## Conclusion
This strategy identifies ABC patterns for generating long/short signals at trend turning points, based on pivot point confirmation of key support/resistance levels, and Fibonacci retracement ratio calculations. The logic is simple and clean, with sensible profit/loss rules that effectively control risks. However, certain misjudgement risks remain, requiring further optimizations and improvements to suit more market conditions.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|len|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-19 23:59:59
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © kerok3g

//@version=5
strategy("ABCD Strategy", shorttitle="ABCDS", overlay=true, commission_value=0.04)
calcdev(fprice, lprice, fbars, lbars) =>
    rise = lprice - fprice
    run = lbars - fbars
    avg = rise/run
    ((bar_index - lbars) * avg) + lprice

len = input(5)

ph = ta.pivothigh(len, len)
pl = ta.pivotlow(len, len)

var bool ishigh = false
ishigh := ishigh[1]

var float currph = 0.0
var int currphb = 0
currph := nz(currph)
currphb := nz(currphb)

var float oldph = 0.0
var int oldphb = 0
oldph := nz(oldph)
oldphb := nz(oldphb)

var float currpl = 0.0
var int currplb = 0
currpl := nz(currpl)
currplb := nz(currplb)

var float oldpl = 0.0
var int oldplb = 0
oldpl := nz(oldpl)
oldplb := nz(oldplb)

if (not na(ph))
    ishigh := true
    oldph := currph
    oldphb := currphb
    currph := ph
    currphb := bar_index[len]
else
    if (not na(pl))
        ishigh := false
        oldpl := currpl
        oldplb := currplb
        currpl := pl
        currplb := bar_index[len]

endHighPoint = calcdev(oldph, currph, oldphb, currphb)
endLowPoint = calcdev(oldpl, currpl, oldplb, currplb)

plotshape(ph, style=shape.triangledown, color=color.red, location=location.abovebar, offset=-len)
plotshape(pl, style=shape.triangleup, color=color.green, location=location.belowbar, offset=-len)

// var line lnhigher = na
// var line lnlower = na
// lnhigher := line.new(oldphb, oldph, bar_index, endHighPoint)
// lnlower := line.new(oldplb, oldpl, bar_index, endLowPoint)
// line.delete(lnhigher[1])
// line.delete(lnlower[1])

formlong = oldphb < oldplb and oldpl < currphb and currphb < currplb
longratio1 = (currph - oldpl) / (oldph - oldpl)
longratio2 = (currph - currpl) / (currph - oldpl)

formshort = oldplb < oldphb and oldphb < currplb and currplb < currphb
shortratio1 = (oldph - currpl) / (oldph - oldpl)
shortratio2 = (currph - currpl) / (oldph - currpl)

// prevent multiple entry for one pattern
var int signalid = 0
signalid := nz(signalid[1])

longCond = formlong and 
           longratio1 < 0.7 and 
           longratio1 > 0.5 and 
           longratio2 > 1.1 and 
           longratio2 < 1.35 and 
           close < oldph and 
           close > currpl and 
           signalid != oldplb
if (longCond)
    signalid := oldplb
    longsl = currpl - ta.tr
    longtp = ((close - longsl) * 1.5) + close
    strategy.entry("Long", strategy.long)
    strategy.exit("Exit Long", "Long", limit=math.min(longtp, oldph), stop=longsl)

shortCond = formshort and 
             shortratio1 < 0.7 and 
             shortratio1 > 0.5 and 
             shortratio2 > 1.1 and 
             shortratio2 < 1.35 and 
             close > oldpl and 
             close < currph and 
             signalid != oldphb

if (shortCond)
    signalid := oldphb
    shortsl = currph + ta.tr
    shorttp = close - ((shortsl - close) * 1.5)
    strategy.entry("Short", strategy.short)
    strategy.exit("Exit Short", "Short", limit=math.max(shorttp, oldpl), stop=shortsl)

```

> Detail

https://www.fmz.com/strategy/437740

> Last Modified

2024-01-05 11:34:17

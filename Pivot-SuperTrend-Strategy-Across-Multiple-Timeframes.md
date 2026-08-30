
> Name

Pivot-SuperTrend-Strategy-Across-Multiple-Timeframes
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12d99dd2a6950dcc06c.png)
[trans]
## Overview
This strategy combines the Pivot Point indicator and the Average True Band indicator to implement a multi-time frame trend following system. It can capture the trend of the mid-cycle, while using pivot points to determine long-term support and resistance to achieve better entry and exit.
## Strategy Principle
This strategy is mainly based on two indicators:
1. Pivot point indicator: determine the upper pivot point and lower pivot point by calculating the average of the highest price, lowest price, and closing price in a certain period. Pivot points serve as key support and resistance areas.
2. Average true fluctuation zone: Calculate the average true fluctuation range for a certain period, and move up and down the channel on the central axis. The upper and lower edges of the channel can be used as dynamic stop loss lines.
The specific trading logic of the strategy is:
When the price breaks through the average true fluctuation band channel, take the long or short direction consistent with the breakthrough direction. When the price returns to the channel, close the position. At the same time, when the price breaks through the upper pivot point, take a long position; when the price breaks through the lower pivot point, take a short position.
This strategy also introduces the midline concept of pivot points. When the take profit breaks through the midline, you may choose to harvest half of the profit and control risks.
## Advantage Analysis
This strategy has several advantages:
1. Multi-time frame design, medium and long-term Determines are the general trend, and short-term Determines are specific entry points.
2. The pivot point midline can be used as a risk control option to harvest half of the profits and ensure profitability.
3. The average true fluctuation band channel provides a clear stop loss position.
4. The strategy has fewer parameters and is easy to optimize and find the best parameter combination.
5. The risk of false breakthroughs is avoided to the greatest extent.
## Risk Analysis
There are also some risks with this strategy:
1. When the market fluctuates violently, the risk of stop loss is greater.
2. When the market fluctuates, pressure is likely to form on the central axis, and losses may be stopped frequently.
3. Improper parameter selection may lead to frequent transactions or too few transactions.
4. The recent price breakthrough of the pivot point may be a false breakthrough.
## Optimization direction
This strategy can be optimized from the following directions:
1. Combine with more indicators to filter entry signals to avoid false breakthroughs. For example, combined with energy indicators, Bollinger Bands indicators, etc.
2. Optimize the period parameters of the pivot point and the average true fluctuation band to find the best parameter combination.
3. Set up a buffer zone near the center line of the pivot point to prevent the center line from being triggered frequently.
4. Add appropriate trend filtering to ensure that the general trend operates in the same direction.
## Summarize
This strategy is overall a very useful trend following strategy. It solves the problem of stop loss difficulties in most trend systems and realizes risk-controllable trend trading. It is a very recommended strategy. Through subsequent appropriate optimization and improvement, the effect of this strategy can be further improved.
||

## Overview

This strategy combines the Pivot Points indicator and Average True Range Bands to implement a trend tracking system across multiple timeframes. It can capture trends over intermediate cycles while using Pivot Points to determine long-term support and resistance for better entry and exit.

## Strategy Logic  

This strategy is mainly based on two indicators:

1. Pivot Points: Calculate the average of highest, lowest and closing prices over a certain period to determine upper and lower pivot points. Pivot points can serve as key support and resistance areas. 

2. Average True Range Bands: Calculate the average true range over a certain period, and move the middle band up and down to form a channel. The upper and lower bands can serve as dynamic stop loss lines.

The specific trading logic is:

When the price breaks through the Average True Range channel, take long or short positions along the breakout direction. When the price returns into the channel, close positions. Also, when the price breaks through the upper pivot point, take long stance; when the price breaks through the lower pivot point, take short stance.  

The strategy also introduces the pivot middle line concept. When take profit breaks the middle line, it’s possible to close half position to lock in some profit and control risk.

## Advantage Analysis 

The strategy has the following advantages:

1. Multiple timeframe design. Long and intermediate cycles determine major trends while short cycles determine specific entries.  

2. The pivot middle line provides an option to close half position, locking in some profit while ensuring winning trades.

3. Average True Range Bands provide clear stop loss levels.  

4. The strategy has few parameters, easy to optimize for best parameter combinations. 

5. It maximally avoids the risk of false breakouts.

## Risk Analysis

The strategy also has some risks:

1. Larger stop loss risks during high market volatility. 

2. The middle line may frequently trigger stop loss during market consolidations.  

3. Improper parameter selections may result in too few or too frequent trades. 

4. Recent pivot point breaks may turn out to be false breaks.

## Optimization Directions

The strategy can be optimized from the following aspects:

1. Combine more filters like volume and Bollinger Bands to avoid false signals.  

2. Optimize periods of Pivot Points and ATR to find best parameter combinations.  

3. Set a buffer zone around the middle line to avoid frequent triggers. 

4. Add proper trend filters to ensure operating along major trends.

## Conclusion

In general, this is a very practical trend tracking strategy. It solves the common stop loss difficulties of trend systems and achieves risk-controllable trend trading. It is a highly recommendable strategy. With proper optimizations and improvements, its performance can be further enhanced.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2|Pivot Point Period|
|v_input_2|3|ATR Factor|
|v_input_3|10|ATR Period|
|v_input_4|false|Use Center Line to Close Entry for 50%|
|v_input_5|false|Show Pivot Points|
|v_input_6|false|Show PP Center Line|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © LonesomeTheBlue

//@version=4
strategy("Pivot Point SuperTrend [Backtest]", overlay = true)
prd = input(defval = 2, title="Pivot Point Period", minval = 1, maxval = 50)
Factor=input(defval = 3, title = "ATR Factor", minval = 1, step = 0.1)
Pd=input(defval = 10, title = "ATR Period", minval=1)
usecenter = input(defval = false, title="Use Center Line to Close Entry for 50%")
showpivot = input(defval = false, title="Show Pivot Points")
showcl = input(defval = false, title="Show PP Center Line")


float ph = na
float pl = na
ph := pivothigh(prd, prd)
pl := pivotlow(prd, prd)

plotshape(ph and showpivot, text="H",  style=shape.labeldown, color=na, textcolor=color.red, location=location.abovebar, transp=0, offset = -prd)
plotshape(pl and showpivot, text="L",  style=shape.labeldown, color=na, textcolor=color.lime, location=location.belowbar, transp=0, offset = -prd)

float center = na
center := center[1]
float lastpp = ph ? ph : pl ? pl : na
if lastpp
    if na(center)
        center := lastpp
    else
        center := (center * 2 + lastpp) / 3

Up = center - (Factor * atr(Pd))
Dn = center + (Factor * atr(Pd))

float TUp = na
float TDown = na
Trend = 0
TUp := close[1] > TUp[1] ? max(Up, TUp[1]) : Up
TDown := close[1] < TDown[1] ? min(Dn, TDown[1]) : Dn
Trend := close > TDown[1] ? 1: close < TUp[1]? -1: nz(Trend[1], 1)
Trailingsl = Trend == 1 ? TUp : TDown

linecolor = Trend == 1 and nz(Trend[1]) == 1 ? color.lime : Trend == -1 and nz(Trend[1]) == -1 ? color.red : na
plot(Trailingsl, color = linecolor ,  linewidth = 2, title = "PP SuperTrend")

plot(showcl ? center : na, color = showcl ? center < hl2 ? color.blue : color.red : na, transp = 0)

bsignal = Trend == 1 and Trend[1] == -1
ssignal = Trend == -1 and Trend[1] == 1

if bsignal
    strategy.entry("Buy", true, 2, comment = "Buy")
if ssignal
    strategy.entry("Sell", false, 2, comment = "Sell")

if strategy.position_size == 2 and center > hl2 and usecenter
    strategy.close("Buy", qty_percent = 50, comment = "close buy entry for 50%")
if strategy.position_size == -2 and center < hl2 and usecenter
    strategy.close("Sell", qty_percent = 50, comment = "close sell entry for 50%")
    
if change(Trend)
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/440565

> Last Modified

2024-01-31 17:29:37

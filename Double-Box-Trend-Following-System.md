
> Name

Double-Box-Trend-Following-System Double-Box-Trend-Following-System
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1abc0fa4702b6eca3c3.png)

[trans]

## Overview
The trend following system is a trend following strategy based on a two-box system. It uses the long-term cycle box to determine the overall trend direction, and when the short-term box generates a signal, it selects a trading signal consistent with the long-term trend direction to enter the market. This strategy follows the trend and controls risks while maximizing profits.
## Strategy Principle
This strategy uses two boxes to determine the trend. The long-term box uses a longer period to judge the main trend direction, and the short-term box uses a shorter period to judge specific trading signals.
The strategy first calculates the highest price and lowest price of the long-term box to determine the main trend direction. There are three types of trend directions:
- The highest price with a K line on the highest price is defined as an upward trend and assigned a value of 1
- The lowest price with a K line under the lowest price is defined as a downward trend and assigned a value of -1
- Otherwise, keep the original trend direction unchanged.
After determining the main trend direction, the strategy begins to enter the market based on short-term boxes. Specifically:
- When the main trend is upward and the lowest price of the short-term box is equal to the lowest price of the previous K line and lower than the current lowest price of the short-term box, go long
- When the main trend is downward and the highest price of the short-term box is equal to the highest price of the previous K line and higher than the current highest price of the short-term box, go short
In addition, the strategy also sets stop loss and take profit:
- The stop loss for long orders is the lowest price of the long-term box, and the stop loss for short orders is the highest price of the long-term box.
- Take-profit for long orders is the highest price of the short-term box, and take-profit for short orders is the lowest price of the short-term box.
When the main trend turns, close all positions.
## Advantage Analysis
This strategy has the following advantages:
1. Using the dual-box judgment system, it can effectively identify the trend direction and reduce the probability of wrong transactions.
2. Only enter the market when short-term reversal signals are consistent with the long-term trend direction to avoid being misled by short-term market noise.
3. The combination of long and short cycles not only ensures the ability to capture the main trends, but also has the flexibility to adjust positions appropriately.
4. It is more reasonable to set stop-loss and stop-profit points, which can control the risk while grasping the trend.
5. Quickly close positions when the main trend turns and control losses in a timely manner
## Risk Analysis
This strategy also has the following risks:
1. Improper setting of long and short cycles can easily lead to frequent transactions or missed opportunities.
2. A short-term trend reversal caused by an unexpected event does not necessarily represent a long-term trend change, and there is still a risk of loss at this time.
3. If the stop loss point is too close, you may be shaken out of the market.
4. The profit stop point is too loose and may not maximize profits.
5. If there is an error in long-term trend judgment, subsequent transactions will suffer losses expands
6. Methods to deal with these risks include: adjusting long and short cycle parameters, optimizing stop loss and take profit positions, adding filtering conditions, etc.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add filter conditions to avoid misleading signals by short-term false breakthroughs
2. Optimize long and short cycle parameters to make them more consistent with the characteristics of different varieties
3. Dynamically adjust the stop-loss and take-profit positions to make the stop-loss more accurate and the take-profit more adequate.
4. Add position management strategies to make the position size more reasonable
5. Use volume and other indicators to determine the reliability of trend turning points
6. Use machine learning methods to automatically optimize parameters and filtering conditions
## Summarize
The trend following system overall is a very practical trend following strategy. It has the ability to judge trends and make short-term adjustments at the same time, and it can control risks while tracking trends. Through continuous optimization, this strategy can become a powerful automated trend trading system. It contains the core philosophy of trend trading and is worthy of in-depth study.
[/trans]

||

# 

## Overview

The Trend Following System is a trend tracking strategy based on a double box system. It uses a long-term box to determine the overall trend direction and takes signals that align with the major trend when the short-term box triggers. This strategy follows trends while managing risks.

## Strategy Logic

The strategy uses two boxes to determine the trend. The long-term box uses a longer period to judge the major trend direction, and the short-term box uses a shorter period to generate trading signals.

First, the strategy calculates the highest and lowest prices of the long-term box to determine the major trend direction. The trend direction can be:

- If the highest price crosses above the highest price of the previous bar, it is defined as an uptrend, assigned a value of 1
- If the lowest price crosses below the lowest price of the previous bar, it is defined as a downtrend, assigned a value of -1  
- Otherwise, maintain the original trend direction

After determining the major trend, the strategy starts taking positions based on the short-term box signals. Specifically:

- When the major trend is up and the short-term box's lowest price equals the previous bar's lowest price and is lower than the current short-term box's lowest price, go long.
- When the major trend is down and the short-term box's highest price equals the previous bar's highest price and is higher than the current short-term box's highest price, go short.

In addition, stop loss and take profit are configured:

- Long stop loss is the lowest price of the long-term box, short stop loss is the highest price of the long-term box
- Long take profit is the highest price of the short-term box, short take profit is the lowest price of the short-term box

When the major trend reverses, close all positions.

## Advantage Analysis 

The advantages of this strategy include:

1. The double box system effectively identifies trend directions and reduces incorrect trades
2. Only taking reversal signals that align with the major trend avoids being misled by short-term market noise
3. The combination of long and short periods ensures capturing major trends while maintaining position adjustment flexibility
4. Reasonable stop loss and take profit points control risk while following trends
5. Quickly flattening all positions when the major trend reverses minimizes losses

## Risk Analysis

The risks of this strategy include:

1. Improper long and short period settings may cause overtrading or missing opportunities
2. Short-term reversals may not represent long-term trend changes, still posing loss risks
3. Stop loss too close may get stopped out prematurely 
4. Take profit too loose may not maximize profits
5. Wrong judgment of the major trend leads to losses
6. Solutions include adjusting periods, optimizing stops/targets, adding filters etc.

## Optimization Directions

The strategy can be improved by:

1. Adding filters to avoid false breakouts
2. Optimizing long and short periods for different products  
3. Dynamically adjusting stop loss and take profit levels
4. Incorporating position sizing rules
5. Using volume etc. to judge reliability of trend changes
6. Utilizing machine learning to auto-optimize parameters and filters

## Summary

The Trend Following System is a practical trend trading strategy combining trend determination and short-term adjustments. With continuous optimizations, it can become a robust automated system that tracks trends while controlling risks. It contains the core philosophies of trend trading and is worth in-depth studying.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|80|Longterm Period|
|v_input_2|21|Shortterm Period|
|v_input_3|true|Show Target|
|v_input_4|true|Show Trend|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-25 00:00:00
end: 2023-10-26 07:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © LonesomeTheBlue

//@version=4
strategy("Grab Trading System", overlay = true)
flb = input(defval = 80, title = "Longterm Period", minval = 1)
slb = input(defval = 21, title = "Shortterm Period", minval = 1)
showtarget = input(defval = true, title = "Show Target")
showtrend = input(defval = true, title = "Show Trend")

major_resistance = highest(flb)
major_support = lowest(flb)
minor_resistance = highest(slb)
minor_support = lowest(slb)

var int trend = 0
trend := high > major_resistance[1] ? 1 : low < major_support[1] ? -1 : trend
strategy.entry("Buy", true, when = trend == 1 and low[1] == minor_support[1] and low > minor_support)
strategy.entry("Sell", false, when = trend == -1 and high[1] == minor_resistance[1] and high < minor_resistance)

if strategy.position_size > 0
    strategy.exit("Buy", stop = major_support, comment = "Stop Buy")
    if high[1] == minor_resistance[1] and high < minor_resistance
        strategy.close("Buy", comment ="Close Buy")
    
if strategy.position_size < 0
    strategy.exit("Sell", stop = major_resistance, comment = "Stop Sell")
    if low[1] == minor_support[1] and low > minor_support
        strategy.close("Sell", comment ="Close Sell")

if strategy.position_size != 0 and change(trend)
    strategy.close_all()
    
majr = plot(major_resistance, color = showtrend and trend == -1 and trend[1] == -1 ? color.red : na)
majs = plot(major_support, color = showtrend and trend == 1 and trend[1] == 1 ? color.lime : na)
minr = plot(minor_resistance, color = showtarget and trend == 1 and strategy.position_size > 0 ? color.yellow : na, style = plot.style_circles)
mins = plot(minor_support, color = showtarget and trend == -1 and strategy.position_size < 0 ? color.yellow : na, style = plot.style_circles)

fill(majs, mins, color = showtrend and trend == 1 and trend[1] == 1 ? color.lime : na, transp = 85)
fill(majr, minr, color = showtrend and trend == -1 and trend[1] == -1 ? color.red : na, transp = 85)

```

> Detail

https://www.fmz.com/strategy/430901

> Last Modified

2023-11-02 17:19:22

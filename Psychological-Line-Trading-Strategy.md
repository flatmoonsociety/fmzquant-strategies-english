
> Name

Psychological-Line-Trading-Strategy Psychological-Line-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses psychological line indicators to determine the market buying and selling power ratio to capture changes in market trends. Go long when the buying force is stronger than the selling force, and go short when the selling force is stronger than the buying force. Psychological lines are simple and easy to use and can be used as an auxiliary tool for trend identification.
## Strategy Principle
1. The psychological line indicator calculates the proportion of rising closing prices within a certain period.
2. When the ratio exceeds 50%, it is considered that the buying power is greater than the selling power, and a long signal is given.
3. When the ratio is lower than 50%, it is considered that the selling force is greater than the buying force, and a short signal is given.
4. When the ratio fluctuates around 50%, it is considered that buying and selling are balanced and the market has no clear direction.
5. Parameters can be flexibly adjusted to judge short-term or long-term trends.
## Advantage Analysis
1. The calculation method is simple and easy to operate.
2. Visually display the strength of buying and selling and assist in judging the flow of funds.
3. Can discover partially inverted signals.
4. Can be used in conjunction with other indicators to improve strategy effectiveness.
## Risk Analysis
1. Unable to judge the duration and intensity of the trend.
2. Improper parameter settings may produce a large number of error signals.
3. It is easy to be trapped when used alone and should be combined with other indicators.
4. Parameters need to be optimized to adapt to different varieties and cycles.
## Optimization direction
1. Test the effects of different parameters on various varieties to find the best cycle.
2. Combine more indicators to determine the sustainability of the trend.
3. Optimize fund management strategies and set stop loss and take profit.
4. Evaluate the strength of the trend and avoid opening reverse positions too early.
5. Turn off the policy during a specific time period to avoid error-prone time periods.
## Summarize
The psychological line indicator itself is relatively simple, but it works well when used together. It can be used as one of the auxiliary tools for discovering trend changes, but it should not be used alone. Through parameter optimization and integration of other indicators, the psychological line strategy can be brought to a new level and is worthy of further research.
|| 

## Overview

This strategy uses the Psychological Line indicator to gauge the buying/selling power in the market and capture trend changes. It goes long when buying power is stronger than selling power, and goes short when selling power exceeds buying power. The Psychological Line is simple and easy to use as a trend discovery tool.

## Strategy Logic

1. Psychological Line calculates the percentage of closing prices that have risen over a period. 

2. When the percentage exceeds 50%, it indicates buying power is greater than selling power, giving long signal.

3. When the percentage is below 50%, it indicates selling power exceeds buying power, giving short signal.

4. When the percentage oscillates near 50%, it indicates balanced buying/selling and no clear direction.

5. The parameters can be flexibly adjusted to judge short or long term trends.

## Advantage Analysis

1. Simple calculation method, easy to implement for live trading.

2. Intuitively displays the strength of buying/selling power as supplementary judgment of capital flows.

3. Can discover some reversal signals. 

4. Can be used together with other indicators to improve strategy performance.

## Risk Analysis

1. Unable to determine the duration and strength of trends.

2. Improper parameter settings may generate excessive false signals.

3. Prone to whipsaws when used alone, should combine with other indicators.

4. Need parameter optimization for different products and timeframes.

## Improvement Directions

1. Test different parameters on various products to find optimal periods.

2. Incorporate more indicators to determine trend persistence.

3. Optimize money management strategies by setting stop loss and take profit. 

4. Assess trend strength to avoid premature reverse entries.

5. Disable strategy during specific hours to avoid wrong signal-prone periods.

## Summary

The Psychological Line indicator itself is quite simple, but works well when combined with other tools. It can serve as an auxiliary tool for discovering trend changes, but should not be used alone. By optimizing parameters and integrating with other indicators, the Psychological Line strategy can be enhanced to a new level and is worth further research.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Length|
|v_input_2|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-12 00:00:00
end: 2023-09-19 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 10/04/2018
// Psychological line (PSY), as an indicator, is the ratio of the number of 
// rising periods over the total number of periods. It reflects the buying 
// power in relation to the selling power.
//
// If PSY is above 50%, it indicates that buyers are in control. Likewise, 
// if it is below 50%, it indicates the sellers are in control. If the PSY 
// moves along the 50% area, it indicates balance between the buyers and 
// sellers and therefore there is no direction movement for the market.
//
// You can change long to short in the Input Settings
// WARNING:
//  - For purpose educate only
//  - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Psychological line Backtest")
Length = input(20, minval=1)
reverse = input(false, title="Trade reverse")
xPSY = sum(close > close[1],Length) / Length * 100
clr = iff(xPSY >= 50, green, red)
pos = iff(xPSY > 50, 1,
       iff(xPSY < 50, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
p1 = plot(50, color=black, title="0")
p2 = plot(xPSY, color=blue, title="PSY")
fill(p1, p2, color=clr)
```

> Detail

https://www.fmz.com/strategy/427375

> Last Modified

2023-09-20 14:50:47

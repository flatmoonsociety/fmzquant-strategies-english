
> Name

Three-Line-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is improved based on the three-line pattern representation. It consists of two lines composed of closing prices forming a "cloud" pattern. If the price falls below the bottom of the cloud while in a bull trend, a new short trend begins; if the price breaks through the top of the cloud while in a bear trend, a new bull trend begins. This strategy is a pure price action strategy and can be used in combination with indicators such as Super Trend.
## Strategy Principle
1. Define the current price xu, and xu1, xu2, xu3 used to draw the three-line pattern.
2. Determine the price as the upper and lower limits of the three-line pattern drawing, and update xu1, xu2, and xu3.
3. If xu breaks through xu3, the short position will start; if xu breaks through xu1, the long position will start.
4. Draw the cloud shape with xu and xu3 as the upper and lower limits.
5. You can choose forward trading or reverse trading.
6. Go long and short when it breaks through the cloud, and close the position when it returns to the cloud.
## Advantage Analysis
The main advantages of this strategy:
1. Based on pure price action and not affected by external indicators.
2. The three-line pattern is clear and intuitive, making it easy to judge and operate.
3. Configurable reverse trading, suitable for bearish opportunities.
4. Easily combined with trends and other indicators.
5. Backtesting and visualization are convenient, easy to master and optimize.
## Risk Analysis
The main risks of this strategy are:
1. Pure price behavior is susceptible to false breakthroughs caused by unexpected events.
2. Without stop loss settings, there is a greater risk of loss.
3. The impact of transaction costs is not considered.
4. The parameters are fixed, and the effects of different varieties may be different.
5. Continuous breakthroughs are not considered.
6. Be cautious when trading in the opposite direction, as it may go against the general trend.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Set up a stop loss strategy and optimize the stop loss point.
2. Consider the impact of transaction fees.
3. Test the parameter effects of different varieties and establish parameter optimization.
4. Optimize the pattern breakthrough judgment logic and handle continuous breakthroughs.
5. Increase the combination with trend indicators to avoid going against the trend.
6. Add position quantity control.
7. Expand the backtest time range and verify the robustness.
## Summarize
The three-line pattern breakout strategy is intuitive and easy to operate, and generates trading signals based on price action judgments. Combining trends and other indicators can enhance your strategy. By adding stop loss, optimized parameters and logic, position control, etc., it can be improved into a more stable short-term trading strategy.
||

## Overview

This strategy is based on a modified three line break chart. Two lines made of closing prices form a "cloud" shape. Breakout below the cloud signals a new bearish trend. Breakout above the cloud signals a new bullish trend. It is a price action strategy that can be combined with trend filters like SuperTrend.

## Strategy Logic  

1. Define current price xu, xu1, xu2, xu3 for plotting three lines.

2. Update xu1, xu2, xu3 based on price as upper/lower band.

3. xu breaking xu3 starts a short trend, breaking xu1 starts a long trend.

4. Plot cloud band using xu and xu3. 

5. Option to trade in reverse direction.

6. Enter on cloud breakouts, exit on returning inside cloud.

## Advantage Analysis

The advantages of this strategy are:

1. Based purely on price action, unaffected by indicators.

2. Clear and intuitive three line pattern. 

3. Flexibility to trade reversals.

4. Easy to combine with trends and other indicators.

5. Easy backtesting and visualization for refinement.

## Risk Analysis

The main risks of this strategy are:

1. Price patterns prone to false breakouts from events.

2. No stop loss exposes to large losses.

3. Ignores trading costs. 

4. Fixed parameters may not suit different products.

5. Doesn't account for consecutive breakouts.

6. Reversal trading risky against major trends. 

## Optimization Directions 

The strategy can be improved by:

1. Adding stop loss and optimizing stops.

2. Accounting for trading costs.

3. Testing parameters for different products. 

4. Improving breakout logic for consecutive breaks.

5. Adding trend filter to avoid counter-trend trades.

6. Controlling position sizing.

7. Expanding backtest period for robustness.

## Summary

The three line breakout strategy provides intuitive signals based on price patterns. It can be strengthened by adding trends, indicators, stops, optimized logic and parameters, and position sizing. This can transform it into a robust short-term trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-22 00:00:00
end: 2023-09-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 31/05/2019
// This is a modified version of the three line break price representation. 
// It is composed with 2 lines made of Close price values forming a “cloud”.
//    If the trend is bullish and the price breach the lower level of the green 
//       cloud, a new bearish trend is taking place.
//    If the current trend is bearish and the price breakout the upper band of 
//       the cloud, a new bullish trend is forming.
// This is a “price action” indicator, signals may be filtered by long term trend 
// analysis with other indicators such as Supertrend for instance.
//
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Three Line Break", overlay = true)
reverse = input(false, title="Trade reverse")
xtrend = 1
xu = close
xu1 = close
xu2 = close
xu3 = close
if xtrend[1] == 1
    if close > xu[1]
        xu3 := xu2[1]
        xu2 := xu1[1]
        xu1 := xu[1]
        xu := close
        xtrend := 1
    else 
        if close < xu3[1]
            xu3 := xu1[1]
            xu2 := xu1[1]
            xu1 := xu1[1]
            xu := close
            xtrend := -1        
        else
            xtrend := 1
else
    if close > xu3[1]
        xu3 := xu1[1]
        xu2 := xu1[1]
        xu1 := xu1[1]
        xu := close
        xtrend := 1
    else
        if close < xu[1] 
            xu3 := xu2[1]
            xu2 := xu1[1]
            xu1 := xu[1]
            xu := close
            xtrend := -1
        else
            xtrend := -1
colorm = xtrend == -1 ? red: xtrend == 1 ? green : blue 
possig = iff(reverse and xtrend == 1, -1,
          iff(reverse and xtrend == -1, 1, xtrend))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	 
if (possig == 0) 
    strategy.close_all()
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 		
p1 = plot(xu, color=colorm)
p2 = plot(xu3, color=colorm)
fill(p1, p2, color=colorm)
```

> Detail

https://www.fmz.com/strategy/427684

> Last Modified

2023-09-23 16:02:20


> Name

Long-Breakout-Range-Trading-Strategy Based on Breakout Range
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy is a strategy that generates trading signals based on price breaking out of a fixed lookback range. When the price breaks through the highest price during the lookback period, the long operation is carried out; when the price falls below the highest price, the position is closed. You can easily switch between long and short directions.
## Strategy Principle
1. Set the review period parameters, such as 4 days.
2. Calculate the highest price in the past 4 days.
3. When today’s highest price breaks through the highest price in the past 4 days, go long.
4. When the price cannot break through the highest price in the past 4 days, close the position.
5. The reverse parameter can be used to switch the long and short direction.
## Advantage Analysis
This strategy has the following advantages:
1. Breakthrough is simple and easy, and the signal is clear.
2. Fixed breakthrough range parameters to avoid complex parameter optimization and over-optimization.
3. It can easily switch between long and short directions and adapt to various market environments.
4. The fixed range of lookback filters out part of the noise, enabling continuous tracking of trends.
5. No need to calculate complex indicators, the strategy is simple and efficient.
## Risk Analysis
The main risks of this strategy are:
1. The breakthrough range is fixed and cannot adapt to market changes.
2. Stop loss was not considered and there was a huge loss that exceeded the risk tolerance.
3. Fixed parameters are susceptible to the probability of market failure.
4. Noise trading may occur too frequently, increasing transaction costs.
5. Without parameter optimization, it is difficult to achieve the best results using default parameters.
## Optimization direction
It can be optimized from the following aspects:
1. Optimize key parameters and find the best parameter combination.
2. Add dynamic breakthrough range calculation based on ATR, etc.
3. Consider adding a trailing stop or a fixed ratio stop.
4. Combine with trend indicators to avoid excessive trading that can shock the market.
5. Test parameter robustness in more trading instruments.
6. Add machine learning algorithm to realize automatic optimization of parameters.
## Summarize
The strategy overall is a very simple trading strategy based on price breakouts. By optimizing the parameter range, adding a stop loss mechanism, trend judgment, etc., it can become an easy-to-implement and practical quantitative strategy.
||


## Overview

This is a trading strategy based on generating signals when price breaks out of a fixed lookback range. When price breaks above the highest high of the lookback period, long positions are taken; when price falls below the high, positions are closed. Trade direction can be easily switched.

## Strategy Logic

1. Set lookback period parameter, e.g. 4 days. 

2. Calculate highest high of the past 4 days.

3. Go long when today's high breaks out above this 4-day highest high.

4. Close positions when price fails to break the 4-day highest high.

5. Trade direction can be switched via the reverse parameter.

## Advantage Analysis

Advantages of this strategy:

1. Breakout is simple and signals are clear.

2. Fixed breakout range avoids complex optimization and overfitting.

3. Easily switch between long/short, adaptable to various market conditions.

4. Lookback range filters noise for sustained trend tracking.

5. No complex indicators required, efficient strategy.

## Risk Analysis  

Main risks:

1. Fixed breakout range cannot adapt to market changes.

2. No stop loss exposes strategy to excessive losses beyond risk tolerance.

3. Fixed parameters vulnerable to market regime changes. 

4. Excessive noise trades may increase transaction costs.

5. Lack of parameter optimization prevents achieving optimal results.

## Optimization Directions

Improvements:

1. Optimize key parameters to find best combinations.

2. Introduce dynamic ranges based on ATR etc.

3. Consider adding trailing stop loss or fixed percentage stop loss.

4. Incorporate trend filter to avoid overtrading in ranging markets.

5. Test parameter robustness across more trading instruments. 

6. Add machine learning for automatic parameter optimization.

## Summary

Overall this is a very simple price breakout trading strategy. With enhancements like optimized parameter range, stop losses, trend filters and more, it can become an easy to implement and practical quantitative strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|4|Look Bak|
|v_input_2|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-19 00:00:00
end: 2023-09-18 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version = 2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 28/11/2016
// Breakout Range Long Strategy
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
strategy(title="Breakout Range Long Strategy Backtest", overlay = true)
look_bak = input(4, minval=1, title="Look Bak")
reverse = input(false, title="Trade reverse")
xHighest = highest(high, look_bak)
pos =	iff(high > xHighest[1], 1, 0)
if (pos == 1 and strategy.position_size == 0 and reverse == false) 
    strategy.entry("Long", strategy.long)
if (pos == 1 and strategy.position_size == 0 and reverse == true) 
    strategy.entry("Short", strategy.short)
if (pos == 0 and strategy.position_size > 0)
    strategy.close("Long")
if (pos == 0 and strategy.position_size < 0)
    strategy.close("Short")
barcolor(strategy.position_size > 0 ? green: strategy.position_size < 0 ? red: blue)   
plotshape(pos, style=shape.triangleup, location = location.belowbar, color = green)
```

> Detail

https://www.fmz.com/strategy/427282

> Last Modified

2023-09-19 17:19:55

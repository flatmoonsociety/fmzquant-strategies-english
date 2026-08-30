
> Name

Moving Average Double Line Judgment Signal Strategy Double-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/19fd05c7f21cbbfb5a7.png)
[trans]


## Overview
This strategy uses Bollinger Bands indicators and moving averages to judge signals, and the Arnoud Legoux indicator calculates the moving average, combined with Parabolic SAR to judge market entry signals. The strategy name is "Moving Average Double Line Strategy", which includes both the moving average indicator and the characteristics of double line conditional judgment.
## Principle
This strategy mainly determines the relationship between the Bollinger Bands and the moving average indicator, and determines the long and short signals through the intersection of the moving average tube band with a certain width in the Bollinger Band indicator and the moving average.
Specifically, the strategy uses a combination of the Arnoud Legoux Moving Average indicator and the Parabolic SAR indicator.
The Arnoud Legoux Moving Average indicator is an indicator that improves on the traditional moving average. Compared with the ordinary moving average, it can adjust the angle of the moving average more flexibly by introducing the Offset; at the same time, the smoothness of the moving average can be adjusted through the Sigma value.
Parabolic SAR indicator is a very common stop loss system indicator. It can give a very clear signal of price reversal to track the price trend. When the Parabolic SAR indicator is below the price, it means that the current situation is bullish; conversely, when it is above the price, it means that the current situation is bearish.
The logic of this strategy to determine the relationship between indicators is as follows:
1. Determine whether the closing price is positive during the day (the closing price is higher than the opening price)
2. Determine whether Parabolic SAR is lower than the lowest price: it is a bullish signal
3. Determine whether the closing price crosses the Arnoud Legoux moving average: it means that the price breaks through the moving average, which is also a bullish signal.
4. When the above three conditions are met at the same time, a bullish signal is generated and you go long.
The logic behind identifying a bearish signal is the opposite, as follows:
1. Determine whether the closing price is negative during the day (the closing price is lower than the opening price)
2. Determine whether Parabolic SAR is higher than the highest price: it is a bearish signal
3. Determine whether the closing price falls below the Arnoud Legoux moving average: it means that the price falls below the moving average, which is also a bearish signal.
4. When the above three conditions are met at the same time, a bearish signal is generated and short selling
## Advantages
This strategy combines the Bollinger Bands indicator and the moving average indicator, taking into account trend judgment and breakout trading. The specific advantages are as follows:
1. The moving average indicator can effectively determine the direction of price trends.
2. Parabolic SAR indicator can accurately determine price reversal points
3. The Arnoud Legoux moving average is highly flexible and can adjust its shape through parameters.
4. Combining dual indicator judgments avoids the probability of misjudgment by a single indicator.
5. By judging the yin and yang within the day, unnecessary transactions can be further avoided
## Risk
This strategy also has some risks, mainly as follows:
1. Improper parameter settings may lead to too high or too low transaction frequency
2. When judging dual indicator combinations, improper parameter matching will also affect strategy performance.
3. Moving average strategies are less adaptable to volatile market conditions
4. The strategy does not take into account fund management factors and may face the risk of excessive positions.
The corresponding solutions are as follows:
1. Parameter optimization to make indicators more consistent
2. Optimize fund management strategies and control single positions
3. Combine with more indicator filters to reduce the probability of mistaken transactions
## Optimization direction
There are many directions in which this strategy can be optimized, mainly as follows:
1. Introduce machine learning models during the development process to achieve automatic optimization of parameters
2. Use advanced fund management strategies, such as fixed rate orders, fund withdrawal control, etc.
3. Introduce more auxiliary indicators, build a composite trading system, and improve system stability
4. Optimize the retracement control strategy and introduce stop-loss methods to avoid loss expansion
5. Build an algo trading system to connect faster market data and order channels
## Summarize
This strategy uses the dual indicator judgment of Bollinger Bands and Moving Average as a whole, and has a lot of room for optimization in terms of parameter optimization and strategy combination. By introducing more quantitative methods, this strategy can be further optimized to become an algorithmic trading strategy with stable returns.
||


## Overview

This strategy adopts the Bollinger Bands indicator and moving average to determine trading signals. The Arnoud Legoux indicator is used to calculate the moving average, combined with the Parabolic SAR indicator to judge the entry signals. The strategy name is "Double Moving Average Crossover Strategy", containing both the moving average indicator and the double line condition judgment characteristics.  

## Principles  

The core logic of this strategy is to judge the relationship between the Bollinger Bands and the moving average indicator. It uses the Bollinger Bands with a certain width of moving average bands to determine the long and short signals when the moving average line crossovers.

Specifically, the strategy combines the Arnoud Legoux moving average indicator and the Parabolic SAR indicator.  

The Arnoud Legoux moving average indicator is an improved version based on the traditional moving average. Compared with the ordinary moving average, it introduces the Offset displacement to adjust the angle of the moving average line more flexibly. At the same time, the Sigma value is used to adjust the smoothness of the moving average line.

The Parabolic SAR indicator is a very common stop-loss indicator. It can give very clear reversal signals to track the price trend. When the Parabolic SAR indicator is below the price, it represents a bullish state. On the contrary, above the price is a bearish state.

The logic for judging the indicator relationship is as follows:

1. Judge whether the close is greater than the open within the day
2. Judge if the Parabolic SAR is lower than the lowest price: a bullish signal 
3. Judge if the close breaks through the Arnoud Legoux moving average line: it also represents a bullish signal
4. When all the above 3 conditions are met at the same time, a buy signal is generated for long position

The logic for judging the short signal is the opposite:  

1. Judge whether the close is lower than the open within the day
2. Judge if the Parabolic SAR is higher than the highest price: a bearish signal
3. Judge if the close breaks the Arnoud Legoux moving average line: it also represents a bearish signal
4. When all the above 3 conditions are met at the same time, a sell signal is generated for short position  

## Advantages  

This strategy combines the Bollinger Bands indicator and the moving average indicator to take into account both trend judgment and breakout trading. The main advantages are:

1. The moving average indicator can effectively determine the price trend  
2. The Parabolic SAR indicator can accurately determine price reversal points
3. The Arnoud Legoux moving average has high flexibility and its shape can be adjusted through parameters  
4. The combination of double indicator judgment avoids the probability of misjudgment of a single indicator  
5. Intraday Yin and Yang further avoid unnecessary trading  

## Risks   

There are also some risks in this strategy:   

1. Inappropriate parameter settings may lead to too high or too low trading frequency  
2. Mismatching parameters when combining double indicators can also affect strategy performance   
3. Moving average strategies are less adaptable to volatile markets   
4. The strategy does not consider capital management factors and may face overleverage risks  

The corresponding solutions are:

1. Parameter optimization to make a better match between indicators  
2. Optimize capital management strategies to control single position size   
3. Introduce more indicator filters to reduce mis-trading possibilities  

## Optimization Directions   

There are many directions for optimizing this strategy:

1. Introduce machine learning models in development for automatic parameter optimization 
2. Implement advanced capital management strategies like fixed ratio ordering and drawdown control  
3. Incorporate more auxiliary indicators to build a composite trading system to improve system stability  
4. Optimize the drawdown control strategy by introducing stop loss methods to avoid expanding losses  
5. Building algo trading systems, connecting faster market data and order execution channels  

## Summary   

This strategy uses the double judgment of Bollinger Bands and moving average indicators. There is a large space for optimization in terms of parameter tuning and strategy combination. By introducing more quantitative methods, the strategy can be further optimized into a stable profit-generating algorithmic trading strategy.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|Window Size|
|v_input_2|0.85|Offset|
|v_input_3|6|Sigma|
|v_input_4|0.02|Start|
|v_input_5|0.02|Increase|
|v_input_6|0.2|Max|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-26 00:00:00
end: 2023-12-26 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//Author: HighProfit

//Lead-In
strategy("Parabolic SAR & Arnoud Legoux Moving Avarage Strategy", shorttitle="ST-PSAR+ALMA", overlay=true)

//Arnoud Legoux Moving Avarage Inputs
source = close
windowsize = input(title="Window Size",defval=50)
offset = input(title="Offset", type=float, defval=0.85)
sigma = input(title="Sigma", type=float, defval=6)

//Parabolic SAR Inputs
start = input(title="Start", type=float, defval=0.02)
increase = input(title="Increase", type=float, defval=0.02)
max = input(title="Max", type=float, defval=.2)

//Conditions
longCondition = close>open and sar(start, increase, max) < low and crossover(close, alma(source, windowsize, offset, sigma))
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = close<open and sar(start, increase, max) > high and crossunder(close, alma(source, windowsize, offset, sigma))
if (shortCondition)
    strategy.entry("Short", strategy.short)

//Plots   
plot(alma(source, windowsize, offset, sigma), linewidth=2, title="ALMA")
plot(sar(start, increase, max), style=circles, linewidth=2, title="PSAR")
```

> Detail

https://www.fmz.com/strategy/436797

> Last Modified

2023-12-27 17:45:43


> Name

N-Bar-Close-Below-Open-Short-Strategy for N consecutive K lines to close negative
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b35c7aa861b2b1802f.png)
[trans]


## Overview
This strategy is based on technical indicators to determine the market trend. When there are N consecutive negative K lines, shorting is a short-term trading strategy.
## Strategy Principle
This strategy uses the nCounter variable to count the number of consecutive negative draws. When the close price is lower than the open price, increase the nCounter value; when the close price is higher than the open price, reset nCounter to 0. When nCounter reaches the input parameter nLength, it indicates that N consecutive K lines have closed negative, and the output signal C2=1.
When a signal appears, if there is no current position, open a short position; if you already hold a short order, continue to hold it. After opening a position, use posprice to record the opening price. Based on the opening price, set the take-profit and stop-loss conditions: if the price reaches the take-profit point (opening price + input parameter takeprofit), close the position and reset; if the price reaches the stop-loss point (opening price - input parameter stoploss), close the position and reset.
## Advantage Analysis
The main advantages of this strategy are:
1. The rules are simple and clear, easy to understand and implement.
2. Parameters can be customized to flexibly respond to different market conditions.
3. Adopting a stop-profit and stop-loss mechanism can effectively control risks.
## Risk Analysis
The main risks of this strategy are:
1. If N consecutive K lines close negative, the trend reversal cannot be completely determined, and a false break may occur. The N value can be appropriately adjusted or verified in combination with other indicators.
2. Improper setting of stop-profit and stop-loss may result in premature exit or expansion of losses. Reasonable parameters should be set based on the degree of market volatility.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add trend filtering to avoid misjudgment of short-term adjustments in unclear markets. For example, combining indicators such as moving averages to determine the overall trend.
2. Increased volume can be verified. For example, increased trading volume can better confirm trend turning.
3. Optimize the stop-profit and stop-loss strategy, such as using free stop-loss, proportional stop-loss, etc. to make the stop-loss more intelligent.
4. Use machine learning methods to optimize parameters so that the nLength value can be adjusted according to real-time market changes.
## Summarize
This strategy determines the short-term trend based on the relationship between the closing price and the opening price, and generates a trading signal when N consecutive negative K lines are detected. The strategy is simple and intuitive, with adjustable parameters and a stop-profit and stop-loss mechanism, which can filter out some noise transactions. However, there is also a certain risk of false signals, and it is recommended to optimize it in combination with other filtering indicators. Through parameter adjustment, risk management and model optimization, this strategy can become a very practical short-term selection tool.
||


## Overview

This strategy identifies short-term trend based on technical indictors and takes short position when detecting N consecutive bar closing below opening price. It is an intraday trading strategy.

## Strategy Logic

The strategy uses a nCounter variable to count the number of consecutive bar with close below open. When close price is lower than open price, nCounter increments by 1. When close price is higher than open price, nCounter resets to 0. When nCounter reaches the input parameter nLength, it indicates N consecutive bars closing below opening price and the signal C2 becomes 1.

Upon signal, if there is no position, a short order will be sent. If already in short position, keep holding the position. After opening position, posprice records the entry price. Take profit and stop loss are set based on entry price: if price reaches take profit point (entry + input takeprofit), close position and reset; if price reaches stop loss point (entry - input stoploss), close position and reset.

## Advantage Analysis

The main advantages of this strategy:

1. Simple and clear logic, easy to understand and implement.  
2. Customizable parameters, flexible across different market conditions.
3. Equipped with take profit and stop loss, effectively control risks.

## Risk Analysis

The main risks of this strategy:

1. N bar close below open cannot fully confirm trend reversal, false signal may occur. Fine tune N value or add other filters for verification.
2. Improper stop loss or take profit setting may lead to premature exit or amplified losses. Reasonable parameters should be set according to market volatility.

## Optimization Directions

The strategy can be improved from the following aspects:

1. Add trend filter to avoid misjudging short-term corrections in sideways market. For example, combine with moving average to determine overall trend.

2. Add volume confirmation. Surging volume can better confirm trend reversal.  

3. Optimize take profit and stop loss, such as using trailing stop loss, percentage stop loss to make more intelligent exits.

4. Utilize machine learning models to dynamically adjust parameters like nLength according to real-time market changes.

## Conclusion

This strategy identifies short-term trend simply based on the relationship between close price and open price. Trading signals are generated when detecting N consecutive bars closing below opening price. The strategy is intuitive, customizable and equipped with effective risk management. However, certain level of false signals exist. It is recommended to combine additional filters for optimization. With parameter tuning, risk management and model enhancement, this can be a very practical tool for short-term trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|4|nLength|
|v_input_2|20|Take Profit pip|
|v_input_3|10|Stop Loss pip|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-18 00:00:00
end: 2023-12-25 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 05/02/2020
// Evaluates for n number of consecutive lower closes. Returns a value 
// of 1 when the condition is true or 0 when false.
//
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="N Bars Down", shorttitle="NBD Backtest", overlay = false) 
nLength = input(4, minval=1)
input_takeprofit = input(20, title="Take Profit pip", step=0.01)
input_stoploss = input(10, title="Stop Loss pip", step=0.01)
nCounter = 0
nCounter := iff(close[1] <= open[1], nz(nCounter[1],0)+1,
             iff(close[1] > open[1], 0, nCounter))
C2 = iff(nCounter >= nLength, 1, 0)
posprice = 0.0
pos = 0
barcolor(nz(pos[1], 0) == -1 ? color.red: nz(pos[1], 0) == 1 ? color.green : color.blue ) 
posprice := iff(C2== 1, close, nz(posprice[1], 0)) 
pos := iff(posprice > 0, -1, 0)
if (pos == 0) 
    strategy.close_all()
if (pos == -1)
    strategy.entry("Short", strategy.short)
posprice := iff(low <= posprice - input_takeprofit and posprice > 0, 0 ,  nz(posprice, 0))
posprice := iff(high >= posprice + input_stoploss and posprice > 0, 0 ,  nz(posprice, 0))
plot(C2, title='NBD', color=color.red)
```

> Detail

https://www.fmz.com/strategy/436599

> Last Modified

2023-12-26 10:29:12

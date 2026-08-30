
> Name

ATR trailing stop loss strategy based on UT-Bot indicatorUT-Bot-Indicator-Based-ATR-Trailing-Stop-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/c2db27ef5a6693ac6087fc013edbeb5431e16185f11998695e2a8f65c923a311.png)
[trans]
## Overview
This strategy is based on the UT Bot indicator developed by QuantNomad and combines the idea of ​​trailing stop loss. The original code was written by @Yo_adriiiiaan and modified by @HPotter. This strategy will work with LuxAlgo’s Smart Money Concepts. The strategy is currently in the testing phase.
## Strategy Principle
The main principles of this strategy are as follows:
1. When the closing price is higher than the 50-period simple moving average, enter a long trade.
2. For long positions, set a trailing stop price. The trailing stop price is 80% (1-20%) of the current closing price. The trailing stop price will move up as the price rises, but will not move down, thereby protecting profits.
3. For short positions, also set the trailing stop price. The trailing stop price is 120% (1+20%) of the current closing price. The trailing stop price will move downward as the price falls, but will not move upward.
4. Use ATR (Average True Range, average true range) as a reference for moving stop loss. The calculation method of ATR moving stop price is: when moving upward, take the larger value of the previous ATR moving stop price and (current closing price - ATR*Key Value); when moving downward, take the smaller value of the previous ATR moving stop price and (current closing price + ATR*Key Value). The Key Value is a parameter set by the user, which is used to adjust the sensitivity of the trailing stop loss.
5. Determine the current position direction based on the breakthrough of the ATR moving stop price. When the price breaks through the ATR moving stop price upward, hold a long position; when the price breaks through the ATR moving stop price downward, hold a short position; in other cases, keep the current position unchanged.
## Advantage Analysis
1. The setting of trailing stop loss can protect profits well, allowing the strategy to gain more profits in trending markets.
2. Set stop losses for long and short positions respectively to adapt to different market conditions.
3. Using ATR as a reference for stop loss can dynamically adjust the stop loss position, making it more flexible and effective.
4. Key Value parameters are provided for users to optimize, which can be adjusted according to different varieties and cycles to improve adaptability.
## Risk Analysis
1. In volatile market conditions, frequent stop losses may lead to excessive transactions, increase handling fee costs, and reduce returns.
2. The fixed percentage trailing stop method is relatively simple and may not be able to cope with price fluctuations well in some markets.
3. The strategy only considers the trailing stop loss but does not set a trailing stop profit, which may result in missing some profit opportunities.
4. The selection of parameters has a great impact on the performance of the strategy. Improper parameters may bring greater retracement risks.
## Optimization direction
1. You can consider combining other indicators or conditions, such as trading volume, volatility, etc., to optimize entry conditions and improve signal reliability.
2. For the calculation method of trailing stop loss, you can explore more complex and effective methods, such as using parabolic stop loss, dynamic percentage stop loss, etc.
3. You can add a moving take-profit mechanism, such as setting a dynamic take-profit level based on ATR or percentage, to better lock in profits.
4. For different varieties and cycles, parameter optimization can be performed to find the most suitable parameter combination. Parameters can also be dynamically adjusted according to changes in market conditions.
## Summarize
This strategy adds the logic of trailing stop loss on the basis of the UT Bot indicator, which can play a role in protecting profits in trending markets. At the same time, the strategy sets stop losses for long and short positions respectively, which is highly adaptable. Using ATR as a reference for moving stop loss can dynamically adjust the stop loss position and improve flexibility. However, this strategy may face the risk of high transaction costs caused by frequent stop losses in volatile market conditions, and lacks a moving stop profit setting, which may result in missed profits. In addition, the choice of parameters has a greater impact on strategy performance.
In the future, the strategy can be improved by optimizing entry conditions, exploring more complex trailing stop loss methods, adding a trailing stop profit mechanism, and optimizing parameters for different varieties and cycles, in order to obtain more stable returns. In general, the strategy is simple and clear, easy to understand and implement, but there is room for further optimization and is worthy of continued exploration and improvement.
|| 

## Overview

This strategy is based on the UT Bot indicator developed by QuantNomad and incorporates the idea of a trailing stop loss. The original code was written by @Yo_adriiiiaan and modified by @HPotter. The strategy will be used in conjunction with LuxAlgo's Smart Money Concepts. Currently, the strategy is in the testing phase.

## Strategy Principle

The main principles of this strategy are as follows:

1. When the closing price is higher than the 50-period simple moving average, a long trade is entered.
2. For long positions, a trailing stop loss price is set. The trailing stop loss price is 80% (1-20%) of the current closing price. The trailing stop loss price moves up with rising prices but does not move down, thus protecting profits.
3. For short positions, a trailing stop loss price is also set. The trailing stop loss price is 120% (1+20%) of the current closing price. The trailing stop loss price moves down with falling prices but does not move up.
4. ATR (Average True Range) is used as a reference for the trailing stop. The calculation method for the ATR trailing stop price is: when moving up, take the larger of the previous ATR trailing stop price and (current closing price - ATR * Key Value); when moving down, take the smaller of the previous ATR trailing stop price and (current closing price + ATR * Key Value). The Key Value is a user-set parameter used to adjust the sensitivity of the trailing stop.
5. Based on the breakthrough of the ATR trailing stop price, the current position direction is determined. When the price breaks above the ATR trailing stop price, a long position is held; when the price breaks below the ATR trailing stop price, a short position is held; in other cases, the current position status remains unchanged.

## Advantage Analysis

1. The setting of the trailing stop can effectively protect profits, allowing the strategy to obtain more gains in trend markets.
2. Setting stop losses separately for long and short positions can adapt to different market conditions.
3. Using ATR as a reference for the stop loss allows for dynamic adjustment of the stop loss position, making it more flexible and effective.
4. The Key Value parameter is provided for user optimization, which can be adjusted according to different varieties and cycles to improve adaptability.

## Risk Analysis

1. In choppy markets, frequent stop-outs may lead to excessive transactions, increasing commission costs and reducing returns.
2. The fixed percentage trailing stop method is relatively simple and may not be able to cope well with price fluctuations in some market conditions.
3. The strategy only considers trailing stops and does not set trailing profit targets, which may miss some profit opportunities.
4. The choice of parameters has a significant impact on strategy performance, and inappropriate parameters may bring greater drawdown risks.

## Optimization Direction

1. Other indicators or conditions, such as trading volume and volatility, can be considered to optimize entry conditions and improve signal reliability.
2. For the calculation method of the trailing stop, more complex and effective methods can be explored, such as using parabolic stop loss or dynamic percentage stop loss.
3. A trailing profit target mechanism can be added, for example, setting dynamic profit targets based on ATR or percentages to better lock in profits.
4. Parameter optimization can be performed for different varieties and cycles to find the most suitable parameter combinations. Parameters can also be dynamically adjusted according to changes in market conditions.

## Summary

Based on the UT Bot indicator, this strategy incorporates trailing stop logic, which can protect profits in trend markets. At the same time, the strategy sets stop losses separately for long and short positions, making it highly adaptable. Using ATR as a reference for the trailing stop allows for dynamic adjustment of the stop loss position, improving flexibility. However, this strategy may face the risk of high transaction costs due to frequent stop-outs in choppy markets, and it lacks a trailing profit target setting, which may miss profit opportunities. In addition, the choice of parameters has a significant impact on strategy performance.

In the future, the strategy can be improved by optimizing entry conditions, exploring more complex trailing stop methods, adding a trailing profit target mechanism, and optimizing parameters for different varieties and cycles, in order to obtain more stable returns. Overall, the strategy idea is simple and straightforward, easy to understand and implement, but there is room for further optimization and it is worth continuing to explore and improve.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|Key Value. 'This changes the sensitivity'|
|v_input_2|10|ATR Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-03-05 00:00:00
end: 2024-03-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Trailingstop", overlay=true)

if close > sma(close, 50)
    strategy.entry("long", strategy.long)

// Trailing stop loss for long positions
Trailperc = 0.20
price_stop_long = 0.0

if (strategy.position_size > 0)
    stopValue = close * (1 - Trailperc)
    price_stop_long := max(stopValue, price_stop_long[1])
else
    price_stop_long := 0

if (strategy.position_size > 0)
    strategy.exit(id="stoploss_long", stop=price_stop_long)

// Trailing stop loss for short positions
Trailperc_short = 0.20
price_stop_short = 0.0

if (strategy.position_size < 0)
    stopValue_short = close * (1 + Trailperc_short)
    price_stop_short := min(stopValue_short, price_stop_short[1])
else
    price_stop_short := 0

if (strategy.position_size < 0)
    strategy.exit(id="stoploss_short", stop=price_stop_short)

// ATR Trailing Stop for visualization
keyvalue = input(3, title="Key Value. 'This changes the sensitivity'", step=0.5)
atrperiod = input(10, title="ATR Period")
xATR = atr(atrperiod)
nLoss = keyvalue * xATR

xATRTrailingStop = 0.0
xATRTrailingStop := iff(close > nz(xATRTrailingStop[1], 0) and close[1] > nz(xATRTrailingStop[1], 0), max(nz(xATRTrailingStop[1]), close - nLoss),
   iff(close < nz(xATRTrailingStop[1], 0) and close[1] < nz(xATRTrailingStop[1], 0), min(nz(xATRTrailingStop[1]), close + nLoss),
   iff(close > nz(xATRTrailingStop[1], 0), close - nLoss, close + nLoss)))

pos = 0  
pos :=   iff(close[1] < nz(xATRTrailingStop[1], 0) and close > nz(xATRTrailingStop[1], 0), 1,
   iff(close[1] > nz(xATRTrailingStop[1], 0) and close < nz(xATRTrailingStop[1], 0), -1, nz(pos[1], 0)))

xcolor = pos == -1 ? color.red: pos == 1 ? color.green : color.blue

plot(xATRTrailingStop, color = xcolor, title = "Trailing Stop")
```

> Detail

https://www.fmz.com/strategy/444344

> Last Modified

2024-03-11 11:17:33

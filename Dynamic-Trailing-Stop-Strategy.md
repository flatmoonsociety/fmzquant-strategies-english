
> Name

Based on dynamic trailing stop loss strategyDynamic-Trailing-Stop-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1afc532d51fa268bbc2.png)
[trans]
## Overview
This strategy aims to use the trailing stop loss function of the Viemstra platform to dynamically adjust the stop loss price to achieve a more accurate and flexible stop loss. The strategy is not used for entry and exit, but gives a reasonable stop loss range under different market conditions. It is recommended that you optimize different parameters through backtesting. This strategy can also be integrated into existing entry and exit strategies as a stop loss.
## Strategy Principle
This strategy mainly uses 3 indicators: highest price, lowest price and closing price. The strategy first defines the stop loss range of long positions and short positions, that is, the long trailing stop loss distance `longoffset` and the short trailing stop loss distance `shortoffset`. The long position distance defaults to 228.5 points, and the short position distance defaults to 243.5 points.
The strategy then uses the following logic to adjust the trailing stop price `trailstop`:
- The lowest price of the latest K line is lower than the trailing stop price of the previous K line, and the lowest price of the previous K line is higher than the trailing stop price of the previous two K lines, then the trailing stop price of the current K line = closing price + short trailing stop distance
- The highest price of the latest K line is higher than the trailing stop price of the previous K line, and the highest price of the previous K line is lower than the trailing stop price of the previous two K lines, then the trailing stop price of the current K line = closing price - long trailing stop distance
- The highest price of the most recent K line is higher than the trailing stop price of the previous K line, then the trailing stop price of the current K line = the maximum value (the trailing stop price of the previous K line, the highest price of the most recent K line - long position trailing stop distance)
- The lowest price of the most recent K line is lower than the trailing stop price of the previous K line, then the trailing stop price of the current K line = minimum value (the trailing stop price of the previous K line, the lowest price of the most recent K line + short position trailing stop distance)
- Otherwise, the trailing stop price of the current K line = the closing price
In this way, the tracking stop price can be adjusted in real time according to changes in the highest and lowest prices in the market to achieve dynamic stop loss.
## Advantage Analysis
The biggest advantage of this strategy is that it achieves a truly dynamic and flexible trailing stop. Compared with a fixed stop-loss price, dynamic tracking can adjust the stop-loss range according to market fluctuations, avoiding unnecessary losses caused by too large a stop-loss distance, and avoiding being hit by ordinary price fluctuations if the stop-loss distance is too small. This not only reduces unnecessary losses, but also reduces the probability of premature stop loss.
Another advantage is that the stop loss distance can be customized and optimized. Users can choose the stop loss range that suits them based on the characteristics and trading styles of different varieties. This allows the strategy to be applied to a wider range of scenarios.
Finally, the stop loss logic of this strategy is simple, clear and easy to understand, and it is also easy to develop and integrate into other strategies, which is one of its advantages.
## Risk Analysis
The main risks of this strategy are as follows:
1. Dynamic stop loss can only reduce losses under normal market conditions, but cannot withstand losses caused by major emergencies or extreme market conditions. This is a limitation of dynamic stop loss itself.
2. If the trailing stop loss distance is set too large, it may cause losses to expand. If the distance is too small, the loss may be stopped prematurely. The setting of distance needs to be carefully tested and optimized based on breed characteristics.
3. In the first few K lines after opening a position, due to the trailing stop loss mechanism, the stop loss distance may be too large, and there will be certain additional risks during this period.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimization of parameters for different varieties: Select reasonable long and short tracking stop loss distances based on indicators such as the degree of volatility and intraday fluctuation range of different varieties. This is the most critical optimization direction.
2. Reduce additional risks on several K lines after opening a position: You can limit the adjustment range of the trailing stop loss distance on several K lines after opening a position to avoid excessive stop loss distance.
3. Combined with trading volume indicators: For example, during the stage of amplified trading volume, reduce the stop loss distance to avoid arbitrage stop loss.
4. Combine with other entry and exit strategies: The main function of this strategy is to track stop loss, which can be integrated into other strategies and used in conjunction with entry and exit rules.
## Summarize
This strategy implements a dynamic tracking stop function based on changes in the highest and lowest market prices. This can effectively reduce unnecessary losses under normal market conditions, and also better solve the problem of too large or too small fixed stop loss distance. The key optimization direction is to test the appropriate parameters of different varieties and the risk control of several K lines after opening a position. The stop loss logic of this strategy is simple and clear, easy to understand and develop, and can be integrated into other strategies or used alone as a stop loss tool.
||

## Overview

This strategy aims to utilize Bitmex's trailing stop function to dynamically adjust the stop loss price for more accurate and flexible stops. The strategy is not used for entries or exits, but rather gives reasonable stop loss ranges under different market conditions. It is suggested to backtest with different values. The strategy can also be integrated into existing strategies that give entries/exits to act as a stop loss.

## Strategy Logic  

The strategy mainly uses 3 indicators: highest price, lowest price and close price. The strategy first defines the stop loss ranges for long and short positions, namely the `longoffset` for long trailing stop distance and `shortoffset` for short trailing stop distance. The default long distance is 228.5 points and the short distance is 243.5 points.  

Then the strategy uses the following logic to adjust the trailing stop price `trailstop`:  

- If the lowest price of the latest candle is lower than the trailing stop price of the previous candle, and the lowest price of the candle before that is higher than the trailing stop price of the previous 2 candles, then the current candle's trailing stop price = close price + short trailing stop distance

- If the highest price of the latest candle is higher than the trailing stop price of the previous candle, and the highest price of the candle before that is lower than the trailing stop price of the previous 2 candles, then the current candle's trailing stop price = close price - long trailing stop distance  

- If the highest price of the latest candle is higher than the trailing stop price of the previous candle, then the current candle's trailing stop price = max(previous candle's trailing stop price, latest candle's highest price - long trailing stop distance)

- If the lowest price of the latest candle is lower than the trailing stop price of the previous candle, then the current candle's trailing stop price = min(previous candle's trailing stop price, latest candle's lowest price + short trailing stop distance)  

- Otherwise the current candle's trailing stop price = close price

This dynamically adjusts the trailing stop price based on changes in the highest and lowest market prices to achieve dynamic stops.  

## Advantage Analysis

The biggest advantage of this strategy is the implementation of truly dynamic and flexible trailing stops. Compared to fixed stop loss prices, dynamic trailing can adjust the stop loss range based on market fluctuations, avoiding unnecessary losses due to too large stop distances, while also avoiding being stopped out by normal price fluctuations when the distance is too small. This reduces unnecessary losses while also reducing the probability of premature stops.  

Another advantage is that the stop loss distance is customizable and optimizable. Users can choose stop loss ranges suitable for themselves according to the characteristics of different products and trading styles. This allows the strategy to be applied to a wider range of scenarios.   

Finally, the stop loss logic of this strategy is simple and clear, easy to understand, and easy to further develop and integrate into other strategies. This is also one of its advantages.

## Risk Analysis

The main risks of this strategy are:  

1. Dynamic stops can only reduce losses under normal market conditions, but cannot withstand major events or extreme market conditions. This is an inherent limitation.   

2. If the trailing stop distance is set too large, it may lead to greater losses. If set too small, it may stop out prematurely. The setting needs careful testing and optimization based on product characteristics.

3. In the first few candles after opening a position, due to the mechanism of trailing stops, the stop distance may be too large, posing some additional risk during this period.

## Optimization Directions

This strategy can be optimized in the following aspects:  

1. Parameter optimization for different products: Choose reasonable long and short trailing stop distances based on volatility, intraday range and other metrics for different products. This is the most critical direction.  

2. Reduce extra risk in early candles after opening positions: Limit the adjustment range of trailing stop distances in the first few candles to avoid too large distances.

3. Incorporate trading volume indicators: For example, reduce stop distance during surges in volume to avoid being stopped out by arbitrage.   

4. Combine with other entry/exit strategies: The main function of this strategy is trailing stop loss. It can be integrated with other strategies with entry and exit rules.  

## Conclusion

This strategy implements dynamic trailing stop loss based on changes in highest and lowest market prices. It can effectively reduce unnecessary losses under normal market conditions, and solves the problem of fixed distances being too large or small. The key optimization directions are testing suitable parameters across different products, and controlling risks in the early candles after opening positions. The stop loss logic is simple and clear, easy to understand and integrate into other strategies or use standalone as a stop loss tool.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|228.5|Long Trailing Stop Size|
|v_input_2|243.5|Short Trailing Stop Size |


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-20 00:00:00
end: 2024-02-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//By River
strategy("BitMex Trailing Stop Strategy", overlay=true)
longoffset = input(defval=228.5, title="Long Trailing Stop Size", type=float, minval=0.5, maxval=1000, step=0.5)
shortoffset = input(defval=243.5, title="Short Trailing Stop Size ", type=float, minval=0.5, maxval=1000, step=0.5)

hiprice = request.security(syminfo.tickerid, "1", high)
loprice = request.security(syminfo.tickerid, "1", low)
price = request.security(syminfo.tickerid, "1", close)

trailstop = price
trailstop := (loprice <= trailstop[1] and loprice[1] >= trailstop[2]) ? price + shortoffset : ((hiprice >= trailstop[1] and hiprice[1] <= trailstop[2]) ? price - longoffset : (hiprice > trailstop[1] ? max(hiprice - longoffset, trailstop[1]) : (loprice < trailstop[1] ? min(loprice + shortoffset, trailstop[1]) : price)))

trailcol = trailstop > price ? red : green
plot(trailstop, color=trailcol)

longCondition =  trailcol == green
alertcondition(longCondition, "Long Stop alert", "BUY")
if (longCondition)
    strategy.entry("Long", strategy.long)
shortCondition = trailcol == red
alertcondition(shortCondition, "Short alert", "SELL")
if (shortCondition)
    strategy.entry("Short", strategy.short)


```

> Detail

https://www.fmz.com/strategy/442937

> Last Modified

2024-02-27 15:02:34

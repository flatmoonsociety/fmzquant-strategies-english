
> Name

Candlestick-Body-Based-Dual-Thrust-Strategy based on K-line entity
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/5a2f9300a6cac14703.png)
[trans]


## Overview
This strategy determines the long and short direction based on the physical length of the K line. It calculates the average physical length of the last 30 K lines. When the physical length of the positive line is greater than the average physical length, it goes long. When the physical length of the negative line is greater than the average physical length, it goes short.
## Strategy Principle
This strategy first calculates the entity length body of the K line and the average sbody of the entity length of the recent 30 K lines.
When today's K line is a negative line (bar==-1) and the real body length is greater than the average real body length, open a long order (up1).
When today's K line is a positive line (bar==1) and the real body length is greater than the average real body length, open a short order (dn1).
After the long order is opened, if today's K line is positive (bar==1) and the current position is profitable, the long order will be closed.
After the short order is opened, if today's K line is negative (bar==-1) and the current position is profitable, the short order will be closed.
This strategy simply and effectively uses the length of the K-line entity to determine the market trend. The longer the entity, the stronger the trend. Therefore, the length of the entity is used as the basis for judging long and short.
## Advantage Analysis
This strategy has the following advantages:
1. The strategic ideas are simple and clear, easy to understand and implement.
2. Use the length of the K-line entity to determine the trend and avoid being disturbed by noise.
3. Using dynamic average calculation, it can adapt to market changes.
4. Set profit closing conditions to increase strategy profitability.
5. Configurable strategy parameters, suitable for different market environments.
## Risk Analysis
There are also some risks with this strategy:
1. A longer entity does not necessarily mean a strong trend, it may be a normal fluctuation.
2. Improper setting of the time window of the average entity length may lead to missed trading opportunities.
3. Unexpected events may lead to strategic losses.
4. Holding long and short positions for too long may lead to expanded losses.
Solutions corresponding to risks:
1. Combine with other indicators to determine trends and avoid wrong trades.
2. Test different parameter values ​​and optimize the calculation of the average entity length.
3. Set stop-loss and stop-profit conditions to control single losses.
4. Optimize the logic of opening and closing positions to avoid holding positions for too long.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Combine MACD, RSI and other indicators to determine the trend and avoid false signals caused by regular fluctuations.
2. Test different average entity length time window parameters and find the optimal parameter combination.
3. Add the opening volume control logic to gradually reduce the opening volume as the number of losses increases.
4. Set trailing stop loss or profit margin stop loss exit conditions to control the single loss ratio.
5. Optimize the conditions for opening and closing positions to avoid invalid transactions. For example, if 3 consecutive K-line entities are longer, then open a position.
6. Avoid transactions during specific time periods or before and after the release of important data to control losses caused by exchange rate shocks.
## Summarize
The overall idea of ​​this strategy is clear and easy to understand, and the entry timing is judged by comparing the K-line entity with its average length. There is a large space for strategy optimization, and optimization and adjustment can be made from many aspects to make the strategy parameters more consistent with different market environments. Overall, this strategy is simple and reliable as an introductory strategy for quantitative trading, and is suitable for novice traders to use and learn. By continuously optimizing and combining more indicators, the rate of return and stability of the strategy can be further improved.
||


## Overview

This strategy uses the length of the candlestick body to determine the long and short direction. It calculates the average body length of the recent 30 candlesticks. When the bullish candle body length is greater than average, it goes long. When the bearish candle body length is greater than average, it goes short.

## Strategy Logic

This strategy first calculates the candlestick body length body and the average body length of recent 30 candlesticks sbody. 

When today's candlestick is bearish (bar==-1) and the body length is greater than average body length, it opens long position (up1).

When today's candlestick is bullish (bar==1) and the body length is greater than average body length, it opens short position (dn1).

After opening long, if today's candlestick is bullish (bar==1) and the current position is profitable, it closes long position. 

After opening short, if today's candlestick is bearish (bar==-1) and the current position is profitable, it closes short position.

The strategy simply and effectively uses the candlestick body length to determine the market trend. The longer the body, the stronger the trend. So it uses body length as the criterion for long and short.

## Advantage Analysis

The advantages of this strategy:

1. The logic is simple and clear, easy to understand and implement.

2. Using candlestick body length to determine trend, avoid noise interference. 

3. Adopt dynamic average calculation, can adapt to market changes.

4. Set profitable exit condition to improve profitability.

5. Configurable parameters, adaptable to different market environments.

## Risk Analysis

The risks of this strategy:

1. Long body does not necessarily represent strong trend, could be normal fluctuation.

2. Improper average body length time window may miss trading opportunities.

3. Black swan events may cause losses. 

4. Holding positions for too long may amplify losses.

Solutions:

1. Combine with other indicators to determine trend, avoid wrong trades.

2. Test different parameter values, optimize average body length calculation.

3. Set stop loss to control single loss.

4. Optimize entry and exit logic to avoid holding too long.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Combine MACD, RSI to determine trend, avoid wrong signals from normal fluctuations.

2. Test different average body length time window parameters to find optimal parameter set.

3. Add position sizing control logic, gradually reduce position size when incurring losses.

4. Set trailing stop loss or profit target to control single loss percentage.

5. Optimize entry and exit conditions to avoid ineffective trades. For example, wait for 3 consecutive long candlesticks before entering.

6. Avoid trading at certain periods or around important data release to control loss from volatility.

## Conclusion

The strategy has clear and easy-to-understand logic of comparing candlestick body to its average length for entry timing. Large room for optimization from multiple dimensions to tailor it better for different market environments. Overall a simple and reliable introductory quant trading strategy suitable for novice traders to use and learn. Further combine more indicators and optimize to improve profitability and robustness.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|true|Use body|
|v_input_4|1900|From Year|
|v_input_5|2100|To Year|
|v_input_6|true|From Month|
|v_input_7|12|To Month|
|v_input_8|true|From day|
|v_input_9|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-16 00:00:00
end: 2023-11-15 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=3
strategy(title = "Noro's ColorBar Strategy v1.0", shorttitle = "ColorBar str v1.0", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100.0, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
usebody = input(true, defval = true, title = "Use body")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Signals
bar = close > open ? 1 : close < open ? - 1 : 0
body = abs(close - open)
sbody = ema(body, 30)

up1 = bar == -1 and (body > sbody or usebody == false)
dn1 = bar == 1 and (body > sbody or usebody == false)

plus = (close > strategy.position_avg_price and strategy.position_size > 0) or (close < strategy.position_avg_price and strategy.position_size < 0)
exit = ((strategy.position_size > 0 and bar == 1) or (strategy.position_size < 0 and bar == -1)) and plus

if up1
    strategy.entry("Long", strategy.long, needlong == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, 01, 00, 00) and time < timestamp(toyear, tomonth, 31, 00, 00)))

if dn1
    strategy.entry("Short", strategy.short, needshort == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, 01, 00, 00) and time < timestamp(toyear, tomonth, 31, 00, 00)))
    
if time > timestamp(toyear, tomonth, 31, 00, 00) or exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/432354

> Last Modified

2023-11-16 17:14:48

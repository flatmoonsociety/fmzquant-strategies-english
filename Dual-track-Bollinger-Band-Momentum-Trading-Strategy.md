
> Name

Dual-track-Bollinger-Band-Momentum-Trading-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](assets/images/a16e2252d2452969c41b790a81dd805a0d2eb987e80a023e2d70f1ce807123dd.png)
[trans]

## Overview
This strategy is based on the concept of Bollinger Bands, setting the upper and lower rails of the price channel, and using it to judge trends and generate trading signals. Specifically, the average absolute deviation of the price is calculated as the channel bandwidth. The middle rail of the channel is the simple moving average of the price. The upper rail and the lower rail are respectively plus or minus 1 times or 2 times the channel bandwidth of the middle rail. Go long when the price breaks through the upper band, and go short when it breaks through the lower band.
## Principle
This strategy mainly includes the following key points:
1. Calculate the midline of the price, which is the simple moving average of the price.
2. Calculate a simple moving average of the absolute price deviation as the channel bandwidth.
3. Determine the upper and lower rails based on the middle rail and bandwidth. The upper rail is the middle rail plus 1 or 2 times the bandwidth, and the lower rail is the middle rail minus 1 or 2 times the bandwidth.
4. Calculate long and short trend judgment indicators. When the price is higher than the upper rail 2, it is a long position, and when the price is lower than the lower rail 2, it is a short position.
5. Generate trading signals. Go long when the price crosses the upper rail 2, and go short when it crosses the lower rail 2.
6. Set a stop loss line. The stop-loss line for long orders is the lower rail 1, and the stop-loss line for short orders is the upper rail 1.
7. Calculate positions according to fund management requirements.
This strategy combines the ideas of moving averages to judge trends, Bollinger Bands to judge overbought and oversold, and reversal on breakthroughs. By judging the strength of the trend through the difference between the two tracks, and at the same time exerting the function of Bollinger Bands returning to the central axis, a relatively stable trading system is formed as a whole.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Using the dual-track system, you can better judge the strength of the trend.
2. Bollinger Bands has a strong regression function, which can effectively avoid false breakthroughs.
3. The double-track difference cooperates with the Bollinger Bands to return to the central axis, forming a more stable trading signal.
4. There is a clear stop-loss exit logic to control risks.
5. The position setting complies with the capital management requirements and avoids super leverage.
6. The strategy is clear and easy to understand and optimize.
7. Parameters can be set flexibly, suitable for optimization in different markets.

## Risk Analysis
There are also some risks with this strategy:
1. Improper setting of Bollinger Band parameters may lead to a moat effect and the inability to effectively track prices.
2. The double-track difference cannot completely avoid trend misjudgment.
3. In a volatile market, many invalid signals may be generated.
4. Loss will occur in case of false breakthrough.
5. There is a certain time lag and the cycle conversion point may be missed.
6. The profit-loss ratio is limited by the stop loss point, and the trend cannot be tracked indefinitely.
Corresponding risk management measures:
1. Optimize parameters so that Bollinger Bands can adapt to different cycles.
2. Combine other indicators for confirmation to avoid misjudgment.
3. Reduce positions and control single losses.
4. Optimize the stop loss point to ensure the profit and loss ratio.
5. Shorten the cycle appropriately and reduce lag.
6. Risk control must be steady and you cannot chase the rise and fall without limit.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize Bollinger Bands parameters so that they can better track prices. Adaptive parameters can be introduced.
2. Try different moving averages, such as EMA, DWMA, etc.
3. Add trend filtering to avoid market shock and wrong trading. You can consider MACD, etc.
4. Increase aggressive exits to obtain more trend profits. You can consider small stop loss, trailing stop loss, exit indicators, etc.
5. Introduce multiple time periods for combination, and different periods are suitable for different market conditions.
6. Add additional conditional logic, such as a sudden increase in trading volume, to avoid false breakthroughs.
7. You can consider the reverse Bollinger Bands, selling the upper track and buying the lower track.
8. Carry out parameter optimization testing to find the optimal parameter combination.
## Summarize
The overall idea of ​​this strategy is clear and has strong stability. At the same time, there is also some room for improvement. Through further improvement in parameter optimization, logic optimization, risk management, etc., it can become a very practical quantitative trading strategy. This strategy provides a good reference for the introductory strategy of quantitative trading.
||

## Overview

This strategy is based on the concept of Bollinger Bands, setting upper and lower rails for the price channel and using them for trend judgment and trade signal generation. Specifically, it calculates the average absolute deviation of the price as the channel bandwidth. The middle rail of the channel is the simple moving average of the price, and the upper and lower rails are the middle rail plus or minus 1 or 2 times the channel bandwidth. When the price breaks through the upper rail, go long. When it breaks through the lower rail, go short.

## Principle 

The main points of this strategy include:

1. Calculate the middle rail of the price, which is the simple moving average of the price.

2. Calculate the simple moving average of the absolute deviation of the price as the channel bandwidth.

3. Determine the upper and lower rails according to the middle rail and bandwidth. The upper rail is the middle rail plus 1 or 2 times the bandwidth. The lower rail is the middle rail minus 1 or 2 times the bandwidth.

4. Calculate the trend judgment indicator for long and short. When the price is above the upper rail 2, it is long. When the price is below the lower rail 2, it is short.

5. Generate trading signals. When the price crosses above the upper rail 2, go long. When it crosses below the lower rail 2, go short.

6. Set stop loss line. The stop loss line for long orders is the lower rail 1, and for short orders it is the upper rail 1. 

7. Calculate the position size according to capital management requirements.

The strategy integrates the ideas of using moving averages to judge trends, Bollinger Bands to judge overbought and oversold, and breakouts to make reversals. The difference between the double rails is used to judge the strength of the trend, while the regression function of Bollinger Bands is utilized to form a relatively stable trading system.

## Advantage Analysis

The main advantages of this strategy are:

1. The dual-rail system can better judge the strength of the trend.

2. Bollinger Bands have a strong regression function to effectively avoid false breakouts.

3. The difference between the dual rails combined with the regression of Bollinger Bands forms relatively stable trading signals.

4. There is a clear stop loss/exit logic to control risks. 

5. The position sizing follows capital management requirements, avoiding super leverage.

6. The strategy idea is clear and easy to understand and optimize. 

7. Flexible parameter settings make it adaptable for different markets.

## Risk Analysis

The strategy also has some risks:

1. Improper Bollinger Bands parameters may cause ditching effects, failing to effectively track prices.

2. The difference between dual rails cannot completely avoid erroneous trend judgments.

3. It may generate more invalid signals in range-bound markets. 

4. Losses may occur in false breakout situations.

5. There is some time lag, possibly missing cycle turning points.

6. The risk/reward ratio is limited by the stop loss point, unable to unlimitedly chase trends.

Corresponding risk management measures:

1. Optimize parameters to make Bollinger Bands adaptable to different cycles.

2. Combine other indicators for confirmation to avoid misjudgment. 

3. Reduce position size to control single loss.

4. Optimize stop loss points to ensure risk/reward ratio.

5. Appropriately shorten cycle to reduce lag.

6. Risk control should be robust, no unlimited chasing.

## Optimization Directions

The strategy can be optimized in the following directions:

1. Optimize Bollinger Bands parameters for better price tracking. Adaptive parameters can be introduced.

2. Try different moving averages like EMA, DWMA, etc.

3. Add trend filtering to avoid trading in range-bound markets. MACD can be considered.

4. Add aggressive exit methods to capture more trend profits. Trailing stop loss, exit signals etc. can be considered.

5. Introduce multiple time frames for combination, suitable for different market conditions. 

6. Add additional conditions like volume surges to avoid false breakouts.

7. Consider reverse Bollinger Bands, selling upper band, buying lower band.

8. Perform parameter optimization for best parameter combinations.

## Summary

The overall idea of this strategy is clear and stable. There is also room for improvement via parameter optimization, logic enhancement, risk management etc. to further refine it into a very practical quantitative trading strategy. The strategy provides a good reference for beginners in quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|Lot, %|
|v_input_4|20|Length|
|v_input_5_ohlc4|0|Source: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|
|v_input_6|true|Show Bands|
|v_input_7|true|Show Offset|
|v_input_8|false|Show Background|
|v_input_9|1900|From Year|
|v_input_10|2100|To Year|
|v_input_11|true|From Month|
|v_input_12|12|To Month|
|v_input_13|true|From day|
|v_input_14|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-09 00:00:00
end: 2023-11-15 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © noro

//@version=4
strategy(title = "Noro's Bands Strategy", shorttitle = "Bands", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0, commission_value = 0.1)

//Sattings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
lotsize = input(100, defval = 100, minval = 1, maxval = 10000, title = "Lot, %")
len = input(20, defval = 20, minval = 1, maxval = 1000, title = "Length")
src = input(ohlc4, title = "Source")
showbb = input(true, title = "Show Bands")
showof = input(true, title = "Show Offset")
showbg = input(false, title = "Show Background")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//PriceChannel
lasthigh = highest(src, len)
lastlow = lowest(src, len)
center = (lasthigh + lastlow) / 2

//Distance
dist = abs(src - center)
distsma = sma(dist, len)
hd = center + distsma
ld = center - distsma
hd2 = center + distsma * 2
ld2 = center - distsma * 2

//Trend
trend = 0
trend := high > hd2 ? 1 : low < ld2 ? -1 : trend[1]
bgcol = showbg == false ? na : trend == 1 ? color.lime : color.red
bgcolor(bgcol, transp = 70)

//Lines
colo = showbb == false ? na : color.black
offset = showof ? 1 : 0
plot(hd2, color = colo, linewidth = 1, transp = 0, offset = offset, title = "High band 2")
plot(hd, color = colo, linewidth = 1, transp = 0, offset = offset, title = "High band 1")
plot(center, color = colo, linewidth = 1, transp = 0, offset = offset, title = "center")
plot(ld, color = colo, linewidth = 1, transp = 0, offset = offset, title = "Low band 1")
plot(ld2, color = colo, linewidth = 1, transp = 0, offset = offset, title = "Low band 2")

//Trading
size = strategy.position_size
needstop = needlong == false or needshort == false
truetime = time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)
lot = 0.0
lot := size != size[1] ? strategy.equity / close * lotsize / 100 : lot[1]
if distsma > 0
    strategy.entry("Long", strategy.long, lot, stop = hd2, when = truetime and needlong)
    strategy.entry("Short", strategy.short, lot, stop = ld2, when = truetime and needshort)
sl = size > 0 ? ld2 : size < 0 ? hd2 : na
if size > 0 and needstop
    strategy.exit("Stop Long", "Long", stop = sl)
if size < 0 and needstop
    strategy.exit("Stop Short", "Short", stop = sl)
if time > timestamp(toyear, tomonth, today, 23, 59)
    strategy.close_all()
    strategy.cancel("Long")
    strategy.cancel("Short")
```

> Detail

https://www.fmz.com/strategy/432359

> Last Modified

2023-11-16 17:36:00

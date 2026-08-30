
> Name

Robot-White-Box-Iceberg-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is based on moving average trading. By setting three entry lines for long and short positions, it achieves two-way opening of long and short positions. It is a trend following strategy. When the price breaks through the moving average, open long and short positions in sequence, and enter the market in batches through hanging orders.
## Strategy Principle
This strategy is mainly based on the breakthrough of the moving average to determine the trend direction. Specifically, it obtains a moving average indicator by calculating the arithmetic mean of the opening price, closing price, highest price, lowest price, etc. Then set the long entry line above the moving average and the short entry line below the moving average. When the price breaks through the moving average from below, long orders are triggered in turn; when the price breaks through the moving average from above, short orders are triggered in turn.
The number of long and short orders increases in sequence, and positions are opened in batches by setting hanging orders. For example, entry line 1 is triggered to open 1 long/short position, entry line 2 is triggered to add 1 holding position, and entry line 3 is triggered to add 1 holding position. This can spread the cost of entry and reduce the risk of a single order.
The strategy also sets up a cover mechanism. When the position is not 0, a trailing stop loss order will be set based on the moving average price. If the price falls below the moving average again, the position will be stopped and closed. This can lock in some profits and protect funds.
Generally speaking, this strategy makes full use of moving average indicators to determine the trend direction, maximizes the profit range through multi-level entry lines, and sets stop loss orders to control risks. It is a typical trend following strategy.
## Advantage Analysis
This strategy has the following advantages:
1. It is clear and feasible to use the moving average to determine the trend direction. Moving averages can effectively filter market noise and determine the main trend direction.
2. Multi-level entry lines, making full use of the trend operating range. Through multiple entry lines, the entire operating range of the trend can be captured to the greatest extent and the profit margin can be expanded.
3. Open positions in batches to reduce single risk. Entering the market multiple times can spread the risk of orders and reduce the average holding cost of the position.
4. Set up a stop loss mechanism to effectively control risks. By covering the stop loss order, you can quickly stop the loss when the price falls below the moving average again to avoid excessive losses.
5. The strategic ideas are clear and easy to understand, and the parameter settings are flexible and can be optimized for different markets.
## Risk Analysis
There are also some risks with this strategy:
1. The probability of the moving average sending a wrong signal. There is a lag in judging the trend of the moving average, which may send out wrong signals.
2. Risk of loss caused by trend reversal. The strategy is based on the trend. Once the trend reverses, it will result in large losses.
3. The entry lines are set too densely, which increases transaction frequency and slippage costs.
4. Opening positions in batches increases the risk of position concentration. When the position is too large, risks are concentrated.
5. The stop loss point setting is unreasonable, and the stop loss may be stopped too early or the stop loss point is too small.
Corresponding risk management measures:
1. Optimize the moving average parameters and select the appropriate periodic moving average.
2. Pay attention to important technical indicators, judge trend reversal signals, and stop losses in time.
3. Adjust the entry line setting distance and reduce the trading frequency.
4. Optimize the size and proportion of positions to control concentration risks.
5. Test and optimize stop loss points to reduce stop loss risks.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test different moving average parameters and data sources, and choose the moving average indicator that best determines the trend.
2. Optimize the distance interval and the ratio of the number of positions between the long and short entry lines to find the best parameters.
3. Combine with other indicators as filter conditions to avoid the moving average from sending out wrong signals. Such as MACD, RSI, etc.
4. Optimize the position of the stop loss line and dynamically set the stop loss point based on ATR.
5. Increase the judgment of trend reversal and set conditions for closing all positions.
6. The parameters of the strategy can be optimized according to different market periods.
7. Add a dynamic adjustment function for the number of positions, and determine the number of positions to be opened based on the capital usage ratio.
## Summarize
This strategy uses moving averages to determine the direction of the trend as a whole, and takes the movement of the trend as the main source of profit. By entering the market at multiple levels and opening positions in batches, you can effectively grasp the trend and expand the profit range. At the same time, set up a stop-loss mechanism to control risks. This strategy has a simple and clear idea. It is suitable for beginners to learn and can also be optimized in depth. It is a typical trend following strategy.
||


## Overview 

This strategy is based on moving average trading. It sets up three levels of long and short entry lines to implement bidirectional opening positions, belonging to the trend following strategy. When the price breaks through the moving average, the strategy opens long and short positions in batches by placing pending orders.

## Strategy Logic

The strategy mainly uses the breakthrough of the moving average to determine the trend direction. Specifically, it calculates the arithmetic mean of opening price, closing price, highest price, lowest price and so on to obtain a moving average indicator. Then it sets up long entry lines above the moving average and short entry lines below it. When the price breaks through the moving average from below, long orders are triggered one by one. When the price breaks through from above, short orders are triggered one by one.

The number of long and short orders increases progressively. By setting pending orders, it implements batch opening positions. For example, entry line 1 triggers opening 1 contract long/short, entry line 2 triggers adding 1 contract, and entry line 3 adds another 1 contract. This helps diversify the entry cost and reduce the risk of a single order.

The strategy also has a hedging mechanism. When the position size is not 0, it will set a trailing stop loss order based on the moving average price. If the price breaks through the moving average again, it will close the position to lock in partial profit and protect the capital.

In summary, this strategy makes full use of the moving average indicator to determine the trend direction, maximizes the profit range through multiple entry lines, and controls risks with stop loss orders. It is a typical trend following strategy.

## Advantage Analysis

The advantages of this strategy are:

1. Using moving average to determine the trend direction is clear and feasible. Moving averages can filter market noise effectively and determine the main trend direction.

2. Multiple entry lines maximize the use of trend runs. With multiple entry lines, it can capture the whole run range of the trend as much as possible and expand the profit space.

3. Opening positions in batches reduces single order risk. Entering the market in multiple times diversifies the risks of orders and reduces the average holding cost. 

4. The hedging stop loss mechanism effectively controls risks. The hedging stop loss order realizes quick stop loss when price breaks the moving average again, avoiding huge losses.

5. The strategy logic is clear and easy to understand, with flexible parameter settings that can be optimized for different markets.

## Risk Analysis

There are some risks in this strategy:

1. The probability of wrong signals from the moving average. Moving averages have lag and may give wrong signals.

2. Trend reversal risk leading to losses. The strategy assumes a trend, so trend reversals can lead to huge losses.

3. Too frequent entry lines increase trading frequency and slippage costs. 

4. Batch opening positions increases concentration risk when position size is too large.

5. Improper stop loss point settings may lead to premature stop loss or the stop loss point is too small.

Corresponding risk management measures:

1. Optimize moving average parameters and select proper periods.

2. Pay attention to key technical indicators to spot trend reversal signals and stop loss in time.

3. Adjust the distance between entry lines to decrease trading frequency. 

4. Optimize position sizing and proportion to control concentration risk.

5. Backtest and optimize stop loss points to reduce stop loss risk.

## Optimization Directions

The strategy can be optimized from the following aspects:

1. Test different moving average parameters and data sources to find the best performing moving average indicator for determining trends.

2. Optimize the interval distance and position size proportion of long and short entry lines to find the optimal parameters.

3. Add other indicators as filter conditions to avoid wrong signals from the moving average, such as MACD, RSI etc.

4. Optimize stop loss line position, or set stop loss points dynamically based on ATR. 

5. Add judgment of trend reversal to set close all positions conditions.

6. Optimize parameters for different market periods.

7. Add dynamic adjustment of position size based on account usage percentage.

## Summary

This strategy judges the trend direction mainly based on moving averages, and takes advantage of trend runs as the profit source. By using multiple entry lines and opening positions in batches, it can effectively capture trends and expand profit zones. At the same time, stop loss mechanisms are used to control risks. The strategy logic is simple and clear, suitable for beginners to learn, and also for deep optimization. It is a typical trend following strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|100|Lot|
|v_input_2|3|MA Length|
|v_input_3|0|Data: 7. OHLC4|2. High|3. Low|4. Close|5. HL2|6. HLC3|1. Open|8. OC2|9. PCMA|
|v_input_4|true|short 3|
|v_input_5|true|short 2|
|v_input_6|true|short 1|
|v_input_7|true|long 1|
|v_input_8|true|long 2|
|v_input_9|true|long 3|
|v_input_10|15|Short line 3|
|v_input_11|10|Short line 2|
|v_input_12|5|Short line 1|
|v_input_13|-5|Long line 1|
|v_input_14|-10|Long line 2|
|v_input_15|-15|Long line 3|
|v_input_16|true|Offset|
|v_input_17|1900|From Year|
|v_input_18|2100|To Year|
|v_input_19|true|From Month|
|v_input_20|12|To Month|
|v_input_21|true|From day|
|v_input_22|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-19 00:00:00
end: 2023-09-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2019

//@version=4
strategy(title = "Robot WhiteBox Iceberg", shorttitle = "Robot WhiteBox Iceberg", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 3)

//Settings
capital = input(100, defval = 100, minval = 1, maxval = 10000, title = "Lot")
len = input(3, minval = 1, title = "MA Length")
s = input(defval = "7. OHLC4", options = ["1. Open", "2. High", "3. Low", "4. Close", "5. HL2", "6. HLC3", "7. OHLC4", "8. OC2", "9. PCMA"], title = "Data")
short3 = input(true, title = "short 3")
short2 = input(true, title = "short 2")
short1 = input(true, title = "short 1")
long1 = input(true, title = "long 1")
long2 = input(true, title = "long 2")
long3 = input(true, title = "long 3")
shortlevel3 = input(15.0, title = "Short line 3")
shortlevel2 = input(10.0, title = "Short line 2")
shortlevel1 = input(5.0, title = "Short line 1")
longlevel1 = input(-5.0, title = "Long line 1")
longlevel2 = input(-10.0, title = "Long line 2")
longlevel3 = input(-15.0, title = "Long line 3")
needoffset = input(true, title = "Offset")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//Variables
lots = 0.0
size = strategy.position_size
mult = 1 / syminfo.mintick
needtime = true

//MA
oc2 = (open + close) / 2
pcma = (highest(high, len) + lowest(low, len)) / 2
src = s == "1. Open" ? open : s == "2. High" ? high : s == "3. Low" ? low : s == "4. Close" ? close : s == "5. HL2" ? hl2 : s == "6. HLC3" ? hlc3 : s == "7. OHLC4" ? ohlc4 : s == "8. OC2" ? oc2: close
sma = sma(src, len)
ma = s == "9. PCMA" ? round(pcma * mult) / mult : round(sma * mult) / mult

//Levels
longline1 = 0.0
longline2 = 0.0
longline3 = 0.0
shortline1 = 0.0
shortline2 = 0.0
shortline3 = 0.0
longline1 := long1 ? round(ma * ((100 + longlevel1) / 100) * mult) / mult : close
longline2 := lots[1] == 0 ? long2 ? round(ma * ((100 + longlevel2) / 100) * mult) / mult : close : longline2[1]
longline3 := lots[1] == 0 ? long3 ? round(ma * ((100 + longlevel3) / 100) * mult) / mult : close : longline3[1]
shortline1 := short1 ? round(ma * ((100 + shortlevel1) / 100) * mult) / mult : close
shortline2 := lots[1] == 0 ? short2 ? round(ma * ((100 + shortlevel2) / 100) * mult) / mult : close : shortline2[1]
shortline3 := lots[1] == 0 ? short3 ? round(ma * ((100 + shortlevel3) / 100) * mult) / mult : close : shortline3[1]

//Lines
colorlong1 = long1 ? color.lime : na
colorlong2 = long2 ? color.lime : na
colorlong3 = long3 ? color.lime : na
colorshort1 = short1 ? color.red : na
colorshort2 = short2 ? color.red : na
colorshort3 = short3 ? color.red : na
offset = needoffset ? 1 : 0
plot(shortline3, offset = offset, color = colorshort3, title = "Short line 3")
plot(shortline2, offset = offset, color = colorshort2, title = "Short line 2")
plot(shortline1, offset = offset, color = colorshort1, title = "Short line 1")
plot(ma, offset = offset, color = color.blue, title = "MA line")
plot(longline1, offset = offset, color = colorlong1, title = "Long line 1")
plot(longline2, offset = offset, color = colorlong2, title = "Long line 2")
plot(longline3, offset = offset, color = colorlong3, title = "Long line 3")

//Trading
lot = 0.0
lot := size == 0 ? strategy.equity / close * capital / 100 : lot[1]
if ma > 0
    lots := round(size / lot)
    strategy.entry("L1", strategy.long, lot, limit = longline1, when = (lots == 0 and long1 and needtime))
    lots := round(size / lot)
    strategy.entry("L2", strategy.long, lot, limit = longline2, when = (lots <= 1 and long2 and needtime))
    lots := round(size / lot)
    strategy.entry("L3", strategy.long, lot, limit = longline3, when = (lots <= 2 and long3 and needtime))
    lots := round(size / lot)
    strategy.entry("S1", strategy.short, lot, limit = shortline1, when = (lots == 0 and short1 and needtime))
    lots := round(size / lot)
    strategy.entry("S2", strategy.short, lot, limit = shortline2, when = (lots >= -1 and short2 and needtime))
    lots := round(size / lot)
    strategy.entry("S3", strategy.short, lot, limit = shortline3, when = (lots >= -2 and short3 and needtime))
if size > 0
    strategy.entry("TPL", strategy.short, 0, limit = ma, when = needtime)
if size < 0
    strategy.entry("TPS", strategy.long, 0, limit = ma, when = needtime)
if time > timestamp(toyear, tomonth, today, 23, 59)
    strategy.close_all()
    strategy.cancel("L1")
    strategy.cancel("L2")
    strategy.cancel("L3")
    strategy.cancel("S1")
    strategy.cancel("S2")
    strategy.cancel("S3")
    strategy.cancel("TPL")
    strategy.cancel("TPS")
```

> Detail

https://www.fmz.com/strategy/427934

> Last Modified

2023-09-26 21:02:21

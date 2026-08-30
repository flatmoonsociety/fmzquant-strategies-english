
> Name

Trend-Following-Strategy Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The Noro trend following trading strategy is a simple trend following strategy based on price channels, RSI and body filtering. It identifies the direction of the price channel as a general trend, uses the overbought and oversold indicator RSI for entry, and cooperates with entity filtering to issue trading signals. This strategy is suitable for stocks with continuous trends such as stock indexes and foreign exchange.
## Strategy Principle
The main trading logic of this strategy includes:
1. Use price channels to determine the general trend direction. A channel is formed by calculating the highest and lowest prices within a certain period. If the price is above the channel, it is bullish, and if it is below the channel, it is bearish.
2. The RSI indicator determines the overbought and oversold ranges and assists in finding entry points. An RSI above 60 is an overbought zone, and an RSI below 40 is an oversold zone.
3. The entity filter emits the final signal. Only trade when the entity is larger than a certain size to avoid noise.
4. Combine the general trend, RSI signals and entity filters for entry. Enter the market to go long when there is a bullish signal in a bullish trend, and go short when there is a bearish signal in a bearish trend.
5. Provides the option to turn on the background color to intuitively determine the direction of the general trend.
6. You can customize the strategy trading time period and only trade within the selected time period.
This strategy resonates with multiple indicators, the general trend determines the direction, RSI determines the time point, and entity filtering determines the quality, forming a relatively stable trend following strategy.
## Advantage Analysis
This strategy has the following main advantages:
1. The price channel intuitively determines the direction of the general trend and avoids carrying orders in the opposite direction.
2. The RSI indicator can effectively identify overbought and oversold entry points.
3. Physical filtering enhances signal quality to avoid being deceived by noise or false signals.
4. Multi-index filtering and confirmation to improve the accuracy of decision-making.
5. Use simple indicators to reduce the risk of curve optimization.
6. The trading time period can be customized and applied flexibly in accordance with the general trend direction.
7. Easy to operate with few parameters, even novices can use it easily.
8. Provide background color options to form a clear visual effect.
## Risk Analysis
This strategy also faces certain risks:
1. The risk of misjudgment of the general trend, and the price channel may fail.
2. The risk of RSI sending wrong signals, and inaccurate judgments of overbought and oversold.
3. Entity filtering eliminates the risk of normal signals and misses trading opportunities.
4. Retracement risk, deep adjustments will also occur in the general trend.
5. Optimization risks, improper parameter settings may lead to over-optimization.
6. Position risk, default full position trading may amplify losses.
7. Variety selection risk, this strategy is only suitable for trending varieties.
8. The risk of setting the trading time period needs to be set appropriately to be effective.
## Optimization direction
This strategy can consider the following optimization points:
1. Add a stop loss strategy to control single losses.
2. Optimize parameters to make them more consistent with the characteristics of specific trading varieties.
3. Add a position management module to adjust positions according to the strength of the trend.
4. Retracement control can be set to avoid losses from expanding.
5. Combine volume and price indicators for signal verification to improve accuracy.
6. Add machine learning and other technologies for parameter optimization.
7. Classify and optimize trading varieties and formulate personalized strategies.
8. Optimize the setting logic of the trading time period to make it more flexible.
## Summarize
The Noro trend following strategy integrates price channels, RSI and entity filters to form a simple and practical trend following strategy. It can go with the trend and avoid trading against the trend. Through parameter optimization, risk control and other improvements, this strategy is expected to become a sustainable and profitable trend trading strategy.
||


## Overview

Noro's trend following strategy is a simple trend trading strategy based on price channel, RSI and body filter. It identifies the overall trend using price channel, enters based on RSI overbought/oversold levels, and uses body filter for additional signal confirmation. The strategy suits trending instruments like indices and forex.

## Strategy Logic 

The key aspects are:

1. Price channel determines the overall trend. Channel formed by looking back high/low defines uptrend/downtrend.

2. RSI indicates overbought/oversold for entry timing. RSI above 60 is overbought, below 40 is oversold zone.

3. Body filter provides final signal. Trades only if candle body exceeds a threshold to avoid noise.

4. Entries based on combining trend, RSI signal and body filter. Long entries in uptrend on bullish signals, short entries in downtrend on bearish signals.

5. Optional background colors clearly visualize the trend. 

6. Customizable trading time frames to selectively trade.

Multiple indicators align to create a relatively stable trend following system.

## Advantages

The main advantages are:

1. Price channel intuitively identifies the overall trend direction.

2. RSI effectively detects overbought/oversold levels for timing entry.

3. Body filter enhances signal quality and avoids false signals. 

4. Multi-indicator confirmation improves accuracy.

5. Simple indicators reduce curve fitting risks.

6. Customizable trading time frames add flexibility.

7. Easy to use with minimal parameters. Beginner friendly.

8. Background colors provide visual clarity.

## Risks

Some risks to consider:

1. Price channel trend misidentification risk.

2. Inaccurate RSI signal risks. 

3. Body filter eliminating valid signals.

4. Drawdown risk during trend corrections.

5. Optimization risk from bad parameter tuning. 

6. Position sizing risk from default full allocation.

7. Instrument selection risk if applied on non-trending assets. 

8. Trading time frame risks if improperly configured.

## Enhancement Opportunities

Some enhancement possibilities:

1. Add stop loss strategy to control loss per trade.

2. Optimize parameters based on instrument behavior.

3. Incorporate position sizing rules based on trend strength.

4. Implement drawdown limits to contain losses.

5. Add volume price analysis for signal verification.

6. Introduce machine learning for parameter optimization. 

7. Specialize parameters based on asset class.

8. Refine trading time frame logic for more flexibility.

## Conclusion

Noro's trend following strategy integrates price channel, RSI and body filter into a simple and practical trend trading system. It can trade along the trends and avoid counter-trend trades. With parameter optimization, risk controls and other improvements, the strategy has potential to become a consistently profitable trend trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|long|
|v_input_2|true|short|
|v_input_3|21|MA Period|
|v_input_4|false|Need trend Background?|
|v_input_5|1900|From Year|
|v_input_6|2100|To Year|
|v_input_7|true|From Month|
|v_input_8|12|To Month|
|v_input_9|true|From day|
|v_input_10|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-25 00:00:00
end: 2023-09-24 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title = "Noro's TrendMaster Strategy v1.0", shorttitle = "TrendMaster str 1.0", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "long")
needshort = input(true, defval = true, title = "short")
len = input(21, defval = 20, minval = 2, maxval = 200, title = "MA Period")
needbg = input(false, defval = false, title = "Need trend Background?")
fromyear = input(1900, defval = 1900, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")

//PriceChannel 1
lasthigh = highest(close, len)
lastlow = lowest(close, len)
center = (lasthigh + lastlow) / 2

//Trend
trend = low > center and low[1] > center[1] ? 1 : high < center and high[1] < center[1] ? -1 : trend[1]

//Bars
bar = close > open ? 1 : close < open ? -1 : 0

//Fast RSI
fastup = rma(max(change(close), 0), 2)
fastdown = rma(-min(change(close), 0), 2)
rsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))

//Body filter
nbody = abs(close - open)
abody = sma(nbody, 10)
body = nbody > abody / 2

//Signals
up1 = trend == 1 and rsi < 60 and (strategy.position_avg_price > close or strategy.position_size <= 0) and body
dn1 = trend == -1 and rsi > 40 and (strategy.position_avg_price < close or strategy.position_size >= 0) and body

//Lines
plot(center, color = blue, linewidth = 3, transp = 0, title = "MA")

//Background
col = needbg == false ? na : trend == 1 ? lime : red
bgcolor(col, transp = 80)

//Trading

if up1
    strategy.entry("Long", strategy.long, needlong == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))

if dn1
    strategy.entry("Short", strategy.short, needshort == false ? 0 : na, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
    
if time > timestamp(toyear, tomonth, today, 23, 59)
    strategy.close_all()
    
```

> Detail

https://www.fmz.com/strategy/427814

> Last Modified

2023-09-25 17:50:11

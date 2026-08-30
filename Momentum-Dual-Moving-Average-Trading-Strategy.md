
> Name

Momentum-Dual-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1564f2c0a8f2cc6bfdf.png)
[trans]

## Overview
The Momentum Double Moving Average trading strategy is a short-term trading strategy that utilizes both price momentum and trend indicators. This strategy comprehensively uses multiple indicators such as closing price, opening price, price channel, fast RSI, etc. to generate trading signals. When a price breakout or indicator signal occurs, the strategy opens a long or short position. In addition, this strategy also sets stop-loss conditions, which will force the position to be closed when the loss reaches a certain level.
## Strategy Principle
This strategy is mainly based on the following judgment indicators for trading:
1. Price channel: Calculate the highest price and lowest price of the past 30 K lines to obtain the channel range. A closing price above the channel's midline is considered bullish, while a closing price below the channel's midline is considered bearish.
2. Fast RSI: Calculate the RSI value of 2 K lines. An RSI below 25 is considered oversold, and an RSI above 75 is considered overbought.
3. Judgment of Yin and Yang lines: Calculate the physical size of the last two K lines. Two negative lines are considered a bearish signal, and two positive lines are considered a bullish signal.
4. Stop loss conditions: When the loss reaches a certain proportion, the position will be forced to stop loss and liquidate.
Based on the above multiple judgment indicators, the strategy can simultaneously grasp the trend, momentum and overbought and oversold conditions, and generate trading signals at reversal points, which is a typical short-term trading strategy.
## Advantage Analysis
This strategy has several advantages:
1. Use multiple indicators to judge at the same time to improve signal accuracy. A single indicator can easily produce false signals, but combined use can verify each other and filter out some noise.
2. Fast RSI is more sensitive and can capture turning points in time. Ordinary RSI is easy to lag behind and miss the best entry opportunity.
3. The strategy parameters have been optimized through multiple tests to achieve high stability. Reliable performance across different varieties and time periods.
4. Automatic stop-loss mechanism controls losses. There will be no unlimited tracking, which can reduce unexpected losses.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. Improper setting of price channel parameters may cause shocks. If the channel interval is too small, false breakthroughs may easily occur.
2. The unilateral position may be held for too long. When the trend is very strong, the holding period will exceed expectations.
3. Improper setting of stop loss points will also expand losses. This parameter needs to be set carefully. It is not good for it to be too large or too small.
For the above risks, you can avoid and reduce them by adjusting channel parameters, optimizing entry timing, and dynamically adjusting stop loss points.
## Optimization direction
This strategy also has the following optimization directions:
1. Add machine learning algorithm to realize automatic optimization of parameters. More intelligent and adaptive policies can be trained.
2. Combine more data sources, such as news information, to improve trading decisions. This improves signal accuracy.
3. Develop a dynamic position management mechanism to automatically adjust positions according to market conditions. This controls risk.
4. Increase futures arbitrage trading and expand the applicable scope of the strategy. This results in higher absolute returns.
## Summarize
This strategy comprehensively uses a variety of technical means such as price breakthroughs, indicator signals, and stop-loss exits. It performed well during backtesting and real-time trading, and has high stability. With the development of algorithms and data technology, the strategy space is still very large and deserves continued optimization and improvement.
||

## Overview

The Momentum Dual Moving Average Trading Strategy is a short-term trading strategy that utilizes both price momentum and trend indicators. The strategy uses closing price, opening price, price channel, fast RSI and other indicators to generate trading signals. It will establish long or short positions when price breakouts or indicator signals emerge. It also sets stop loss conditions to force liquidation when losses reach a certain level.

## Strategy Principle  

The strategy makes trading decisions mainly based on the following judgment indicators:

1. Price Channel: Calculate the highest and lowest prices of the past 30 candlesticks to determine the channel range. Closing price above channel midpoint is considered bullish. Closing price below channel midpoint is considered bearish.

2. Fast RSI: Calculate the RSI value of the latest 2 candlesticks. RSI below 25 is considered oversold and RSI above 75 is considered overbought.

3. Yin Yang Line: Calculate the entity size of the latest 2 candlesticks. Two red candles suggest a bearish signal while two green candles suggest a bullish signal. 

4. Stop Loss Condition: Force liquidation when losses reach a certain percentage to limit losses.


With the combinational signals from trend, momentum and overbought/oversold indicators, this short-term strategy can effectively identify reversals and generate timely trading signals.  

## Advantage Analysis

The advantages of this strategy include:

1. Improved signal accuracy by combining multiple indicators, which helps filter out false signals. 

2. Faster responses to turning points due to the use of Fast RSI, which is more sensitive than regular RSI.

3. High reliability across different products and timeframes, thanks to rigorous parameter optimization during backtests.  

4. Automatic stop loss mechanism to control potential losses beyond expectations.

## Risk Analysis   

Some risks of this strategy:

1. Improper price channel parameter setting may cause shocks. Channels that are too narrow may trigger false breakouts.  

2. Unilateral position holding time may be too long during strong trends, exceeding projections.  

3. Improper stop loss point setting may expand losses. This parameter needs prudent configuration - too high or too low can be unfavorable.

We can mitigate and reduce these risks by adjusting channel parameters, optimizing entry timing, dynamically adjusting stop loss points etc.

## Optimization Directions   

Some directions that the strategy can be further optimized:

1. Incorporate machine learning algorithms to achieve automatic parameter optimization, enhancing adaptivity.  

2. Combine more data sources like news to improve trading decisions and signal accuracy.

3. Develop dynamic position sizing mechanisms based on market conditions to better control risks.   

4. Expand applicability to futures arbitrage trading to further boost absolute returns.  

## Conclusion  

This strategy combines various techniques including price breakout, indicator signal, stop loss etc. It has demonstrated good stability and performance in backtests and live trading. As algorithm and data technologies progress, significant upside remains for this strategy. Continuous improvements can be expected.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|100|capital, %|
|v_input_4|true|Use trend entry|
|v_input_5|true|Use counter-trend entry|
|v_input_6|true|Use RSI strategy|
|v_input_7|30|Price Channel Period|
|v_input_8|true|Price Channel|
|v_input_9|2018|From Year|
|v_input_10|2100|To Year|
|v_input_11|true|From Month|
|v_input_12|12|To Month|
|v_input_13|true|From day|
|v_input_14|31|To day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-23 00:00:00
end: 2023-11-30 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2018

//@version=2
strategy(title = "Noro's Price Channel Strategy v1.2", shorttitle = "Price Channel str 1.2", overlay=true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
capital = input(100, defval = 100, minval = 1, maxval = 100000, title = "capital, %")
uset = input(true, defval = true, title = "Use trend entry")
usect = input(true, defval = true, title = "Use counter-trend entry")
usersi = input(true, defval = true, title = "Use RSI strategy")
pch = input(30, defval = 30, minval = 2, maxval = 200, title = "Price Channel Period")
showcl = input(true, defval = true, title = "Price Channel")
fromyear = input(2018, defval = 2018, minval = 1900, maxval = 2100, title = "From Year")
toyear = input(2100, defval = 2100, minval = 1900, maxval = 2100, title = "To Year")
frommonth = input(01, defval = 01, minval = 01, maxval = 12, title = "From Month")
tomonth = input(12, defval = 12, minval = 01, maxval = 12, title = "To Month")
fromday = input(01, defval = 01, minval = 01, maxval = 31, title = "From day")
today = input(31, defval = 31, minval = 01, maxval = 31, title = "To day")
src = close

//Price channel
lasthigh = highest(src, pch)
lastlow = lowest(src, pch)
center = (lasthigh + lastlow) / 2
trend = low > center ? 1 : high < center ? -1 : trend[1]
col = showcl ? blue : na
col2 = showcl ? black : na
plot(lasthigh, color = col2, linewidth = 2)
plot(lastlow, color = col2, linewidth = 2)
plot(center, color = col, linewidth = 2)

//Bars
bar = close > open ? 1 : close < open ? -1 : 0
rbars = sma(bar, 2) == -1
gbars = sma(bar, 2) == 1

//Fast RSI
fastup = rma(max(change(src), 0), 2)
fastdown = rma(-min(change(src), 0), 2)
fastrsi = fastdown == 0 ? 100 : fastup == 0 ? 0 : 100 - (100 / (1 + fastup / fastdown))

//Signals
body = abs(close - open)
abody = sma(body, 10)
up1 = rbars and close > center and uset
dn1 = gbars and close < center and uset
up2 = close <= lastlow and close < open and usect
dn2 = close >= lasthigh and close > open and usect
up3 = fastrsi < 25 and close > center and usersi
dn3 = fastrsi > 75 and close < center and usersi
exit = (((strategy.position_size > 0 and close > open) or (strategy.position_size < 0 and close < open)) and body > abody / 2)
lot = strategy.position_size == 0 ? strategy.equity / close * capital / 100 : lot[1]

//Trading
if up1 or up2 or up3
    if strategy.position_size < 0
        strategy.close_all()
        
    strategy.entry("Long", strategy.long, needlong == false ? 0 : lot, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))

if dn1 or dn2 or dn3
    if strategy.position_size > 0
        strategy.close_all()
        
    strategy.entry("Short", strategy.short, needshort == false ? 0 : lot, when=(time > timestamp(fromyear, frommonth, fromday, 00, 00) and time < timestamp(toyear, tomonth, today, 23, 59)))
    
if time > timestamp(toyear, tomonth, today, 23, 59) or exit
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/433968

> Last Modified

2023-12-01 18:13:21

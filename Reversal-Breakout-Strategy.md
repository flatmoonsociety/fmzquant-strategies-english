
> Name

Reversal-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1238db321ac633adc6e.png)
[trans]


## Overview
The swing breakout strategy uses Bollinger Bands and stochastic indicators to identify potential reversal points when asset prices reach overbought and oversold areas, and is suitable for day traders to profit from small price fluctuations. The main idea of ​​this strategy is to look for trading opportunities when the price of a specific asset breaks through the upper and lower Bollinger Bands and the stochastic indicator shows overbought and oversold signals.
## Strategy Principle
This strategy uses both Bollinger Bands and Stochastics as the main technical indicators. Bollinger Bands obtains the upper and lower rails by calculating the moving average and standard deviation of a specified period (such as 20 days). When the price reaches the upper band, it is considered overbought, and when it reaches the lower band, it is considered oversold. The stochastic indicator RSI determines whether the price is excessively overbought or oversold. When the RSI is below 20, it is oversold, and when it is above 80, it is overbought.
The specific trading strategy is: when the price breaks through the lower Bollinger Band and the stochastic RSI is below 20, go long; when the price breaks through the upper Bollinger Band and the stochastic RSI is above 80, go short. When going long, the stop-loss price is set a few points below the current K-line low, and when going short, the stop-loss price is set a few points above the current K-line high. The target profit is set outside the average fluctuation points of the recent K-lines.
The code uses the cross function to realize the Bollinger Band track breakthrough judgment, RSI high and low judgment, and draws a shape to mark the breakthrough signal. Set stop loss and take profit after entering the market, and follow the price changes to exit.
## Advantage Analysis
This strategy combines Bollinger Bands to determine the support pressure area and RSI to determine the overbought and oversold area, which can improve the quality of trading signals. Compared with a single indicator, false signals can be reduced.
Using the K-line to break through the upper and lower tracks of Bollinger Bands and combining with RSI filtering, you can capture reversal opportunities. This type of reversal trade has greater potential profit potential.
The stop loss distance is small, which is beneficial to controlling single losses. The take profit is set according to the average fluctuation, which can better balance the profit size.
This strategy has a high trading frequency and is suitable for short-term trading within the day. It can make full use of small-scale market fluctuations to make profits.
## Risk Analysis
The Bollinger Band track breakthrough assumes that the price will reverse back to the moving average, but some breakthroughs may be false breakthroughs and cannot form a trend reversal. This can lead to losses.
RSI is lagging and may trigger overbought and oversold signals in advance, thereby missing some trading opportunities.
The stop loss distance is small, aiming to control a single loss, but it also limits the profit potential of a single transaction.
High-frequency trading requires strong psychological quality, and stopping losses too frequently may affect overall profits.
## Optimization direction
You can test and adjust the Bollinger Band parameters, such as increasing the period length, to improve the quality of the breakthrough signal.
You can try to use the K-line closing price to break through the Bollinger Bands as a signal instead of directly judging the breakthrough to reduce false breakthroughs.
It can be combined with other indicators such as MACD, KD, etc. and RSI to form a combination to improve the accuracy of overbought and oversold determinations.
Dynamic stop loss distance can be set according to the characteristics of different varieties instead of fixed point stop loss.
## Summarize
This strategy integrates the Bollinger Bands to determine the support pressure area and the RSI indicator to determine the overbought and oversold area. In theory, it can better detect reversal opportunities. In actual operation, the key is to find the appropriate parameter configuration, control risks, and continue to optimize.

|| 

## Overview

The reversal breakout strategy utilizes Bollinger Bands and Stochastic Oscillator to identify potential reversal points when an asset is overbought or oversold. It is suitable for intraday traders to capitalize on small price fluctuations for profits. The main idea is to look for trading opportunities when the price breaks out of the Bollinger Bands and Stochastic shows overbought/oversold signals.

## Strategy Logic

The strategy uses both Bollinger Bands and Stochastic as the main technical indicators. Bollinger Bands are plotted at standard deviation levels above and below a simple moving average. Prices reaching the upper band are considered overbought while lower band oversold. Stochastic Oscillator determines if prices have moved too far and are due for a reversal. Readings above 80 suggest overbought conditions while below 20 oversold. 

The trading rules are: go long when price breaks below the lower Bollinger band and Stochastic is below 20; go short when price breaks above the upper band and Stochastic is above 80. The stop loss is placed a few pips below the low (for longs) or above the high (for shorts). Take profit target is set at average price swing beyond recent bars.

The crossovers identify the band breakouts. Shape markers plot the entry signals. Stops and profit targets are defined after entry.

## Advantages

Combining bands for support/resistance and Stochastic for overbought/oversold improves signal quality vs. a single indicator. Reversal trading after band breakouts has potential for larger gains.

The tight stop loss helps limit losses. Take profit based on average true range aims for balanced reward/risk. High frequency trading captures small moves.

## Risks 

Band breakouts assume mean reversion which may fail. Stochastic lags price so some moves may be missed.

Small stops restrain the profit potential. Frequent trading needs strong psychology - avoiding over-stopping.

## Enhancements

Test longer Bollinger periods or confirm closes outside bands to improve quality.

Combine other indicators like MACD and KD with Stochastic for better overbought/oversold signals.

Consider dynamic stops based on volatility instead of fixed pips.

## Conclusion

The strategy seeks to identify reversals by combining Bollinger Bands for support/resistance and Stochastic for overbought/oversold conditions. Fine tuning parameters, controlling risk, and ongoing optimization are key for real-world performance. Transaction costs should be considered. Past performance is no guarantee of future results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Bollinger Bands Length|
|v_input_2_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|2|Multiplier|
|v_input_4|14|Stochastic Length|
|v_input_5|5|Stochastic %K Smoothing|
|v_input_6|3|Stochastic %D Smoothing|
|v_input_7|50|Take Profit (pips)|
|v_input_8|3|Stop Loss (pips)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-20 00:00:00
end: 2023-10-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Bollinger Bands & Stochastic Scalping Strategy", shorttitle="BB & Stoch Scalp", overlay=true)

// Bollinger Bands
length = input(20, title="Bollinger Bands Length")
src = input(close, title="Source")
mult = input(2, title="Multiplier")
basis = sma(src, length)
dev = mult * stdev(src, length)
upperBB = basis + dev
lowerBB = basis - dev

// Stochastic
stochLength = input(14, title="Stochastic Length")
smoothK = input(5, title="Stochastic %K Smoothing")
smoothD = input(3, title="Stochastic %D Smoothing")
k = sma(stoch(close, high, low, stochLength), smoothK)
d = sma(k, smoothD)

// Entry Conditions
longCondition = crossover(close, lowerBB) and crossover(k, 20)
shortCondition = crossunder(close, upperBB) and crossunder(k, 80)

// Exit Conditions
takeProfit = input(50, title="Take Profit (pips)")

plotshape(series=longCondition, title="Long Entry Signal", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(series=shortCondition, title="Short Entry Signal", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)

// Stop Loss
stopLossPips = input(3, title="Stop Loss (pips)")
stopLossLong = close - stopLossPips * syminfo.mintick
stopLossShort = close + stopLossPips * syminfo.mintick

strategy.entry("Long", strategy.long, when=longCondition)
strategy.entry("Short", strategy.short, when=shortCondition)

strategy.exit("Take Profit/Stop Loss", from_entry="Long", profit=takeProfit, stop=stopLossLong)
strategy.exit("Take Profit/Stop Loss", from_entry="Short", profit=takeProfit, stop=stopLossShort)

plot(upperBB, title="Upper Bollinger Band", color=color.red)
plot(lowerBB, title="Lower Bollinger Band", color=color.green)

hline(80, "Overbought", color=color.red)
hline(20, "Oversold", color=color.green)

```

> Detail

https://www.fmz.com/strategy/430368

> Last Modified

2023-10-27 16:14:16

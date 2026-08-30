
> Name

Bollinger-Bands-and-RSI-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/1070fff7ae3574d522a37b1b00efc90be0c55413bb1fbce6889f56c2e3c00389.png)
[trans]

## Overview
This strategy combines the technical indicators of the Bollinger Bands and the Relative Strength Index (RSI). When the RSI indicator has a golden cross or a dead cross, it determines whether the price touches or breaks through the upper or lower Bollinger Bands to send buy and sell signals.
## Strategy Principle
1. Calculate the 20-period SMA as the baseline, the upper track is the baseline + 2 times the standard deviation, and the lower track is the baseline - 2 times the standard deviation, and construct the Bollinger Band.
2. Calculate the 14-period RSI value. RSI above 70 is the overbought zone, and RSI below 30 is the oversold zone.
3. When the RSI indicator crosses below 30, if the price is below the lower rail, a buy signal is generated; when the RSI indicator crosses above 70, if the price is above the upper rail, a sell signal is generated.
## Advantage Analysis
1. Bollinger Bands use the standard deviation range to judge price fluctuations and future trends, and have strong trend judgment capabilities.
2. The RSI indicator determines overbought and oversold conditions, and combined with the Bollinger Band track judgment, can effectively discover reversal opportunities.
3. The RSI indicator easily forms a breakthrough signal, and combined with the Bollinger Bands, the signal is more accurate and reliable.
## Risk Analysis
1. The Bollinger Band is not 100% accurate, and the price may break through the upper and lower rails and continue to run.
2. The RSI indicator may also form a false breakthrough signal, which is inconsistent with the Bollinger Bands judgment results.
3. It is very important to adjust parameters appropriately. Improper parameter settings may lead to too frequent or infrequent trading signals.
## Optimization direction
1. Can test parameters of different periods and find the best parameter combination.
2. It can be combined with other indicators, such as KD, MACD, etc., to improve the reliability of the signal.
3. Based on the backtest results, you can optimize the stop-loss and take-profit strategies to control risks.
## Summarize
This strategy integrates Bollinger Bands trend analysis and RSI indicator overbought and oversold judgment to form trading signals. In general, the strategic ideas are clear, easy to implement, and have certain practical value. However, there are also certain risks, and it is necessary to pay attention to parameter adjustment and indicator integration, and continuous optimization to adapt to different market environments.
||

## Overview

This strategy combines the Bollinger Bands and Relative Strength Index (RSI) technical indicators. It generates buy and sell signals when the RSI indicator crosses over the oversold or overbought levels and the price touches or breaks through the Bollinger Bands.

## Strategy Logic  

1. Calculate the 20-period SMA as the basis line. The upper band is the basis + 2 standard deviations and the lower band is the basis - 2 standard deviations to construct the Bollinger Bands.

2. Calculate the 14-period RSI. RSI above 70 is overbought zone and below 30 is oversold zone.   

3. When RSI breaks below 30 and price is lower than the lower band, a buy signal is generated. When RSI breaks above 70 and price is higher than the upper band, a sell signal is generated.

## Advantage Analysis

1. Bollinger Bands uses standard deviation to judge price volatility and future trends with strong capability. 

2. RSI judges overbought and oversold levels. Combined with Bollinger Bands, it can effectively discover reversal opportunities.

3. RSI is easy to form breakout signals. Combined with Bollinger Bands, the trading signals are more accurate and reliable.

## Risk Analysis  

1. Bollinger Bands are not 100% accurate and prices may break through the upper or lower band and keep running.

2. RSI may also form false breakout signals which are inconsistent with Bollinger Bands.

3. Proper parameter tuning is important. Improper settings may lead to too frequent or rare trading signals.

## Optimization  

1. Test different parameter periods to find the optimal parameter combination.

2. Incorporate other indicators like KD, MACD to improve signal reliability.  

3. Optimize stop loss and take profit based on backtest results to control risks.

## Summary  

This strategy integrates Bollinger Bands' trend analysis and RSI's overbought-oversold judgment to generate trading signals. Overall, the strategy logic is clear and easy to implement with certain practical value. But it also has some risks. Parameters tuning and indicators integration are needed to continuously optimize it to adapt to different market environments.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|Length|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|2|StdDev|
|v_input_int_2|14|RSI Length|
|v_input_int_3|70|RSI Overbought Level|
|v_input_int_4|30|RSI Oversold Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-21 00:00:00
end: 2023-12-28 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Bollinger Bands and RSI Strategy", overlay=false)

// Define the parameters
length = input.int(20, "Length", minval=1)
src = input(close, "Source")
mult = input.float(2.0, "StdDev", minval=0.001, maxval=50)
rsiLength = input.int(14, "RSI Length", minval=1)
rsiOverbought = input.int(70, "RSI Overbought Level", minval=1, maxval=100)
rsiOversold = input.int(30, "RSI Oversold Level", minval=1, maxval=100)

// Calculate the Bollinger Bands
basis = ta.sma(src, length)
dev = mult * ta.stdev(src, length)
upper = basis + dev
lower = basis - dev

// Plot the Bollinger Bands
plot(basis, "Basis", color=#FF6D00)
p1 = plot(upper, "Upper", color=#2962FF)
p2 = plot(lower, "Lower", color=#2962FF)
fill(p1, p2, color=color.rgb(33, 150, 243, 90), title="Background")

// Calculate the RSI
rsi = ta.rsi(src, rsiLength)

// Plot the RSI
plot(rsi, "RSI", color=#FF6D00)

// Define the entry and exit conditions
longCondition = ta.crossover(rsi, rsiOversold) and src < lower // Use ta.crossover here
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = ta.crossunder(rsi, rsiOverbought) and src > upper // Use ta.crossunder here
if (shortCondition)
    strategy.entry("Short", strategy.short)

// Plot the buy and sell signals
plotshape(longCondition, title="Buy", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(shortCondition, title="Sell", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)

```

> Detail

https://www.fmz.com/strategy/437035

> Last Modified

2023-12-29 16:40:19

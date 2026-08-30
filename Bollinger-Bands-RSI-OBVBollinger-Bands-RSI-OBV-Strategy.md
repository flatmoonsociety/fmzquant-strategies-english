
> Name

Bollinger-Bands-RSI-OBV-Strategy Bollinger-Bands-RSI-OBV-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/137636ba3c3b3e555ac.png)
[trans]
## Overview
The Bollinger Bands RSI OBV strategy combines Bollinger Bands, the Relative Strength Index (RSI) and the Balanced Balanced Index (OBV) to identify breakout and reversal points in stock prices. This strategy will send a trading signal when the stock price breaks through the upper and lower Bollinger Bands, the RSI indicator shows overbought and oversold, and the OBV indicator turns around.
## Strategy Principle
The trading logic of this strategy is mainly based on Bollinger Bands, RSI indicator and OBV indicator. Specifically:
1. When the stock price breaks through the middle track of the Bollinger Bands and goes upward, and the RSI is greater than 50, it indicates the formation of a bullish trend. If the OBV indicator falls back at this time, indicating a short-term decline, then this is the time to open a long position.
2. When the stock price falls below the lower Bollinger Band, close the previous long position.
3. When the stock price breaks through the middle track of the Bollinger Bands and goes downwards, and the RSI is less than 50, it indicates the formation of a short trend. If the OBV indicator rises at this time, indicating a rebound in the short term, then this is the time to open a short position.
4. When the stock price breaks through the upper Bollinger Band again, close the previous short position.
Therefore, this strategy uses the breakthrough of the Bollinger Band to determine the direction; then combines it with RSI to determine the strength and OBV to determine the short-term reversal to form a trading signal.
## Advantage Analysis
The biggest advantage of this strategy is that it combines three different types of indicators, Bollinger Bands, RSI and OBV, to capture change signals in advance when the stock price begins to change in direction. For example, after the stock price breaks through the Bollinger Band upwards, if you only look at the K-line, you may directly open a long order, but combined with RSI and OBV, you can judge whether there is the possibility of short-term adjustment at this time and avoid opening a position. Therefore, this combination of indicators can improve the stability of the strategy.
Secondly, this strategy also sets entry conditions for breaking through the Bollinger Band and stop-loss conditions for breaking through the Bollinger Band again in the opposite direction. This can control the profit and loss ratio of each order within a certain reasonable range and reduce the possibility of a single loss.
Finally, the logic of the strategy code is clear and concise, the parameter settings are reasonable and easy to understand, and it is suitable for optimization and improvement as a strategy framework for simulating real trading. This reduces the risks that may arise when the strategy is implemented.
## Risk Analysis
The biggest risk of this strategy is that improperly setting the Bollinger Band width may lead to missed trading opportunities. If the distance between Bollinger Bands is set too large, the stock price will need to fluctuate significantly to trigger the logic of opening a position or stopping loss. This may miss some relatively small trend opportunities.
In addition, the strategy currently only considers the logic of buying and selling point selection, and does not integrate the optimization of fund management, position management, etc. This leads to the possibility of unlimited unilateral addition of positions, which can easily result in larger losses due to the inability to stop losses and exit in time.
Finally, wrong signals may also appear in the judgment of the combination of RSI and OBV indicators. RSI only considers the speed of stock price rise and fall within a certain period and cannot judge the long-term trend; OBV may also become less reliable due to the characteristics of individual stocks. This may affect the accuracy of the strategy signal.
## Optimization direction
Considering the above analysis, this strategy can be optimized from the following directions:
1. Optimize the width of the Bollinger Track and set the adaptive Bollinger Track width to automatically adapt to market fluctuations.
2. Integrate position management logic and reduce the position size when there are continuous losses. When making continuous profits, increase the position appropriately.
3. Test and optimize the parameters of the RSI indicator such as bullish cycles.
4. Try different short-term indicators such as KDJ, MACD, etc. to replace the OBV indicator to determine whether the signal accuracy can be improved.
5. Test different medium and long-term indicators such as MVSL, DMI, etc. and use them in conjunction with RSI to help determine the medium- and long-term trend of stock prices.
## Summary
Bollinger Bands RSI OBV strategy comprehensively uses three different types of technical indicators, which not only ensures certain stability and screening standards, but also provides a framework basis for subsequent optimization and improvement. This strategy is suitable for medium and long-term stock selection and holding, and can also be used as the basis for short-term strategies to make substantial adjustments and optimizations.
||

## Overview
The Bollinger Bands RSI OBV strategy combines Bollinger Bands, Relative Strength Index (RSI) and On Balance Volume (OBV) to identify breakout and reversal points of stock prices. When the stock price breaks through the upper and lower rails of the Bollinger Bands, and the RSI indicator shows overbought or oversold, while the OBV indicator shows a turn, this strategy will issue trading signals.

## Strategy Principle  
The trading logic of this strategy is mainly based on Bollinger Bands, RSI indicators and OBV indicators. Specifically:

1. When the stock price breaks through the middle rail of the Bollinger Bands and goes up, while the RSI is greater than 50 indicating the formation of a bullish trend, if the OBV indicator falls back at this time indicating a short-term decline, this is the time to open long positions.

2. When the stock price breaks through the lower rail of the Bollinger Bands, close the previous long positions.  

3. When the stock price breaks through the middle rail of the Bollinger Bands and goes down, while the RSI is less than 50 indicating the formation of a bearish trend, if the OBV indicator rises at this time indicating a short-term rebound, this is the time to open short positions.

4. When the stock price breaches the upper rail of the Bollinger Bands again, close the previous short positions.

So this strategy uses the breakout of Bollinger rails to determine direction; combines RSI to judge strength and weakness and OBV to judge short-term reversals to generate trading signals.

## Advantage Analysis
The biggest advantage of this strategy is that it combines three different types of indicators: Bollinger Bands, RSI and OBV, which can capture changes in signals in advance when stock prices start to change directionally. For example, after the stock price breaks through the middle rail of the Bollinger Bands upwards, if you just look at the K-line chart, you may directly open long positions. However, combining RSI and OBV can determine if there is a possibility of short-term adjustment at this time thereby avoiding opening positions. Therefore, such a combination of indicators can improve the stability of the strategy.

Secondly, this strategy sets the entry condition of breaking through the Bollinger Bands as well as the stop loss condition of breaking through the Bollinger Bands in the opposite direction. This can keep the risk-reward ratio of each position within a reasonable range and reduce the possibility of a single loss.

Finally, the code logic of this strategy is clear and concise, and the parameter settings are reasonable and easy to understand, making it suitable as a simulation strategy framework for optimization and improvement. This reduces the risks that may occur when the strategy goes live.

## Risk Analysis
The biggest risk of this strategy is that improper setting of the width of the Bollinger Bands may result in missing a lot of trading opportunities. If the interval between Bollinger Bands is set too large, stock prices need to fluctuate greatly in magnitude to trigger opening or stop loss logic. This may miss some relatively small trend opportunities.

In addition, the current strategy only considers the logic of selecting buying and selling points without integrating capital management, position management and other optimizations. This can lead to unlimited one-sided accumulation, which can easily lead to greater losses due to inability to stop losses in time.

Finally, the combination of RSI and OBV indicators may also have wrong signals. The RSI only considers the speed of rises and falls in stock prices over a certain period of time, and cannot determine long-term trends; The OBV can also become less reliable due to the characteristics of individual stocks. These can all affect the accuracy of strategy signals.  

## Optimization Direction  

In view of the above analysis, the strategy can be optimized in the following aspects:

1. Optimize the width of Bollinger Bands to set adaptive widths to automatically adapt to market volatility.

2. Integrate position management logic to reduce position size when continuous losses occur. And appropriately increase positions when continuous profits occur.  

3. Test and optimize parameters of RSI indicators such as lookback period for rises etc.  

4. Try different short-term indicators such as KDJ, MACD etc. to replace OBV indicators to determine if signal accuracy can be improved.

5. Test different medium and long term indicators such as MVSL, DMI combined with RSI to assist in determining the medium and long term trend of stock prices.

## Conclusion  
The Bollinger Bands RSI OBV strategy comprehensively uses three different types of technical indicators to provide a framework basis for subsequent optimization and improvement while ensuring certain stability and screening criteria. This strategy is suitable for mid-to-long term stock selection and holdings, and can also be used as the basis for short-term strategies to make significant adjustments and optimizations.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|length|
|v_input_2|2|mult|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © atakhadivi

//@version=4
strategy("BB+RSI+OBV", overlay=true)

src = close
obv = cum(sign(change(src)) * volume)
// plot(obv, color=#3A6CA8, title="OnBalanceVolume")

source = close
length = input(20, minval=1)
mult = input(2.0, minval=0.001, maxval=50)
basis = sma(source, length)
dev = mult * stdev(source, length)
upper = basis + dev
lower = basis - dev
buyEntry = source > basis and rsi(close, 14) > 50 and obv[1] < obv 
buyExit = source < lower
sellEntry = source < basis and rsi(close, 14) < 50 and obv[1] > obv
sellExit = source > upper
strategy.entry("BBandLE", strategy.long, stop=lower, oca_name="BollingerBands",comment="BBandLE", when=buyEntry)
strategy.exit(id='BBandLE', when=buyExit)
strategy.entry("BBandSE", strategy.short, stop=upper, oca_name="BollingerBands", comment="BBandSE", when=sellEntry)
strategy.exit(id='BBandSE', when=sellExit)
```

> Detail

https://www.fmz.com/strategy/440339

> Last Modified

2024-01-29 14:49:29

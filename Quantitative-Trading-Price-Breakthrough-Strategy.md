
> Name

Quantitative-Trading-Price-Breakthrough-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](assets/images/ea3164f1b0f7dc1a969e3e22b52591ac0286c82f0a14a87dfd79711eca7e7915.png)
[trans]

## Overview
This strategy is a short-term quantitative trading strategy based on simple moving average (SMA), exponential moving average (EMA), Keltner channel, MACD indicator, and stochastic indicator. It realizes automated trading entry and exit based on whether the price breaks through the SMA and EMA, combined with the long and short signals of the Keltner channel, MACD indicator, and Stochastic indicator.
## Strategy Principle
This strategy uses a 25-period SMA and a 200-period EMA to construct a double moving average indicator. When the price breaks through the double moving average line from bottom to top, a buy signal is generated; when the price breaks through the double moving average line from top to bottom, a sell signal is generated.
At the same time, this strategy uses 10 periods to construct the Keltner channel, and the price breakthrough of the upper and lower rails of the channel will also be used as auxiliary signals. The MACD indicator generates buy and sell signals through the fast line, slow line and MACD histogram. The Stochastic indicator also forms a long and short signal through the golden cross of the %K line and the %D line.
Specifically, when the closing price is higher than the SMA and EMA, and is within the Keltner channel, the MACD histogram is negative, and the Stochastic%K value is lower than 50, a buy signal is generated and a long position is generated; when the closing price is lower than the SMA and EMA, and is within the Keltner channel, the MACD histogram is positive, and the Stochastic%K value is higher than 50, a sell signal is generated and the short position is entered.
## Strategic Advantages
1. Using double moving averages combined with channel indicators can effectively filter out false market breakthroughs.
2. Integrating multiple technical indicator signals can improve the reliability of the signal. 
3. The long and short signal rules are clear and the program execution efficiency is high.
4. Quantitative strategy suitable for short-term frequent trading.
## Strategy Risk and Optimization
1. As a short-term trading strategy, there is a certain risk of excessive trading frequency.
2. There is no stop loss mechanism and there is a greater risk of loss.
3. Consider adding volatility indicators to optimize position opening and stop loss conditions.
4. Can test the pros and cons of different cycle parameters and find the best parameter combination.
## Summarize
This strategy integrates four common technical indicators: moving average, channel indicator, MACD indicator and Stochastic indicator. Judging long and short through price breakthroughs or non-breakthroughs is a typical short-term quantitative trading strategy. Compared with a single indicator, its comprehensive use of multiple indicators can improve signal accuracy and is worthy of further testing and optimization.
||

## Overview

This is a short-term quantitative trading strategy based on Simple Moving Average (SMA), Exponential Moving Average (EMA), Keltner Channels, MACD indicator and Stochastic oscillator. It uses the price breakthrough of SMA and EMA, combined with long and short signals from Keltner Channels, MACD and Stochastic to automate trading entries and exits.

## Strategy Principle  

The strategy uses 25-period SMA, 200-period EMA to build dual moving average lines. When price breaks through the dual moving averages upwards, a buy signal is generated. When price breaks through the dual moving averages downwards, a sell signal is generated.

At the same time, this strategy uses 10-period Keltner Channels. The breakthrough of channel upper and lower bands also serves as assistant signals. The MACD indicator generates trading signals with its fast line, slow line and histogram. The Stochastic oscillator also forms long and short signals with the golden cross and dead cross of its %K line and %D line. 

Specifically, when close price is above both SMA and EMA, and within the Keltner Channels, MACD histogram is negative and Stochastic %K is below 50, a long entry signal is triggered. When close price is below both SMA and EMA, and within the Keltner Channels, MACD histogram is positive and Stochastic %K is above 50, a short entry signal is triggered.

## Strategy Advantages

1. Using dual moving average combined with channel indicator can effectively filter false breakouts.  
2. Integrating signals from multiple technical indicators can improve reliability.
3. Clear long/short rules facilitate programmatic execution efficiency.  
4. Suitable for high-frequency quantitative trading strategies.

## Strategy Risks and Optimization

1. As a short-term trading strategy, it has high trading frequency risks.  
2. No stop loss mechanism exists, leading to large loss risks.
3. Consider adding volatility indicators to optimize entry and stop loss conditions.
4. Different parameter periods can be tested to find optimal combinations.  

## Conclusion

This strategy integrates four commonly used technical indicators - moving averages, channel, MACD and Stochastic. It determines long/short based on price breakthrough, a typical short-term quantitative trading strategy. Compared to single indicator strategies, its multiple indicator combination improves signal accuracy and is worth further testing and optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_low|0|Source: low|high|close|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_1|25|(?Moving Averages)Length SMA|
|v_input_int_2|200|Length EMA|
|v_input_int_3|10|(?Keltner)Length Keltner Channel|
|v_input_2|2|Multiplier|
|v_input_string_1|0|Bands Style: Average True Range|True Range|Range|
|v_input_3|14|ATR Length|
|v_input_int_4|10|(?Stochastic)%K Length|
|v_input_int_5|true|%K Smoothing|
|v_input_int_6|true|%D Smoothing|
|v_input_4|4|(?MACD Fast)Fast Length MACD|
|v_input_5|34|Slow Length MACD|
|v_input_int_7|5|Signal Smoothing MACD|
|v_input_string_2|0|Oscillator MA Type MACD: EMA|SMA|
|v_input_string_3|0|Signal Line MA Type MACD: EMA|SMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-15 00:00:00
end: 2023-12-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © exlux99

//@version=5
strategy(title="Scalping Trading System Crypto and Stocks", overlay=true)
src = input(low, title="Source")

//sma and ema
len = input.int(25, minval=1, title="Length SMA" , group="Moving Averages")
len2 = input.int(200, minval=1, title="Length EMA", group="Moving Averages")

out = ta.sma(src, len)
out2 = ta.ema(src, len2)


//keltner
lengthk = input.int(10, minval=1, title="Length Keltner Channel",group="Keltner")
mult = input(2.0, "Multiplier",group="Keltner")
BandsStyle = input.string("Average True Range", options = ["Average True Range", "True Range", "Range"], title="Bands Style",group="Keltner")
atrlength = input(14, "ATR Length",group="Keltner")

ma = ta.sma(src, lengthk)
rangema = BandsStyle == "True Range" ? ta.tr(true) : BandsStyle == "Average True Range" ? ta.atr(atrlength) : ta.rma(high - low, lengthk)
upper = ma + rangema * mult
lower = ma - rangema * mult

//stoch
periodK = input.int(10, title="%K Length", minval=1,group="Stochastic")
smoothK = input.int(1, title="%K Smoothing", minval=1,group="Stochastic")
periodD = input.int(1, title="%D Smoothing", minval=1,group="Stochastic")
k = ta.sma(ta.stoch(close, high, low, periodK), smoothK)
d = ta.sma(k, periodD)

//macd 1
fast_length = input(title="Fast Length MACD", defval=4,group="MACD Fast")
slow_length = input(title="Slow Length MACD", defval=34,group="MACD Fast")
signal_length = input.int(title="Signal Smoothing MACD",  minval = 1, maxval = 50, defval = 5,group="MACD Fast")
sma_source = input.string(title="Oscillator MA Type MACD",  defval="EMA", options=["SMA", "EMA"],group="MACD Fast")
sma_signal = input.string(title="Signal Line MA Type MACD", defval="EMA", options=["SMA", "EMA"],group="MACD Fast")

fast_ma = sma_source == "SMA" ? ta.sma(src, fast_length) : ta.ema(src, fast_length)
slow_ma = sma_source == "SMA" ? ta.sma(src, slow_length) : ta.ema(src, slow_length)
macd = fast_ma - slow_ma
signal = sma_signal == "SMA" ? ta.sma(macd, signal_length) : ta.ema(macd, signal_length)
hist = macd - signal




long= close > out and close < upper and close > lower and hist < 0 and k < 50 and close > out2 

short= close < out and close < upper and close > lower and hist > 0 and k > 50 and close < out2 

strategy.entry("long",strategy.long,when= long)

strategy.entry("short",strategy.short,when=short)

```

> Detail

https://www.fmz.com/strategy/436219

> Last Modified

2023-12-22 12:42:15

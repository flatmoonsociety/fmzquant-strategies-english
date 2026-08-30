
> Name

Dual-Bollinger-Quant-Options-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The Double Bohr Line quantitative option strategy is an options trading strategy that uses the Double Bohr Line channel and the RSI indicator to generate trading signals. This strategy detects when the market reverses after a violent unilateral move. Although there are fewer signals, it is worth a try. It is recommended to use a 5-minute cycle and trade 5 K lines each time, which is 25 minutes.
## Strategy Principle
This strategy uses two sets of Bohr bands with different parameters simultaneously. The length of the first set of Bohr band parameters is 20, and the standard deviation multiple is 2. The length of the second group of Bohr band parameters is 20, and the standard deviation multiple is 3.
A buy signal is generated when the price is lower than the lower track of the second group of Bol Bands and RSI(14)<=20; a sell signal is generated when the price is higher than the upper track of the second group of Bol Bands and RSI(14)>=80.
According to the Bol Band theory, when the price exceeds the upper and lower rails of the Bol Band, it indicates a greater possibility of a reversal of the current trend. Combining RSI overbought and oversold signals can improve efficiency. Using Double Bohr Bands allows you to capture more reversal opportunities with different parameters.
## Advantage Analysis
- Use double Boer bands to increase the probability of catching reversal opportunities
This strategy uses two sets of Bohr bands with different parameters, making it easier to capture price reversal signals when volatility intensifies. Compared with a single Boer band, it effectively improves the achievability of reversal trading.
- RSI indicator avoids false breakthroughs and filters out invalid signals
The RSI indicator can effectively determine whether the market is overbought and oversold and filter out some invalid breakthrough signals. RSI can complement the Bohr band to improve signal reliability.
- Suitable for capturing dramatic market reversals
Double Bol Bands combined with RSI can quickly capture reversal opportunities after a violent unilateral breakthrough in the market. This type of reversal signal has a large profit potential but does not appear frequently, so it is suitable for trading with options.
- Low trading frequency and controllable drawdowns
This strategy has low transaction frequency and can effectively control transaction retracements and slippage costs. Not pursuing high-frequency trading is also more consistent with the characteristics of options trading.
## Risk Analysis
- There are few signals and there is a possibility of no trading for a long time.
Since this strategy focuses on capturing reversals, there may be fewer signals in sustained trend markets. You need to bear the risk of no transactions within a certain period of time.
- Difficulty generating signals when there is insufficient volatility
When market fluctuations are gentle, it is difficult for prices to break through the upper and lower bands of the Bol Band, resulting in insufficient trading signals. This involves accepting the risk of no trading for a period of time.
- Risk of reversal failure
## Optimization direction
- Optimize Bohr band parameters
Parameter combinations of different lengths and standard deviation multiples can be tested to find the best parameters to improve the strategy effect.
- Add other indicator filters
You can test adding MACD, KD and other indicators to assist in filtering trading signals and improve signal quality.
- Optimize options contract selection
Choosing the appropriate option contract based on market fluctuations can maximize the strategic effect.
- Optimize trading time period selection
Through testing, you can find the best trading time period, avoid invalid signals, and improve the strategy effect.
## Summarize
The double Bohr line quantitative option strategy is generally a low-frequency reversal trading strategy with acceptable results. It uses double Bohr bands to improve the capture probability, and adds the RSI indicator to improve the signal quality. However, this strategy has a low trading frequency and cannot be traded at high frequencies, and there is also a certain risk of reversal failure. The effect of this strategy can be further improved through parameter optimization and adding other filtering indicators. Generally speaking, this strategy is suitable for quantitative traders who pursue stable returns rather than high-frequency trading.

||

## Overview

The Dual Bollinger Quant Options Strategy is an options trading strategy that utilizes double Bollinger Bands and the RSI indicator to generate trading signals. It detects market reversals after aggressive one-sided moves. Although signals are less frequent, it is worth trying. Use 5-minute timeframe and trade for 5 candles, i.e. 25 minutes.

## Strategy Logic

The strategy uses two sets of Bollinger Bands with different parameters simultaneously. The first BBs has length of 20 and multiplier of 2. The second BBs has length of 20 and multiplier of 3. 

A buy signal is generated when price closes below the lower band of the second BBs and RSI(14) <= 20. A sell signal is generated when price closes above the upper band of the second BBs and RSI(14) >= 80.

According to Bollinger Bands theory, closing outside the bands indicates a higher chance of trend reversal. Combining with RSI overbought/oversold signals improves efficiency. Using double BBs captures more reversal opportunities with different parameters.

## Advantage Analysis

- Improved probability of catching reversals with double BBs

The dual BBs increase the chance of catching reversal signals during increased volatility. Using two sets of parameters is more likely to detect reversals than a single BB.

- RSI filters false breaks and invalid signals

RSI effectively judges overbought/oversold levels, filtering some invalid breakout signals. It complements BBs well and improves signal reliability.

- Suitable for catching sharp reversals 

The dual BBs with RSI can quickly capture reversal opportunities after aggressive one-sided moves. Such signals have large profit potential but less frequency, suitable for options trading.

- Low frequency trading controls drawdowns

The low trading frequency effectively controls drawdowns and slippage costs. It also suits the characteristics of options trading.

## Risk Analysis

- Possibility of prolonged no trading

As the strategy focuses on catching reversals, signals may be sparse during persistent trends. There is risk of no trading for some period.

- Difficult to generate signals when volatility is low

When volatility is low, price may fail to breakout of the BB bands, leading to insufficient signals. This carries risk of no trading for some duration.

- Failed reversal risk

Capturing reversals carries the risk of failed reversal. The price may reverse again after giving signal, causing losses. Proper position sizing and stop loss can help manage such risk.

## Optimization Directions 

- Optimize BB parameters

Test different combinations of length and multiplier to find optimal parameters for better performance.

- Add other indicators as filters 

Test adding MACD, KD etc. to filter trading signals and improve quality.

- Optimize options contracts selection

Choose suitable options contracts according to market volatility to maximize strategy performance.

- Optimize trading session selection

Testing can find the best trading sessions to avoid invalid signals and improve results.

## Conclusion

The Dual Bollinger Quant Options Strategy is an average-performing low-frequency mean reversion strategy overall. It improves capture rate with dual BBs and signal quality with RSI. But the low frequency trading limits high frequency trading. There are also risks of failed reversals. Further improvements can be made through optimizations and adding filters. It suits quant traders seeking steady returns over high frequency trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|length1|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_1|2|StdDev|
|v_input_int_2|20|length2|
|v_input_2_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_float_2|3|StdDev|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-27 00:00:00
end: 2023-09-26 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Trade_by_DB


//@version=5
strategy("Double Bollinger Binary Options", overlay=true, margin_long=100, margin_short=100)

// Bollinger bands #1 (20,2)
length1 = input.int(20, minval=1)
src1 = input(close, title="Source")
mult1 = input.float(2.0, minval=0.001, maxval=50, title="StdDev")
basis1 = ta.sma(src1, length1)
dev1 = mult1 * ta.stdev(src1, length1)
upper1 = basis1 + dev1
lower1 = basis1 - dev1

//Bollinger bands #2
length2 = input.int(20, minval=1)
src2 = input(close, title="Source")
mult2 = input.float(3.0, minval=0.001, maxval=50, title="StdDev")
basis2 = ta.sma(src2, length2)
dev2 = mult2 * ta.stdev(src2, length2)
upper2 = basis2 + dev2
lower2 = basis2 - dev2


//Buy Condition
buy = close < lower2 and ta.rsi(close,14) <=20
sell = close > upper2 and ta.rsi(close,14) >=80

// plotshape(buy, style = shape.arrowup , color = color.green, location = location.belowbar)
// plotshape(sell, style = shape.arrowdown , color = color.red, location = location.abovebar)





if (buy)
    strategy.entry("CALL", strategy.long)


if (sell)
    strategy.entry("PUT", strategy.short)

```

> Detail

https://www.fmz.com/strategy/427986

> Last Modified

2023-09-27 16:19:30

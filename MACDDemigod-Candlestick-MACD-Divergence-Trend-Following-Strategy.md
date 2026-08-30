
> Name

Pythagorean Candlestick MACD Indicator Divergence Trend Following Strategy Demigod-Candlestick-MACD-Divergence-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ba794f72ecc2a8cb19.png)
[trans]

### Overview
This strategy calculates the MACD indicator and its MACD bar line, detects the divergence signal between the MACD bar line and the price trend, and then generates trading signals. A bearish divergence signal is generated when a new price high is detected but the MACD histogram does not make a new high; a bullish divergence signal is generated when a new price low is detected but the MACD histogram does not make a new low. Combined with the ATR indicator, set stop loss and take profit levels to conduct trend following transactions.
### Strategy Principles
The core principle of this strategy is to use the characteristics of the MACD indicator and its MACD bar line to reflect changes in price trends, and to detect the divergence signal between the MACD bar line and the price as a trigger condition for trading signals.
Specifically, the strategy first calculates the MACD line, Signal line and MACD-Histogram. Then by defining the fractal function, detect the peaks and valleys of the MACD histogram and extract the local maximum and minimum points. Combined with the highest price and lowest price of the price, determine whether there is a divergence between the MACD histogram and the price.
When the price reaches a new high, but the MACD histogram does not reach a new high, the regulark_bearish_div bearish divergence signal is generated; when the price reaches a new low, but the MACD histogram does not reach a new low, the regulark_bullish_div bullish divergence signal is generated.
Finally, when the bearish divergence and bullish divergence signals are generated, the strategy issues short and long orders respectively, and exits the position with ATR stop loss and take profit.
### Advantage Analysis
This strategy has several advantages:
1. Use the divergence characteristics between the MACD histogram and price to capture changes in price trends in advance.
2. The ATR stop-loss and stop-profit settings are reasonable and can effectively control the maximum loss of a single transaction.
3. Use trend following methods to lock in profits to the maximum extent.
4. Reasonable parameter settings can filter out some noisy trading signals.
5. The strategy logic is clear and easy to understand and easy to verify.
### Risk Analysis
There are also some risks with this strategy:
1. MACD divergence may not necessarily bring about price reversal, and there is a certain risk of false signals.
2. Unreasonable stop-loss and stop-profit settings may lead to excessive losses or small profits.
3. The divergence signal period is too short, which may be caused by noise and should be filtered appropriately.
4. Mismatch between transaction types and parameter settings will also affect the strategy effect.
Corresponding solutions:
1. Appropriately increase the divergence length and divergence amplitude requirements to filter out false signals.
2. Use ATR as a stop-loss and take-profit indicator, and adjust the ATR multiple to control the risk of a single transaction.
3. Select different parameters for different trading varieties. Carry out parameter optimization and find the best parameter combination.

### Optimization direction
This strategy can also be optimized from the following directions:
1. More complex divergence confirmation, such as Volume divergence confirmation.
2. Optimize MACD parameters and find the best parameter combination.
3. Optimize the multiple of ATR stop loss and take profit.
4. Add machine learning algorithms to assist in judging the reliability of divergence signals.
5. Add model predictions to determine the probability of price reversal.
6. Dynamically adjust strategy parameters according to changes in the market environment.
### Summarize
In general, the Pythagoras candlestick MACD indicator deviates from the trend following strategy and uses the divergence characteristics between the MACD bar line and price to achieve trend capture. The ATR stop-loss and stop-profit settings are reasonable and can control the risk of a single transaction. The logic of this strategy is clear and easy to understand, and it is worthy of actual testing. In the future, strategies can be optimized from many aspects to obtain better results.
||

### Overview  

This strategy calculates the MACD indicator and its MACD histogram to detect divergence signals between the MACD histogram and price movement, thereby generating trading signals. When a new high in price but no new high in MACD histogram is detected, a bearish divergence signal is generated. When a new low in price but no new low in MACD histogram is detected, a bullish divergence signal is generated. Combined with ATR indicator for stop loss and take profit, it carries out trend following trades.

### Strategy Logic   

The core principle of this strategy is to utilize the MACD indicator and its MACD histogram to reflect changes in price trends, and detect divergence signals between the MACD histogram and price as the trigger condition for trading signals.  

Specifically, the strategy first calculates the MACD line, Signal line and MACD histogram. Then by defining the fractal function to detect peaks and valleys of the MACD histogram to extract local maximums and minimums. Combined with the highest price and lowest price, it determines whether there is a divergence between the MACD histogram and price.  

When price reaches a new high but MACD histogram does not reach a new high, a regular_bearish_div bearish divergence signal is generated. When price drops to a new low but MACD histogram does not drop to a new low, a regular_bullish_div bullish divergence signal is generated.   

Finally, when bearish and bullish divergence signals are generated, the strategy issues short and long orders respectively, and exits positions with ATR stop loss and take profit.

### Advantage Analysis   

This strategy has the following advantages:  

1. By utilizing the divergence feature between MACD histogram and price, it can capture turns in price trends early.  

2. The ATR stop loss and take profit settings are reasonable to effectively control maximum loss per trade.

3. Using trend following method can maximize locked profit.  

4. Reasonable parameter settings filter out some noisy trading signals.   

5. The strategy logic is clear and easy to understand, easy to validate in live trading.

### Risk Analysis   

This strategy also has some risks:   

1. MACD divergence does not necessarily lead to price reversal, there are some false signal risks.

2. Unreasonable stop loss and take profit settings may lead to excessive losses or insufficient profits.  

3. Divergence signals with short cycles may be caused by noise and should be filtered properly.  

4. Incompatible trading products and parameter settings will also affect strategy performance.

Corresponding solutions:  

1. Increase the length and magnitude requirements of divergence to filter false signals.

2. Use ATR as stop loss and take profit benchmark, adjust ATR multiples to control risks per trade.  

3. Select different parameters for different trading products.  Perform parameter optimization to find optimum parameter combinations.

### Optimization Directions   

This strategy can also be optimized in the following directions:  

1. More complex divergence confirmation, such as volume divergence confirmation.  

2. Optimize MACD parameters to find the best parameter combination.  

3. Optimize the multiples of ATR stop loss and take profit.   

4. Add machine learning algorithms to assist in judging reliability of divergence signals.  

5. Add model prediction to determine probability of price reversal.

6. Dynamically adjust strategy parameters according to market condition changes.  

### Summary   

In summary, this Demigod Candlestick MACD Divergence Trend Following Strategy utilizes the divergence between MACD histogram and price to capture trends. The reasonable ATR stop loss and take profit settings can control risks per trade. The strategy logic is clear and easy to understand, worth validating in live trading. Follow up optimizations can be made in many aspects to obtain better results.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|13|(?CDMA)fast Length|
|v_input_int_2|34|slow Length|
|v_input_source_1_close|0|source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_3|9|ma Length|
|v_input_int_4|5|(?Divergence)Divergenc Length|
|v_input_float_1|2|Divergenc Strength|
|v_input_int_5|13|(?ATR)ATR Length|
|v_input_float_2|true|ATR multyple|
|v_input_color_1|teal|upper color|
|v_input_color_2|red|under color|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-04 00:00:00
end: 2024-02-03 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © bigwin_sun
// copyright： Tradingvue Limited    

//@version = 5
strategy(title = "Demigod : CDMA histogram Divergence strategy", shorttitle = "Demigod strategy", overlay = false, pyramiding = 100)

//macd input
fastMA = input.int(13, title = "fast Length", minval = 1,     group = "CDMA")
slowMA = input.int(34, title = "slow Length", minval = 1,     group = "CDMA")
src          = input.source(title = "source", defval = close, group = "CDMA")
signalSmooth = input.int(9, title="ma Length", minval = 1,    group = "CDMA")
//Divergenc
divLength    = input.int(title = "Divergenc Length",   defval = 5, minval = 1,   maxval = 50,  inline = "ATRLength",  group = "Divergence")
divStren     = input.float(title="Divergenc Strength", defval = 2, minval = 1.0, maxval = 5.0, inline = "ATRLength",  group = "Divergence")

//atr input
atrLength = input.int(13, title = "ATR Length", minval = 1,   inline = "ATRLength", group = "ATR")
m         = input.float(1.0,  "ATR multyple",   minval = 0.5, inline = "ATRLength", group = "ATR", step = 0.5)
collong   = input.color(color.teal, title = "upper color",  inline = "ATR显示", group = "ATR")
colshort  = input.color(color.red,  title = "under color",  inline = "ATR显示", group = "ATR")

// MACD---------------------------------------------------------------------------------------------------------------------------------
DivOffset = -2
macdLine   = ta.ema(src, fastMA) - ta.ema(src, slowMA)    
signalLine = ta.ema(macdLine, signalSmooth)
histogram  = macdLine - signalLine

histogramColor = if histogram > 0
    histogram > histogram[1] ? color.lime : color.green
else 
    histogram < histogram[1] ? color.maroon : color.red

// cdma histogram
plot(histogram, title = "MACD histogram", linewidth = 2, style = plot.style_histogram, color = histogramColor)
plot(0,         title = "zero line",      linewidth = 1,                               color = color.gray)

// Divergenc calculation-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
//peak / valley fundation
f_top_fractal(_src)=>_src[4] < _src[2] and _src[3] < _src[2] and _src[2] > _src[1] and _src[2] > _src[0] and _src > 0
f_bot_fractal(_src)=>_src[4] > _src[2] and _src[3] > _src[2] and _src[2] < _src[1] and _src[2] < _src[0] and _src < 0
f_fractalize(_src)=>f_top_fractal(_src) ? 1 : f_bot_fractal(_src) ? -1 : 0

//peak / valley value
fractal_top1 = f_fractalize(histogram) > 0 ? true : false //histogram[2] : na
fractal_bot1 = f_fractalize(histogram) < 0 ? true : false //histogram[2] : na

//previouse peak or valley
high_prev1  = ta.valuewhen(fractal_top1, histogram[2], 0)[2]
high_price1 = ta.valuewhen(fractal_top1, high[2], 0)[2]
low_prev1   = ta.valuewhen(fractal_bot1, histogram[2], 0)[2]
low_price1  = ta.valuewhen(fractal_bot1, low[2], 0)[2]

//Divergenc : cdma histogram against candle value
regular_bearish_div1 = high[2] > high_price1 + divStren and histogram[2] < high_prev1 / divStren and ta.barssince(fractal_top1[1]) > divLength
regular_bullish_div1 = low[2]  < low_price1 - divStren  and histogram[2] > low_prev1 / divStren  and ta.barssince(fractal_bot1[1]) > divLength

//-------------------------cdma Divergenc range------------------------------------------------
//histogramColor
col1 = regular_bearish_div1 ? color.red : na
col2 = regular_bullish_div1 ? #00FF00EB : na
//plot
plot(title='看跌背离', series= fractal_top1 ? histogram[2] : na, color=col1, linewidth=3, offset=DivOffset)
plot(title='看涨背离', series= fractal_bot1 ? histogram[2] : na, color=col2, linewidth=3, offset=DivOffset)

// calculate ATR				--------------------------------------------------------------------------------------------------------------------------------------------------
atr = ta.ema(ta.tr(true), atrLength) * m
up = atr + high
dw = low - atr

//stratety : enrty and exit---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
if regular_bearish_div1 and fractal_top1
//if regular_bullish_div1 and fractal_bot1
    //label.new(bar_index, histogram[2], text = "Short", textcolor = color.white, color = color.gray,  style = label.style_label_lower_left)
    strategy.entry("Short", strategy.short, qty = 1)
    strategy.exit("exitShort", "Short", stop = up, limit = dw - atr)
if regular_bullish_div1 and fractal_bot1
//if regular_bearish_div1 and fractal_top1   
    //label.new(bar_index, histogram[2], text = "Long", textcolor = color.white, color = color.fuchsia, style = label.style_label_upper_left)
	strategy.entry("Long", strategy.long, qty = 1)
    strategy.exit("exitLong", "Long", stop = dw, limit = up + atr)

```

> Detail

https://www.fmz.com/strategy/440981

> Last Modified

2024-02-04 15:06:58

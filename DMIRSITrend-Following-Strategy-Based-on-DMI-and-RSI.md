
> Name

Trend-Following-Strategy-Based-on-DMI-and-RSI
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/9ff6db2f6fac0511046798eb84bda6745ba034ebf73e143250ac9be514e705a7.png)
 [trans]
##Overview
This strategy combines the DMI indicator to determine the trend direction and the RSI indicator to determine overbought and oversold, realizing a relatively complete trend following trading strategy. When the DMI indicator determines that there is a trend, and the RSI indicator shows overbought or oversold, it corresponds to going long or short. At the same time, a trailing stop is set to lock in profits.
##Strategy Principle
1. Use the DMI indicator to determine the trend direction
   - DMI consists of three curves: +DI indicates an upward trend, -DI indicates a downward trend, and ADX determines the strength of the trend.
   - When +DI>-DI, it is an upward trend, go long; when -DI>+DI, it is a downward trend, go short
2. Use RSI indicator to determine overbought and oversold
   - RSI determines whether it is overbought or oversold by comparing the average closing increase and decrease over a period of time
   - RSI below 30 is oversold, above 70 is overbought
3. Combined with DMI to determine the trend direction and RSI to determine overbought and oversold, you can better grasp the market rhythm.
   - When DMI determines that there is an upward trend and RSI is oversold, it is a better opportunity to go long.
   - When DMI determines that there is a downward trend and RSI is overbought, it is a better opportunity to short.
4. Set a trailing stop to lock in profits
##Advantage analysis
This is a relatively mature and stable trend following strategy with the following advantages:
1. Combine trend judgment and overbought and oversold judgment to avoid frequent trading in volatile markets
2. Using popular indicators DMI and RSI, parameter selection is easy and fully verified in practice.
3. Set a trailing stop to lock in profits and avoid stop losses to a certain extent.
4. The rules are clear and easy to understand, the program is simple to implement, and easy to practice
##Risk Analysis
There are also some risks to be aware of with this strategy:
1. Both DMI and RSI are prone to generating false signals, which may lead to unnecessary losses.
2. Improper setting of trailing stop may result in premature stop loss or excessive stop loss.
3. Unable to effectively filter volatile market conditions, making it easy to get trapped
4. Follow the trend strategy and fail to stop losses in time when the trend reverses.
##Optimization direction
This strategy can also be optimized from the following aspects:
1. Combine with volatility indicators to filter volatile market conditions
2. Combine candle form judgment to avoid false breakthroughs
3. Set appropriate stop losses near key support and resistance levels to limit losses
4. Add machine learning model to judge trend python
5. Dynamically optimize the parameters of DMI and RSI
##Summary
This strategy is overall a relatively stable and practical trend following strategy. It uses DMI to determine the trend direction and RSI to determine overbought and oversold, thereby seizing medium and long-term trading opportunities. Also set a trailing stop to lock in profits. The strategy parameters are simple to select, the trading rules are clear, and it is easy to practice. However, there is also the risk of being trapped and not stopping the loss promptly enough. Through some parameter and model optimization, the effect of this strategy can be made better.
|| 

##Overview
This strategy combines the DMI indicator to determine the trend direction and the RSI indicator to determine overbought and oversold conditions, implementing a relatively complete trend following trading strategy. When the DMI indicator judges that a trend appears and the RSI indicator shows overbought or oversold, long or short positions are taken accordingly. At the same time, a moving stop loss is set to lock in profits.

##Strategy Logic  
1. Use DMI indicator to judge trend direction
   - DMI consists of three lines: +DI indicates uptrend, -DI indicates downtrend, ADX judges strength of the trend  
   - When +DI>-DI, it is an uptrend, go long; when -DI>+DI, it is a downtrend, go short
2. Use RSI indicator to judge overbought and oversold
   - RSI compares average gain and loss over a period to determine overbought or oversold
   - RSI below 30 is oversold, above 70 is overbought
3. Combining DMI to determine trend direction and RSI for overbought/oversold can better capture market rhythm
   - When DMI shows uptrend and RSI oversold, good timing for long
   - When DMI shows downtrend and RSI overbought, good timing for short
4. Set moving stop loss to lock in profits  

##Advantage Analysis 
This is a relatively mature and steady trend following strategy with the following strengths:
1. Combining trend and overbought/oversold avoids frequent trading in range-bound market
2. Popular indicators DMI and RSI with easy parameter tuning and thorough practical verification
3. Trailing stop loss locks in profits and avoids stop loss to some extent  
4. Clear and easy rules, simple to implement

##Risk Analysis
There are also some risks to note:
1. DMI and RSI can easily generate false signals, causing unnecessary losses
2. Improper trailing stop loss setting may stop loss too early or too much
3. Cannot effectively filter whipsaw markets, prone to being trapped
4. Trend following fails to exit promptly when trend reverses  

##Optimization Directions
The strategy can be optimized in the following aspects:
1. Add volatility filter to avoid choppy market
2. Combine candlestick patterns to avoid false breakout 
3. Set proper stop loss near key support/resistance to limit losses
4. Increase machine learning model for trend prediction
5. Dynamic optimization of DMI and RSI parameters

##Summary
Overall this is a relatively steady and practical trend following strategy. By judging trend direction with DMI and overbought/oversold levels with RSI, it captures medium-to-long term trading opportunities. Trailing stop loss locks in profits. The strategy has simple parameter tuning, clear rules and is easy to implement. But risks include being trapped and untimely stop loss. With some parameter and model optimization, performance can be further improved.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|ADX Smoothing|
|v_input_int_2|14|DI Length|
|v_input_float_1|0.5|Trailing Stop Loss Factor|
|v_input_int_3|14|RSI Length|
|v_input_1_close|0|RSI Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_4|70|RSI Overbought Level|
|v_input_int_5|30|RSI Oversold Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-24 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © YingYangJPN

//@version=5
strategy("DMI and RSI Strategy", overlay=true, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// DMI indikatörünü tanımlayalım
lensig = input.int(14, title="ADX Smoothing", minval=1, maxval=50)
len = input.int(14, minval=1, title="DI Length")
up = ta.change(high)
down = -ta.change(low)
plusDM = na(up) ? na : (up > down and up > 0 ? up : 0)
minusDM = na(down) ? na : (down > up and down > 0 ? down : 0)
trur = ta.rma(ta.tr, len)
plus = fixnan(100 * ta.rma(plusDM, len) / trur)
minus = fixnan(100 * ta.rma(minusDM, len) / trur)
sum = plus + minus
adx = 100 * ta.rma(math.abs(plus - minus) / (sum == 0 ? 1 : sum), lensig)
trailing_stop_loss_factor = input.float(0.50, "Trailing Stop Loss Factor", step = 0.01)

// RSI indikatörünü tanımlayalım
rsiLength = input.int(14, minval=1, title="RSI Length")
rsiSource = input(close, title="RSI Source")
rsiOverbought = input.int(70, title="RSI Overbought Level")
rsiOversold = input.int(30, title="RSI Oversold Level")
rsiValue = ta.rsi(rsiSource, rsiLength)

// Uzun pozisyon açma koşullarını tanımlayalım
longCondition1 = rsiValue < rsiOversold // RSI oversold seviyesinin altındaysa
longCondition2 = adx > 20 // ADX 20'den büyükse
longCondition3 = minus > plus

// Kısa pozisyon açma koşullarını tanımlayalım
shortCondition1 = rsiValue > rsiOverbought // RSI overbought seviyesinin üstündeyse
shortCondition2 = adx > 20 // ADX 20'den büyükse
shortCondition3 = plus > minus

// Uzun pozisyon açalım
if longCondition1 and longCondition2 and longCondition3
    strategy.entry("Long", strategy.long)
    

// Kısa pozisyon açalım
if shortCondition1 and shortCondition2 and shortCondition3
    strategy.entry("Short", strategy.short)
    
// Trailing Stop Loss
longTrailingStopLoss = strategy.position_avg_price * (1 - trailing_stop_loss_factor / 100)
shortTrailingStopLoss = strategy.position_avg_price * (1 + trailing_stop_loss_factor / 100)
if strategy.position_size > 0 
    strategy.exit("Exit Long", "Long", stop  = longTrailingStopLoss)
if strategy.position_size < 0 
    strategy.exit("Exit Short", "Short", stop = shortTrailingStopLoss)

// DMI ve RSI indikatörlerini grafiğe çizelim
plot(adx, color=#F50057, title="ADX")
plot(plus, color=#2962FF, title="+DI")
plot(minus, color=#FF6D00, title="-DI")
plot(rsiValue, color=#9C27B0, title="RSI")
hline(rsiOverbought, title="RSI Overbought Level", color=#E91E63, linestyle=hline.style_dashed)
hline(rsiOversold, title="RSI Oversold Level", color=#4CAF50, linestyle=hline.style_dashed)


```

> Detail

https://www.fmz.com/strategy/439994

> Last Modified

2024-01-25 15:56:41

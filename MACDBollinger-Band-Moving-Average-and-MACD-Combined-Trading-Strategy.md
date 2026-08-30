
> Name

Bollinger-Band-Moving-Average-and-MACD-Combined-Trading-Strategy based on Bollinger Band Moving Average and MACD
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/df4135597a79bd2fc851b345557c6e42cda4b2953d0d1efb3807955ff2534a6e.png)
[trans]

## Strategy Overview
This strategy combines three indicators: Bollinger Bands, Moving Averages and MACD to form a relatively complete trading system. While it can judge market trends, it can also seize some reversal opportunities.
## Strategy name and principle
The name of this strategy is "Triangle Anchoring Trend Following Strategy". The name highlights its characteristic of using three technical indicators at the same time when judging the trend direction and anchoring the market entry point.
Its basic trading logic is:
1. Determine the trend direction. By comparing the middle track of the Bollinger Bands, the EMA moving average and the zero axis of MACD, we can determine whether the current market is in the bull stage or the short stage.
2. Find opportunities to enter the market. After determining the long (or short) trend, the strategy will determine market entry based on whether the EMA moving average breaks through the Bollinger Band and whether the MACD column line breaks through the signal line in a positive (or negative) direction.
3. Set take profit and stop loss. After entering the market, fixed take-profit and stop-loss levels will be preset.
## Strategic advantage analysis
The biggest advantage of this strategy is that it uses three different types of technical indicators, including trend, moving average and MACD, to guide decision-making. This allows it to more accurately judge market trends and is more conducive to seizing some reversal opportunities.
First of all, the middle trajectory of Bollinger Bands can clearly reflect the main trend direction of the current stage. The role of the EMA moving average is to track the trend. Their comparison and combination can more accurately judge the current long and short conditions.
Secondly, Bollinger Bands itself has relatively strong inclusiveness. A certain level of support and pressure is also reflected near the mid-rail line, so the breakthrough of the EMA line has certain signal value.
Furthermore, the addition of MACD also shows the rise and fall of long and short energy. Its absolute value represents the high or cold mood of the masses, and can also indicate the possibility of reversal.
Finally, the strategy presets stop-profit and stop-loss conditions, which can control the risk and return of a single transaction to ensure overall stable operation.
## Strategy risk analysis
Although this strategy uses a combination of analytical tools, there are still the following major risks:
1. The Bollinger Band parameters are improperly set, and the middle track cannot clearly reflect the main trend.
2. The moving average system sends a bullish signal, but MACD has not clearly turned positive, and the power of shorts may expand.
3. If the stop-profit and stop-loss range is set too large, a single loss may expand.
The main solution ideas are:
1. Adjust the Bollinger Band parameters to ensure that the mid-rail line effectively reflects the main trend.
2. Introduce more technical indicators to judge long and short energy.
3. Evaluate historical trading conditions and optimize take-profit and stop-loss parameters.
## Strategy optimization direction
This strategy can be further optimized from the following aspects:
1. Introduce more indicators into trend judgment. Such as KDJ, ATR, etc. to assist judgment and improve judgment accuracy.
2. Set up more detailed stop loss methods at the operational level. Such as moving stop loss, increasing the stop loss ratio after breaking through new highs (lows), etc.
3. Evaluate the performance effects of different varieties. Adjust parameters to adapt to more market characteristics.
4. Test effectiveness and evaluate backtest results on different time frames and markets. Adjust parameters accordingly.
5. Add machine learning algorithms to realize automatic optimization of parameters and dynamic updating of policy rules.
## Summarize
This strategy uses three major technical indicators: Bollinger Bands, Moving Averages and MACD. It clearly determines the trend, has a certain tolerance, and can also seize some reversal opportunities. By introducing more auxiliary tools to judge and optimize stop-profit and stop-loss strategies, it is expected to achieve more stable trading performance. This strategy deserves further evaluation and improvement, and is expected to become a powerful tool for quantitative decision-making.
||

## Strategy Overview  

This strategy combines Bollinger Band, moving average and MACD, forming a relatively complete trading system. While judging the market trend, it can also capture some reversal opportunities.

## Strategy Name & Rationale

The strategy is named "Triangle Anchoring Trend Tracking Strategy". The name highlights its use of three technical indicators to determine trend direction and anchor entry points.  

The basic trading logic is:

1. Judge trend direction. Compare Bollinger Mid Band, EMA and MACD zero line to determine if the market is in an uptrend or downtrend phase.

2. Find entry opportunities. After a trend is identified, the strategy checks if EMA crosses BB Mid Band and if MACD histogram crosses signal line to determine entries.

3. Set profit target and stop loss. Once entered, fixed target and stop loss levels are preset.

## Advantage Analysis

The biggest advantage of this strategy is the simultaneous use of trend, moving average and MACD tools to guide decisions. This allows more accurate judgments of market momentum and also helps capture some reversals.

Firstly, BB Mid Band clearly reflects the current primary trend direction. The role of EMA is to track the progress of trends. Their comparison and combination enables more precise trend identification.  

Secondly, BB itself has strong envelope characteristics. The area around the mid band also indicates certain support/resistance levels. Hence EMA crossovers have signal value. 

Additionally, the MACD measures the wax and wane of bullish/bearish momentum. Its absolute size represents high or low crowd emotions, also hinting potential reversals.   

Finally, the pre-set profit target and stop loss controls risk/reward of individual trades, ensuring overall stability.

## Risk Analysis

Despite the use of multiple analytical tools, main risks are:

1. Improper BB parameters fail to clearly reflect the primary trend.  

2. EMA system signals long but MACD does not clearly turn positive, bearish forces may expand.

3. Profit target/stop loss range too wide, single trade loss widens.

Main solutions are:

1. Adjust BB parameters to ensure mid band effectively reflects main trend.

2. Introduce more technical indicators to judge bull/bear momentum.  

3. Evaluate historical trades and optimize profit target/stop loss.

## Optimization Directions

The strategy can be further improved in the following aspects:

1. Introduce more indicators like KDJ, ATR etc to aid trend judgment and improve accuracy.

2. Implement more sophisticated stops like trailing stop, breakout stop etc.  

3. Assess performance across different products. Fine tune parameters to suit various market conditions.

4. Test and tweak strategy based on backtest results over different timeframes and markets.

5. Incorporate machine learning for automatic parameter optimization and dynamic strategy update.  

## Conclusion  

This strategy leverages BB, MA and MACD together. It has clear trend judgment, certain envelope characteristics and also captures some reversals. With more auxiliary tools for judging entries/exits, it can achieve more reliable performance. Further evaluation and enhancement of this strategy is warranted and expected to produce a robust quantitative tool.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|150|BB Length|
|v_input_2_close|0|BB Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|2|BB StdDev|
|v_input_4|34|EMA Length|
|v_input_5_close|0|EMA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_6|SMA|Method|
|v_input_7|5|Length|
|v_input_8|9|Fast Length|
|v_input_9|17|Slow Length|
|v_input_10_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_1|9|Signal Smoothing|
|v_input_string_1|0|Oscillator MA Type: EMA|SMA|
|v_input_string_2|0|Signal Line MA Type: EMA|SMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-04 00:00:00
end: 2024-02-03 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Combined Strategy", overlay=true, shorttitle="Comb Strat", default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// Precio de beneficio y Stop Loss
takeProfitTicks = 87636
stopLossTicks = 53350

// Bollinger Bands + EMA
length_bb = input(150, title="BB Length")
src_bb = input(close, title="BB Source")
mult = input(2.0, title="BB StdDev")
basis = ta.sma(src_bb, length_bb)
dev = mult * ta.stdev(src_bb, length_bb)
upper = basis + dev
lower = basis - dev

len_ema = input(34, title="EMA Length")
src_ema = input(close, title="EMA Source")
out_ema = ta.ema(src_ema, len_ema)

typeMA = input("SMA", title="Method")
smoothingLength = input(5, title="Length")

var float smoothingLine = na
if (typeMA == "SMA")
    smoothingLine := ta.sma(out_ema, smoothingLength)
else if (typeMA == "EMA")
    smoothingLine := ta.ema(out_ema, smoothingLength)

// MACD
fast_length = input(title="Fast Length", defval=9)
slow_length = input(title="Slow Length", defval=17)
src_macd = input(title="Source", defval=close)
signal_length = input.int(title="Signal Smoothing", minval=1, maxval=50, defval=9)
sma_source = input.string(title="Oscillator MA Type", defval="EMA", options=["SMA", "EMA"])
sma_signal = input.string(title="Signal Line MA Type", defval="EMA", options=["SMA", "EMA"])

fast_ma = sma_source == "SMA" ? ta.sma(src_macd, fast_length) : ta.ema(src_macd, fast_length)
slow_ma = sma_source == "SMA" ? ta.sma(src_macd, slow_length) : ta.ema(src_macd, slow_length)
macd = fast_ma - slow_ma
signal = sma_signal == "SMA" ? ta.sma(macd, signal_length) : ta.ema(macd, signal_length)
hist = macd - signal

// Condiciones de compra y venta
longCondition = (out_ema > basis) and (macd > signal) and (signal > 0)
shortCondition = (out_ema < basis) and (macd < signal) and (signal < 0)

// Variables de estado
var bool longExecuted = na
var bool shortExecuted = na

// Estrategia
if (longCondition and not longExecuted)
    strategy.entry("Long", strategy.long)
    longExecuted := true
    shortExecuted := na
if (shortCondition and not shortExecuted)
    strategy.entry("Short", strategy.short)
    shortExecuted := true
    longExecuted := na

// Take Profit y Stop Loss para Compras y Ventas Cortas
strategy.exit("Take Profit/Close Long", from_entry="Long", profit=takeProfitTicks, loss=stopLossTicks)
strategy.exit("Take Profit/Close Short", from_entry="Short", profit=takeProfitTicks, loss=stopLossTicks)

// Cierre de posiciones cuando la dirección cambia
if ((out_ema < basis) and (macd < signal))
    strategy.close("Long")
    longExecuted := na
if ((out_ema > basis) and (macd > signal))
    strategy.close("Short")
    shortExecuted := na

// Plots
plot(basis, "BB Basis", color=#FF6D00)
plot(upper, "BB Upper", color=color.new(#2962FF, 0.5))
plot(lower, "BB Lower", color=color.new(#2962FF, 0.5))

plot(smoothingLine, title="Smoothing Line", color=#f37f20, linewidth=2)

hline(0, "Zero Line", color=color.new(#787B86, 50))
plot(hist, title="Histogram", style=plot.style_columns, color=(hist >= 0 ? (hist[1] < hist ? color.green : color.red) : (hist[1] < hist ? color.red : color.green)))
plot(macd, title="MACD", color=color.blue)
plot(signal, title="Signal", color=color.orange)

```

> Detail

https://www.fmz.com/strategy/440995

> Last Modified

2024-02-04 15:42:23

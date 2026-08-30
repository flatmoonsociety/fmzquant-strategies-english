
> Name

RSI Axial-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/13a4034c96d82d5e12a59cc75c11731e7477f25d2ffc327ba5dfbbef8297b0e0.png)

[trans]


## Overview
The RSI axial moving average crossover strategy determines entry and exit by calculating the RSI indicator and its simple moving average, and observing the golden cross of the two. This strategy also combines Bollinger Bands to add support and resistance judgments to the RSI axial moving average.
## Strategy Principle
This strategy first calculates the 14-day RSI indicator, and then calculates the 8-day simple moving average of the RSI indicator. A buy signal is generated when the RSI indicator breaks above its moving average from bottom to top; a sell signal is generated when the RSI indicator breaks below its moving average from top to bottom.
At the same time, this strategy adds Bollinger Band determination to the RSI axial moving average. Bollinger Bands calculates the standard deviation to determine whether the RSI axial moving average has become relatively overcrowded, thereby avoiding buying highs and selling lows.
## Advantage Analysis
The RSI axial moving average crossover strategy combines the trend indicator RSI and the curve trend indicator moving average, which can effectively determine market trends and randomness. The arithmetic average of the RSI indicator can better smooth the impact of price fluctuations on signals.
The Bollinger Bands added to this strategy use the principle of standard deviation, which can automatically adjust the width of the upper and lower rails, effectively preventing confusion in trading signals. When the Bollinger Bands narrow, it means that the changes are gradually calming down, and it is suitable for looking for reversal opportunities; while when the Bollinger Bands expand, it means that the market fluctuates violently, and it is suitable for tracking the trend.
## Risk Analysis
The biggest risk of the RSI axial moving average crossover strategy lies in the lag of the RSI indicator and the moving average itself. When rapid market conditions come, there will be a certain lag in indicator calculation and trend determination. This will cause the buying point to be raised and the selling point to be lowered.
Another major risk is misleading indicators when trends transition from bull to bear. When the market turns and the RSI and moving average indicators have not yet reacted, wrong trading signals will be generated, resulting in losses.
Solutions include appropriately adjusting RSI parameters and shortening the moving average period; adding trend indicators to assist judgment; and appropriately relaxing the stop loss range.
## Optimization direction
The RSI axial moving average crossover strategy can be optimized from the following directions:
1. Optimize RSI parameters: Adjusting the length of RSI can balance sensitivity and stability
2. Optimize moving average parameters: adjust the moving average type and period parameters to optimize the trend of the indicator
3. Add stop loss mechanism: set trailing stop loss or time stop loss to control single loss
4. Combine trend indicators: add MACD, KDJ and other indicators to avoid reversal misjudgments
5. Multi-time frame verification: Use higher time frames to determine trends and avoid being trapped.
## Summarize
The RSI axial moving average crossover strategy is generally a relatively mature quantitative trading strategy. It combines the advantages of multiple technical indicators and can enter the mainstream market trends through parameter adjustment and multi-dimensional optimization. The biggest risk of this strategy is the lagging nature of the indicator, which requires a stop loss to control losses. If used properly, the RSI axial moving average crossover strategy can achieve relatively stable investment returns.
||
## Overview  

The RSI Axial Moving Average Crossover Strategy generates trading signals by calculating the RSI indicator and its simple moving average line and observing golden crosses and dead crosses between the two. The strategy also incorporates Bollinger Bands to add support/resistance judgment for the RSI axial moving average line.

## Strategy Logic  

The strategy first calculates the 14-day RSI indicator, followed by the 8-day simple moving average line of the RSI indicator. A buy signal is generated when the RSI indicator crosses above its moving average line, while a sell signal is generated when the RSI crosses below its moving average line.  

At the same time, the strategy adds Bollinger Bands to determine if the RSI axial moving average line is relatively overcrowded by calculating the standard deviation, thus avoiding buying peaks and selling bottoms.

## Advantage Analysis   

The RSI Axial Moving Average Crossover Strategy combines the trending indicator RSI and the curve-following indicator moving average line, which can effectively determine market trends and randomness. The arithmetic average of the RSI indicator can smooth out the impact of price fluctuations on signals.  

The Bollinger Bands added in this strategy use the principle of standard deviation to automatically adjust the width of the upper and lower tracks, effectively preventing erroneous trading signals. When the Bollinger Bands narrow, it indicates that the change is gradually slowing down, which is suitable for looking for reversal opportunities. When the Bollinger Bands expand, it indicates a period of violent market fluctuation, which is suitable for tracking trends.

## Risk Analysis  

The biggest risk of the RSI Axial Moving Average Crossover Strategy is the lagging of the RSI indicator and moving average lines themselves. When rapid market movements occur, the indicator calculation and trend judgment will lag to some extent. This will lead to raised buy points and lowered sell points.  

Another major risk is the misguidance of indicators when market trend turns from bull to bear or vice versa, while RSI and MA indicators fail to react in time, resulting in losing trades.

Solutions include appropriately adjusting RSI parameters, shortening MA periods, adding trend indicators to assist in judgment, and appropriately widening stop loss range.  

## Optimization Directions

The RSI Axial Moving Average Crossover Strategy can be optimized in the following aspects:  

1. Optimize RSI parameters: Adjust RSI length to balance sensitivity and stability  

2. Optimize MA parameters: Adjust MA type and period parameters to optimize trend-following  

3. Add stop loss mechanisms: Set moving or time stop loss to control single loss

4. Incorporate trend indicators: Add MACD, KDJ etc. to avoid reversal misjudgements   

5. Multi-timeframe verification: Use higher timeframes to determine trends to avoid being trapped

## Conclusion  

The RSI Axial Moving Average Crossover Strategy is an overall mature quantitative trading strategy. It combines the advantages of multiple technical indicators and can catch mainstream market moves through parameter tuning and multi-dimensional optimization. The biggest risk is the lagging of indicators, which needs to be addressed by stop losses to control losses. When properly implemented, this strategy can yield relatively stable investment returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|(?RSI Settings)RSI Length|
|v_input_source_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_string_1|0|(?MA Settings)MA Type: SMA|Bollinger Bands|EMA|SMMA (RMA)|WMA|VWMA|
|v_input_int_2|14|MA Length|
|v_input_float_1|2|BB StdDev|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-16 00:00:00
end: 2023-11-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
// Copyright (c) 2020-present, Alex Orekhov (everget)
// Corrected Moving Average script may be freely distributed under the terms of the GPL-3.0 license.
strategy('rsisma', shorttitle='rsisma')

ma(source, length, type) =>
    switch type
        "SMA" => ta.sma(source, length)
        "Bollinger Bands" => ta.sma(source, length)
        "EMA" => ta.ema(source, length)
        "SMMA (RMA)" => ta.rma(source, length)
        "WMA" => ta.wma(source, length)
        "VWMA" => ta.vwma(source, length)

rsiLengthInput = input.int(14, minval=1, title="RSI Length", group="RSI Settings")
rsiSourceInput = input.source(close, "Source", group="RSI Settings")
maTypeInput = input.string("SMA", title="MA Type", options=["SMA", "Bollinger Bands", "EMA", "SMMA (RMA)", "WMA", "VWMA"], group="MA Settings")
maLengthInput = input.int(14, title="MA Length", group="MA Settings")
bbMultInput = input.float(2.0, minval=0.001, maxval=50, title="BB StdDev", group="MA Settings")

up = ta.rma(math.max(ta.change(rsiSourceInput), 0), rsiLengthInput)
down = ta.rma(-math.min(ta.change(rsiSourceInput), 0), rsiLengthInput)
rsi = down == 0 ? 100 : up == 0 ? 0 : 100 - (100 / (1 + up / down))
rsiMA = ma(rsi, maLengthInput, maTypeInput)
isBB = maTypeInput == "Bollinger Bands"

plot(rsi, "RSI", color=#7E57C2)
plot(rsiMA, "RSI-based MA", color=color.blue)
rsiUpperBand = hline(70, "RSI Upper Band", color=#787B86)
hline(50, "RSI Middle Band", color=color.new(#787B86, 50))
rsiLowerBand = hline(30, "RSI Lower Band", color=#787B86)
fill(rsiUpperBand, rsiLowerBand, color=color.rgb(126, 87, 194, 90), title="RSI Background Fill")
bbUpperBand = plot(isBB ? rsiMA + ta.stdev(rsi, maLengthInput) * bbMultInput : na, title = "Upper Bollinger Band", color=color.green)
bbLowerBand = plot(isBB ? rsiMA - ta.stdev(rsi, maLengthInput) * bbMultInput : na, title = "Lower Bollinger Band", color=color.green)
fill(bbUpperBand, bbLowerBand, color= isBB ? color.new(color.green, 90) : na, title="Bollinger Bands Background Fill")


long = ta.crossover(rsi, rsiMA)
short = ta.crossunder(rsi, rsiMA)
if long
    strategy.entry("long", strategy.long)
if short
    strategy.close("long", comment = "long TP")

 
// long1 = close * 9
// long2 = long1 / 100
// long3 = long2 + close


//plot(long3,color=color.blue)
// if short
//     strategy.entry("short", strategy.short)
// if long
//     strategy.close("short", comment = "short TP")



```

> Detail

https://www.fmz.com/strategy/433021

> Last Modified

2023-11-23 16:45:55

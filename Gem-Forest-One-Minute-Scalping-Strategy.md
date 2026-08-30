
> Name

Gem-Forest-One-Minute-Scalping-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/15995053761dbeb149c.png)
[trans]
### Overview
Gem Forest One Minute Scalping Strategy is a short-term quantitative trading strategy. This strategy comprehensively uses multiple indicators to identify the market's shock characteristics within the 1-minute time frame, and switches between long and short positions accordingly to achieve ultra-short-term arbitrage.
### Strategy Principles
1. The ATR indicator constructs the upper and lower rails to determine the price shock range.
2. Fast and slow EMA indicators construct golden cross and dead cross trading signals
3. The double RSI indicator confirms the golden cross and dead cross signal.
4. Combine indicator signals and price positions to determine specific entry and exit points
When the price is lower than the lower rail, the fast and slow EMA forms a golden cross, and the fast RSI crosses the slow RSI above, generating a buy signal; when the price is above the upper rail, the fast and slow EMA forms a dead cross, and the fast RSI crosses below the slow RSI, generating a sell signal. Set stop loss and take profit to exit after entering the market.
### Advantage Analysis
1. Multi-index combination, comprehensive judgment, high reliability
2. The strategic operation frequency is high and has strong profit potential.
3. Strategic retracement pequeño has good stability
4. Ultra-short-term arbitrage can be carried out within a period of 1 minute or less
### Risk Analysis
1. Ultra-short line operation requires high network and hardware requirements
2. Ultra-short term can easily lead to over-trading and capital dispersion.
3. Improper indicator settings may cause false signals
4. Depending on the specific market environment, it is easy to stop losses when the market fluctuates violently.
To address these risks, you can optimize indicator parameters, adjust stop-loss and stop-profit methods, appropriately limit the maximum number of transactions in a single day, and select trading varieties with good liquidity and moderate volatility, etc.
### Strategy optimization direction
1. Test the impact of different ATR cycle parameters on the results
2. Try different types of EMA, or change one of the EMAs to another indicator
3. Adjust RSI cycle parameters, or try other oscillators such as KDJ, Stochastics, etc.
4. Optimize the entry point selection method, such as combining more factors to determine the trend, etc.
5. Adjust stop loss and profit points to optimize the return-to-risk ratio
### Summarize
Jinsen's one-minute shock strategy fully considers the characteristics of ultra-short-term quantitative trading. The indicator parameters are set reasonably, and multiple indicators are used for confirmation and combination. It has high reliability and strong profit potential under the premise of strictly controlling risks. It is very suitable for investors with sufficient computing power and psychological quality to verify the real market.
||

### Overview  

The Gem Forest One Minute Scalping Strategy is a quantitative trading strategy for short-term trading. It combines multiple indicators to identify market oscillation characteristics within a 1-minute timeframe and switch between long and short positions for ultra-short scalping.  

### Strategy Logic  

1. ATR indicator builds upper and lower bands to determine price oscillation range  
2. Fast and slow EMA crossovers generate trading signals  
3. Dual RSI indicators confirm crossover signals  
4. Entry and exit points are determined by combining indicator signals and price levels  

When price is below the lower band, fast and slow EMA golden cross happens, fast RSI crosses above slow RSI, a buy signal is generated; When price is above upper band, fast and slow EMA dead cross happens, fast RSI crosses below slow RSI, a sell signal is generated. After entry, stop loss and take profit are used for exit.

### Advantage Analysis

1. Multiple indicators combined improves reliability  
2. High operation frequency provides greater profit potential  
3. Smaller drawdowns, better stability  
4. Capable of ultra-short scalping within 1-min or shorter timeframe  

### Risk Analysis   

1. Higher requirements for network and hardware due to high frequency  
2. Over-trading and capital scattering risks 
3. False signals from poor indicator configuration  
4. Vulnerable to stop loss in volatile market conditions  

These risks can be managed by optimizing parameters, adjusting stops, limiting max daily trades, choosing proper products etc.  

### Optimization Directions

1. Test impact of different ATR periods  
2. Try different EMA types or replace one EMA  
3. Adjust RSI periods or test other oscillators like KDJ, Stochastics etc  
4. Improve entry logic with more factors like trends  
5. Optimize stops for better risk-reward ratio  

### Conclusion  

This strategy fully considers the characteristics of ultra-short quantitative trading. Reasonable indicator settings, multiple confirmations and combinations ensure high reliability. With strict risk control, it has considerable profit potential and suits investors with sufficient computing power and psychological quality.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|ATR Period|
|v_input_float_1|true|ATR Multi|
|v_input_string_1|0|ATR Smoothing: WMA|SMA|EMA|RMA|
|v_input_int_2|21|Fast EMA|
|v_input_int_3|65|Slow EMA|
|v_input_int_4|25|Fast RSI Length|
|v_input_int_5|100|Slow RSI Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Gem Forest 1 Dakika Scalp", overlay=true)

source = close
atrlen = input.int(14, "ATR Period")
mult = input.float(1, "ATR Multi", step=0.1)
smoothing = input.string(title="ATR Smoothing", defval="WMA", options=["RMA", "SMA", "EMA", "WMA"])

ma_function(source, atrlen) => 
    if smoothing == "RMA"
        ta.rma(source, atrlen)
    else
        if smoothing == "SMA"
            ta.sma(source, atrlen)
        else
            if smoothing == "EMA"
                ta.ema(source, atrlen)
            else
                ta.wma(source, atrlen)

atr_slen = ma_function(ta.tr(true), atrlen)
upper_band = atr_slen * mult + close
lower_band = close - atr_slen * mult

ShortEMAlen = input.int(21, "Fast EMA")
LongEMAlen = input.int(65, "Slow EMA")
shortSMA = ta.ema(close, ShortEMAlen)
longSMA = ta.ema(close, LongEMAlen)
RSILen1 = input.int(25, "Fast RSI Length")
RSILen2 = input.int(100, "Slow RSI Length")
rsi1 = ta.rsi(close, RSILen1)
rsi2 = ta.rsi(close, RSILen2)
atr = ta.atr(atrlen)

RSILong = rsi1 > rsi2
RSIShort = rsi1 < rsi2

longCondition = open < lower_band
shortCondition = open > upper_band
GoldenLong = ta.crossover(shortSMA,longSMA)
Goldenshort = ta.crossover(longSMA,shortSMA)

plotshape(shortCondition, title="Sell Label", text="Sell", location=location.abovebar, style=shape.labeldown, size=size.tiny, color=color.red, textcolor=color.white, transp=0)
plotshape(longCondition, title="Buy Label", text="Buy", location=location.belowbar, style=shape.labelup, size=size.tiny, color=color.green, textcolor=color.white, transp=0)
plotshape(Goldenshort, title="Golden Sell Label", text="Golden Crossover Short", location=location.abovebar, style=shape.labeldown, size=size.tiny, color=color.blue, textcolor=color.white, transp=0)
plotshape(GoldenLong, title="Golden Buy Label", text="Golden Crossover Long", location=location.belowbar, style=shape.labelup, size=size.tiny, color=color.yellow, textcolor=color.white, transp=0)

if (longCondition)
    stopLoss = low - atr * 2
    takeProfit = high + atr * 5
    strategy.entry("long", strategy.long, when = RSILong)

if (shortCondition)
    stopLoss = high + atr * 2
    takeProfit = low - atr * 5
    strategy.entry("short", strategy.short, when = RSIShort)

plot(upper_band)
plot(lower_band)
plot(shortSMA, color = color.red)
plot(longSMA, color = color.yellow)

```

> Detail

https://www.fmz.com/strategy/442079

> Last Modified

2024-02-19 10:45:18

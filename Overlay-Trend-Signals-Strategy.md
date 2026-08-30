
> Name

Based on the two-way motion index strategy Overlay-Trend-Signals-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/7f0e4e3f0cf3f9d040aa697f80c918a550398f726d085be7f92c43439d9100ce.png)
[trans]
### Overview
This strategy generates trading signals by calculating the two-way movement volume index DI+, DI- and the average direction index ADX, combined with the exponential moving average EMA. A buy signal is generated when DI+ crosses DI- above and ADX is above 20; a sell signal is generated when DI- crosses DI+ below and ADX is above 25. The trade stop signal is when DI- crosses DI+ and ADX is above 30.
### Strategy Principles
1. Calculate DI+, DI-, ADX
    - Call the ta.dmi() function to calculate DI+, DI-, and ADX
    - DI+/DI- reflects the directionality of price
    - ADX reflects the average magnitude of price changes
2. Calculate exponential moving average EMA
    - Call the custom my_ema() function to calculate EMA
    - EMA can effectively smooth price data
3. Trading signal generation
    - Buy signal: DI+ crosses DI- and ADX>20 and closing price>EMA
        - Indicates that the price trend is upward and the change range is large
    - Sell signal: DI- crosses DI+ and ADX>25 and closing price <EMA
        - Indicates that the price trend is downward and the change range is large.
4. Trading stop loss
    - Buy stop: DI- crosses DI+ and ADX>30
        - Indicates price trend reversal
    - Sell stop loss: DI+ crosses DI- and ADX>30
        - Indicates price trend reversal
In summary, this strategy combines movement volume indicators and trend indicators to generate trading signals when the price trend is strong. At the same time, set stop loss conditions to limit losses.
### Advantage Analysis
1. Use dual DI to avoid false signals
    - A single DI is prone to produce false signals, but combining DI+ and DI- can ensure trending
2. ADX conditions ensure large price changes
    - Only trade when price fluctuations intensify to avoid market shocks
3. EMA conditions combined with DI
    - EMA can effectively identify medium and long-term price trends
4. Strict stop loss conditions
    - Stop losses in time to avoid huge losses
### Risk Analysis
1. Frequent stop loss
    - If the market fluctuates violently, stop loss will be too frequent
2. Parameter dependency
    - DI and ADX parameters need to be optimized to find the best combination
3. Low transaction frequency
    - Stricter trading conditions will reduce trading frequency
It can be optimized by expanding the stop loss range, adjusting the parameter combination, or adding additional filtering conditions to increase the trading frequency.
### Optimization direction
1. Parameter optimization
    - Optimize DI and ADX parameters to find the best parameter combination
2. Add filters
    - For example, add trading volume, divergence and other conditions to filter signals
3. Expand the stop loss range
    - Relax stop loss conditions appropriately and reduce frequent stop losses
### Summarize
This strategy integrates movement volume indicators and trend analysis indicators to generate trading signals when the price trend is strong. Set strict stop loss conditions to control risks. The strategy effect can be further improved through parameter optimization, adding signal filters and appropriately expanding the stop loss range.
||

### Overview  

This strategy generates trading signals by calculating the Directional Movement Indexes (DMI) DI+ and DI- along with Average Directional Index (ADX) and Exponential Moving Average (EMA). It triggers a long signal when DI+ crosses above DI- and ADX is above 20. A short signal is triggered when DI- crosses below DI+ and ADX is above 25. The stop loss signal is when DI- crosses above DI+ with ADX above 30.

### Strategy Logic  

1. Calculate DI+, DI-, ADX
    - Use ta.dmi() to compute DI+, DI-, ADX
    - DI+/DI- measures directional price movement 
    - ADX measures strength of price movement

2. Calculate Exponential Moving Average 
    - Use custom my_ema() function to compute EMA
    - EMA smoothes price data  

3. Generate trading signals
    - Long signal: DI+ crosses above DI- and ADX > 20 and close > EMA
        - Indicates upward trend and increased volatility  
    - Short signal: DI- crosses below DI+ and ADX > 25 and close < EMA
        - Indicates downward trend and high volatility

4. Set stop loss
    - Long stop loss: DI- crosses above DI+ and ADX > 30 
        - Indicates trend reversal  
    - Short stop loss: DI+ crosses below DI- and ADX > 30
        - Indicates trend reversal  

In summary, this strategy combines momentum and trend analysis indicators to trade when strong price trends emerge, with stop losses to limit losses.  

### Advantage Analysis   

1. Dual DI avoids false signals  
    - Single DI can give false signals, dual DI ensures trend  
2. ADX threshold requires increased volatility 
    - Only trades high volatility moves, avoids ranging  
3. EMA complements DI
    - EMA identifies mid/long term trends
4. Strict stop loss  
    - Cuts losses quickly  

### Risk Analysis  

1. Frequent stop loss
    - Volatile swings may trigger frequent stops
2. Parameter dependence
    - Optimal DI and ADX parameters need to be found
3. Low trade frequency
    - Strict rules reduce trades

Can optimize by expanding stop loss, tuning parameters, adding filters to increase frequency.  

### Optimization Opportunities

1. Parameter optimization 
    - Optimize DI and ADX parameters  
2. Add filters 
    - Volume, divergence etc.
3. Widen stop loss
    - Relax stops to reduce frequency  

### Conclusion   

This strategy combines momentum and trend analysis indicators to trade strong trends, with strict stops to control risk. Can further improve performance through parameter optimization, additional filters, and relaxed stops.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|DI Length|
|v_input_int_2|14|ADX Smoothing|
|v_input_int_3|26|EMA Length|
|v_input_source_1_close|0|EMA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_bool_1|true|Signal Labels|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Tamil_FNO_Trader

//@version=5
strategy("Overlay Signals by TFOT", overlay=true)

// Calculate DMI
len = input.int(14, minval=1, title="DI Length")
lensig = input.int(14, title="ADX Smoothing", minval=1, maxval=50)
[diplus, diminus, adx] = ta.dmi(len, lensig)

// Get EMA
emalen = input.int(26, minval=1, title = "EMA Length")
emasrc = input.source(close, title = "EMA Source")

my_ema(src, length) =>
    alpha = 2 / (length + 1)
    sum = 0.0
    sum := na(sum[1]) ? src : alpha * src + (1 - alpha) * nz(sum[1])
EMA2 = my_ema(emasrc, emalen)

// Variables
var bool buycondition1 = false
var bool sellcondition1 = false

var int firstbuybar = na
var int firstsellbar = na

var int buyexitbar = na
var int sellexitbar = na

var bool buyexit1 = false
var bool sellexit1 = false

// Buy & Sell Conditions
buycondition1 := (ta.crossover(diplus, diminus)) and (adx > 20) and (close > EMA2) and na(firstbuybar)
sellcondition1 := (ta.crossover(diminus, diplus)) and (adx > 25) and (close < EMA2) and na(firstsellbar)

buyexit1 := ta.crossover(diminus, diplus) and (adx > 30) and na(buyexitbar)
sellexit1 := ta.crossover(diplus, diminus) and (adx > 30) and na(sellexitbar)

if buycondition1
    if(na(firstbuybar))
        firstbuybar := bar_index
        buyexitbar := na
        firstsellbar := na
        strategy.entry("Buy", strategy.long)

if sellcondition1
    if(na(firstsellbar))
        firstsellbar := bar_index
        sellexitbar := na
        firstbuybar := na
        strategy.entry("Sell", strategy.short)

if buyexit1 and not na(firstbuybar)
    if(na(buyexitbar))
        buyexitbar := bar_index
        firstbuybar := na
        firstsellbar := na
        strategy.close("Buy")

if sellexit1 and not na(firstsellbar)
    if(na(sellexitbar))
        sellexitbar := bar_index
        firstsellbar := na
        firstbuybar := na
        strategy.close("Sell")

// Plot signals on chart
hl = input.bool(defval = true, title = "Signal Labels")

plotshape(hl and buycondition1 and bar_index == firstbuybar ? true : na, "Buy", style = shape.labelup, location = location.belowbar, color = color.green, text = "Buy", textcolor = color.white, size = size.tiny)
plotshape(hl and sellcondition1 and bar_index == firstsellbar ? true : na, "Sell", style = shape.labeldown, location = location.abovebar, color = color.red, text = "Sell", textcolor = color.white, size = size.tiny)

plotshape(hl and buyexit1 and bar_index == buyexitbar ? true : na, "Buy Exit", style = shape.labelup, location = location.belowbar, color = color.red, text = "Buy X", textcolor = color.white, size = size.tiny)
plotshape(hl and sellexit1 and bar_index == sellexitbar ? true : na, "Sell Exit", style = shape.labeldown, location = location.abovebar, color = color.red, text = "Sell X", textcolor = color.white, size = size.tiny)


```

> Detail

https://www.fmz.com/strategy/441958

> Last Modified

2024-02-18 10:00:22

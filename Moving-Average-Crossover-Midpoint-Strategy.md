
> Name

Moving-Average-Crossover-Midpoint-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/3a7af32862ed01e714a2ba819f1a1fc5b0dbc8955a04f7cf5058ce80a3f0297a.png)

[trans]

#### Overview
The Moving Average Crossover Midpoint Strategy is a trend following strategy. It combines the midpoint indicator and the moving average to generate trading signals by determining whether the price breaks through the intersection of the midpoint indicator and the moving average.
#### Strategy Principle
The core indicator of this strategy is the midpoint indicator. The midpoint indicator takes the average of the highest and lowest prices within a certain period. Since the highest and lowest prices can reflect the extremes of market fluctuations, their averages become important support or resistance levels.
In addition, moving averages are also introduced in the strategy. Moving averages can smooth price data and determine trend direction.
When the price crosses above the intersection of the midpoint indicator and the moving average, a buy signal is generated; when the price crosses below the intersection, a sell signal is generated.
According to the logic of this strategy, as long as the price breaks through the midpoint and the moving average crosses the area, you can follow the trend and seize the intermediate callback for reversal operations.
#### Advantage Analysis
This strategy combines midpoint indicators and moving averages to quickly determine key support, resistance levels and trend directions. It has the following advantages:
1. The midpoint indicator can accurately locate the support resistance level, and the moving average can determine the trend direction. The combination of the two has high reliability.
2. Determine the turning point of the trend through cross situations, reducing the probability of false breakthroughs.
3. Use double-line cross judgment to avoid misleading by a single indicator.
4. The strategy idea is simple and clear, easy to understand and implement, and is suitable for quantitative trading.

#### Risk Analysis
There are also some risks with this strategy:
1. When the market fluctuates violently, the midpoint indicator and moving average may fail.
2. When the two lines cross, there may be a certain degree of pullback test or callback pressure, which brings the risk of stop loss.
3. This strategy focuses on short- and medium-term operations and is not suitable for long-term operations.
Corresponding risk management measures include:
1. Optimize the moving average parameters and improve smoothness.
2. Appropriately enlarge the stop loss range to cope with the callback pressure.
3. Shorten the holding period and stop profits and losses in a timely manner.

#### Optimization direction
This strategy can also be optimized from the following directions:
1. Optimize the period parameters of the midpoint indicator and moving average to find the best parameter combination.
2. Add other indicator filters, such as MACD, RSI, etc., to improve signal quality.
3. Increase transaction volume verification to avoid low-volume false breakthroughs.
4. Combined with the volatility indicator, adjust the stop loss and profit levels according to market fluctuations.
5. Test the applicability of different markets and varieties.

#### Summarize
The moving average crossover midpoint strategy integrates the advantages of midpoint indicators and moving averages, and uses the crossover situation to determine the breakthrough of key support and resistance levels to capture market turning points. There is a large space for strategy optimization and stable returns are expected.
||

#### Overview  

The Moving Average Crossover Midpoint Strategy is a trend following strategy. It combines the midpoint indicator and moving average lines to generate trading signals when price breaks through the crossover point of the midpoint indicator and moving averages.


#### Strategy Logic  

The core indicator of this strategy is the midpoint indicator. The midpoint indicator takes the average value of the highest and lowest prices over a certain period to locate key support and resistance levels.

In addition, the moving average is introduced to smooth price data and determine the trend direction.

Buy signals are generated when price breaks above the crossover point of the midpoint and moving average, and sell signals are generated when price breaks below the crossover point.

According to this strategy logic, catching the breakout of the midpoint and moving average crossover area can follow the trend well and take reversal trades during pullbacks.


#### Advantage Analysis   

This strategy combines the advantages of midpoint indicator and moving averages, with the following edges:

1. The midpoint indicator accurately locates key support/resistance levels, and moving averages determine the trend direction. The combination enhances reliability.  

2. Judging reversals via crossover situations reduces the probability of false breakouts.

3. Adopting dual-line crossover prevents misleading by a single indicator.  

4. The strategy idea is simple and clear, easy to understand and implement, suitable for algorithm trading.


#### Risk Analysis

There are also some risks in this strategy:   

1. The midpoint and moving averages may fail when the market fluctuates violently.  

2. There could be some pullback pressure when the crossover happens, causing stop loss risks.

3. This strategy focuses on medium-term operations and does not apply to overly long-term operations.

The corresponding risk management measurements include:

1. Optimizing moving average parameters to increase smoothness. 

2. Properly widening stop loss range to cope with pullback pressure.  

3. Shortening holding period for timely profit taking and stop loss.


#### Optimization Directions   

This strategy can also be optimized in the following aspects:

1. Optimize periods of midpoint indicator and moving averages to find the best parameter combination.  

2. Add other indicators like MACD, RSI for filtration to improve signal quality.

3. Add trading volume confirmation to avoid false breakouts with low volume. 

4. Incorporate volatility indicators to adjust stops and profit taking levels based on market fluctuation.

5. Test applicability in different markets and products.  


#### Conclusion

The Moving Average Crossover Midpoint Strategy integrates the advantages of midpoint indicator and moving averages, catching trend reversal by judging breakouts of key support/resistance levels. This strategy has large room for optimization and is expected to achieve steady profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|131|Başlangıç Period|
|v_input_2|14|Kaydırma Seviyesi|
|v_input_float_1|0.0006|Yüzde Seviyesi|
|v_input_int_1|44|Length|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_string_1|0|(?Smoothing)Method: EMA|SMA|SMMA (RMA)|WMA|VWMA|
|v_input_int_2|53|Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-12 00:00:00
end: 2023-12-12 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © MGULHANN
//@version=5
strategy('Forex Midpoint Stratejisi For Nasdaq ', overlay=true)
BPeriod = input(131, 'Başlangıç Period')
kaydirma = input(14, 'Kaydırma Seviyesi')
yuzdeseviyesi = input.float(0.0006, 'Yüzde Seviyesi', step=0.0001)
len = input.int(44, minval=1, title="Length")
src = input(close, title="Source")
out = ta.sma(src, len)

ma(source, length, type) =>
    switch type
        "SMA" => ta.sma(source, length)
        "EMA" => ta.ema(source, length)
        "SMMA (RMA)" => ta.rma(source, length)
        "WMA" => ta.wma(source, length)
        "VWMA" => ta.vwma(source, length)

typeMA = input.string(title = "Method", defval = "EMA", options=["SMA", "EMA", "SMMA (RMA)", "WMA", "VWMA"], group="Smoothing")
smoothingLength = input.int(title = "Length", defval = 53, minval = 1, maxval = 100, group="Smoothing")
smoothingLine = ma(out, smoothingLength, typeMA)
//plot(smoothingLine, title="Smoothing Line", color=color.red, linewidth = 2)

//zararDurdurmaYuzde = input.float(0.2, title='Zarar Durdurma %', step=0.01) / 100
//karAlmaYuzde = input.float(0.5, title='Kar Alma %', step=0.01) / 100


//MIDPOINT HESAPLA
midpoint1 = ta.highest(high, BPeriod) + ta.lowest(low, BPeriod)
midpoint2 = midpoint1 / 2
midyuzdeseviyesi = midpoint2 * yuzdeseviyesi
midtopdeger = midyuzdeseviyesi + midpoint2

//GİRİŞ KOŞULLARI
buycross = ta.crossover(smoothingLine, midtopdeger[kaydirma]) //? aort > ta.sma(close,50) : na
sellcross = ta.crossover(midtopdeger[kaydirma], smoothingLine) // ? aort < ta.sma(close,50) : na

//LONG GİRİŞ
if (buycross)
    strategy.entry("BUY", strategy.long)
    //longKarAl = strategy.position_avg_price * (1 + karAlmaYuzde)
    //longZararDurdur = strategy.position_avg_price * (1 - zararDurdurmaYuzde)
    //strategy.exit("Long Exit","Long", stop=longZararDurdur)
    
   
//SHORT GİRİŞ    
if (sellcross)
    strategy.entry("SELL", strategy.short)
    //shortKarAl = strategy.position_avg_price * (1 - karAlmaYuzde)
    //shortZararDurdur = strategy.position_avg_price * (1 + zararDurdurmaYuzde)
    //strategy.exit("Short Exit","Short", stop=shortZararDurdur)
   
//plot(midtopdeger, offset=kaydirma, linewidth=2, color=color.blue)

```

> Detail

https://www.fmz.com/strategy/435284

> Last Modified

2023-12-13 17:38:23

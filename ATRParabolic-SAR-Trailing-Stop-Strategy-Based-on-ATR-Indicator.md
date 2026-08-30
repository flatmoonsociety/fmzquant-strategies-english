
> Name

Parabolic-SAR-Trailing-Stop-Strategy-Based-on-ATR-Indicator Parabolic-SAR-Trailing-Stop-Strategy-Based-on-ATR-Indicator
> Author

ChaoZhang

> Strategy Description



[trans]
The name of this strategy is "Parabolic Stop Loss Strategy Based on ATR Indicator". This strategy uses the ATR indicator to adjust the contraction speed of the parabolic stop loss curve so that it can adapt to changes in market volatility.
The acceleration factor of traditional parabolic stop loss is fixed and cannot cope with the increase in volatility. This strategy makes the contraction speed of the parabola accelerate as the ATR value increases. In this way, when the fluctuation increases, the stop loss curve can approach the price faster and effectively control risks.
Specifically, after the strategy determines the direction of the price trend, it calculates an adaptive acceleration factor based on the ATR value, and draws a parabolic stop loss curve accordingly. When the price breaks through the stop loss line, stop loss is executed to close the position.
The advantage of this strategy is that it enables traditional parabolic stops to dynamically adjust based on market volatility. However, the ATR parameters need to be optimized, and the stop loss line is easily too sensitive and can be breached.
Overall, adaptive stops are important to protect profits and control risks. Traders should choose appropriate stop loss indicators based on market conditions and conduct parameter testing and optimization to maximize the effectiveness of the stop loss strategy.

||


This strategy is named "Parabolic SAR Trailing Stop Strategy Based on ATR Indicator". It uses the ATR indicator to adjust the acceleration factor of Parabolic SAR for adapting to changing market volatility.

The acceleration factor of traditional Parabolic SAR remains fixed and cannot adapt to increased volatility. This strategy makes the SAR curve contract faster as ATR value expands, so the stop can tighten quicker around prices when volatility rises to effectively control risks.

Specifically, after determining price trend, an adaptive acceleration factor is calculated based on ATR value to plot the Parabolic SAR trailing stop curve. When prices breach the stop level, the stop loss is triggered. 

The advantage of this strategy is making traditional Parabolic SAR stops dynamic based on market volatility. But ATR parameters need optimization, and the stop line can be prone to premature breach.

In general, adaptive stops are important for protecting profits and limiting risks. Traders should choose suitable stop indicators based on market conditions, and test and optimize parameters, in order to maximize the utility of stop loss strategies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|atr_length|
|v_input_2|0.02|start|
|v_input_3|0.02|increment|
|v_input_4|0.2|maximum|
|v_input_5|true|Entry on Nth trend bar|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-13 00:00:00
end: 2023-09-12 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="ATR Parabolic SAR Strategy [QuantNomad]", shorttitle="ATR PSAR Strategy [QN]", overlay=true, default_qty_type = strategy.percent_of_equity,  default_qty_value = 100)

atr_length = input(14)
start      = input(0.02)
increment  = input(0.02)
maximum    = input(0.2)
entry_bars = input(1, title = "Entry on Nth trend bar") 

atr = atr(atr_length)

atr := na(atr) ? tr : atr

psar        = 0.0 // PSAR
af          = 0.0 // Acceleration Factor
trend_dir   = 0   // Current direction of PSAR
ep          = 0.0 // Extreme point
trend_bars  = 0

sar_long_to_short = trend_dir[1] == 1  and close <= psar[1] // PSAR switches from long to short
sar_short_to_long = trend_dir[1] == -1 and close >= psar[1] // PSAR switches from short to long

trend_change = barstate.isfirst[1] or sar_long_to_short or sar_short_to_long

// Calculate trend direction
trend_dir    :=  barstate.isfirst[1] and close[1]  > open[1] ?  1 : 
                 barstate.isfirst[1] and close[1] <= open[1] ? -1 : 
                 sar_long_to_short ? -1 : 
                 sar_short_to_long ?  1 : nz(trend_dir[1])

trend_bars := sar_long_to_short ? -1 : 
              sar_short_to_long ?  1 : 
              trend_dir ==  1   ? nz(trend_bars[1]) + 1 : 
              trend_dir == -1   ? nz(trend_bars[1]) - 1 : 
              nz(trend_bars[1])

// Calculate  Acceleration Factor
af := trend_change ? start : 
   (trend_dir == 1 and high > ep[1]) or  
   (trend_dir == -1 and low < ep[1]) ? 
   min(maximum, af[1] + increment) : 
   af[1]

// Calculate extreme point
ep := trend_change and trend_dir == 1 ? high :  
   trend_change and trend_dir == -1 ? low : 
   trend_dir == 1 ? max(ep[1], high) : 
   min(ep[1], low)

// Calculate PSAR
psar :=  barstate.isfirst[1] and close[1]  > open[1] ? low[1]  : 
         barstate.isfirst[1] and close[1] <= open[1] ? high[1] : 
         trend_change ? ep[1] :    
         trend_dir == 1 ? psar[1] + af * atr : 
                          psar[1] - af * atr

plot(psar, style=plot.style_cross, color=trend_dir == 1 ? color.green : color.red,  linewidth = 2)


// Strategy 
strategy.entry("Long",  true,  when = trend_bars ==  entry_bars)
strategy.entry("Short", false, when = trend_bars == -entry_bars)
```

> Detail

https://www.fmz.com/strategy/426598

> Last Modified

2023-09-13 15:53:00

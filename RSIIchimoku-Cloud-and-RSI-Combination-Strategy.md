
> Name

Ichimoku-Cloud-and-RSI-Combination-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy combines the use of the Ichimoku Balance Sheet and the Relative Strength Index (RSI) indicator to determine the direction of the trend and enter the market when the trend starts. When the three line segments of the Ichimoku Balance Sheet form a permutation that meets the conditions and are combined with the RSI signal, a trading signal is generated.
### Strategy Principles
1. Calculate the conversion line, baseline line, and delay line of the Ichimoku Balance Table
2. Calculate RSI indicator value
3. Go long when the conversion line crosses the baseline, the delay line is above the Yang line, the closing price breaks through the cloud chart, and the RSI is below 50
4. When the conversion line crosses the baseline, the delay line is below the negative line, the closing price falls below the cloud chart, and the RSI is above 50, go short.
5. Close the position when the reverse signal appears
Specifically, this strategy combines the trend judgment of Ichimoku Balance Sheet and the overbought and oversold judgment of RSI. When the three-line combination pattern of the Ichimoku Balance Sheet shows that the trend has started, and the RSI also shows that there is no overbought or oversold, an entry signal is generated. RSI filtering helps avoid false entries during consolidation. The closing signal is completely based on the reverse FORMATION of the Ichimoku Balance Sheet.
### Advantage Analysis
1. Integrate RSI indicator to improve entry accuracy
2. The Ichimoku balance meter can determine the trend direction and has strong trend tracking capabilities.
3. Trading signals are simple, intuitive and easy to master
4. Adjustable moving average and RSI parameters to adapt to different cycles
5. Have a stop-profit and stop-loss strategy to control risks
### Risk Analysis
1. The judgment of the Ichimoku Balance Sheet sometimes lags behind and may lead to consolidation by mistake.
2. Parameters need to be optimized, otherwise the trading signal may be inaccurate
3. Long-term positions face overnight risks
4. RSI is prone to sending out false signals
5. Possibly trapped due to reversal
Risks can be managed through parameter optimization, optimizing stop-profit and stop-loss strategies, and appropriately shortening the position period.
### Optimization direction
1. Test different moving averages and RSI parameters to find the best combination
2. Introduce trailing stop loss to track price changes
3. Evaluate the effect of limited trading hours
4. Study the parameter preferences of different varieties
5. Test to add re-entry and position addition rules
6. Compare different take-profit and stop-loss strategies
### Summarize
This strategy combines the Ichimoku Balance Sheet and the RSI indicator for trend judgment and trading. The advantage is that the signal is simple and intuitive, and the ROI is high; the disadvantage is that there is lag and risk of being trapped. The strategy effect can be improved and risks controlled through parameter optimization, stop-profit and stop-loss optimization, and limited trading time. This strategy provides traders with a comprehensive understanding of the application of the Ichimoku Balance Sheet.
|| 

### Overview

This strategy combines Ichimoku Cloud and Relative Strength Index (RSI) indicators to determine trend direction and enter positions when a trend starts. It generates trading signals when the three Ichimoku lines align in valid combinations together with RSI signals.

### Strategy Logic 

1. Calculate Tenkan-sen, Kijun-sen, Chikou Span lines of Ichimoku Cloud
2. Calculate RSI values
3. Go long when Tenkan-sen crosses above Kijun-sen, Chikou Span above cloud, price breaks out above cloud, and RSI below 50
4. Go short when Tenkan-sen crosses below Kijun-sen, Chikou Span below cloud, price breaks down cloud, and RSI above 50  
5. Close position when reverse signal occurs

Specifically, it combines Ichimoku Cloud's trend analysis and RSI's overbought-oversold gauge. Entry signals are generated when Ichimoku lines align in trend start formation, and RSI shows no overbought-oversold condition. RSI filters help avoid false breakout during consolidation. Exits follow Ichimoku reverse FORMATION completely.

### Advantage Analysis

1. Combining RSI improves entry accuracy
2. Ichimoku Cloud has strong trend following capacity  
3. Signals are simple and intuitive
4. Customizable parameters fit different cycles
5. Risk managed by stop profit/loss

### Risk Analysis

1. Ichimoku Cloud may lag, causing false breakouts
2. Requires parameter optimization, otherwise inaccurate signals
3. Long holding introduces overnight risk 
4. RSI prone to false signals
5. Risks of being trapped on reversals

Risks can be managed via parameter optimization, stop profit/loss tuning, limiting holding period etc.

### Optimization Directions

1. Test different line and RSI parameters for best combinations
2. Introduce trailing stop loss
3. Evaluate limiting trading hours 
4. Study parameter preferences across products
5. Test adding re-entry and pyramiding rules
6. Compare different stop profit/loss strategies

### Summary

This strategy combines Ichimoku Cloud and RSI for trend analysis and trading. Pros are simple intuitive signals and high ROI; Cons are lags and trapped risks. Performance can be improved and risks controlled through parameter optimization, stop profit/loss tuning, trading hours control etc. It allows comprehensive understanding of Ichimoku Cloud application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Date Range|
|v_input_int_1|9|Tenkan-Sen Bars|
|v_input_int_2|26|Kijun-Sen Bars|
|v_input_int_3|52|Senkou-Span B Bars|
|v_input_int_4|26|Chikou-Span Offset|
|v_input_int_5|26|Senkou-Span Offset|
|v_input_2|true|Long Entry|
|v_input_3|true|Short Entry|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-14 00:00:00
end: 2023-09-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Coinrule

//@version=5
strategy("Ichimoku Cloud with RSI (By Coinrule)",
         overlay=true,
         initial_capital=1000,
         process_orders_on_close=true,
         default_qty_type=strategy.percent_of_equity,
         default_qty_value=30,
         commission_type=strategy.commission.percent,
         commission_value=0.1)

showDate = input(defval=true, title='Show Date Range')
timePeriod = time >= timestamp(syminfo.timezone, 2022, 6, 1, 0, 0)


// RSI inputs and calculations
lengthRSI = 14
RSI = ta.rsi(close, lengthRSI)


//Inputs
ts_bars = input.int(9, minval=1, title="Tenkan-Sen Bars")
ks_bars = input.int(26, minval=1, title="Kijun-Sen Bars")
ssb_bars = input.int(52, minval=1, title="Senkou-Span B Bars")
cs_offset = input.int(26, minval=1, title="Chikou-Span Offset")
ss_offset = input.int(26, minval=1, title="Senkou-Span Offset")
long_entry = input(true, title="Long Entry")
short_entry = input(true, title="Short Entry")

middle(len) => math.avg(ta.lowest(len), ta.highest(len))


// Components of Ichimoku Cloud
tenkan = middle(ts_bars)
kijun = middle(ks_bars)
senkouA = math.avg(tenkan, kijun)
senkouB = middle(ssb_bars)


// Plot Ichimoku Cloud
plot(tenkan, color=#0496ff, title="Tenkan-Sen")
plot(kijun, color=#991515, title="Kijun-Sen")
plot(close, offset=-cs_offset+1, color=#459915, title="Chikou-Span")
sa=plot(senkouA, offset=ss_offset-1, color=color.green, title="Senkou-Span A")
sb=plot(senkouB, offset=ss_offset-1, color=color.red, title="Senkou-Span B")
fill(sa, sb, color = senkouA > senkouB ? color.green : color.red, title="Cloud color")

ss_high = math.max(senkouA[ss_offset-1], senkouB[ss_offset-1])
ss_low = math.min(senkouA[ss_offset-1], senkouB[ss_offset-1])


// Entry/Exit Conditions
tk_cross_bull = tenkan > kijun
tk_cross_bear = tenkan < kijun
cs_cross_bull = ta.mom(close, cs_offset-1) > 0
cs_cross_bear = ta.mom(close, cs_offset-1) < 0
price_above_kumo = close > ss_high
price_below_kumo = close < ss_low

bullish = tk_cross_bull and cs_cross_bull and price_above_kumo
bearish = tk_cross_bear and cs_cross_bear and price_below_kumo

strategy.entry("Long", strategy.long, when=bullish and long_entry and RSI < 50 and timePeriod)
strategy.close("Long", when=bearish and not short_entry)

strategy.entry("Short", strategy.short, when=bearish and short_entry and RSI > 50 and timePeriod)
strategy.close("Short", when=bullish and not long_entry)
```

> Detail

https://www.fmz.com/strategy/427447

> Last Modified

2023-09-21 10:52:13


> Name

Breakout Strategy Ichimoku-Kinko-Hyo-Breakout-Strategy Based on the Ichimoku-Kinko-Hyo Indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14ccc1e1237dfda1458.png)
[trans]

### 1. Strategy Overview
The name of this strategy is "long-short two-way breakthrough strategy based on the Ichimoku Kinko Hyo indicator". This strategy uses the transition line, baseline, leading line and Kumo cloud chart in the Ichimoku Kinko Hyo indicator to determine the long and short direction and trend of the stock to achieve breakthrough buying and breakthrough selling.
### 2. Detailed principles of strategy
1. Calculate the components of the Ichimoku Kinko Hyo indicator, including:
    - Tenkan-Sen (turning line): Calculate the middle value of the highest price and the lowest price
    - Kijun-Sen (baseline): Calculate the middle value of the highest price and the lowest price
    - Senkou Span A (leading line A): Calculate the intermediate value of Tenkan-Sen and Kijun-Sen
    - Senkou Span B (leading line B): Calculate the middle value of the highest price and the lowest price
    - Chikou Span (delay line)
2. Determine the buy signal:
    - When Tenkan-Sen wears Kijun-Sen;
    - When the closing price of the day goes above the Kumo cloud chart;
    - When the delay line crosses the Kumo cloud, a buy signal is generated.
3. Determine the sell signal:
   - When Tenkan-Sen is worn under Kijun-Sen;
   - When the closing price of the day falls below the Kumo cloud chart;
   - When the delay line crosses the Kumo cloud chart, a sell signal is generated.   
### 3. Analysis of strategic advantages
1. Use the Ichimoku Kinko Hyo indicator to judge trends with high accuracy.
2. The addition of the delay line avoids the occurrence of false breakthroughs. 
3. Long and short two-way trading can earn profits in both rising and falling markets.
4. Parameters can be adjusted to adapt to different cycles.
### 4. Strategic Risk Analysis
1. When the market fluctuates, frequent trading losses may occur.
2. Multiple conditions need to be met at the same time to determine the signal, and the best entry point may be missed.
3. High turnover rate and high long-term transaction costs.
#### Risk Solutions
1. Adjust parameters to avoid frequent trading in volatile markets.
2. Combine with other indicators to confirm the signal and reduce the error rate. 
3. Properly extend the holding period and reduce the turnover rate.
### 5. Strategy optimization direction
1. Confirm trading signals by combining indicators such as moving averages.
2. Add stop-loss logic to reduce single losses.
3. Optimize parameters to make them more adaptable to different cycles and varieties.
### 6. Strategy Summary
This strategy uses the Ichimoku Kinko Hyo multi-indicator combination to determine the stock trend, and uses price and cloud chart breakthroughs as trading signals to achieve long and short two-way trading. Compared with a single indicator, this strategy has higher judgment accuracy and avoids many false breakthroughs. At the same time, there is also a certain degree of lag and the problem of being unable to grasp the best buying time. Overall, this strategy has a strong ability to accurately determine the direction of the trend, and the risks are within controllable range, so it deserves further optimization and verification.
||

### I. Strategy Overview

The strategy is named "Ichimoku Kinko Hyo Indicator Based Breakout Strategy". It utilizes the Tenkan-Sen, Kijun-Sen lines, Senkou Span lines and Kumo cloud from the Ichimoku Kinko Hyo indicator to determine the trend direction and implement breakout entry and exit signals. 

### II. Strategy Details   

1. Calculate the components of the Ichimoku Kinko Hyo indicator:
    - Tenkan-Sen: middle of highest and lowest prices
    - Kijun-Sen: middle of highest and lowest prices
    - Senkou Span A: middle of Tenkan-Sen and Kijun-Sen 
    - Senkou Span B: middle of highest and lowest prices
    - Chikou Span: lagging span

2. Determine long signal:
    - When Tenkan-Sen cross above Kijun-Sen;
    - And close price break above the Kumo cloud; 
    - And Chikou Span break above the Kumo cloud.
    
3. Determine short signal:
    - When Tenkan-Sen cross below Kijun-Sen;
    - And close price break below the Kumo cloud;
    - And Chikou Span break below the Kumo cloud.
    
### III. Advantage Analysis   

1. Ichimoku Kinko Hyo is accurate in determining trends. 
2. Chikou Span avoids false breakouts.
3. Allow long and short trading in both uptrend and downtrend.  
4. Customizable parameters for different periods.

### IV. Risk Analysis

1. Frequent losing trades during market consolidation.  
2. Missing best entry points due to multiple criteria.
3. High turnover rate increases transaction costs.

#### Solutions
1. Adjust parameters to avoid overtrading.
2. Combine with other indicators to confirm signals.
3. Extend holding period to decrease turnover. 

### V. Optimization Directions  

1. Add moving averages to confirm trading signals.  
2. Implement stop loss to limit downside risk.
3. Optimize parameters to improve robustness.  

### VI. Strategy Summary

The strategy determines trend direction accurately using Ichimoku Kinko Hyo indicators and takes breakout signals as entry and exit points, allowing long and short trading. Compared with single indicator strategies, it has higher accuracy and avoids many false signals. There is also some lagging in capturing best entry price. In conclusion, the strategy is quite effective in determining trends and the risks are manageable. Further optimizations and walk-forward testing are recommended.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|7|Tenkan-Sen Bars|
|v_input_int_2|14|Kijun-Sen Bars|
|v_input_int_3|28|Senkou-Span B Bars|
|v_input_int_4|14|Chikou-Span Offset|
|v_input_int_5|14|Senkou-Span Offset|
|v_input_1|true|Long Entry|
|v_input_2|false|Short Entry|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-09 00:00:00
end: 2024-01-15 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('Ichimoku Kinko Hyo: Basic Strategy', overlay=true)

//Inputs
ts_bars = input.int(7, minval=1, title='Tenkan-Sen Bars')
ks_bars = input.int(14, minval=1, title='Kijun-Sen Bars')
ssb_bars = input.int(28, minval=1, title='Senkou-Span B Bars')
cs_offset = input.int(14, minval=1, title='Chikou-Span Offset')
ss_offset = input.int(14, minval=1, title='Senkou-Span Offset')
long_entry = input(true, title='Long Entry')
short_entry = input(false, title='Short Entry')

middle(len) =>
    math.avg(ta.lowest(len), ta.highest(len))

// Ichimoku Components
tenkan = middle(ts_bars)
kijun = middle(ks_bars)
senkouA = math.avg(tenkan, kijun)
senkouB = middle(ssb_bars)

// Plot Ichimoku Kinko Hyo
plot(tenkan, color=color.new(#0496ff, 0), title='Tenkan-Sen')
plot(kijun, color=color.new(#991515, 0), title='Kijun-Sen')
plot(close, offset=-cs_offset + 1, color=color.new(#459915, 0), title='Chikou-Span')
sa = plot(senkouA, offset=ss_offset - 1, color=color.new(color.green, 0), title='Senkou-Span A')
sb = plot(senkouB, offset=ss_offset - 1, color=color.new(color.red, 0), title='Senkou-Span B')
fill(sa, sb, color=senkouA > senkouB ? color.green : color.red, title='Cloud color', transp=90)

ss_high = math.max(senkouA[ss_offset - 1], senkouB[ss_offset - 1])
ss_low = math.min(senkouA[ss_offset - 1], senkouB[ss_offset - 1])

// Entry/Exit Signals
tk_cross_bull = tenkan > kijun
tk_cross_bear = tenkan < kijun
cs_cross_bull = ta.mom(close, cs_offset - 1) > 0
cs_cross_bear = ta.mom(close, cs_offset - 1) < 0
price_above_kumo = close > ss_high
price_below_kumo = close < ss_low

bullish = tk_cross_bull and cs_cross_bull and price_above_kumo
bearish = tk_cross_bear and cs_cross_bear and price_below_kumo

strategy.entry('Long', strategy.long, when=bullish and long_entry)
strategy.entry('Short', strategy.short, when=bearish and short_entry)

strategy.close('Long', when=bearish and not short_entry)
strategy.close('Short', when=bullish and not long_entry)


```

> Detail

https://www.fmz.com/strategy/438972

> Last Modified

2024-01-16 17:12:49

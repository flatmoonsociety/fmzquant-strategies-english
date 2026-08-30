
> Name

Ichimoku-Early-Cloud-Trend-Following-Strategy-one cloud double advance opportunity moving average trend tracking strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13e48f7c4135f2fe6ce.png)
[trans]

## Overview
The one-cloud and two-advance opportunity moving average trend following strategy is a trend following strategy based on a popularity indicator and a cloud chart. This strategy uses the turning line of a cloud chart to send out buying and selling signals in advance to capture the trend in advance. At the same time, the strategy also integrates the trend judgment of moving averages and conducts multi-layer confirmation to avoid false breakthroughs.
## Strategy Principle
This strategy is mainly based on the following points:
1. Construct a cloud chart using the Conversion Line and Base Line, and draw the cloud chart with a displacement of 26 periods.
2. When the closing price breaks through the upper band of the cloud chart, a buy signal is issued; when the closing price falls below the lower band of the cloud chart, a sell signal is issued.
3. In order to filter out false breakthroughs, the current closing price is required to break through the maximum and minimum values ​​of the conversion line and the baseline at the same time.
4. The stop loss line is set to 5% of the entry price and can be closed.
Through such multiple filters, trend turning points can be effectively identified and new trading opportunities can be captured in a timely manner. At the same time, strict breakthrough filtering can also reduce the issuance of false signals.
## Strategic Advantages
This strategy has several advantages:
1. The turning line of a cloud chart has obvious early characteristics and can capture the turning point of the trend earlier.
2. Integrate moving average judgment to avoid false breakthroughs caused by overnight gaps.
3. Multiple condition filtering can reduce false signals and improve signal quality.
4. For long-term operations, the retracement is relatively small and it is easy to find the take-profit position.
5. Can be applied to different varieties, especially trend varieties.
## Strategy Risk
This strategy also has the following risks:
1. Trending markets have better applicability, while consolidation markets will increase false signals.
2. The cloud chart parameter settings will affect the effect and need to be optimized for different varieties. 
3. The stop loss position needs to be set with caution to avoid being trapped.
4. The signal frequency is low, making it easy to miss short-term opportunities.
Risks can be reduced by:
1. Choose varieties with obvious trends and avoid trading consolidating varieties.
2. Optimize the cloud chart parameters and determine the best parameter combination for different periods.
3. Use trailing stop loss or timely stop loss to control single losses.
4. Can be combined with other indicators to increase signal release frequency.
## Strategy optimization
This strategy can also be optimized from the following aspects:
1. Add a position management mechanism and control the position opening ratio through operators such as `strategy.position_size`.
2. Add variety filtering, filter the variety pool through `security()`, and automatically identify the trend degree.
3. Add stop-loss and take-profit strategies and set trailing stop-loss or partial take-profit to further control risks.
4. Combine with other indicators, such as Bollinger Bands, RSI, etc., to build a multi-indicator trading system to improve signal quality.
5. Apply machine learning methods, judge the reliability of buying and selling signals through training, and dynamically adjust the order quantity.
## Summarize
The one-cloud and two-advance moving average trend tracking strategy realizes trend judgment in advance through one-cloud chart, and then integrates the moving average multi-layer filter to effectively identify high-quality trading opportunities. The strategy is relatively stable, has large room for optimization, and can be widely used in real trading.
||

## Overview

The Ichimoku Early Cloud Trend Following Strategy is a trend following strategy based on the popular Ichimoku Cloud indicator. It utilizes the crossover lines of the Ichimoku Cloud to generate early entry signals and capture trends ahead of time. The strategy also incorporates moving averages for trend validation to avoid false breakouts.

## Strategy Logic

The strategy is mainly based on the following elements:

1. Construct the Ichimoku Cloud using the Conversion Line and Base Line, and plot the cloud with a 26-period displacement.

2. Trigger a long signal when close breaks above the top of the cloud; trigger a short signal when close breaks below the bottom of the cloud.  

3. Require close to also break the max/min of the Conversion and Base Lines to filter out false breakouts.

4. Optionally set a 5% stop loss based on entry price.

With such multilayer filtering, it can effectively identify trend reversal points and capture emerging trading opportunities in a timely manner. The strict breakout criteria also help reduce false signals.   

## Advantages

The strategy has the following advantages:

1. Ichimoku Cloud crossover lines have clear early indication before trend reversal.  
2. Incorporating moving averages avoids false breakout due to overnight gaps.
3. Multiple filter conditions reduce false signals and improve signal quality.  
4. Long holding periods result in smaller drawdowns and easier profit taking.
5. Applicable to different products, especially trending instruments.

## Risks

There are also some risks to consider:

1. Works better for trending markets; may generate more false signals during range-bound periods.  
2. Ichimoku parameters need to be optimized for different products.
3. Stop loss placement requires caution to avoid premature exit.  
4. Relatively low signal frequency, tends to miss short-term opportunities.  

Risks can be reduced by:

1. Select strongly trending products, avoid ranging products.
2. Optimize Ichimoku parameters for different timeframes to find best combinations. 
3. Employ trailing stop loss to control loss on single trades.
4. Add other indicators to increase signal frequency.

## Enhancements

The strategy can be further improved on the following aspects:

1. Add position sizing to control amount traded programmatically via `strategy.position_size`.

2. Add security universe filtering to auto detect trend strength via `security()`.  

3. Incorporate stop loss/profit taking techniques for risk management.

4. Build multi-indicator system combining indicators like Bollinger Bands and RSI to improve signal quality.  

5. Apply machine learning to judge signal reliability and dynamically adjust order quantities.

## Conclusion

The Ichimoku Early Cloud Trend Following Strategy utilizes Ichimoku Cloud for early trend identification, reinforced by moving average filters, to reliably detect high-quality trading opportunities. The strategy is stable with much room for enhancements and can be widely adopted for live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Conversion Line Period|
|v_input_2|26|Base Line Period|
|v_input_3|52|Lagging Span 2 Period|
|v_input_4|26|Displacement|
|v_input_5|false|Long Only|
|v_input_6|5|Stop-loss (%)|
|v_input_7|false|Use Stop-Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-05 00:00:00
end: 2023-12-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © QuantCT

//@version=4
strategy("Ichimoku Cloud Strategy Idea",
         shorttitle="Ichimoku", 
         overlay=true,
         pyramiding=0,     
         default_qty_type=strategy.percent_of_equity, 
         default_qty_value=99, 
         initial_capital=1000,           
         commission_type=strategy.commission.percent, 
         commission_value=0.1)

// ____ Inputs

conversion_period = input(9, minval=1, title="Conversion Line Period")
base_period = input(26, minval=1, title="Base Line Period")
lagging_span2_period = input(52, minval=1, title="Lagging Span 2 Period")
displacement = input(26, minval=1, title="Displacement")
long_only = input(title="Long Only", defval=false)
slp = input(title="Stop-loss (%)", minval=1.0, maxval=25.0, defval=5.0)
use_sl = input(title="Use Stop-Loss", defval=false)

// ____ Logic

donchian(len) => avg(lowest(len), highest(len))

conversion_line = donchian(conversion_period)
base_line = donchian(base_period)
lead_line1 = avg(conversion_line, base_line)
lead_line2 = donchian(lagging_span2_period)
chikou = close

chikou_free_long = close > high[displacement] and close > max(lead_line1[2 * displacement], lead_line2[2 * displacement])
enter_long = chikou_free_long and close > max(lead_line1[displacement], lead_line2[displacement])
exit_long = close < lead_line1[displacement] or close < lead_line2[displacement]

chikou_free_short = close < low[displacement] and  close < min(lead_line1[2 * displacement], lead_line2[2 * displacement])
enter_short = chikou_free_short and close < min(lead_line1[displacement], lead_line2[displacement])
exit_short = close > lead_line1[displacement] or close > lead_line2[displacement]

strategy.entry("Long", strategy.long, when=enter_long)
strategy.close("Long", when=exit_long) 
if (not long_only)
    strategy.entry("Short", strategy.short, when=enter_short)
    strategy.close("Short", when=exit_short) 

// ____ SL

sl_long = strategy.position_avg_price * (1- (slp/100))
sl_short = strategy.position_avg_price * (1 + (slp/100))
if (use_sl)
    strategy.exit(id="SL", from_entry="Long", stop=sl_long)
    strategy.exit(id="SL", from_entry="Short", stop=sl_short)

// ____ Plots

colors = 
 enter_long ? #27D600 :
 enter_short ? #E30202 :
 color.orange
 
p1 = plot(lead_line1, offset = displacement, color=colors,
	 title="Lead 1")
p2 = plot(lead_line2, offset = displacement, color=colors,
	 title="Lead 2")
fill(p1, p2, color = colors)
plot(chikou, offset = -displacement, color=color.blue)


```

> Detail

https://www.fmz.com/strategy/435139

> Last Modified

2023-12-12 16:11:09

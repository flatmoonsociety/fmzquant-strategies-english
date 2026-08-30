
> Name

Trend-Following-Strategy-Based-on-Pivot-Point-Breakout
> Author

ChaoZhang

> Strategy Description



[trans]
The name of this strategy is "Trend Following Strategy Based on Support and Resistance Breakthroughs". This strategy works by identifying key support and resistance levels and then trend trading when price breaks through these levels.
The specific logic is as follows:
1. Calculate the highest point and lowest point within a certain period as key support and resistance levels.
2. When the price rises and breaks through the highest support of the previous day, a buy signal is generated.
3. When the price falls and breaks through the lowest support of the previous day, a sell signal is generated.
4. Quickly follow a trend run after a breakout occurs. If it falls below the support level again, stop the loss and exit.
The advantage of this strategy is to seize the opportunity to trade trends when key support and resistance levels are broken. However, it is necessary to pay attention to the indicator shape to avoid generating too many uncertain signals in the volatile market.
Generally speaking, focusing on the breakthrough of key support and resistance levels is a simpler and more intuitive tracking strategy. However, traders still need to assist other technical indicators to confirm and adjust parameters appropriately so that both strategies can make profits and enter the trend and stop losses in time.

||



This strategy is named “Trend Following Strategy Based on Pivot Point Breakout”. It identifies key support and resistance levels, and trades breakouts of these levels to follow trends.

The logic is:

1. Calculate the highest high and lowest low prices over a period as key support/resistance levels. 

2. When prices break above the previous day’s high pivot, a buy signal is generated.

3. When prices break below the previous day’s low pivot, a sell signal is generated.

4. Quickly follow the trend after breakout occurs. If support is broken again, a stop loss exits.

The advantage is capitalizing on pivot breakout timing for trend trading. But indicator patterns should be watched to avoid excessive uncertain signals during ranging markets.

In summary, watching pivotal support/resistance level breakouts is a relatively simple and intuitive tracking approach. But traders still need confirmation from additional technical indicators, and parameter tuning, for the strategy to Both profit from trend entries and timely stop losses.

[/trans]


> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|left|
|v_input_2|10|right|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-12 00:00:00
end: 2023-09-12 00:00:00
period: 3d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Yo_adriiiiaan

//@version=4
strategy("Breakout Strategy", overlay = true, commission_type=strategy.commission.percent,commission_value=0, initial_capital = 1000,  default_qty_type=strategy.percent_of_equity, default_qty_value=100)
left =  input(10)
right = input(10)
pivot_high = 0.000
pivot_low = 0.000
pivot_high := nz(pivothigh(high,left,right), pivot_high[1])
pivot_low := nz(pivotlow(low,left,right), pivot_low[1])
plot(pivot_high)
plot(pivot_low)
breakout_bull = close > pivot_high[1]
breakdown_bear = close < pivot_low[1]

barcolor(close > pivot_high[1]? color.green:close < pivot_low[1]? color.red:close < pivot_high[1]? color.orange:na)
strategy.entry("Long", strategy.long, when = breakout_bull)
strategy.close_all(when = breakdown_bear) 
//strategy.entry("Short", strategy.short, when = breakdown_bear)

```

> Detail

https://www.fmz.com/strategy/426613

> Last Modified

2023-09-13 17:20:40

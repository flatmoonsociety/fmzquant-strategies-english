
> Name

Reverse PercentR-Reversa-Channe-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1503c838a714f59f4ec.png)

[trans]
### Strategy Overview
This is a reversal trading strategy based on the LaRue Fee Channel indicator. It determines whether the current price is in the overbought or oversold area by calculating the highest and lowest prices within a certain period of time in the past. If the price is close to the upper track or lower track, open a reverse position and wait for the price to return to the midline.
### Strategy Principles
This strategy is mainly based on two indicators: **Percent R indicator (%R)** and **Laru Lianfei Channel Upper and Lower Tracks**.
The percentage R indicator shows the distance between the current closing price and the highest and lowest prices in the most recent period. The value range is from 0 to -100. A value close to 0 means that the current closing price is close to the highest point in the most recent period. A value close to -100 means that the current closing price is close to the lowest point in the most recent period.
Lalu Lianfei Channel consists of upper rail, middle rail and lower rail. The upper rail is equal to the highest price in the most recent period, the lower rail is equal to the lowest price in the most recent period, and the middle line is the average of the upper and lower rails. If the price exceeds the upper band, it is considered overbought, and if the price is below the lower band, it is considered oversold.
This strategy first calculates the **percent R indicator** and the upper and lower rails of the LaRue Fee Channel**, and then uses the two indicators to determine whether it is currently overbought or oversold:
1. When the percentage R is lower than -87, it is considered to be oversold.
2. When the percentage R is higher than -20, it is considered to be overbought.
If it is neither overbought nor oversold, open a long position when the market opens. Close the position and exit before the market closes that day.
In this way, you can make profits in the short term by capturing price reversals.
### Strategic Advantages
1. The strategy is simple and clear, easy to understand and implement.
2. It is more reliable to use the percentage R indicator to determine the overbought and oversold status.
3. Make orders every day when the market opens and close positions when the market closes to avoid overnight risks.
4. Reversal trading strategy, suitable for short-term profits.
### Strategy Risk
1. The reversal is unsuccessful and you cannot exit with a profit.
2. Improper parameter settings prevent the correct judgment of overbought and oversold conditions.
3. The single-day trading time is too short, and there may be fewer trading signals.
Risks can be reduced by optimizing parameters, adjusting order time, or combining with other indicators.
### Strategy optimization
1. You can introduce a stop-loss mechanism and set a stop-loss line to avoid the expansion of losses.
2. The parameters of percentage R can be optimized to make overbought and oversold judgments more accurate.  
3. This strategy can be used in multiple time periods at the same time to achieve multi-period trading.
4. Can be combined with other indicators, such as KDJ, MACD, etc., to make trading signals more reliable.
### Summarize
Overall, this strategy is relatively simple and practical. It is designed through reversal trading ideas and is suitable for short-term frequent transactions. There is a lot of room for optimization, more technical indicators can be introduced in combination, and an automatic stop-loss mechanism can be established to control risks.
||

### Strategy Overview

This is a reversal trading strategy based on the Laruent Channel indicator. It calculates the highest and lowest prices over a certain period of time in the past to determine if the current price is in the overbought or oversold area. If the price is close to the upper or lower rail, it will open a position in the opposite direction and wait for the price to return to the middle line.

### Strategy Principle  

The strategy is mainly based on two indicators: **PercentR indicator (%R)** and **Laruent Channel rails**.

The PercentR indicator shows the distance between the current closing price and the highest and lowest prices over the most recent period. The value range is from 0 to -100. A value close to 0 means the current closing price is near the highest point recently. And a value close to -100 means the current closing price is near the lowest price recently.

The Laruent Channel consists of upper rail, middle line and lower rail. The upper rail equals the highest price over the most recent period. The lower rail equals the lowest price over that period. The middle line is the mean of the upper and lower rails. If the price exceeds the upper rail, it is considered overbought. If the price is below the lower rail, it is considered oversold.

The strategy first calculates the **PercentR indicator** and **Laruent Channel rails**, then uses the two indicators to determine if the current status is overbought or oversold:  

1. When PercentR is below -87, the status is considered oversold.
2. When PercentR is above -20, the status is considered overbought.

If the current status is neither overbought nor oversold, it will long at market open. And close the position before market close on the same day.

By capturing the price reversal, it can make profits in short term.

### Advantages

1. The strategy is simple and clear, easy to understand and implement.
2. Using PercentR indicator to judge overbought/oversold status is reliable. 
3. Making orders at market open and closing positions before market close avoids overnight risk.
4. As a reversal trading strategy, it is suitable for short term profit making.

### Risks

1. Failed reversal, cannot exit with profit.
2. Improper parameter settings, cannot judge overbought/oversold status correctly.  
3. Too short intraday trading time, fewer trading signals.

Risks can be reduced by optimizing parameters, adjusting order placement time, or combining with other indicators.

### Optimization

1. A stop loss mechanism can be introduced to set a stop loss line to avoid loss expansion.
2. The parameters of PercentR can be optimized to make overbought/oversold judgment more accurate.
3. The strategy can be used on multiple timeframes simultaneously to implement multi-timeframe trading.
4. It can be combined with other indicators like KDJ, MACD to make trading signals more reliable.

### Summary  

In general, this strategy is quite simple and practical. It is designed based on the reversal trading idea and suitable for short term frequent trading. There is large room for optimization. More technical indicators can be introduced for combination. And automatic stop loss mechanisms can also be established to control risks.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|-87|Low Marker|
|v_input_2|-20|High Marker|
|v_input_3|3|Length|
|v_input_4_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-04 00:00:00
end: 2023-12-04 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

//@version=4
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © zweiprozent original strategy by larry williams

strategy("Daily PercentR Strategy", overlay=false)
D_High = security(syminfo.tickerid, 'D', high[1])
D_Low = security(syminfo.tickerid, 'D', low[1])
D_Close = security(syminfo.tickerid, 'D', close[1])
D_Open = security(syminfo.tickerid, 'D', open[1])

LowMarker = input(-87,"Low Marker",input.integer)

HighMarker =  input(-20,"High Marker",input.integer)

length = input(title="Length", type=input.integer, defval=3)
src = input(close, "Source", type = input.source)
_pr(length) =>
	max = highest(length)
	min = lowest(length)
	100 * (src - max) / (max - min)
percentR = _pr(length)
obPlot = hline(LowMarker, title="Upper Band", color=#606060)
hline(-50, title="Middle Level", linestyle=hline.style_dotted, color=#606060)
osPlot = hline(HighMarker, title="Lower Band", color=#606060)
fill(obPlot, osPlot, title="Background", color=color.new(#9915ff, 90))
plot(percentR, title="%R", color=#3A6CA8, transp=0)

// Go Long - if percentR is not overbought/sold

ordersize=floor(strategy.equity/close) 

if percentR<HighMarker and percentR>LowMarker
    strategy.entry("Long", strategy.long,comment="Long")

//exit at end of session
if low[0]<high[0]
    strategy.close("Long", comment="exit")
    
```

> Detail

https://www.fmz.com/strategy/434305

> Last Modified

2023-12-05 12:04:13

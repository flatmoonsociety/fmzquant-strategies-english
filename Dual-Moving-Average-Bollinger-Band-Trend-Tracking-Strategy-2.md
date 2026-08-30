
> Name

Dual-Moving-Average-Bollinger-Band-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/94b787ba05408ce2249354004a61e0b223fd70d0939ca359eb5d3a7bbe3135f2.png)
[trans]

## Overview
This strategy is a quantitative trading strategy that uses a combination of Bollinger Bands and moving averages to determine trends and enter the market. It combines the trend identification ability of Bollinger Bands and the filtering effect of moving averages, which can effectively identify the market trend direction and enter the market in the trend direction.
## Strategy Principle
1. Use the highest price and lowest price to calculate the Bollinger Bands channel and determine the market trend direction.
- The highest price and the lowest price calculate the upper and lower rails of the channel
    - The center axis of the channel is the average price of the highest price and the lowest price
    - Determine the price position on the channel to determine the trend direction    
2. Calculate the size of the positive body and determine stop loss and reversal signals
- The real body of the Yang line is the absolute value of the closing price minus the opening price.
    - Calculate the average value of the positive body in N periods, compare it with the size of the current positive body, and determine stop loss and reversal
3. After confirming the trend direction, enter the market in the channel direction
- Long buy near the lower track when the trend is upward
    - Short positions near the upper band when the trend is down    
4. Use moving averages for filtering to avoid false signals
- Calculate the closing price moving average of N periods
    - Only issue trading signals when price breaks above the moving average
## Strategic Advantages
1. Combine Bollinger Bands Channel and Moving Average to judge the trend, which is highly systematic
Bollinger Bands can clearly judge the price channel and trend direction, and the moving average can filter. The combination of the two can effectively identify trends, avoid the impact of market emergencies, and ensure system stability.
2. Use the physical size of the Yang line to stop losses and effectively control risks.
By calculating the average size of the positive body in a certain period and comparing it with the size of the current period, we can clearly judge the trend reversal and carry out stop loss and lighten positions, thereby effectively controlling strategic risks.
3. Clear quantitative entry and stop loss rules
The strategy enters the market under the condition that the moving average and channel direction cooperate, and uses the positive line entity size rule to stop loss, making the entire system's entry and stop loss rules very clear and systematic.
## Risk Analysis
1. Potential risk of loss in volatile market conditions
In a volatile market, the price may touch the upper and lower rails multiple times, resulting in the possibility of repeated small losses. At this time, the position size should be reduced to reduce single losses.
2. The stop loss point is too close, resulting in excessive fluctuations and the risk of being hit.
In a strong trend, a short-term price correction may trigger the stop loss rule to be hit. At this time, the stop loss range should be appropriately relaxed and follow the trend.
3. Improper parameters may cause error signals
Improper parameter settings for moving averages and Bollinger Bands may lead to misidentification of signals. Parameters should be optimized appropriately to make the signal stable and reliable.

## Strategy optimization direction
1. Optimize the moving average cycle parameters
Adjust the parameters of the moving average and reduce the degree of smoothing to discover trend changes faster.
2. Test the effects of different stop loss rules
Try different stop loss rules, such as trailing stop loss, ATR stop loss, etc., and choose the optimal stop loss method.
3. Add machine learning model assistance
Training models based on a large amount of historical data to assist in judging trends and issuing trading signals.
## Summarize
This strategy comprehensively considers trend judgment and risk control, uses Bollinger Bands channels and moving averages to identify trends, and uses the size of the Yang line entity to stop losses. The strategy is highly systematic and has clear quantitative rules, which can effectively control risks and obtain excess returns. Subsequent improvements will be made through parameter optimization and machine learning to make the strategy more stable and reliable.
||

## Overview

This strategy utilizes a combination of Bollinger Bands and moving averages for trend identification and entry. It leverages the trend recognition capability of Bollinger Bands and the filtering effect of moving averages to effectively identify market trend directions for entry in trending markets.

## Strategy Logic

1. Calculate Bollinger Channel to determine market trend direction

    - Use highest high and lowest low to calculate channel bands 
    - Channel middle band is average of high and low
    - Determine trend direction based on price location within channel
    
2. Compute bullish candle body size for stop loss and reversal signals

    - Bullish candle body is absolute value of close minus open
    - Compute N-period average of candle bodies, compare to current body for stop loss and reversal

3. Enter trades in channel direction upon trend confirmation

    - Long entries near lower band in uptrends
    - Short entries near upper band in downtrends

4. Utilize moving averages for filtration to avoid false signals

    - Compute N-period moving average of closing price 
    - Generate signals only on moving average breakthroughs

## Advantages

1. Systematic trend identification combining bands and moving averages  

    Bands clearly identify price channels and trend direction. Moving averages filter noise. Combination enables robust trend detection immune to sporadic market shocks.

2. Effective risk control via candle body stop loss

    Comparing current candle body to historical average detects trend reversal for stop loss and position reduction. Effectively controls strategy risk.

3. Clear quantitative entry and stop loss rules

    Strict moving average and channel direction requirements for entry. Candle body size stop loss rule. Makes entire system entry and exits clear and systematic.

## Risk Analysis  

1. Potential losses in range-bound markets

    Whip-sawing price oscillating around bands can cause repeated minor losses. Position sizing should be reduced to limit loss impact.

2. Premature stop loss in strong trends

    Short-term retracements can trigger stops in strong uptrends/downtrends. Stop loss width should be relaxed to ride trends. 

3. Erroneous signals from poor parameter tuning

    Suboptimal moving average and bands parameters can cause spurious signals. Parameters should be optimized for signal reliability.

## Enhancement Opportunities

1. Optimize moving average lookback period  

    Adjust period to reduce smoothing for quicker trend change detection.

2. Test alternative stop loss mechanisms   

    Evaluate trailing stops, ATR stops etc. to find optimal system.

3. Incorporate machine learning models

    Train models on extensive historical data to augment trend and signal prediction.

## Conclusion

This strategy balances trend identification and risk control using Bollinger Bands and moving averages. The systematic quantitative approach with clear entry/exit rules enables effective reward capture with controlled risk. Further improvements via parameter tuning and machine learning integration will enhance robustness.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|true|Short|
|v_input_3|false|take, %|
|v_input_4|false|Counter-trend entry|
|v_input_5|20|Period|
|v_input_6|true|Show Bands|
|v_input_7|true|Show Background|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-14 00:00:00
end: 2023-12-21 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


//@version=2
strategy("Noro's Bands Scalper Strategy v1.3", shorttitle = "Scalper str 1.3", overlay=true, default_qty_type = strategy.percent_of_equity, default_qty_value=100.0, pyramiding=0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(true, defval = true, title = "Short")
takepercent = input(0, defval = 0, minval = 0, maxval = 1000, title = "take, %")
needct = input(false, defval = false, title = "Counter-trend entry")
len = input(20, defval = 20, minval = 2, maxval = 200, title = "Period")
needbb = input(true, defval = true, title = "Show Bands")
needbg = input(true, defval = true, title = "Show Background")
src = close

//PriceChannel 1
lasthigh = highest(src, len)
lastlow = lowest(src, len)
center = (lasthigh + lastlow) / 2

//Distance
dist = abs(src - center)
distsma = sma(dist, len)
hd = center + distsma
ld = center - distsma
hd1 = center + distsma / 2
ld1 = center - distsma / 2

//Trend
trend = close < ld and high < center ? -1 : close > hd and low > center ? 1 : trend[1]

//Lines
colo = needbb == false ? na : black
plot(hd, color = colo, linewidth = 1, transp = 0, title = "High band")
plot(center, color = colo, linewidth = 1, transp = 0, title = "center")
plot(ld, color = colo, linewidth = 1, transp = 0, title = "Low band")

//Background
col = needbg == false ? na : trend == 1 ? lime : red
bgcolor(col, transp = 80)

//Body
body = abs(close - open)
smabody = ema(body, 30)
candle = high - low

//Engulfing
min = min(open, close)
max = max(open, close)
bar = close > open ? 1 : close < open ? -1 : 0
upeng = bar == 1 and bar[1] == -1 and min >= min[1] and max <= max[1] ? 1 : 0
dneng = bar == -1 and bar[1] == 1 and min >= min[1] and max <= max[1] ? 1 : 0

//Signals
up7 = trend == 1 and ((bar == -1 and bar[1] == -1) or (body > smabody and close < open)) ? 1 : 0
dn7 = trend == 1 and bar == 1 and bar[1] == 1 and close > strategy.position_avg_price * (100 + takepercent) / 100 ? 1 : 0
up8 = trend == -1 and bar == -1 and bar[1] == -1 and close < strategy.position_avg_price * (100 - takepercent) / 100 ? 1 : 0
dn8 = trend == -1 and ((bar == 1 and bar[1] == 1) or (body > smabody and close > open)) ? 1 : 0

if up7 == 1 or up8 == 1 
    strategy.entry("Long", strategy.long, needlong == false ? 0 : trend == -1 and needct == false ? 0 : na)

if dn7 == 1 or dn8 == 1
    strategy.entry("Short", strategy.short, needshort == false ? 0 : trend == 1 and needct == false ? 0 : na)
```

> Detail

https://www.fmz.com/strategy/436249

> Last Modified

2023-12-22 14:54:20

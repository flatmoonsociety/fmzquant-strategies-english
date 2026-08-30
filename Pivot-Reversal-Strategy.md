
> Name

Pivot-Reversal-Strategy Pivot-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/185a11cb484a9f73dbc.png)
 [trans]


### Overview
This article will analyze in detail a reversal trading strategy based on pivot points. This strategy determines possible pivot support and resistance levels by calculating the highest and lowest prices for a certain period. When price crosses these pivot levels, it indicates a trend reversal and a reversal trade can be made.
### Strategy Principles
This strategy relies primarily on two indicators: Pivot High and Pivot Low. The pivot high and low points are the highest and lowest prices within a period, which can be calculated through the `pivothigh()` and `pivotlow()` functions. When calculating the pivot point, you need to set the number of periods on the left and right sides. In this strategy, the number of periods on the left is 4 and the number of periods on the right is 2.
A reversal signal occurs when the highest point of the latest period is lower than the pivot high of the previous period. At this time, if it was a short-term operation before, you should now consider establishing a long position to seek reversal opportunities. Likewise, shorts should consider opening a reversal position when the latest cycle low is above the previous cycle's pivot low.
Specifically, the main logic of this strategy is:
1. Calculate pivot high and low points
2. Determine whether the price breaks through the pivot point
   1. If the low crosses the pivot low, go long
   2. If the high falls below the pivot high, go short.
3. Set stop loss level
### Advantage Analysis
The biggest advantage of this strategy is identifying potential trend reversal points, which is especially important for reversal traders. Compared with other indicators, pivot points can judge support and resistance more clearly without frequent false signals.
In addition, this strategy establishes long and short conditions at the same time to cover different market conditions to the greatest extent and avoid missing trading opportunities. Control risks through stop loss so that the profit-loss ratio can be guaranteed.
Overall, this is a very practical reversal strategy.
### Risk Analysis
Although this strategy attempts to reduce the probability of false signals, any strategy based on breakouts will inevitably lead to early Signals or late Signals. This can result in planning to take a long position but the market has turned bearish, or planning to take a short position but a bull market suddenly breaks out. This type of problem of not being able to perfectly predict reversals is a limitation of technical analysis itself.
In addition, the pivot point cannot 100% determine the key support and resistance levels and is for reference only. If you are unlucky, the pivot point may just miss the true support level to form a stop loss. This problem of fuzzy intervals cannot be completely avoided.
### Optimization direction
1. Cycle optimization. The existing left and right period numbers are set to 4 and 2, which can be used as the initial setting. However, pivots in different markets and different cycles may work better, and you can try to optimize to find the best parameter combination.
2. Filter in combination with other indicators. For example, you can add a trading volume indicator, and only when the trading volume is enlarged will the breakthrough be considered effective, which can reduce false breakthroughs.
3. Dynamic stop loss. The existing stop loss is to leave a minimum trading unit space above and below the pivot. This can use dynamic stop loss to try the best stop loss position according to the degree of market volatility.
4. Only operate in the trend direction. Now the conditions for long and short positions are parallel. In fact, you can only look for long opportunities in the long market and short selling opportunities in the short market. Better results may be obtained by combining trend indicators.

### Summarize
Overall this strategy is a simple and practical reversal strategy. The core idea is to determine potential trend turning points by calculating pivot points and monitoring their breakthroughs. This strategy simultaneously establishes long and short conditions to capture reversal opportunities to the maximum extent. Stop loss settings are used to control risk.
Overall, the strategy is clear and easy to implement. Parameter setting is also relatively straightforward and friendly to novices. Through continuous testing and optimization, strategy performance can be gradually improved, which is worth recommending.
||

### Overview

This article will analyze in detail a reversal trading strategy based on pivot points. The strategy calculates potential support and resistance pivot levels over a period, and identifies trend reversals when price breaks through these pivot levels, allowing reversal trades.

### Strategy Logic

The strategy mainly relies on two indicators: Pivot High and Pivot Low. Pivot highs and lows are the highest and lowest prices within a period, and can be obtained using the `pivothigh()` and `pivotlow()` functions. When computing pivot points, the periods to the left and right need to be set; this strategy uses 4 periods to the left and 2 periods to the right.  

When the highest price of the latest period is lower than the previous period's pivot high, it signals a reversal opportunity. If previous positions were short, long positions should now be considered to capitalize on the reversal. Similarly, when the latest period's lowest price is higher than the previous pivot low, existing long positions should consider reversing to short.

Specifically, the main logic is:

1. Compute pivot high/low levels 
2. Identify breakthroughs
   1. Long when price breaks above pivot low
   2. Short when price breaks below pivot high
3. Set stop loss levels

### Advantage Analysis

The biggest advantage of this strategy is identifying potential trend reversal points, which is crucial for reversal traders. Compared to other indicators, pivot points can more clearly identify key support/resistance levels without frequent false signals.

Moreover, the strategy has conditions for both long and short entries, covering different market situations to avoid missing opportunities. The use of stop loss controls risk and ensures a good risk/reward ratio.

In summary, this is a very practical reversal strategy.  

### Risk Analysis

Despite efforts to reduce false signals, any breakout-based strategy inevitably faces issues like premature or lagging signals. This could result in planning a long entry but the market has already reversed, or planning a short but a bull run suddenly erupts. Such inability to perfectly predict reversals is an inherent limitation of technical analysis.

Additionally, pivot points cannot guarantee perfect support/resistance levels either. Bad luck could result in stop loss hitting just before the real support level. Such uncertainty around key zones cannot be fully avoided.

### Enhancement Opportunities

1. Period optimization. The current left/right periods are set at 4 and 2. These can serve as initial values and be further optimized for each market.

2. Add filters with other indicators. For example, combine with volume to only consider breakouts as valid when accompanied by increasing volume. This helps avoid false breakouts.  

3. Dynamic stop loss. Currently stops are set with a buffer of one minimum tick above/below pivot levels. The buffer zone can be dynamically adjusted based on market volatility.

4. Operate only in trend direction. Currently long/short conditions are in parallel. An optimization is to only long in uptrends and short in downtrends based on a trend filter.

### Conclusion 

In summary, this is a simple yet practical reversal strategy. Identifying pivot points over a period and monitoring price breakthroughs forms the core idea for detecting potential trend reversals. The parallel long/short conditions maximize opportunities while stop losses manage risk.

The strategy logic is straightforward and easy to implement. The parameters are also intuitive for beginners. Further optimizations can improve performance for adoption. Overall this is a recommended strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|4|leftBars|
|v_input_2|2|rightBars|
|v_input_3|true|From Day|
|v_input_4|3|From Month|
|v_input_5|2018|From Year|
|v_input_6|true|To Day|
|v_input_7|true|To Month|
|v_input_8|2100|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-11 00:00:00
end: 2023-12-17 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Pivot Reversal Strategy", overlay=true)

leftBars  = input(4)
rightBars = input(2)

// backtesting date range
from_day   = input(defval = 1,    title = "From Day",   minval = 1)
from_month = input(defval = 3,    title = "From Month", minval = 1)
from_year  = input(defval = 2018, title = "From Year",  minval = 1970)

to_day     = input(defval = 1,    title = "To Day",     minval = 1)
to_month   = input(defval = 1,    title = "To Month",   minval = 1)
to_year    = input(defval = 2100, title = "To Year",    minval = 1970)

time_cond = (time > timestamp(from_year, from_month, from_day, 00, 00)) and (time < timestamp(to_year, to_month, to_day, 23, 59))

swh = pivothigh(leftBars, rightBars)
swl = pivotlow(leftBars, rightBars)

swh_cond = not na(swh)

hprice = 0.0
hprice := swh_cond ? swh : hprice[1]

le = false
le := swh_cond ? true : (le[1] and high > hprice ? false : le[1])

if (le and time_cond)
    strategy.entry("PivRevLE", strategy.long, comment="PivRevLE", stop=hprice + syminfo.mintick)

swl_cond = not na(swl)

lprice = 0.0
lprice := swl_cond ? swl : lprice[1]


se = false
se := swl_cond ? true : (se[1] and low < lprice ? false : se[1])

if (se and time_cond)
    strategy.entry("PivRevSE", strategy.short, comment="PivRevSE", stop=lprice - syminfo.mintick)

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/435761

> Last Modified

2023-12-18 16:59:59

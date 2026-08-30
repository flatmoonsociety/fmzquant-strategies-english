
> Name

Parabolic-SAR-Reversal-Strategy Parabolic-SAR-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy trades based on the Parabolic SAR indicator, which shows trend reversal points in the market. A trading signal is generated when the SAR point breaks through the price.
## Principle
Parabolic SAR (Stop and Reverse) mainly determines the reversal of market trends and is a trend following indicator.
When the SAR point is below the price, it is bullish. At this time, if the SAR crosses the price, it is a short signal.
When the SAR point is above the price, it represents a bearish trend. If the SAR points below the price, it is a long signal.
This strategy uses the breakthrough of the SAR indicator as the direction of the trading signal. And use the SAR point as the stop loss level.
## Advantages
1. The SAR indicator can accurately locate potential reversal points.
2. Due to the adoption of trend following mechanism, false signals can be reduced.
3. As a stop loss position, SAR can be set along with the trend to avoid being trapped.
4. Works without other indicators or filters.
5. Parameter optimization is simple, just use the default settings.
## Risks and Solutions
1. The SAR indicator may generate frequent signals during consolidation. Filters can be added to identify trending quotes.
2. The stop loss point is close to the current price and may be penetrated. The stop loss point should be appropriately loosened.
3. Transaction volume factors are not considered. Volume energy indicators can be added to avoid price-volume discrepancies.
4. The retracement may be large. Positions should be set up appropriately to limit risk.
5. Trend reversal may not be successful. Confirmation can be reversed again.
## Optimization ideas
1. Test whether adjusting SAR parameters can obtain better results.
2. Add indicators such as MACD to determine the reversal success rate.
3. Establish a dynamic moving stop loss mechanism.
4. Optimize opening positions and make full use of SAR signals.
5. Study the addition of continued reversal confirmation logic.
## Summarize
This strategy uses the Parabolic SAR indicator to determine potential reversal points and trade when the SAR breaks through the price. The advantage is to take advantage of the trend to stop losses and avoid being trapped. However, the selection of SAR signal time points may be inaccurate and needs further optimization. Overall, the parabolic steering idea is worth learning from.
|| 

## Overview

This strategy trades based on Parabolic SAR indicator which identifies potential reversal points in trends. Entry signals are generated when SAR flips above or below price. 

## Principles

Parabolic SAR is a trend following indicator that mainly identifies trend reversals.

When SAR is below price, it represents uptrend. SAR flipping above price gives short signal.

When SAR is above price, it represents downtrend. SAR flipping below price gives long signal.

The strategy simply trades the SAR flip as signal direction, with SAR as stop loss.

## Advantages

1. SAR accurately locates potential reversal points.

2. Trend following mechanism reduces false signals.

3. SAR acts as trailing stop, avoiding being trapped.

4. No other indicators or filters required. 

5. Easy parameter optimization, defaults often work.

## Risks and Mitigations

1. SAR may whipsaw in ranging markets. Trend filter can be added.

2. SAR too close to price risks being hit. Wider stops needed.

3. Volume is ignored, risk of divergence. Volume indicators can help.

4. Drawdowns may be significant. Appropriate position sizing is key.

5. Reversals do not always succeed. Confirmation may be needed.

## Enhancement Opportunities

1. Test if SAR parameters can be improved.

2. Add indicators like MACD to confirm reversal probability.

3. Build dynamic trailing stop mechanism. 

4. Optimize entry position sizing to capitalize on SAR signals.

5. Research adding reversal confirmation logic.

## Summary

The strategy trades potential reversal points identified by SAR, taking trades when SAR flips price. Benefits include trailing stops to avoid traps. But SAR timing may be inaccurate and needs refinement. Overall the SAR reversal concept is worth learning.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.02|start|
|v_input_2|0.02|increment|
|v_input_3|0.2|maximum|
|v_input_4|true|From Day|
|v_input_5|true|From Month|
|v_input_6|2018|From Year|
|v_input_7|true|To Day|
|v_input_8|true|To Month|
|v_input_9|2019|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-18 00:00:00
end: 2023-09-17 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Parabolic SAR Strategy", overlay=true)

// 
// author: Kozlod
// date: 2018-09-03
// https://www.tradingview.com/u/Kozlod/
// 

start = input(0.02)
increment = input(0.02)
maximum = input(0.2)

////////////////////////////////////////////////////////////////////////////////
// BACKTESTING RANGE
 
// From Date Inputs
fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2018, title = "From Year", minval = 1970)
 
// To Date Inputs
toDay = input(defval = 1, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 1, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2019, title = "To Year", minval = 1970)
 
// Calculate start/end date and time condition
startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true
 
////////////////////////////////////////////////////////////////////////////////

psar = sar(start, increment, maximum)

// Signals
psar_long  = high[1] < psar[2] and high > psar[1] 
psar_short = low[1]  > psar[2] and low  < psar[1] 

// Plot PSAR
plotshape(psar, location = location.absolute, style = shape.cross, size = size.tiny, color = low < psar[1] and not psar_long ? green : red)


if (psar >= high and time_cond)
    strategy.entry("ParLE", strategy.long, stop=psar, comment="ParLE")
else
    strategy.cancel("ParLE")

if (psar <= low and time_cond)
    strategy.entry("ParSE", strategy.short, stop=psar, comment="ParSE")
else
    strategy.cancel("ParSE")

if (not time_cond)
    strategy.close_all()

```

> Detail

https://www.fmz.com/strategy/427190

> Last Modified

2023-09-18 21:59:08


> Name

Gap-Down-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy trades reversals against gap patterns. When the underlying price falls and then reverses to rise, the strategy will perform a buying operation at the opening or closing of the next day and set a trailing stop to lock in profits.
## Strategy Principle
1. Determine whether the underlying asset has a gap, that is, the opening price of the current day is lower than the closing price of the previous day.
2. If there is a gap and falls, observe whether the closing price of the day is higher than the opening price, indicating a reversal and rise.
3. If the gap reversal conditions are met, the buying operation will be carried out at the opening or closing of the next day.
4. Set a certain percentage of trailing stop loss after entering the market, such as 5%. The stop loss line is raised as the price rises.
5. When the price falls back to the stop loss line, a stop loss order is triggered and the trade is stopped.
## Advantage Analysis
Main advantages of this strategy:
1. Capture reversal trading opportunities brought by gap patterns.
2. The reversal pattern has a high probability and is in line with the market rules of the psychological alternation of long and short.
3. Tracking stop loss to lock in profits, no manual monitoring required.
4. The entry time and stop loss level can be flexibly set to adapt to the characteristics of individual stocks.
5. Programmed execution, convenient backtest optimization.
## Risk Analysis
The main risks of this strategy are:
1. There is a probability of failure in the gap reversal, and the form needs to be verified.
2. If the stop loss level is set too high, it will easily be breached, leading to an increase in losses.
3. Improper selection of underlying stocks may lead to a hard landing and sharp reversal.
4. Insufficient data backtesting may lead to the risk of overfitting.
5. There are differences between real operation and backtesting.
Corresponding solutions:
1. Optimize the stop loss level and control the proportion of single loss.
2. Make judgments on the overall market and avoid selecting top and divergent stocks.
3. Verify the form and check the changes in trading volume.
4. Expand the backtest sample size and simulate real market verification.
## Optimization direction
This strategy can be optimized by considering the following points:
1. Combine with trend indicator filtering to avoid counter-trend entries.
2. Dynamically adjust the stop loss level ratio to protect profits.
3. Consider adding time filtering to only trade on specified dates.
4. Evaluate the strength of the pattern and adjust the proportion of admission funds.
5. Test different holding times and find the optimal exit point.
## Summarize
The gap reversal strategy trades high probability reversal patterns. Risks can be effectively controlled through stop-loss strategies. However, we still need to be wary of false rebounds and changes in market structure. When placing a real offer, it is recommended to carefully evaluate the form and trend direction, and at the same time continue to optimize parameters.
|| 
## Overview

This strategy trades gap down reversals. When the current candle opens below the prior close and finishes up on the day with a close greater than the open, the strategy enters long on the next day's open or close.

## Strategy Principle

1. Check if a gap down occurs, i.e. current open below prior close. 

2. If gapped down, observe if the current close is above the open, indicating an upside reversal.

3. If gap down reversal conditions are met, go long on the next day's open or close.

4. Set a trailing stop loss at a percentage, e.g. 5%, after entry. The stop level moves up with the price.

5. When price drops to hit the stop loss, the position is closed.

## Advantage Analysis

Main advantages of this strategy:

1. Captures reversal trading opportunities from gap down patterns.

2. High probability reversal pattern aligns with alternating fear/greed. 

3. Trailing stop locks in profits without needing manual monitoring.

4. Flexible settings for entry and stop loss to suit individual stocks.

5. Automated execution and easy backtesting/optimization.

## Risk Analysis

Main risks of this strategy:

1. Failed gap down reversals can occur, need pattern verification.

2. Oversized stop loss prone to being taken out leading to amplified losses.

3. Poor stock selection may lead to hard reversals.

4. Insufficient backtest data leads to overfit risks.

5. Execution differs between backtest and live.

Solutions:

1. Optimize stop loss level and cap loss percentage per trade.

2. Gauge overall market trend to avoid topping stocks. 

3. Verify pattern and volume changes. 

4. Expand sample size for backtest, simulate live trading.

## Optimization Directions

Some ways to improve the strategy:

1. Add trend filter to avoid countertrend entries.

2. Dynamically adjust stop loss percentage to protect profits.

3. Consider adding time filter to trade on specific dates. 

4. Assess strength of pattern for position sizing.

5. Test different holding periods to find optimal exit spots.

## Summary

The gap down reversal strategy capitalizes on high probability reversal patterns. Stops effectively control risk but beware of false bounces and changing market conditions. When trading live, cautious evaluation of patterns and trends along with ongoing optimizations are recommended.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Start Date|
|v_input_2|true|Start Month|
|v_input_3|2009|Start Year|
|v_input_4|5|Trail Long Loss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-11 00:00:00
end: 2023-09-12 04:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © RolandoSantos

//@version=2

strategy(title="Gap Down reversal strat", overlay=true, pyramiding=1, default_qty_type =  strategy.cash, default_qty_value = 10000, initial_capital = 10000 )

/// Start date

startDate = input(title="Start Date", defval=1, minval=1, maxval=31)
startMonth = input(title="Start Month", defval=1, minval=1, maxval=12)
startYear = input(title="Start Year", defval=2009, minval=1800, maxval=2100)


// See if this bar's time happened on/after start date
afterStartDate = (time >= timestamp(syminfo.timezone, startYear, startMonth, startDate, 0, 0))

// STEP 1:
// Configure trail stop level with input options (optional)
longTrailPerc = input(title="Trail Long Loss (%)",
     type=float, minval=0.0, step=0.1, defval=5.0) * 0.01


// Calculate trading conditions
gap_d_r = open < close[1] and close > open


// Plot Shapes
plotshape(gap_d_r, style=shape.triangleup, location=location.belowbar)
///plotshape(gap_u_r, style=shape.triangledown, location=location.abovebar)

///// Use Low, or close/////

//hlco = input(title="Stop Modifier", defval="close", options=["open", "high", "low"])


// STEP 2:
// Determine trail stop loss prices
longStopPrice = 0.0   ///, shortStopPrice = 0.0

longStopPrice := if (strategy.position_size > 0)
    stopValue = close * (1 - longTrailPerc)
    max(stopValue, longStopPrice[1])
else
    0


// Plot stop loss values for confirmation
plot(series=(strategy.position_size > 0) ? longStopPrice : na,
     color=red, style=circles,
     linewidth=1, title="Long Trail Stop")


// Submit entry orders
if (afterStartDate and gap_d_r)
    strategy.entry(id="EL", long=true)


// Submit exit orders for trail stop loss price
if (strategy.position_size > 0)
    strategy.exit(id="Stop out", stop=longStopPrice)














```

> Detail

https://www.fmz.com/strategy/427266

> Last Modified

2023-09-19 16:19:51

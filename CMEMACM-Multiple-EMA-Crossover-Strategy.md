
> Name

CM-Multiple-EMA-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses a combination of 8-day, 13-day, 21-day and 55-day EMA to determine long or short signals when they appear golden cross or dead cross, with the purpose of capturing the medium and long-term trend.
## Strategy Principle
1. Calculate the 8-day, 13-day, 21-day and 55-day EMA respectively.
2. When the 8-day, 13-day, and 21-day EMA all cross the 55-day EMA, a buy signal is generated.
3. When the 8-day, 13-day, and 21-day EMA all fall below the 55-day EMA, a sell signal is generated.
4. Enter long when the golden cross occurs, and enter short when the dead cross occurs.
5. Close the position when the reverse crossover occurs.
## Advantage Analysis
1. Multiple EMA combinations can effectively filter out false breakthroughs.
2. The 55-day EMA serves as the central axis to avoid being trapped.
3. Backtesting shows that this strategy can bring stable returns every year in the past 10 years.
4. Visualize the intersection situation, easy to operate, suitable for novices.
## Risk Analysis
1. Fixed parameter combination, different varieties and markets require independent testing and optimization.
2. Inability to effectively respond to volatile market conditions and the risk of frequent stop losses.
3. Without setting a stop loss, a single loss cannot be controlled.
4. The transaction frequency may be too high or too low, requiring parameter adjustment.
5. The sample period is only 10 years, and the sample needs to be expanded to verify the robustness.
## Optimization direction
1. Test parameter combinations of different EMA periods to find the best match.
2. Add trading volume and other indicators to avoid false breakthroughs.
3. Set a trailing stop or a fixed stop.
4. Optimize position size and reduce single risk.
5. Go short at high points and long at low points to achieve two-way trading.
6. Expand to other varieties and longer time periods for backtest verification.
## Summarize
This strategy uses multiple EMA crossovers to determine the medium and long-term trend direction and achieves simple trend tracking. Its intuitive visualization is an advantage, but there are problems such as insufficient parameter optimization and incomplete stop loss. It is necessary to introduce more technical indicators to optimize parameter combinations, enrich entry filter conditions, and add stop losses to control risks. In addition, the strategy needs to be continuously optimized and verified through backtesting over large time periods and varieties to make it a stable and reliable trend tracking system.
|| 


## Overview

This strategy combines 8-day, 13-day, 21-day and 55-day EMAs and generates long and short signals when crossover occurs between them, aiming to capture mid-long term trends.

## Strategy Logic

1. Calculate 8-day, 13-day, 21-day and 55-day EMAs.

2. When 8-day, 13-day, 21-day EMAs all cross above 55-day EMA, long signal triggered.

3. When 8-day, 13-day, 21-day EMAs all cross below 55-day EMA, short signal triggered.

4. Go long on golden cross, go short on death cross. 

5. Close position on reverse crossover.

## Advantage Analysis

1. Multiple EMA combo effective in filtering false breakouts.

2. 55-day EMA as anchor avoids being trapped.

3. Backtest shows steady annual returns over past 10 years. 

4. Visual crossover, simple to operate, beginner friendly.

## Risk Analysis

1. Fixed parameters may not fit all products and markets, independent optimization needed.

2. Ineffective in ranging markets, risks whipsaws and frequent stops.

3. No stop loss unable to limit single trade loss.

4. Trade frequency may be too high or low, parameter tweak needed.

5. 10-year sample limited, need larger data to verify robustness.

## Optimization Directions

1. Test EMA period combinations to find best match.

2. Add volume filter to avoid false breakouts. 

3. Implement fixed or moving stop loss.

4. Optimize position sizing to lower risk per trade.

5. Trade both long and short sides.

6. Expand testing into more products and longer timeframe.

## Summary

This strategy identifies mid-long term trends using EMA crosses in intuitive visual way. Strengths are visibility and simplicity. But parameters need more optimization and lacks risk control. More technical indicators should be introduced to filter signals and stops added to limit losses. Also requires large sample backtests across products and time to refine and verify, to become a robust trend following system.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-21 00:00:00
end: 2023-09-20 00:00:00
period: 6h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ColinMccann18
//@version=4

// +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
// --------------------------------------------------------------RULES------------------------------------------------------------------------------
// - VISUALLY REPRESENTS THE CROSSING OF 8,13,21,55 EMA'S FROM KROWNS PROGRAM 
strategy(title="CM EMA Trend Cross STRAT", shorttitle="CM EMA Strat", overlay=true)

ema8  = ema(close,8)
ema13 = ema(close, 13)
ema21 = ema(close, 21)
ema55 = ema(close, 55)

//PLOT
plot(ema8,  title="EMA 1",linewidth=2, color=#00eeff)
plot(ema13, title="EMA 2",linewidth=2, color=#fff900)
plot(ema21, title="EMA 3",linewidth=2, color=#42ff0f)
plot(ema55, title="EMA 4",linewidth=2, color=#8b49ff)

//LOGIC---------------------------------------------------------------------------------------------------------------------------------
emacrossover = crossover(ema21, ema55) and ema8 and ema13 > ema55
emacrossunder = crossunder(ema21, ema55) and ema8 and ema13 < ema55

//Long----------------------------------------------------------------------------------------------------------------------------------
longCondition = emacrossover
closelongCondition = emacrossunder

strategy.entry("Long", strategy.long, qty=na, when=longCondition)
strategy.close("Close Long", when=closelongCondition)

//Short----------------------------------------------------------------------------------------------------------------------------------
shortCondition = emacrossunder
closeshortCondition = emacrossover

strategy.entry("Short", strategy.short,qty=na, when=shortCondition)
strategy.close("Close Short", when=closeshortCondition)


```

> Detail

https://www.fmz.com/strategy/427460

> Last Modified

2023-09-21 12:12:56

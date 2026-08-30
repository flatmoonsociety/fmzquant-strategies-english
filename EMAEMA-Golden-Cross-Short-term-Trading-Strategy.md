
> Name

EMA Golden Cross Short-term Trading Strategy EMA-Golden-Cross-Short-term-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/baf33861ac444217b52793ea2ffaf1884cc7b5a513ff7811b1fe955585913012.png)
 [trans]

## Overview
The EMA golden cross short-term trading strategy is a short-term trading strategy based on the EMA indicator. It uses EMA lines of different periods to judge golden cross and dead cross trading signals, uses shorter period EMA lines as market entry signals, and longer period EMA lines as stop loss signals to achieve a short-term trading mode of fast in and fast out.
## Strategy Principle
This strategy uses 4 EMA moving averages with different periods, specifically 9-period, 26-period, 100-period and 55-period EMA lines. The trading entry signal is to go long when the 9-period EMA line crosses the 26-period EMA line; the stop-loss exit signal is to close the position when the 100-period EMA line crosses below the 55-period EMA line. Fast in and out in this way to avoid being trapped.
## Advantage Analysis
1. It is reliable to use EMA indicator to judge the trend and avoid false signals.
2. Using the golden cross and dead cross combinations of EMA with different periods can capture short-term opportunities.  
3. Short-term trading method of fast in and fast out to avoid long-term losses.
## Risk Analysis
1. The EMA line itself has hysteresis and may miss the best entry opportunity.
2. Short-cycle transactions tend to increase transaction frequency and handling fee burden.
3. Short-term trading requires traders to have higher psychological control abilities.
## Optimization direction
1. You can adjust the period parameters of the EMA line to optimize profitability.
2. You can add other indicators to filter signals and improve your trading winning rate. 
3. You can set stop-loss and stop-profit conditions to control the risk of a single transaction.
## Summarize
This EMA golden cross short-term trading strategy is generally simple, easy to operate and quick to respond. Through parameter optimization and signal filtering, its stability and profitability can be further improved. However, short-term trading also places higher demands on traders' control capabilities. Generally speaking, this strategy is suitable for investors with certain trading experience to use in real trading.
||


## Overview

The EMA golden cross short-term trading strategy is a short-term trading strategy based on the EMA indicator. It uses EMA lines of different cycles to judge golden cross and dead cross trading signals, adopts shorter cycle EMA lines as entry signals, and longer cycle EMA lines as stop loss signals to realize a fast in and fast out short-term trading mode.

## Strategy Principle 

The strategy uses 4 EMA lines of different cycles, specifically 9, 26, 100 and 55 cycle EMA lines. The entry signal is to go long when the 9 cycle EMA line crosses over the 26 cycle EMA line; The exit stop loss signal is to close positions when the 100 cycle EMA line crosses below the 55 cycle EMA line. This allows fast entry and fast exit to avoid being trapped.

## Advantage Analysis

1. Using the EMA indicator to determine trends is reliable to avoid false signals.
2. Adopting EMA combos of different cycles can capture short-term opportunities.
3. The fast in and fast out short-term trading method avoids long-term bearing of losses.

## Risk Analysis   

1. EMA lines themselves have laggingness which may miss the best entry timing.  
2. Short-term trading can easily increase trading frequency and commission burdens.
3. Short-term trading requires higher psychological control skills from traders.

## Optimization Directions

1. EMA line cycle parameters can be adjusted to optimize profitability.
2. Other indicators can be added to filter signals and improve win rate.
3. Stop loss and take profit conditions can be set to control single trade risks.

## Summary   

In general, the EMA golden cross short-term trading strategy has the characteristics of simplicity, ease of operation and quick response. Through parameter optimization and signal filtering, its stability and profit level can be further improved. But short-term trading also raises higher requirements for traders' control capabilities. In conclusion, this strategy is suitable for investors with some trading experience to use in live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|9|EMA_L|
|v_input_int_2|26|EMA_L2|
|v_input_int_3|100|EMA_S|
|v_input_int_4|55|EMA_S2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-07 00:00:00
end: 2023-12-14 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © YukalMoon

//@version=5
strategy(title="EMA SCALPEUR", overlay=true, initial_capital = 1000)


//// input controls

EMA_L = input.int (title = "EMA_L", defval = 9, minval = 1, maxval = 100, step =1)
EMA_L2 = input.int (title = "EMA_L2", defval = 26, minval = 1, maxval = 100, step =1)
EMA_S = input.int (title = "EMA_S", defval = 100, minval = 1, maxval = 100, step =1)
EMA_S2 = input.int (title = "EMA_S2", defval = 55, minval = 1, maxval = 100, step =1)


/// mise en place de ema

shortest = ta.ema(close, 9)
short = ta.ema(close, 26)
longer = ta.ema(close, 100)
longest = ta.ema(close, 55)

plot(shortest, color = color.red)
plot(short, color = color.orange)
plot(longer, color = color.aqua)
plot(longest, color = color.yellow)

plot(close)

//// trading indicators

EMA1 = ta.ema (close,EMA_L)
EMA2 = ta.ema (close,EMA_L2)
EMA3 = ta.ema (close, EMA_S)
EMA4 = ta.ema (close, EMA_S2)


buy = ta.crossover(EMA1, EMA2)
//sell = ta.crossunder(EMA1, EMA2)

buyexit = ta.crossunder(EMA3, EMA4)
//sellexit = ta.crossover(EMA3, EMA4)

/////strategy

strategy.entry ("long", strategy.short, when = buy, comment = "ENTER-SHORT")
//strategy.entry ("short", strategy.short, when = sell, comment = "ENTER-SHORT")


///// market exit

strategy.close ("long", when = buyexit, comment = "EXIT-SHORT")
//strategy.close ("short",  when = sellexit, comment = "EXIT-SHORT")












```

> Detail

https://www.fmz.com/strategy/435477

> Last Modified

2023-12-15 11:16:18

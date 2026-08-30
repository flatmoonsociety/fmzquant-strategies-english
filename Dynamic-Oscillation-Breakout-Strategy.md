
> Name

Dynamic-Oscillation-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/752216eef27f57443537d6104c31c7f21fedb30bbb1c017dab52db32d35f31f3.png)
[trans]


## Overview
This strategy uses a dynamic oscillation channel breakthrough method to determine entry and stop loss points based on dynamic changes in price. The strategy is simple and easy to understand and suitable for operating trend stocks.
## Strategy Principle
This strategy first calculates the highest price and lowest price within 20 days to obtain the dynamic shock channel. Then calculate the 8-day exponential moving average and the 32-day exponential moving average. When the price closing price breaks through the upper track of the channel and the 8-day moving average is higher than the 32-day moving average, go long; when the price falls below the lower track of the channel or the 8-day moving average crosses the 32-day moving average, close the position. The stop loss method is to stop loss when the price is lower than the middle rail of the channel.
Specifically, the entry conditions for the strategy are:
1. The closing price breaks through the dynamic upper track formed by the highest price within 20 days
2. The 8-day moving average is higher than the 32-day moving average
The exit conditions of the strategy are:
1. Stop loss when the price is lower than the middle track of the channel
2. Close the position when the 8-day moving average falls below the 32-day moving average
This strategy uses dynamic channels to determine the trend direction, and at the same time uses the moving average to determine that the current upward trend is in place, which can effectively control risks.
## Strategic Advantages
- Use dynamic channel breakthroughs to determine the trend direction and avoid being trapped in a volatile market.
- The combination of 8-day and 32-day moving average can effectively judge the trend and avoid wrong transactions
- The policy rules are simple and clear, easy to understand and implement
- The stop loss method is relatively stable and reliable
## Strategy Risk
- Failure to break through may result in losses
- Improper setting of dynamic channel parameters may result in channels that are too wide or too narrow
- Improper setting of moving average parameters will also affect the judgment effect
- Stop loss points that are too close may cause excessive stop loss
You can optimize strategies and control risks by adjusting channel cycle parameters, moving average cycle parameters, and setting stop losses appropriately.
## Strategy optimization direction
- Channel cycle parameters can be optimized according to different stock characteristics
- You can test different moving average combinations to find better parameters
- Can be combined with trading volume to confirm breakthrough effects
- Stop loss can be trailed after a breakout
## Summarize
The overall idea of ​​the dynamic shock breakthrough strategy is clear and easy to understand. It uses dynamic channels to determine the trend direction, and then uses the moving average filtering effect to enter the market. Setting stop loss can effectively control risks. The strategy Profit Factor can be improved through parameter optimization. This strategy is suitable for stocks with a breakthrough continuation effect, and is especially suitable for the scenario of an upward breakthrough to a new high.
||


## Overview

This strategy adopts dynamic oscillation channel breakout to determine entry and stop loss points based on price movement. The strategy is simple and suitable for momentum stocks.

## Strategy Logic

The strategy first calculates the highest high and lowest low over the past 20 days to obtain a dynamic oscillation channel. Then it calculates the 8-day and 32-day exponential moving averages. When the closing price breaks through the upper band of the channel and the 8-day EMA is above the 32-day EMA, it goes long. When the price breaks through the lower band or the 8-day EMA crosses below the 32-day EMA, it exits. The stop loss is set below the middle band of the channel. 

Specifically, the entry conditions are:

1. The closing price breaks through the dynamic upper band formed by the highest high over past 20 days.

2. The 8-day EMA is above the 32-day EMA.

The exit conditions are:

1. Stop loss triggered when price drops below the middle band.

2. The 8-day EMA crosses below the 32-day EMA.

The strategy identifies trend direction using the dynamic channel and current uptrend status using the EMA crossover. This helps control risk.

## Advantages

- Dynamic channel breakout identifies trend direction effectively, avoiding whipsaws.
- 8-day and 32-day EMA crossover filters trades well. 
- Simple and clear rules, easy to understand.
- Reasonable stop loss mechanism.

## Risks

- Failed breakout may cause losses.
- Improper parameter tuning of channel range may cause it to be too wide or too narrow.
- Improper EMA periods may impact performance.
- Stop loss too tight may cause excessive stops.

The risks can be managed by optimizing channel period, EMA periods, and stop loss positioning.

## Improvement Areas

- Optimize channel period for different stocks.
- Test different EMA combinations to find optimal periods. 
- Incorporate volume to confirm breakouts.
- Trail stop loss after entry.

## Summary  

The dynamic oscillation breakout strategy has clear logic to identify trend and enter based on channel breakout and EMA crossover. The stop loss helps control risk. Parameter tuning such as channel period and EMA periods can improve profit factor. This strategy works well for stocks with continuation patterns, especially breaking previous highs.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-09 00:00:00
end: 2023-11-15 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Robrecht99

//@version=5
strategy("My Strategy", overlay=true, margin_long=100, margin_short=100)

fast = ta.sma(close, 8)
slow = ta.sma(close, 32)

plot(fast, color=color.red)
plot(slow, color=color.navy)

entrycondition1 = ta.crossover(fast, slow)
entrycondition2 = fast > slow
sellcondition1 = ta.crossunder(fast, slow)
sellcondition2 = slow > fast

atr = ta.atr(14)

//Donchian Channels
days = 20
h1 = ta.highest(high[1], days)
l1 = ta.lowest(low[1], days)
mid = math.avg(h1, l1)
plot(mid, "channel", color=#FF6D00)
u = plot(h1, "Upper", color=#2962FF)
l = plot(l1, "Lower", color=#2962FF)
fill(u, l, color.new(color.blue, 90))

if (close > h1 and entrycondition2)
    strategy.entry("long", strategy.long)
    stoploss = close - atr * 3
    trail = close - atr * 3
    strategy.exit("exit", "long", stop=stoploss, trail_offset=trail)
if (sellcondition1 and sellcondition2)
    strategy.close(id="long")

```

> Detail

https://www.fmz.com/strategy/432332

> Last Modified

2023-11-16 15:40:25

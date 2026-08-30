
> Name

Trailing-Stop-Loss-Strategy-Based-on-Price-Gaps
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/19d786e4e5ea7170dfd.png)
[trans]

## Overview
This strategy uses the price gap principle to buy when the low point is broken, and set stop loss orders and take profit orders to track the lowest price stop loss and achieve profits.
## Strategy Principle
When the price falls below the lowest point in the last N hours, locate the gap, enter the long position according to the set percentage, and set stop loss and take profit orders at the same time. After that, the stop loss line and take profit line will be moved according to the market situation. The specific logic is as follows:
1. Calculate the lowest point within N hours as the binding price
2. Enter long when the real-time price is lower than the binding price multiplied by the buy setting percentage.
3. Set the take-profit order as the entry price multiplied by the sell setting percentage
4. Set the stop loss order as the entry price minus the entry price multiplied by the stop loss percentage
5. The number of long orders is the percentage of strategic equity
6. Track the lowest price moving stop loss line
7. Stop profit or stop loss to close position
## Strategic advantage analysis
This strategy has the following advantages:
1. Adopt the idea of price gap, enter the market when the low point is broken, and increase the winning rate
2. Automatic tracking stop loss can lock in most profits
3. Configurable take-profit and stop-loss percentages to adapt to different markets
4. Suitable for varieties with obvious rotation characteristics
5. Simple operation and easy to implement
## Strategy risk analysis
There are also some risks with this strategy:
1. The gap breakthrough may not be successful, and it may drop again
2. Improper setting of stop loss or take profit may cause premature stop loss or take profit and cause greater market loss.
3. Parameters need to be optimized regularly to adapt to market changes
4. The applicable varieties are limited and may not be effective for some varieties.
5. There is a certain need for manual intervention
## Strategy optimization direction
This strategy can also be optimized from the following aspects:
1. Add machine learning algorithm to realize automatic optimization of parameters
2. Add more stop-loss and stop-profit methods, such as trailing stop, pending order stop, etc.
3. Optimize stop loss and take profit logic to achieve smarter and smoother stop loss and take profit
4. Combine more indicators to judge signal reliability and filter out false signals
5. Expand the application to more varieties and improve the versatility of the strategy
## Summarize
Overall, this strategy is a simple and effective trailing stop loss strategy based on the price gap idea. It reduces the probability of entering the market by mistake and can effectively lock in profits. There is still a lot of room for optimization in terms of parameter optimization and filtering, which is worthy of further research and improvement.
||
## Overview

This strategy adopts the price gap principle to go long when price breaks recent lows, with stop loss and take profit orders to trail the lowest price for profit taking.

## Strategy Logic

It identifies gaps when price breaks below the lowest price in recent N hours, goes long based on configured percentage, with stop loss and take profit orders. Stop loss line and take profit line move according to price action. The logic is:  

1. Calculate lowest price in recent N hours as binding price
2. Go long when realtime price is below binding price * buy percent 
3. Set take profit based on entry price * sell percent
4. Set stop loss based on entry price - entry price * stop loss percent
5. Position size is percent of strategy equity
6. Trail stop loss line with lowest price  
7. Close position when take profit or stop loss is triggered

## Advantage Analysis

The advantages of this strategy:

1. Utilize price gap concept, improve winning rate
2. Automatic trailing stop loss to lock in most profits
3. Customizable stop loss and take profit percentage for different markets
4. Works well for instruments with obvious rebounds  
5. Simple logic and easy to implement

## Risk Analysis  

There are also some risks:

1. Breakout of gaps may fail with lower lows
2. Improper stop loss or take profit settings may cause premature exit  
3. Require periodic parameter tuning for market changes
4. Limited applicable instruments, may not work for some
5. Manual intervention needed from time to time

## Optimization Directions

The strategy can be improved in the following aspects:

1. Add machine learning models for automatic parameter tuning
2. Add more types of stop loss/take profit, e.g. trailing stop loss, bracket orders
3. Optimize stop loss/take profit logic for smarter exits  
4. Incorporate more indicators to filter out false signals
5. Expand to more instruments to improve universality

## Conclusion

In conclusion, this is a simple and effective trailing stop loss strategy based on price gaps. It reduces false entries and locks in profits effectively. There is still much room for improvements in parameters tuning and signal filtering. It is worth further research and refinement.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|(?Squeeze Settings)Buy, %|
|v_input_2|true|Sell, %|
|v_input_3|true|Stop Loss, %|
|v_input_4|true|Max Bars To Sell|
|v_input_5|2|maxBars|
|v_input_6_close|0|Bind: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_7|true|(?Backtesting Period)Fixed Range|
|v_input_8|0|rangeStart: 1 Week|12 Hours|24 Hours|48 Hours|6 Hours|2 Weeks|1 Month|Maximum|
|v_input_9|timestamp(01 Aug 2021 00:00 +0000)|Backtesting Start|
|v_input_10|timestamp(01 Aug 2022 00:00 +0000)|Backtesting End|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-21 00:00:00
end: 2023-11-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

strategy(title="Squeeze Backtest by Shaqi v1.0", overlay=true, pyramiding=0, currency="USD", process_orders_on_close=true, commission_type=strategy.commission.percent, commission_value=0.075, default_qty_type=strategy.percent_of_equity, default_qty_value=100, initial_capital=100, backtest_fill_limits_assumption=0)
strategy.risk.allow_entry_in(strategy.direction.long)

R0 = "6 Hours"
R1 = "12 Hours"
R2 = "24 Hours"
R3 = "48 Hours"
R4 = "1 Week"
R5 = "2 Weeks"
R6 = "1 Month"
R7 = "Maximum"


buyPercent = input( title="Buy, %",         type=input.float,   defval=3,       minval=0.01,                        step=0.01,  inline="Percents",  group="Squeeze Settings") * 0.01
sellPercent = input(title="Sell, %",        type=input.float,   defval=1,       minval=0.01,                        step=0.01,  inline="Percents",  group="Squeeze Settings") * 0.01
stopPercent = input(title="Stop Loss, %",   type=input.float,   defval=1,       minval=0.01,        maxval=100,     step=0.01,  inline="Percents",  group="Squeeze Settings") * 0.01
isMaxBars = input(  title="Max Bars To Sell",               type=input.bool,    defval=true ,                                   inline="MaxBars",   group="Squeeze Settings")
maxBars = input(    title="",       type=input.integer, defval=2,     minval=0,           maxval=1000, step=1,                  inline="MaxBars",   group="Squeeze Settings")
bind = input(       title="Bind",           type=input.source,  defval=close,                                                                       group="Squeeze Settings")
isRange = input(    title="Fixed Range",               type=input.bool,    defval=true,                                         inline="Range",     group="Backtesting Period")
rangeStart = input( title="",                       defval=R4,      options=[R0, R1, R2, R3, R4, R5, R6, R7],                   inline="Range",     group="Backtesting Period")
periodStart = input(title="Backtesting Start", type=input.time,    defval=timestamp("01 Aug 2021 00:00 +0000"),                                     group="Backtesting Period")
periodEnd = input(  title="Backtesting End",   type=input.time,    defval=timestamp("01 Aug 2022 00:00 +0000"),                                     group="Backtesting Period")

int startDate = na
int endDate = na
if isRange
    if rangeStart == R0
        startDate := timenow - 21600000
        endDate := timenow
    else if rangeStart == R1
        startDate := timenow - 43200000
        endDate := timenow
    else if rangeStart == R2
        startDate := timenow - 86400000
        endDate := timenow
    else if rangeStart == R3
        startDate := timenow - 172800000
        endDate := timenow
    else if rangeStart == R4
        startDate := timenow - 604800000
        endDate := timenow
    else if rangeStart == R5
        startDate := timenow - 1209600000
        endDate := timenow
    else if rangeStart == R6
        startDate := timenow - 2592000000
        endDate := timenow
    else if rangeStart == R7
        startDate := time
        endDate := timenow
else 
    startDate := periodStart
    endDate := periodEnd

afterStartDate = (time >= startDate)
beforeEndDate = (time <= endDate)
notInTrade = strategy.position_size == 0
inTrade = strategy.position_size > 0

barsFromEntry = barssince(strategy.position_size[0] > strategy.position_size[1])
entry = strategy.position_size[0] > strategy.position_size[1]
entryBar = barsFromEntry == 0
notEntryBar = barsFromEntry != 0
buyLimitPrice = bind - bind * buyPercent
buyLimitFilled = low <= buyLimitPrice
sellLimitPriceEntry = buyLimitPrice * (1 + sellPercent)
sellLimitPrice = strategy.position_avg_price * (1 + sellPercent)

stopLimitPriceEntry = buyLimitPrice - buyLimitPrice * stopPercent
stopLimitPrice = strategy.position_avg_price - strategy.position_avg_price * stopPercent

if afterStartDate and beforeEndDate and notInTrade
    strategy.entry("BUY", true, limit = buyLimitPrice)
    strategy.exit("INSTANT", limit = sellLimitPriceEntry, stop = stopLimitPriceEntry)
strategy.cancel("INSTANT", when = inTrade)
if isMaxBars
    strategy.close("BUY", when = barsFromEntry >= maxBars, comment = "Don't Sell")
strategy.exit("SELL", limit = sellLimitPrice, stop = stopLimitPrice)

showStop = stopPercent <= 0.03

plot(showStop ? stopLimitPrice : na, title="Stop Loss Limit Order", style=plot.style_linebr, color=color.red, linewidth=1)
plot(sellLimitPrice, title="Take Profit Limit Order", style=plot.style_linebr, color=color.purple, linewidth=1)
plot(strategy.position_avg_price, title="Buy Order Filled Price", style=plot.style_linebr, color=color.blue, linewidth=1)
plot(buyLimitPrice, title="Trailing Buy Limit Order", style=plot.style_stepline, color=color.new(color.blue, 30), offset=1)


```

> Detail

https://www.fmz.com/strategy/433542

> Last Modified

2023-11-28 13:53:16

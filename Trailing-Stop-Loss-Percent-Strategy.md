
> Name

Dynamic stop-loss tracking strategy Trailing-Stop-Loss-Percent-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/e9440ada607c5d1b7d.png)
[trans]
## Overview
This strategy is a strategy with date-specific triggering of long position establishment and trailing stop loss risk management mechanisms. This strategy is particularly suitable for traders who wish to automate position entries based on specific calendar dates and manage positions through dynamic risk control methods such as trailing stops.
## Strategy Principle
This strategy first inputs a specific market entry date, including month and day, and then calculates the accurate market entry timestamp based on these dates. The strategy also enters a percentage parameter for the trailing stop.
On the entry date, the strategy will open a long position. At the same time, record the highest price highestPrice and stop loss price stopLoss. The highest price will be continuously updated in the subsequent time, and the stop loss price will trail downwards based on a certain percentage of the highest price.
If the price is lower than the stop loss price, the position will be closed and exited. Otherwise, the position will be held, and the stop loss price will continue to track downward based on the highest price, thereby locking in profits and controlling risks.
## Advantage Analysis
This strategy has several major advantages:
1. Can automatically enter the market based on specific dates. A strategy suitable for trading around major events.
2. Apply the trailing stop loss mechanism to dynamically lock in profits and effectively control risks.
3. The stop loss is set proportionally, and the operation is simple and intuitive. Stop loss range can be customized.
4. Long-term holdings can be achieved to maximize profits from rising stock prices.
## Risk Analysis
There are also some risks with this strategy:
1. There is a risk of stop loss being ineffective. If the stock price falls sharply in the short term and exceeds the stop loss line and then rebounds, it will be stopped out and will not be able to participate in the subsequent rebound.
2. Unable to limit the maximum loss. If the trailing stop loss ratio is set too large, the maximum loss may exceed the ideal range.
Corresponding optimization measures:
1. When you can combine other indicators to judge that the market is facing an adjustment, you can temporarily close the trailing stop to avoid the stop loss being ineffective.
2. Be cautious when setting the trailing stop loss ratio, which usually does not exceed 10%. Or set the maximum allowable loss value.
## Optimization direction
This strategy can be optimized from the following directions:
1. Add a profit-taking mechanism. When the price exceeds a certain level, say 50%, some or all profits are taken.
2. Use index indicators to determine the market structure and optimize the range of trailing stop loss. For example, when the market is in shock adjustment, the range can be appropriately relaxed.
3. Add a warehouse management module. When the price breaks through a new high again, you can consider adding positions to further increase profits.
## Summarize
This strategy is based on entering the market on a specific date and using the idea of ​​trailing stop loss, which can automatically enter the market and dynamically control risks. The strategy is simple, intuitive, easy to operate, and suitable for long-term positions. Through further optimization, it can become a very practical quantitative trading strategy.
||

## Overview

This strategy is designed for a long position entry with a date-specific trigger and a trailing stop loss mechanism for risk management. It is particularly useful for traders who want to automate their entries based on specific calendar dates and manage their positions with a dynamic risk control method like a trailing stop loss.

## Strategy Logic  

The strategy first takes input of specific entry dates, including month and day, then calculates the accurate entry timestamp based on these dates. It also inputs the percentage parameter for trailing stop loss.  

On the entry date, the strategy will open a long position. At the same time, it records the highest price (highestPrice) and stop loss price (stopLoss). The highestPrice keeps updating over time, while the stopLoss trails it by a certain percentage downwards.  

If the price falls below the stopLoss, the position will be closed. Otherwise, the position remains open, and the stopLoss keeps trailing the highestPrice to lock in profits and control risk.

## Advantage Analysis

The main advantages of this strategy are:

1. Automated entry based on specific dates. Suitable for strategies trading around significant events.  
2. Applies trailing stop loss to dynamically lock in profits and effectively manage risks.
3. Stop loss set as percentage, simple and intuitive to operate. Customizable loss range.  
4. Allows long-term holding to maximize upside potential.

## Risk Analysis  

There are also some risks:

1. Risk of stop loss failure. If price drops sharply below stop loss briefly then bounces back, the position may get stopped out and fail to capture the rebound.
2. No limit on maximum loss. If trailing stop loss percentage set too wide, max loss can exceed expectations.

Possible improvements:
1. Combine other indicators to pause trailing stop when market faces correction, avoiding failure.
2. Set stop loss percentage carefully, usually under 10%. Or set maximum tolerable loss.  

## Optimization  

Possible optimization directions:

1. Add profit taking mechanisms. When price rises 50% etc, take partial or full profits.
2. Optimize trailing width based on market regime signals from indices. Widen when market consolidating.   
3. Enhance position sizing. Consider pyramiding when new highs breakout for greater profits.

## Conclusion  

This strategy provides automated date-based entry and dynamic risk management via trailing stop loss. Simple and intuitive to operate, suitable for long-term holdings. Further optimizations can make it a very practical quant trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|true|Entry Day|
|v_input_int_2|true|Entry Month|
|v_input_int_3|2023|Entry Year|
|v_input_float_1|5|Trailing Stop Loss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-24 00:00:00
end: 2024-01-31 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy(title="Trailing Stop Loss Percent",
     overlay=true, pyramiding=1)

// Input for the specific entry date
entryDay = input.int(defval = 1, title = "Entry Day", minval = 1, maxval = 31)
entryMonth = input.int(defval = 1, title = "Entry Month", minval = 1, maxval = 12)
entryYear = input.int(defval = 2023, title = "Entry Year", minval = 1970)

// Calculate the entry date timestamp
entryDate = timestamp(entryYear, entryMonth, entryDay, 00, 00)

// Trailing Stop Loss Percentage
trailStopPercent = input.float(defval = 5.0, title = "Trailing Stop Loss (%)", minval = 0.1)

// Entry Condition
enterTrade = true

// Variables to track the highest price and stop loss level since entry
var float highestPrice = na
var float stopLoss = na

// Update the highest price and stop loss level
if strategy.position_size > 0
    highestPrice := math.max(highestPrice, high)
    stopLoss := highestPrice * (1 - trailStopPercent / 100)

// Enter the strategy
if enterTrade
    strategy.entry("Long Entry", strategy.long)
    highestPrice := high
    stopLoss := highestPrice * (1 - trailStopPercent / 100)

// Exit the strategy if the stop loss is hit
if strategy.position_size > 0 and low <= stopLoss
    strategy.close("Long Entry")

// Plotting the stop loss level for reference
plot(strategy.position_size > 0 ? stopLoss : na, "Trailing Stop Loss", color=color.red)
```

> Detail

https://www.fmz.com/strategy/440691

> Last Modified

2024-02-01 11:05:36

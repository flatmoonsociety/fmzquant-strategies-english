
> Name

YinYang dual-track trend trading strategy based on RSI and trading volume YinYang-RSI-Volume-Trend-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1949355e380af7d8bd9.png)
[trans]

## Overview
This strategy is a strategy that uses a combination of relative strength index (RSI) and trading volume indicators to identify trend directions and follow trends. The key points are:
1. Use the weighted moving average to calculate the central axis, and combine the transaction volume information to determine the trend central axis.
2. Set the buying area and selling area based on the central axis
3. Use RSI information to adjust the range of buy and sell zones
4. Set stop loss and take profit lines after entering the buying area
5. Has a re-entry mechanism
## Strategy Principle
This strategy uses the following indicators and parameters:
- Central axis: Calculate the weighted moving average of the highest price and lowest price within a certain period, use trading volume as the weight to determine the direction of the central axis of the trend
- RSI: Calculate the relative strength index within a certain period and convert it into a value in the range of 0-1
- Buying zone: the central axis plus a certain proportion of RSI adjustment, you can go long after entering the buying zone
- Sell zone: the central axis minus a certain proportion of RSI adjustment amount, you can go short after entering the sell zone
- Take profit line: central axis
- Stop loss line: set at a certain percentage below the buying area/above the selling area
When the price enters the buying zone or selling zone, open a position in the corresponding direction. Then set the take profit and stop loss positions, and close the position when the take profit or stop loss is triggered. At the same time, a re-entry mechanism is set up. If the configuration allows, you can re-enter when the opening signal is triggered again.
## Strategic Advantages
This strategy has the following advantages:
1. Use the dual indicators of RSI and trading volume to identify trends and improve the accuracy of judgment.
2. RSI parameterizes the buying zone and selling zone ranges to make them more consistent with the actual trend.
3. Trading volume information gives higher weight to price changes, making the central axis more accurate.
4. Have a stop-loss mechanism to control risks
5. Can re-enter to reduce the risk of false breakthroughs
## Risk Analysis
This strategy also has some risks:
1. Improper setting of RSI and trading volume parameters may affect the accuracy of determining the range of the buying and selling zone.
2. The central axis cannot completely accurately judge the trend, and false breakthroughs may occur.
3. Setting the stop loss point too wide may result in higher losses
4. Re-entry mechanism may lead to over-trading
Corresponding optimization measures:
1. Adjust the RSI cycle and trading volume cycle parameters to make them more consistent with market conditions.
2. Combine with other indicators to verify buying and selling signals to avoid false breakthroughs
3. Tighten the stop loss point appropriately to control single loss
4. Limit the number of daily transactions to avoid excessive trading
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Try other indicators to verify buying and selling signals, such as K-line patterns, volatility indicators, etc.
2. Add a position management mechanism, such as adding positions after making profits, etc.
3. Increase the accuracy of machine learning algorithms in judging trends and improve the accuracy of buying and selling zone settings.
4. Evaluate the optimal parameters for setting take-profit and stop-loss points
5. Different varieties have different parameters and need to be tested and optimized individually.
## Summarize
Overall, this strategy is a quantitative strategy that uses RSI and trading volume indicators for trend tracking. It has a double verification mechanism for identifying trend signals, and sets up take-profit and stop-loss to control risks, as well as a re-entry mechanism to increase profit opportunities. Through parameter adjustment and algorithm optimization, this strategy can become a very practical trend following trading strategy.
||

## Overview

This strategy is a trend following strategy that utilizes a combination of Relative Strength Index (RSI) and volume to identify trend direction and follow trends. Key points include:

1. Using Volume Weighted Moving Average to calculate midline and incorporate volume information to determine trend midpoint  
2. Setting up buy zone and sell zone based on midline
3. Using RSI information to adjust range of buy zone and sell zone
4. Setting stop loss and take profit after entering buy/sell zones
5. Having re-entry mechanism 

## Strategy Logic

This strategy uses the following indicators and parameters:

- Midline: Volume Weighted Moving Average of highest and lowest prices in certain periods to determine midpoint of the trend
- RSI: Relative Strength Index calculated over certain periods, converted into 0-1 range  
- Buy Zone: Midline plus RSI adjusted amount at certain ratio, long entry when price enters
- Sell Zone: Midline minus RSI adjusted amount at certain ratio, short entry when price enters
- Take Profit Line: Midline
- Stop Loss Line: Certain percentage below buy zone/above sell zone

When price enters buy or sell zone, a corresponding direction order will be opened. Stop loss and take profit lines are then set. When take profit or stop loss is triggered, position will be closed. A re-entry mechanism is also set so that new orders can be opened when signal triggers again if configured.

## Advantages

The advantages of this strategy include:

1. Using both RSI and volume to identify trends, improving accuracy
2. RSI parameterized adjustment makes buy/sell zone adapt better to actual trend  
3. Volume information assigns higher weight to price actions, making midline more accurate
4. Having stop loss mechanism to control risks
5. Allows re-entry, reducing risks of false breakouts

## Risks

There are also some risks:

1. Improper RSI and volume parameters may affect buy/sell zone accuracy
2. Midline may fail to accurately determine trend, causing false breakout
3. Stop loss too wide may lead to higher losses  
4. Re-entry may cause over-trading

Solutions:

1. Adjust RSI and volume cycle to fit market conditions
2. Use other indicators to verify buy/sell signals 
3. Tighten stop loss to limit losses  
4. Limit trades per day to prevent over-trading

## Optimization

This strategy can be optimized by:

1. Trying other indicators to verify signals e.g. candlestick, volatility indicators etc
2. Adding position sizing mechanisms e.g. pyramiding winners
3. Using machine learning algorithms to improve buy/sell zone accuracy 
4. Evaluating optimum parameters for stop loss and take profit  
5. Parameters need separate test and optimization for different products

## Conclusion  

In conclusion, this is a quantitative trend following strategy utilizing RSI and volume indicators. It has dual verification system to identify signals, stop loss/profit take to control risks, and re-entry mechanism to improve profitability. With parameter tuning and algorithm optimization, it can become a very practical trend trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|80|Trend Length:|
|v_input_source_1_close|0|Purchase Source (Long and Short):: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_source_2_close|0|Exit Source (Long and Short):: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_bool_1|true|Use Take Profit|
|v_input_bool_2|true|Use Stop Loss|
|v_input_float_1|0.1|Stoploss Multiplier %:|
|v_input_string_1|0|Reset Purchase Availability After:: Entry|Stop Loss|None|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-21 00:00:00
end: 2023-12-21 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@    ,@@@@@@@@@@@@@@@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@      @@@@@@@@@@@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@        @@@@@@@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@         @@@@@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@           @@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@        .@@@@@@@@@@@@@@@            @@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@          *@@@@@@@@@@@@@@             @@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@         @@@@@@@@@@@@@@@               @@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@     @@@@@@@@@@@@@@@@                 @@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@                  @@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@.                    @@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@                      @@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@.                         @
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@                             @
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@,                                       @
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@                                                @
// @@@@@@@@@@@@@@@@@@@@@@@@@@@                                                    @
// @@@@@@@@@@@@@@@@@@@@@@@@@                                                     @@
// @@@@@@@@@@@@@@@@@@@@@@@                                                       @@
// @@@@@@@@@@@@@@@@@@@@@@                                                       @@@
// @@@@@@@@@@@@@@@@@@@@@*                @@@@@                                 @@@@
// @@@@@@@@@@@@@@@@@@@@@               @@@@@@@@@                              @@@@@
// @@@@@@@@@@@@@@@@@@@@@              @@@@@@@@@@@                           @@@@@@@
// @@@@@@@@@@@@@@@@@@@@@               @@@@@@@@%                           @@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@                                                @@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@                                            @@@@@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@                                        %@@@@@@@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@                                   @@@@@@@@@@@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@                           @@@@@@@@@@@@@@@@@@@@@@@@
// @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@                @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
// © YinYangAlgorithms

//@version=5
strategy("YinYang RSI Volume Trend Strategy", shorttitle="YinYang RSVT Strategy", overlay=true )
// ~~~~~~~~~~~ INPUTS ~~~~~~~~~~~ //
len = input.int(80, "Trend Length:", tooltip="How far back should we span this indicator?\nThis length effects all lengths of the indicator")
purchaseSrc = input.source(close, "Purchase Source (Long and Short):", tooltip="What source needs to exit the purchase zone for a purchase to happen?")
exitSrc = input.source(close, "Exit Source (Long and Short):", tooltip="What source needs to hit a exit condition to stop the trade (Take profit, Stop Loss or hitting the other sides Purchase Zone)?")
useTakeProfit = input.bool(true, "Use Take Profit", tooltip="Should we take profit IF we cross the basis line and then cross it AGAIN?")
useStopLoss = input.bool(true, "Use Stop Loss", tooltip="Stop loss will ensure you don't lose too much if its a bad call")
stopLossMult = input.float(0.1, "Stoploss Multiplier %:", tooltip="How far from the purchase lines should the stop loss be")
resetCondition = input.string("Entry", "Reset Purchase Availability After:", options=["Entry", "Stop Loss", "None"],
 tooltip="If we reset after a condition is hit, this means we can purchase again when the purchase condition is met. \n" +
 "Otherwise, we will only purchase after an opposite signal has appeared.\n" +
 "Entry: means when the close enters the purchase zone (buy or sell).\n" +
 "Stop Loss: means when the close hits the stop loss location (even when were out of a trade)\n" +
 "This allows us to get more trades and also if our stop loss initally was hit but it WAS a good time to purchase, we don't lose that chance.")

// ~~~~~~~~~~~ VARIABLES ~~~~~~~~~~~ //
var bool longStart = na
var bool longAvailable = na
var bool longTakeProfitAvailable = na
var bool longStopLoss = na
var bool shortStart = na
var bool shortAvailable = na
var bool shortTakeProfitAvailable = na
var bool shortStopLoss = na

resetAfterStopLoss = resetCondition == "Stop Loss"
resetAfterEntry = resetCondition == "Entry"

// ~~~~~~~~~~~ CALCULATIONS ~~~~~~~~~~~ //
// Mid Line
midHigh = ta.vwma(ta.highest(high, len), len)
midLow = ta.vwma(ta.lowest(low, len), len)
mid = math.avg(midHigh, midLow)
midSmoothed = ta.ema(mid, len)

//Volume Filtered
avgVol = ta.vwma(volume, len)
volDiff = volume / avgVol
midVolSmoothed = ta.vwma(midSmoothed * volDiff, 3)

//RSI Filtered
midDifference = ta.sma(midHigh - midLow, len)
midRSI = ta.rsi(midVolSmoothed, len) * 0.01
midAdd = midRSI * midDifference

//Calculate Zones
purchaseZoneHigh = midSmoothed + midAdd
purchaseZoneLow = midSmoothed - midAdd
purchaseZoneBasis = math.avg(purchaseZoneHigh, purchaseZoneLow)

//Create Stop Loss Locations
stopLossHigh = purchaseZoneHigh * (1 + (stopLossMult * 0.01))
stopLossLow = purchaseZoneLow * (1 - (stopLossMult * 0.01))

// ~~~~~~~~~~~ PURCHASE CALCULATIONS ~~~~~~~~~~~ //
//Long
longEntry = ta.crossunder(purchaseSrc, purchaseZoneLow)
longStart := ta.crossover(purchaseSrc, purchaseZoneLow) and longAvailable
longAvailable := ta.crossunder(purchaseSrc, purchaseZoneHigh) or (resetAfterStopLoss and longStopLoss) or (resetAfterEntry and longEntry) ? true : longStart ? false : longAvailable[1]
longEnd = ta.crossover(exitSrc, purchaseZoneHigh)
longStopLoss := ta.crossunder(exitSrc, stopLossLow)
longTakeProfitAvailable := ta.crossover(exitSrc, purchaseZoneBasis) ? true : longEnd ? false : longTakeProfitAvailable[1]
longTakeProfit = ta.crossunder(exitSrc, purchaseZoneBasis) and longTakeProfitAvailable

//Short
shortEntry = ta.crossover(purchaseSrc, purchaseZoneHigh)
shortStart := ta.crossunder(purchaseSrc, purchaseZoneHigh) and shortAvailable
shortAvailable := ta.crossover(purchaseSrc, purchaseZoneLow) or (resetAfterStopLoss and shortStopLoss) or (resetAfterEntry and shortEntry)? true : shortStart ? false : shortAvailable[1]
shortEnd = ta.crossunder(exitSrc, purchaseZoneLow)
shortStopLoss := ta.crossover(exitSrc, stopLossHigh)
shortTakeProfitAvailable := ta.crossunder(exitSrc, purchaseZoneBasis) ? true : shortEnd ? false : shortTakeProfitAvailable[1]
shortTakeProfit = ta.crossover(exitSrc, purchaseZoneBasis) and shortTakeProfitAvailable

// ~~~~~~~~~~~ PLOTS ~~~~~~~~~~~ //
shortLine = plot(purchaseZoneHigh, color=color.green)
shortStopLossLine = plot(stopLossHigh, color=color.green) //color=color.rgb(0, 97, 3)
fill(shortLine, shortStopLossLine, color = color.new(color.green, 90))
plot(purchaseZoneBasis, color=color.white)
longLine = plot(purchaseZoneLow, color=color.red)
longStopLossLine = plot(stopLossLow, color=color.red) //color=color.rgb(105, 0, 0)
fill(longLine, longStopLossLine, color=color.new(color.red, 90))

// ~~~~~~~~~~~ STRATEGY ~~~~~~~~~~~ //
if (longStart)
    strategy.entry("buy", strategy.long)
else if (longEnd or (useStopLoss and longStopLoss) or (useTakeProfit and longTakeProfit))
    strategy.close("buy")

if (shortStart)
    strategy.entry("sell", strategy.short)
else if (shortEnd or (useStopLoss and shortStopLoss) or (useTakeProfit and shortTakeProfit))
    strategy.close("sell")

// ~~~~~~~~~~~ ALERTS ~~~~~~~~~~~ //
if longStart or (longEnd or (useStopLoss and longStopLoss) or (useTakeProfit and longTakeProfit)) or shortStart or (shortEnd or (useStopLoss and shortStopLoss) or (useTakeProfit and shortTakeProfit))
    alert("{{strategy.order.action}} | {{ticker}} | {{close}}", alert.freq_once_per_bar)
```

> Detail

https://www.fmz.com/strategy/436244

> Last Modified

2023-12-22 14:29:05

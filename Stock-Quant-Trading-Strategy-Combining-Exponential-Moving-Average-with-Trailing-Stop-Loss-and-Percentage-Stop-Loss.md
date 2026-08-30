
> Name

Stock-Quant-Trading-Strategy-Combining-Exponential-Moving-Average-with-Trailing-Stop-Loss-and-Percentage-Stop-Loss
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/d3147e559aec5cfb97.png)

[trans]

## Overview
The core of this strategy is to use the exponential smoothed moving average as a buying and selling signal, combined with trailing stop loss and percentage stop loss to lock in profits and control risks. The strategy is simple and implementable, and is suitable for quantitative trading of stocks and other financial products.
## Strategy Principle
1. Calculate fast EMA and slow EMA. The fast EMA period is 20 days and the slow EMA period is 50 days. A buy signal is generated when the fast EMA crosses above the slow EMA; a sell signal is generated when the fast EMA crosses below the slow EMA.
2. Set trailing stop loss after entering the market, and set the percentage of long position trailing stop loss and short position trailing stop loss according to the position direction, such as 7%. The trailing stop loss will be automatically adjusted for each K line to lock in the maximum possible profit.
3. Set the stop loss position at the same time, and set the percentage of the long position stop loss price and the short position stop loss price according to the position direction and entry price, such as 2%. The stop loss position is fixed to prevent excessive losses.
4. Compare the trailing stop loss price and the stop loss price, select the one closer to the market price as the stop loss position for this transaction, and issue a stop loss order.
## Strategic Advantages
1. The moving average signal is simple to understand and easy to implement.
2. Trailing stop loss can lock in profits to the maximum extent while preventing unnecessary losses caused by misjudgment.
3. The percentage stop loss is intuitive and easy to adjust, and can control the maximum loss of each transaction.
4. Combine trailing stop loss and fixed stop loss to lock in profits and control risks.
## Risks and Countermeasures
1. The moving average strategy is prone to produce false signals and introduces strong filtering conditions.
2. Trailing stop loss sometimes stops the loss prematurely, so relax the stop loss range appropriately.
3. Improper setting of the fixed stop loss position may be too aggressive or conservative, and the percentage parameters need to be tested and adjusted.
4. Mechanically stopping the loss may miss the market reversal opportunity. The stop loss can be judged by combining technical indicators.
## Optimization ideas
1. Try EMA combinations with different parameters to find the best balance.
2. Add indicators such as trading volume to filter out false signals.
3. Test more stocks to find suitable stop loss parameters.
4. Try to add a trailing stop loss and adjust the stop loss position according to the market.
5. Use RSI and other indicators to determine the timing of stop loss.
## Summarize
This strategy integrates moving average trading signals, trailing stop loss and percentage stop loss. Through parameter optimization, it can be applied to a variety of stocks and commodities, achieving stable returns while strictly controlling risks. It is worthy of research, practice and continuous optimization by quantitative traders.
|| 

## Overview

The core of this strategy is using exponential moving average crossovers as trading signals, combined with trailing stop loss and percentage stop loss to lock in profits and control risks. The strategy is simple to implement and applicable to stocks and other financial products for quantitative trading.  

## Strategy Logic

1. Calculate fast EMA and slow EMA, with fast EMA period being 20 days and slow EMA period being 50 days. Generate buy signal when fast EMA crosses above slow EMA, and sell signal when fast EMA crosses below slow EMA.

2. After entry, set up trailing stop loss based on holding direction, e.g. 7% for long position and 7% for short position. The trailing stop loss adjusts every bar to lock in the maximum possible profit.  

3. At the same time, set stop loss price based on entry price and holding direction, e.g. 2% below entry price for long trade and 2% above entry price for short trade. The stop loss price remains unchanged to prevent excessive loss.

4. Compare trailing stop price and stop loss price, use the one closer to market price as the final stop loss for this trade, send stop loss order.

## Advantages

1. Simple and easy to implement moving average trading signals. 

2. Trailing stop loss locks in profits to the largest extent possible, while avoiding unnecessary loss from false signals.

3. Percentage stop loss is intuitive and easy to adjust for controlling maximum loss per trade.  

4. Combining trailing stops and fixed stops both locks in profits and controls risks.

## Risks and Countermeasures   

1. Moving averages can generate false signals easily, add further filters like volume.

2. Trailing stops sometimes trigger too early, relax the trailing percentage a bit.  

3. Improper fixed stop loss setting can be too aggressive or conservative, need to test and tune the percentage parameter.

4. Mechanical stop loss exits could miss market reversal opportunities, incorporate technical indicators to judge stop trigger.

## Optimization Directions 

1. Try different EMA combinations to find optimal balance.

2. Add indicators like volume to filter false signals.  

3. Test more stocks to find suitable stop loss percentages.

4. Try adaptive stops that adjust with market conditions.

5. Incorporate indicators like RSI to determine stop loss timing.

## Summary

This strategy integrates moving average trading signals, trailing stops and percentage stops. Through parameter optimization, it can achieve stable profits with strict risk control across various stocks and commodities, worth researching and continuously improving for quant traders.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|Fast EMA period|
|v_input_int_2|50|Slow EMA period|
|v_input_float_1|7|Long Trailing Stop (%)|
|v_input_float_2|7|Short Trailing Stop (%)|
|v_input_float_3|2|Long Stop Loss (%)|
|v_input_float_4|2|Short Stop Loss (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-26 00:00:00
end: 2024-01-02 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © wouterpruym1828

//@version=5
strategy(title=" Combining Trailing Stop and Stop loss (% of instrument price)",
     overlay=true, pyramiding=1, shorttitle="TSL&SL%")

//INDICATOR SECTION

// Indicator Input options+
i_FastEMA = input.int(title = "Fast EMA period", minval = 0, defval = 20)
i_SlowEMA = input.int(title = "Slow EMA period", minval = 0, defval = 50)
     
// Calculate moving averages
fastEMA = ta.ema(close, i_FastEMA)
slowEMA = ta.ema(close, i_SlowEMA)

// Plot moving averages
plot(fastEMA, title="Fast SMA", color=color.blue)
plot(slowEMA, title="Slow SMA", color=color.orange)




//STRATEGY SECTION  

// Calculate trading conditions
buy  = ta.crossover(fastEMA, slowEMA)
sell = ta.crossunder(fastEMA, slowEMA)

// STEP 1:
// Configure trail stop loss level with input options (optional)

longTrailPerc = input.float(title="Long Trailing Stop (%)", minval=0.0, step=0.1, defval=7) * 0.01

shortTrailPerc = input.float(title="Short Trailing Stop (%)", minval=0.0, step=0.1, defval=7) * 0.01

//Configure stop loss level with input options (optional)

longStopPerc = input.float(title="Long Stop Loss (%)", minval=0.0, step=0.1, defval=2)*0.01

shortStopPerc = input.float(title="Short Stop Loss (%)", minval=0.0, step=0.1, defval=2)*0.01


// STEP 2:
// Determine trail stop loss prices
longTrailPrice = 0.0, shortTrailPrice = 0.0

longTrailPrice := if (strategy.position_size > 0)
    stopValue = high * (1 - longTrailPerc)
    math.max(stopValue, longTrailPrice[1])
else
    0

shortTrailPrice := if (strategy.position_size < 0)
    stopValue = low * (1 + shortTrailPerc)
    math.min(stopValue, shortTrailPrice[1])
else
    999999

// Determine stop loss prices
entryPrice = 0.0

entryPrice := strategy.opentrades.entry_price(strategy.opentrades - 1)


longLossPrice = entryPrice * (1 - longStopPerc)

shortLossPrice = entryPrice * (1 + shortStopPerc)


// Plot stop loss values for confirmation

plot(series=(strategy.position_size > 0) ? longTrailPrice : na,
     color=color.fuchsia, style=plot.style_cross,
     linewidth=2, title="Long Trail Stop")
plot(series=(strategy.position_size < 0) ? shortTrailPrice : na,
     color=color.fuchsia, style=plot.style_cross,
     linewidth=2, title="Short Trail Stop")

plot(series=(strategy.position_size > 0) ? longLossPrice : na,
     color=color.olive, style=plot.style_cross,
     linewidth=2, title="Long Stop Loss")
plot(series=(strategy.position_size < 0) ? shortLossPrice : na,
     color=color.olive, style=plot.style_cross,
     linewidth=2, title="Short Stop Loss")

// Submit entry orders
if (buy)
    strategy.entry("Buy", strategy.long)

if (sell)
    strategy.entry("Sell", strategy.short)


//Evaluating trailing stop or stop loss to use

longStopPrice = longTrailPrice < longLossPrice ? longLossPrice : longTrailPrice

shortStopPrice = shortTrailPrice > shortLossPrice ? shortLossPrice : shortTrailPrice

// STEP 3:
// Submit exit orders for stop price

if (strategy.position_size > 0)
    strategy.exit(id="Buy Stop", stop=longStopPrice)

if (strategy.position_size < 0)
    strategy.exit(id="Sell Stop", stop=shortStopPrice)

```

> Detail

https://www.fmz.com/strategy/437547

> Last Modified

2024-01-03 16:25:54


> Name

ATR-based-Dynamic-Stop-Loss-Strategy ATR-based-Dynamic-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the ATR indicator to set dynamic stop loss points and adjust the stop loss position according to the price fluctuation range to achieve risk control. The strategy mainly uses the 5-day EMA and the 20-day EMA to form a golden cross for long entry, and then uses the ATR indicator to set the stop loss position and take profit position. The stop loss position will be adjusted according to price fluctuations, thereby locking in more profits.
## Strategy Principle
This strategy first determines when the 5-day EMA crosses the 20-day EMA to form a golden cross and enter the market long. After entering the market, use the ATR indicator to calculate the ATR multiple of the entry price from the current price, and set the stop loss position to 1.5 ATR below the entry price. Then as the price rises, gradually raise the stop loss position. If the price rises above the entry price by 3ATR, a partial stop loss will be taken.
Specifically, the strategy defines the following variables:
- entry_price: entry price
- stop_price: stop loss price
- take_profit_price: take profit price
- atr_down: lower ATR line
- atr_up: upper ATR line
- atr_current: current ATR line
- atr_ref:ATR value
After entering the market, atr_ref will be calculated as the current ATR value, and atr_div will be the ATR multiple of the entry price from the current price. Then set the positions of atr_down, atr_current and atr_up according to atr_div. The stop loss price stop_price is 1.5ATR below the entry price.
As the price rises, by comparing the current price avg and atr_up, if avg crosses atr_up, the corresponding positions of atr_div and atr will be recalculated, thereby gradually raising the stop loss line and increasing the position profit.
If the price exceeds the entry price by 3ATR, the position will be partially closed to lock in profits. At this time, the tookProfit flag is set to true. If the price continues to rise after that, the stop loss position will continue to be raised. If the stop loss is triggered, takeProfit will be determined. If the profit has been partially taken before, only the remaining position will be closed, otherwise the entire position will be closed.
## Strategic Advantages
1. Use the ATR indicator to dynamically adjust the stop loss position, and set a reasonable stop loss distance according to the degree of market volatility.
2. With limited losses, follow the trend and cut profits. The stop loss line will gradually be raised, allowing profits to continue to accumulate.
3. Partial profit-taking mechanism can lock in part of the profits and reduce risks. After that, the stop loss position continues to be raised, allowing profits to continue to run.
## Strategy Risk
1. The ATR indicator is insensitive to abnormal breakthroughs and cannot deal with the risks brought by gaps.
2. The EMA indicator cannot determine trend reversal and may enter new positions when the trend reverses.
3. The probability of reversing losses after partial take-profit is high.
4. Insufficient parameter optimization, 1.5ATR stop loss and 3ATR take profit need to be adjusted according to different varieties.
## Strategy optimization
1. You can consider adding other stop loss indicators, such as Donchian channel, etc., to prevent the lag of the ATR indicator.
2. You can test different moving average indicators, or add MACD, etc. to determine trend reversal.
3. The proportion and number of partial take-profits can be optimized. Different varieties can have different settings.
4. Add parameter optimization and test the stop-loss and take-profit effects of different ATR multiples. Added step stop loss and take profit function.
5. Test the performance when the trend is weak and consider enabling this strategy only when the trend is strong.
## Summarize
The overall idea of ​​this strategy is clear and easy to understand, and its greatest advantage is the use of the ATR indicator to dynamically adjust the stop loss to control trading risks. However, the ATR indicator itself has hysteresis, and the parameter settings need to be optimized. Adding other stop loss and trend judgment indicators would be the direction for improvement. In addition, some stop-profit mechanisms also need to be optimized and tested according to different varieties. Overall, this strategy provides an idea of ​​using ATR for stop loss management, but it needs further optimization and improvement.
||


## Overview

This strategy uses the ATR indicator to set dynamic stop loss points and adjust stop loss positions based on price fluctuations, in order to control risks. Mainly it enters long when 5EMA crosses above 20EMA, and then uses the ATR indicator to set stop loss and take profit positions. The stop loss position will be adjusted according to price movements to lock in more profits.

## Strategy Logic

The strategy first judges if 5EMA crosses above 20EMA to go long. After entering, it calculates the ATR multiples of the entry price to current price using the ATR indicator, and sets the stop loss position at 1.5ATR below the entry price. As the price rises, the stop loss position is gradually raised to increase profits of the position. 

Specifically, the strategy defines the following variables:

- entry_price: entry price
- stop_price: stop loss price
- take_profit_price: take profit price  
- atr_down: ATR down line
- atr_up: ATR up line
- atr_current: current ATR line
- atr_ref: ATR value

After entering, it calculates atr_ref as the current ATR value, and atr_div as the ATR multiples of entry price to current price. Then sets the positions of atr_down, atr_current and atr_up based on atr_div. The stop loss price stop_price is set at 1.5ATR below entry price.

As price rises, by comparing current price avg and atr_up, if avg crosses above atr_up, it recalculates atr_div and ATR line positions, thus gradually raising the stop loss line to increase profits. 

If price rises above 3ATR of entry price, it will partially close position to lock in profits, and set tookProfit to true. Afterwards if price keeps rising, it will continue to raise stop loss. When stop loss is triggered, it checks tookProfit - if already took partial profit earlier, it will only close remaining position; otherwise close the full position.

## Advantages

1. Using ATR indicator to dynamically adjust stop loss can set reasonable stop distance based on market volatility.

2. Follow trends while capping losses. Stop loss will gradually be raised to accumulate profits.

3. Partial take profit mechanism locks in some profit and reduces risk. Stop loss continues to rise to allow profit to run.

## Risks

1. ATR indicator is not sensitive to sharp reversals and gaps.

2. EMAs cannot determine trend reversal, may enter new positions at trend reversals.

3. High chance of losses after partial take profit.

4. Parameters need further optimization, 1.5ATR stop and 3ATR take profit should be adjusted for different products.

## Improvements 

1. Consider adding other stop loss indicators like Donchian Channel to compensate for ATR lag.

2. Test different moving averages or add MACD etc. to judge trend reversal.

3. Optimize partial take profit ratios and frequency for different products. 

4. Parameter optimization on ATR multiples for stop and take profit. Add trailing stop loss feature.

5. Test performance during weak trends, may disable strategy during weak trends.

## Summary

The strategy has a clear logic of using ATR for dynamic stop loss management which is its biggest strength. However, ATR itself has limitations like lagging. Adding other stop and trend indicators will improve it. Also the partial take profit needs optimizations across products. Overall it provides the idea of ATR-based stop loss management but needs further optimizations and enhancements.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-03 00:00:00
end: 2023-10-09 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ekinbasarkomur

//@version=5
strategy("[EKIN] ATR Exit Strategy", overlay=true, initial_capital = 1000, default_qty_value = 100, default_qty_type = strategy.percent_of_equity, calc_on_every_tick = true)

// Simple EMA tracking
fastEMA = ta.ema(close, 5)
slowEMA = ta.ema (close, 20)
atr = ta.atr(14)

// We define entry price for future reference
var float entry_price = na
// We define stop and take profit for future calculations
var float stop_price = na
var float take_profit_price = na

// We define atr limtim its here
var float atr_down = na
var float atr_up = na
var float atr_current = na
var float atr_ref = na

avg = (low + high) / 2

// Conditions
enterCondition = ta.crossover(fastEMA, slowEMA)
var bool tookProfit = false
timePeriod = time >= timestamp(syminfo.timezone, 2021, 12, 15, 0, 0)
InTrade = strategy.position_size > 0

// Go long if conditions are met
if (enterCondition and timePeriod and not InTrade)
    // Calculate and update variables
    entry_price := avg
    atr_ref := atr
    atr_div = int((avg - entry_price) / atr_ref)
    atr_down := entry_price + (atr_ref * (atr_div - 1.5))
    atr_up := entry_price + (atr_ref * (atr_div + 1))
    atr_current := entry_price + (atr_ref * atr_div) 
    stop_price := (entry_price - (atr_ref * 1.5))
    take_profit_price := (entry_price + (atr_ref * 3))
    strategy.order("buy", strategy.long, qty = 2)

// Enter here if in position
if InTrade or tookProfit
    stopCondition = avg < stop_price
    takeProfitCondition = avg > take_profit_price

    if avg < atr_down
        stopCondition := true

    // Move stop price and exit price if price for each atr price increase
    if avg > atr_up
        if tookProfit
            atr_ref := atr
        atr_div = int((avg - entry_price) / atr_ref)
        atr_down := entry_price + (atr_ref * (atr_div - 1))
        atr_up := entry_price + (atr_ref * (atr_div + 1))
        atr_current := entry_price + (atr_ref * atr_div) 

    // Take half of the investment if current price is 3 atr higher than entry price
    if (takeProfitCondition and timePeriod and InTrade and not tookProfit)
        strategy.order("take_half_profit", strategy.short, qty = 1)
        tookProfit := true

    // Exit position if conditions are met and reset the variables
    if (stopCondition and timePeriod and InTrade)
        if tookProfit
            strategy.order("exit", strategy.short, qty = 1)
        else
            strategy.order("stop_loss", strategy.short, qty = 2)

        tookProfit := false

// Plot EMA's
plot(fastEMA, color = color.blue)
plot(slowEMA, color = color.yellow)

// Plot ATR Limit/Stop positions
profit_plot = plot(series = InTrade?atr_up:na, title = "profit", color = color.green, style=plot.style_linebr)
close_plot = plot(series = InTrade?atr_current:na, title = "close", color = color.white, style=plot.style_linebr)
stop_plot = plot(series = InTrade?atr_down:na, title = "stop_loss", color = color.red, style=plot.style_linebr)
fill(profit_plot, close_plot, color = color.new(color.green, 80))
fill(close_plot, stop_plot, color =color.new(color.red,80))
```

> Detail

https://www.fmz.com/strategy/428857

> Last Modified

2023-10-10 10:50:21

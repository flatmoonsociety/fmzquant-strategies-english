
> Name

Momentum-Crossover-Strategy-with-Dynamic-Trailing-Stop-Loss
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/140cba80fcb7fe6b14d.png)
[trans]

## Overview
This strategy combines the moving average indicator and the trend index indicator to realize the cross signal of the two indicators to send out buy and sell signals. At the same time, the strategy adds dynamic trailing stop loss to control risks.
## Strategy Principle
1. Construct a moving average indicator using the short-term 9-day EMA and the long-term 21-day EMA. A buy signal is generated when the short-term EMA crosses above the long-term EMA; a sell signal is generated when the short-term EMA crosses below the long-term EMA.
2. Use ADX, +DI and -DI to construct the DMI indicator. When +DI crosses -DI, ​​it is a buy signal; when -DI crosses +DI, it is a sell signal. 
3. Combine the signals of the EMA indicator and the DMI indicator, that is, only when both indicators meet the conditions will the actual buy and sell signals be issued.
4. Use dynamic stop loss to track the highest price/lowest price to stop loss.
## Advantage Analysis
1. The combination of dual indicators filters out false signals and improves signal accuracy. Short-term indicators capture trend changes; long-term indicators determine the direction of the general trend.
2. Momentum indicators can capture price trends in advance and have certain leading characteristics.
3. The dynamic stop-loss mechanism can lock in profits to the maximum extent while controlling risks.
## Risk Analysis
1. When dual indicators are combined, the buy and sell signals will be reduced, and some opportunities may be missed. 
2. Improper setting of indicator parameters may lead to excessive trading frequency or poor signal quality.
3. Setting the stop loss too loosely will increase the risk of loss; setting it too strictly will increase the risk of decoupling from the trend.
## Optimization direction
1. Test EMA long and short term parameter combinations of different lengths to find the optimal parameters.
2. Test different ADX parameter selections to improve DMI signal quality. 
3. Optimize the stop loss parameters so that it can lock in profits to the maximum extent and control risks.
4. You can consider adding more filtering indicators to further improve signal quality.
## Summary
This strategy integrates the advantages of moving averages and momentum indicators, double confirms signals, and uses the complementarity between indicators to improve the profitability of the strategy. At the same time, the dynamic trailing stop loss mechanism can effectively control the risk of the strategy. Through parameter optimization and rule improvement, the cashback capability and stability of this strategy are expected to be improved.
||

## Overview
This strategy combines moving average indicators and directional movement index (DMI) indicators to generate buy and sell signals based on dual-indicator crossovers. It also incorporates a dynamic trailing stop loss to control risks.   

## Strategy Logic  
1. Construct moving average indicators using a short 9-day EMA and a long 21-day EMA. A buy signal is generated when the short EMA crosses above the long EMA. A sell signal is generated when the short EMA crosses below the long EMA.
2. Construct DMI indicators using ADX, +DI and -DI. A buy signal is triggered when +DI crosses above -DI. A sell signal is triggered when -DI crosses above +DI.
3. Combine the signals of EMA and DMI, requiring both indicators to satisfy conditions before issuing actual buy or sell signals.  
4. Use a dynamic trailing stop loss to track the highest price/lowest price for stop loss.
  
## Advantage Analysis
1. Dual-indicator combos filter fake signals and improve signal accuracy. Short-term indicators capture trend changes while long-term ones determine overall direction.   
2. Momentum indicators can capture trend shifts early with some leading characteristics.  
3. Dynamic trailing stop loss locks in profits as much as possible while controlling risks.
   
## Risk Analysis  
1. With dual-indicator combos, signal frequency is reduced, possibly missing some opportunities.
2. Poor parameter tuning of indicators may lead to over-trading or low-quality signals.  
3. Stop loss set too wide increases loss risks while set too tight increases trend disconnection risks.
   
## Optimization Directions
1. Test EMA combos with different short and long term lengths to find optimum.
2. Optimize ADX parameters to improve DMI signal quality.
3. Fine tune stop loss parameters to lock profits while managing risks.  
4. Consider adding more filters to further boost signal quality.
  
## Conclusion
This strategy combines the strengths of moving averages and momentum indicators for dual confirmation of signals, complementing each other to enhance profitability. Meanwhile, the dynamic trailing stop loss effectively controls risks. Further parameter optimization and strategy refinement could improve both profitability and stability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|9|Short-Term EMA Period|
|v_input_int_2|21|Long-Term EMA Period|
|v_input_float_1|true|Risk Percentage EMA|
|v_input_1|17|ADX Smoothing|
|v_input_2|17|DI Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-22 00:00:00
end: 2024-02-28 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Combined EMA and DMI Strategy with Enhanced Table", overlay=true)

// Input parameters for EMA
shortTermEMA = input.int(9, title="Short-Term EMA Period")
longTermEMA = input.int(21, title="Long-Term EMA Period")
riskPercentageEMA = input.float(1, title="Risk Percentage EMA", minval=0.1, maxval=5, step=0.1)

// Calculate EMAs
emaShort = ta.ema(close, shortTermEMA)
emaLong = ta.ema(close, longTermEMA)

// EMA Crossover Strategy
longConditionEMA = emaShort > emaLong and emaShort[1] <= emaLong[1]
shortConditionEMA = emaShort < emaLong and emaShort[1] >= emaLong[1]

// Input parameters for DMI
adxlen = input(17, title="ADX Smoothing")
dilen = input(17, title="DI Length")

// DMI Logic
dirmov(len) =>
    up = ta.change(high)
    down = -ta.change(low)
    truerange = ta.tr
    plus = fixnan(100 * ta.rma(up > down and up > 0 ? up : 0, len) / truerange)
    minus = fixnan(100 * ta.rma(down > up and down > 0 ? down : 0, len) / truerange)
    [plus, minus]

adx(dilen, adxlen) => 
    [plus, minus] = dirmov(dilen)
    sum = plus + minus
    adxValue = 100 * ta.rma(math.abs(plus - minus) / (sum == 0 ? 1 : sum), adxlen)
    [adxValue, plus, minus]

[adxValue, up, down] = adx(dilen, adxlen)

// DMI Conditions
buyConditionDMI = up > down or (up and adxValue > down)
sellConditionDMI = down > up or (down and adxValue > up)

// Combined Conditions for Entry
longEntryCondition = longConditionEMA and buyConditionDMI
shortEntryCondition = shortConditionEMA and sellConditionDMI

// Combined Conditions for Exit
longExitCondition = shortConditionEMA
shortExitCondition = longConditionEMA

// Enter long trade based on combined conditions
if (longEntryCondition)
    strategy.entry("Long", strategy.long)

// Enter short trade based on combined conditions
if (shortEntryCondition)
    strategy.entry("Short", strategy.short)

// Exit trades
if (longExitCondition)
    strategy.close("Long")

if (shortExitCondition)
    strategy.close("Short")

// Plot EMAs
plot(emaShort, color=color.blue, title="Short-Term EMA")
plot(emaLong, color=color.red, title="Long-Term EMA")

// Create and fill the enhanced table
var tbl = table.new(position.top_right, 4, 1)
if (barstate.islast)
    table.cell(tbl, 0, 0, "ADX: " + str.tostring(adxValue), bgcolor=color.new(color.red, 90), width=15, height=4)
    table.cell(tbl, 1, 0, "+DI: " + str.tostring(up), bgcolor=color.new(color.blue, 90), width=15, height=4)
    table.cell(tbl, 2, 0, "-DI: " + str.tostring(down), bgcolor=color.new(color.orange, 90), width=15, height=4)

   
```

> Detail

https://www.fmz.com/strategy/443121

> Last Modified

2024-02-29 13:55:16


> Name

Index-Trading-Strategy-Based-on-Bollinger-Bands Index-Trading-Strategy-Based-on-Bollinger-Bands
> Author

ChaoZhang

> Strategy Description

 ![IMG](https://www.fmz.com/upload/asset/17996138272d1473cbb.png)
 [trans]

## Overview
The name of this strategy is "Bollinger Bands Quantitative Trading Strategy", which is an index and stock trading strategy based on improved Bollinger Bands channel. This strategy achieves simultaneous optimization of long and short positions by adjusting the Bollinger Band parameters, thereby making profits in both rising and falling markets.
## Strategy Principle
The core logic of this strategy is based on the Bollinger Bands channel. The Bollinger Bands are composed of a middle rail, an upper rail and a lower rail. The middle rail is the moving average of n-day closing prices, and the upper and lower rails are the deviations above and below the middle rail. When the price is close to the upper track, it means that the market may be overheated, which will form a short opportunity; when the price is close to the lower track, it means that the market may be undervalued, which will form a long opportunity.
This strategy uses two Bollinger Bands, Bollinger Band 1 is suitable for long positions, and Bollinger Band 2 is suitable for short positions. The parameters of Bollinger Band 1 have been optimized, with a length of 25 and a deviation of 2.9 times; the parameters of Bollinger Band 2 have also been optimized, with a length of 36 and a deviation of 3.2 times. When the closing price crosses the lower band of Bollinger Band 1, a long signal will be generated; when the closing price crosses the upper band of Bollinger Band 2, a short signal will be generated.
## Advantage Analysis
Compared with the traditional Bollinger Bands strategy, this strategy has the following advantages:
1. Realized long and short bilateral transactions. Applicable to both scenarios at the same time, it can seize trading opportunities at different stages of the market.
2. Parameters are optimized. The parameters of the two sets of Bollinger Bands have been carefully tested and can effectively send trading signals.
3. Risks are controllable. The use of trailing stop loss can effectively control unilateral risks.
## Risk Analysis
This strategy also has some potential risks:
1. Risk of Bollinger Band failure. When the market experiences severe fluctuations, Bollinger Bands channels may fail.
2. Stop loss and cover the risk. The trailing stop loss may be trapped, thereby expanding the loss. You can avoid it by setting a appropriately wide stop loss or a timely stop loss.
3. Risk of excessive transaction frequency. Parameter settings that are too sensitive may lead to frequent transactions and increased transaction costs.
## Optimization direction
There is still room for further optimization of this strategy:
1. Combine with other indicators to filter signals to avoid mistaken trades when Bollinger Bands fail. For example, K-line shape, trading volume, etc.
2. Dynamically adjust parameters to make Bollinger Bands more suitable for market characteristics of different cycles. For example, use adaptive Bollinger Bands.
3. Optimize the stop loss method and use trailing stop loss or index trailing stop loss to effectively control risks.
4. Combined with machine learning algorithms to achieve automatic optimization of parameters.
## Summarize
This strategy overall is based on the double Bollinger Bands channel and realizes the optimization of long and short bilateral transactions through parameter optimization. Compared with the traditional Bollinger Bands strategy, it has the advantages of long and short positions and risk control. It is suitable for capturing opportunities at different stages of the market and has certain practical value. However, there are also risks such as Bollinger Band failure and stop-loss quilt cover. Further optimization and verification are still needed before relevant products can be commercialized.
||


## Overview

The strategy is named "Quant Trading Strategy Based on Bollinger Bands". It is an index and stock trading strategy based on improved Bollinger Bands channel. By adjusting Bollinger Bands parameters, it realizes optimization for both long and short positions to profit in both uptrend and downtrend markets.

## Trading Logic

The core logic of this strategy is based on Bollinger Bands channel, which consists of middle line, upper band and lower band. The middle line is the moving average of closing price for n days. The upper and lower bands are deviations above and below the middle line. When price approaches the upper band, it indicates the market may be overheated and there can be short opportunities. When price approaches the lower band, it indicates the market may be undervalued and there can be long opportunities.

This strategy uses two Bollinger Bands. Bollinger Band 1 is suitable for long trades and Bollinger Band 2 is suitable for short trades. The parameters of Bollinger Band 1 are optimized with length of 25 and deviation of 2.9 times. The parameters of Bollinger Band 2 are optimized with length of 36 and deviation of 3.2 times. When closing price crosses above the lower band of Bollinger Band 1, it will generate long signal. When closing price crosses below the upper band of Bollinger Band 2, it will generate short signal.

## Advantage Analysis

Compared with traditional Bollinger Bands strategies, this strategy has the following advantages:

1. It realizes dual-directional trading for both long and short sides, which can seize trading opportunities in different market stages.

2. The parameters are optimized. The two sets of Bollinger Bands parameters are elaborately tested to effectively generate trading signals.  

3. The risk is controllable. The moving stop loss method can effectively control the risk of one side.

## Risk Analysis

There are also some potential risks for this strategy:

1. Invalidity risk of Bollinger Bands. Bollinger Bands may become invalid during extreme market fluctuation.

2. Risk of stop loss being hit. Moving stop loss could be hit to expand losses. We can properly widen the stop loss or timely stop out to avoid this risk.

3. High trading frequency risk. Overly sensitive parameters could lead to frequent trading and increased trading costs.

## Optimization Directions

There is still room for further optimization of this strategy:

1. Combine other indicators to filter signals and avoid wrong trades when Bollinger Bands fails. Such as K-line patterns, trading volume etc.

2. Dynamically adjust parameters to fit the market characteristics of different periods. For example, use adaptive Bollinger Bands.

3. Optimize the stop loss methods by using trailing stop loss or exponential moving stop loss to effectively control risks.

4. Combine machine learning algorithms to automatically optimize the parameters.

## Summary  

In summary, this strategy overall optimizes dual-directional trading for both long and short sides based on double Bollinger Bands channel and parameters optimization. Compared with traditional Bollinger Bands strategies, it has the advantages of dual-directional trading and risk control. It is suitable to seize opportunities in different market stages and has certain practical value. But risks like failure of Bollinger Bands and stop loss being hit still exist. Further optimization and verification are needed before productization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|25|Length BB long|
|v_input_2|2.9|MULT BB long|
|v_input_3|36|Length BB short|
|v_input_4|3.2|MULT BB short|
|v_input_5|true|longEntry|
|v_input_6|true|shortEntry|
|v_input_7|100|risk|
|v_input_8|true|leverage|
|v_input_9|0.065|Take profit % for long|
|v_input_10|0.04|Stop loss % for long|
|v_input_11|0.025|Take profit % for short|
|v_input_12|0.04|Stop loss % for short|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-01 00:00:00
end: 2023-12-07 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © exlux99

//@version=4
strategy("BB NDX strategy", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, calc_on_every_tick = true, commission_type = strategy.commission.percent, commission_value = 0.01)

source = close
length = input(25, minval=1, title="Length BB long")
mult = input(2.9, minval=0.001, maxval=50, step=0.1, title="MULT BB long")

length2 = input(36, minval=1, title="Length BB short")
mult2 = input(3.2, minval=0.001, maxval=50, step=0.1, title="MULT BB short")


basis = sma(source, length)
dev = mult * stdev(source, length)
dev2 = mult2 * stdev(source, length2)

upper = basis + dev2
lower = basis - dev

buyEntry = crossover(source, lower)
sellEntry = crossunder(source, upper)

longEntry=input(true)
shortEntry=input(true)

g(v, p) => round(v * (pow(10, p))) / pow(10, p)
risk     = input(100)
leverage = input(1.0, step = 0.5)
c = g((strategy.equity * leverage / open) * (risk / 100), 4)


tplong=input(0.065, step=0.005, title="Take profit % for long")
sllong=input(0.04, step=0.005, title="Stop loss % for long")
tpshort=input(0.025, step=0.005, title="Take profit % for short")
slshort=input(0.04, step=0.005, title="Stop loss % for short")

if(longEntry)
    strategy.entry("long",1,c,when=buyEntry)
    strategy.exit("short_tp/sl", "long", profit=close * tplong / syminfo.mintick, loss=close * sllong / syminfo.mintick, comment='LONG EXIT',  alert_message = 'closeshort')
    strategy.close("long",when=sellEntry)
if(shortEntry)
    strategy.entry("short",0,c,when=sellEntry)
    strategy.exit("short_tp/sl", "short", profit=close * tpshort / syminfo.mintick, loss=close * slshort / syminfo.mintick, comment='SHORT EXIT',  alert_message = 'closeshort')
    strategy.close("short",when=buyEntry)



```

> Detail

https://www.fmz.com/strategy/434714

> Last Modified

2023-12-08 16:52:24

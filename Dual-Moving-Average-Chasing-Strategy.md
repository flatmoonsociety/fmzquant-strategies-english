
> Name

Dual-Moving-Average-Chasing-Strategy based on moving average
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/ef17f34be575f473fca071c7545e7d2e36ca1f61036a7e5474cbda3703c51d1a.png)
[trans]
## Overview
This strategy is a tracking strategy based on moving averages. It uses the direction of the moving average and the shadow line of the candle to judge the price trend and strength to determine entries and exits. The core logic is to go long/short when the color of the second moving average changes, and then use the strong signal of the third moving average to add positions, up to 5 orders.
## Strategy Principle
The strategy uses the Heikin Ashi moving average to determine trends. Specifically, the strategy defines 3 moving averages:
1. The second moving average is used to determine trend turning and enters the market when its color changes.
2. The third moving average is used to identify strong breakthrough signals to decide to increase positions.
AddEntry logic:
1. When the color of the second moving average changes from red to green, go long
2. At this time, if the third moving average is a strong upward signal (green candle without lower shadow), then increase the position
3. A maximum of 5 additional orders are allowed
Exit logic:
1. When the color of any moving average changes, close the position
## Advantage Analysis
This strategy has the following advantages:
1. Use Heikin Ashi noise reduction to reduce false signals
2. Double moving average combination, more accurate judgment of entry timing
3. The position-adding mechanism tracks the trend and makes higher profits
## Risk Analysis
There are also some risks with this strategy:
1. Crossing of double moving averages can easily cause severe stop loss
2. Excessive addition of positions may increase losses
3. Parameters need to be adjusted to suit different varieties and cycles
Risks can be controlled by stopping losses, adjusting the number of positions added, and optimizing parameters.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test the parameter settings of different moving average indicators
2. Optimize stop loss strategies, such as trailing stop loss
3. Test parameters separately according to different varieties
4. Add filter conditions to avoid adding positions too quickly
5. Combine with other indicators to determine the timing of entry
## Summarize
Overall, this strategy is a tracking strategy based on the directionality of double moving averages. It combines the advantages of trend judgment and breakthrough judgment, and expands profits by adding positions. But you also need to pay attention to risk control and adjust parameters appropriately. In the future, improvements can be made from aspects such as stop loss optimization and parameter adjustment.
||

## Overview

This is a moving average based chasing strategy. It utilizes the direction of moving averages and candle shadows to determine price trends and momentum for entries and exits. The core logic is to go long/short when the color of the second moving average changes, and use strong signals from the third moving average to add positions, up to 5 additions.

## Strategy Principle 

The strategy uses Heikin Ashi moving averages to determine trends. Specifically, the strategy defines 3 moving averages:

1. The second moving average is used to determine trend reversal. Enter trades when its color changes. 
2. The third moving average is used to identify strong breakout signals for adding positions.

Entry Logic:

1. When the second moving average color changes from red to green, go long.  
2. If the third moving average now shows a strong uptrend signal (green candle with no lower shadow), add position.
3. Allow up to 5 additions.

Exit Logic:

1. When either moving average color changes, close all positions.

## Advantage Analysis

The advantages of this strategy:

1. Heikin Ashi reduces noise for better signals.
2. Dual moving averages combo improves entry timing accuracy. 
3. Adding positions to chase trends allows bigger profit.

## Risk Analysis

There are also some risks:

1. Dual moving average crossovers can cause whipsaws.  
2. Over-adding may increase losses.
3. Parameters need tuning for different products and timeframes.

Risks can be managed via stop loss, reducing additions, and parameter optimization.

## Optimization Directions

The strategy can be improved in the following aspects:

1. Test different parameter sets for the moving averages.
2. Optimize stop loss methods like trailing stop loss. 
3. Test parameters separately for different products. 
4. Add filters to prevent adding too fast.
5. Incorporate other indicators for entry timing.

## Summary

In summary, this is a trend chasing strategy based on dual moving average directionality. It combines the advantage of trend and momentum analysis for expanded profits from adding positions. But risks need to be managed via stop loss and parameter tuning. Further improvements can be made in optimizing stops, tuning parameters etc.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("平均K腳本交易策略", overlay=true)

// 定義 Heikin Ashi 指標
ha_open = security(heikinashi(syminfo.tickerid), "60", open)
ha_high = security(heikinashi(syminfo.tickerid), "60", high)
ha_low = security(heikinashi(syminfo.tickerid), "60", low)
ha_close = security(heikinashi(syminfo.tickerid), "60", close)

// 確定 Heikin Ashi 指標的顏色
isGreen = ha_open < ha_close

// 定義加碼次數
var int add_on_buy = 10
var int add_on_sell = 10

// 定義進場和出場條件
long_condition = crossover(ha_close, ha_open) and isGreen and ha_low == ha_open
short_condition = crossunder(ha_close, ha_open) and not isGreen and ha_high == ha_open
exit_condition = crossover(ha_open, ha_close) or crossunder(ha_open, ha_close)

// 如果條件符合，進行進場和出場操作
if (long_condition)
    strategy.entry("Buy", strategy.long)
if (short_condition)
    strategy.entry("Sell", strategy.short)
if (exit_condition)
    strategy.close("Buy")
    strategy.close("Sell")

// 繪製 Heikin Ashi 蠟燭圖
plotcandle(iff(ha_open < ha_close, ha_open, na), ha_high, ha_low, ha_close, title='Green Candles', color=#53b987, wickcolor=#53b987, bordercolor=#53b987)
plotcandle(iff(ha_open >= ha_close, ha_open, na), ha_high, ha_low, ha_close, title='Red Candles', color=#eb4d5c, wickcolor=#eb4d5c, bordercolor=#eb4d5c)

```

> Detail

https://www.fmz.com/strategy/442228

> Last Modified

2024-02-20 14:11:31

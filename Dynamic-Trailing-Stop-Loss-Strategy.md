
> Name

Dynamic Trailing Stop Loss StrategyDynamic-Trailing-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/9364f1a8b08ff22007.png)

[trans]
## Overview
This strategy is based on a dynamically calculated trailing stop loss mechanism, which sets stop loss lines for long and short positions based on the highest and lowest prices of the stock price. When the price hits the stop loss line, close the current position and open a new position in the opposite direction. The strategy is simple and easy to understand and can effectively control einzel risks.
## Strategy Principle
This strategy is mainly implemented through the following steps:
1. Input parameters: select long or short, calculate cycle length, trailing stop slippage setting
2. Calculate the highest price and lowest price: Calculate the highest price and lowest price within the period based on the input length
3. Calculate the trailing stop loss line: when going long, the lowest price minus the slippage is used as the stop loss line; when going short, the highest price plus the slippage is used as the stop loss line
4. Opening and closing: When the price touches the stop loss line, close the position in the current direction and open a new position in the opposite direction.
The above is the basic operating logic of the strategy. When the price moves, the stop loss line will be continuously updated to achieve dynamic tracking. Through this trailing stop loss method, single losses can be effectively controlled.
## Advantage Analysis
This strategy mainly has the following advantages:
1. The strategy is simple and clear, easy to understand and implement
2. Apply dynamic trailing stop loss to effectively control single losses
3. Flexible choice of long or short direction, suitable for different market environments
4. The calculation period and slippage can be customized for easy optimization
In general, this strategy can effectively manage Positions through a simple trailing stop loss mechanism, and is a typical Risk Management strategy.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. When the price fluctuates greatly, the stop loss line may be triggered frequently, resulting in too frequent transactions.
2. Unreasonable periods for calculating the highest price and lowest price may lead to inappropriate stop loss lines
3. If the slippage is set too large, the stop loss line may be too loose and the loss cannot be stopped in time.
These risks can be optimized by adjusting the calculation cycle and appropriately reducing the slippage range to make the stop loss line setting more reasonable.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add a stop-loss line optimization mechanism so that it can be dynamically adjusted to avoid the stop-loss line being too loose or too tight.
2. Add judgment on position opening conditions to avoid opening Positions at inappropriate times.
3. Combine trend indicators and adopt trend tracking methods to make profit margins larger
4. Add a position management module to dynamically adjust positions through risk ratings
## Summarize
This trading strategy implements dynamic management of Positions through a simple trailing stop loss method. The strategy is easy to understand and implement, and can effectively control single losses. We analyzed the advantages, possible risks and subsequent optimization directions of the strategy. Overall, this is a very typical and practical Risk Management strategy.
||

## Overview

This strategy is based on a dynamic trailing stop loss mechanism to set stop loss lines for long and short positions based on the highest and lowest prices of a stock. When the price hits the stop loss line, it will close the current position and open a new position in the opposite direction. The strategy is simple and effective in controlling single transaction risk.

## Principle  

The main steps of this strategy are:

1. Input parameters: choose to go long or short, set length for period, trailing stop slippage
2. Calculate highest and lowest prices: get highest and lowest prices based on input length 
3. Calculate trailing stop loss lines: for long, lowest price minus slippage; for short, highest price plus slippage
4. Open and close positions: when price hits stop loss line, close current direction position, and open opposite direction position

The above is the basic logic of the strategy. As price moves, the stop loss line keeps updating for dynamic tracking. By trailing stop loss, it can effectively control losses per trade.

## Advantage Analysis   

The main advantages of this strategy:

1. Simple and clean logic, easy to understand and implement
2. Dynamic trailing stop loss controls single trade loss 
3. Flexible to choose long or short, adaptable to different market environments
4. Customization of period and slippage for optimization

In summary, by simple trailing stop loss mechanisms, this strategy can effectively manage positions and is a typical Risk Management strategy.

## Risk Analysis

There are also some risks to note:

1. Price volatility may trigger stop loss frequently, leading to over-trading
2. Improper period settings may cause unsuitable stop loss lines
3. Excessive slippage setting may result in loose stop loss, unable to stop loss in time

These risks can be optimized by adjusting the period, reducing slippage reasonably to make more sensible stop loss lines. 

## Optimization Directions 

The strategy can be upgraded from the following aspects:

1. Add optimization for dynamic stop loss line adjustment, avoid improper tight or loose stop loss lines
2. Add open position conditions to avoid opening positions at inappropriate times  
3. Incorporate trend indicators for trend-following with more profit potential  
4. Add position sizing to dynamically adjust positions based on risk levels

## Conclusion

The trading strategy realizes dynamic positions management through simple trailing stop loss methods. It is easy to understand and implement, and can effectively control single trade loss. We analyzed the advantages, potential risks and future optimization directions. In conclusion, this is a highly typical and practical Risk Management strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Long|
|v_input_2|false|Short|
|v_input_3|20|length|
|v_input_4|false|Trailing Stop|
|v_input_5|false|background|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Noro
//2019

//@version=4
strategy(title = "Noro's Trailing-Stop Strategy", shorttitle = "Trailing", overlay = true, default_qty_type = strategy.percent_of_equity, default_qty_value = 100, pyramiding = 0)

//Settings
needlong = input(true, defval = true, title = "Long")
needshort = input(false, defval = false, title = "Short")
length = input(20, minval = 1)
shift = input(0.0, minval = 0, title = "Trailing Stop")
background = input(false)

//Levels
max = highest(high, length)
min = lowest(low, length)

//Trailing
size = strategy.position_size
longtrailing = 0.0
shorttrailing = 0.0
longtrailing := size <= 0 ? min - ((min / 100) * shift) : max(min - ((min / 100) * shift), longtrailing[1])
shorttrailing := size >= 0 ? max + ((max / 100) * shift) : min(max + ((max / 100) * shift), shorttrailing[1])
trailing = size <= 0 ? shorttrailing : longtrailing
col = size == size[1] ? size > 0 ? color.red : color.lime : na
plot(trailing, color = col, linewidth = 2, transp = 0)

//Background
bgcol = background ? size > 0 ? color.lime : color.red : na
bgcolor(bgcol, transp = 80)

if trailing > 0 and size <= 0
    strategy.entry("Long", strategy.long, needlong ? na : 0, stop = trailing)
if trailing > 0 and size >= 0
    strategy.entry("Short", strategy.short, needshort ? na : 0, stop = trailing)
```

> Detail

https://www.fmz.com/strategy/440541

> Last Modified

2024-01-31 15:05:30

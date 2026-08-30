
> Name

Gold-Fast-Breakthrough-EMA-Trading-Strategy Gold-Fast-Breakthrough-EMA-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/1f1ff6ead8f2ebac06e5683473d17512fb618c320b59d4139e436d00515caf48.png)
[trans]

## Overview
The Gold Fast Breakthrough EMA Trading Strategy is a gold scaling strategy based on the EMA indicator. This strategy uses the intersection of fast EMA and slow EMA to judge trading signals, and combines the ATR indicator to set stop loss and profit points to achieve gold scaling transactions.
## Strategy Principle
This strategy mainly relies on the intersection of the fast 9-day EMA and the slow 21-day EMA and the relationship between price and EMA to determine entry. The specific logic is that when the fast EMA crosses above the slow EMA and the closing price is higher than the slow EMA, go long; when the fast EMA crosses below the slow EMA and the closing price is lower than the slow EMA, go short.
In addition, this strategy also uses the ATR indicator to calculate the average fluctuation range of the last 2 days. After entry, the stop-loss point is set at the latest lowest (atrLength) minus atr times atrMultiplier; the stop-profit point is set at the latest highest (atrLength) plus atr times atrMultiplier. This is the fluctuation trailing stop mechanism based on the ATR indicator.
## Advantage Analysis
This is a relatively simple golden scalping strategy that has the following advantages:
1. Use EMA cross judgment to capture a clearer trend;
2. Combine the judgment of the relationship between price and EMA to filter out false breakthrough signals and improve the accuracy;
3. The trailing stop based on the ATR indicator can dynamically adjust stop loss and profit according to market fluctuations, which is beneficial to locking in profits.
## Risk Analysis
There are also some risks with this strategy:
1. As a scalping strategy, it requires high transaction capital scale and leverage, otherwise the single profit will be limited;
2. The EMA crossover strategy is prone to produce false signals in price shock markets;
3. The stop-loss and take-profit distance set by the ATR indicator may be too large or too small and needs to be optimized.
In view of the above risks, you can consider appropriately reducing the position size, filtering signals in combination with other indicators, or testing different parameters to optimize the settings of stop loss and take profit.
## Optimization direction
This strategy can also be optimized from the following directions:
1. Add other indicator judgments, such as MACD, Bollinger Bands, etc., to form multiple filters and improve signal quality;
2. Add a volatility-based position size adjustment mechanism, such as appropriately reducing positions when volatility increases;
3. Optimize the ATR fluctuation range parameters and find the optimal parameter combination.
## Summarize
The gold fast breakout EMA trading strategy is a simple and practical gold scaling strategy. It uses the EMA cross to determine the trend and performs stop loss and profit based on the ATR indicator, which can effectively lock in small profits. This strategy can be improved through multiple indicator filtering, position size adjustment, parameter optimization, etc. to make it more suitable for the market environment.
||

## Overview

The Gold Fast Breakthrough EMA Trading Strategy is a gold scalping strategy based on the EMA indicator. This strategy uses the crossover of the fast EMA and slow EMA to generate trading signals, combined with ATR indicators to set stop loss and take profit points to implement gold scalping trading.

## Strategy Principle  

This strategy mainly relies on the crossover of the 9-day fast EMA and 21-day slow EMA, as well as the relationship between price and EMA to determine entry. Specifically, when the fast EMA crosses above the slow EMA and the close price is higher than the slow EMA, go long; when the fast EMA crosses below the slow EMA and the close price is lower than the slow EMA, go short.

In addition, this strategy also uses the ATR indicator to calculate the average range of fluctuations in the most recent 2 days. After entry, the stop loss point is set at the lowest (atrLength) minus atr multiplied by atrMultiplier; the take profit point is set at the highest (atrLength) plus atr multiplied by atrMultiplier. This is a volatility trailing stop mechanism based on the ATR indicator.

## Advantage Analysis  

This is a relatively simple gold scalping strategy with the following advantages:

1. Using EMA crossover to judge, it can capture clearer trends;
2. Combined with the relationship between price and EMA to filter false breakout signals and improve accuracy;
3. The trailing stop based on the ATR indicator can dynamically adjust the stop loss and take profit according to market volatility, which is conducive to locking in profits.

## Risk Analysis   

This strategy also has some risks:

1. As a scalping strategy, it has higher requirements for trading capital size and leverage, otherwise the single profit is limited;
2. EMA crossover strategies are prone to wrong signals in choppy markets;
3. The distance of stop loss and take profit set by the ATR indicator may be too large or too small and needs to be optimized.

In response to the above risks, we can consider appropriately reducing the position size, combining with other indicators to filter signals, or testing different parameters to optimize the setting of stop loss and take profit.

## Optimization Directions   

This strategy can also be optimized in the following directions:  

1. Add other indicators to judge, such as MACD, Bollinger Bands, etc. to form multiple filters and improve signal quality;
2. Add a position sizing adjustment mechanism based on volatility. For example, appropriately reduce the position size when volatility increases;  
3. Optimize the parameters of the ATR volatility range to find the optimal parameter combination.

## Summary  

The Gold Fast Breakthrough EMA Trading Strategy is a simple and practical gold scalping strategy. It uses EMA crossover to determine the trend and sets stop loss and take profit based on the ATR indicator, which can effectively lock in small profits. This strategy can be improved through multiple indicator filtering, position sizing adjustment, parameter optimization, etc., making it more adaptable to market conditions.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Fast EMA Length|
|v_input_2|21|Slow EMA Length|
|v_input_3|2|ATR Length|
|v_input_4|2|ATR Multiplier|
|v_input_5|0.7|Profit Target|
|v_input_6|0.001|Commission|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-18 00:00:00
end: 2024-01-17 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("XAUUSD Trading Strategy", shorttitle="XAUUSD Strategy", overlay=true)

// Inputs
fastLength = input(9, title="Fast EMA Length")
slowLength = input(21, title="Slow EMA Length")
atrLength = input(2, title="ATR Length")
atrMultiplier = input(2, title="ATR Multiplier")
profitTarget = input(0.7, title="Profit Target") * 100 // in percentage
commission = input(0.001, title="Commission") // 0.1% per trade

// Calculations
fastEMA = ema(close, fastLength)
slowEMA = ema(close, slowLength)
atr = atr(atrLength)

// Entry rules
longCondition = crossover(fastEMA, slowEMA) and close > slowEMA
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = crossunder(fastEMA, slowEMA) and close < slowEMA
if (shortCondition)
    strategy.entry("Short", strategy.short)

// Stop loss and take profit
longStop = lowest(atrLength) - atr * atrMultiplier
longTakeProfit = highest(atrLength) + atr * atrMultiplier

shortStop = highest(atrLength) + atr * atrMultiplier
shortTakeProfit = lowest(atrLength) - atr * atrMultiplier

strategy.exit("Exit Long", "Long", stop=longStop, limit=longTakeProfit)
strategy.exit("Exit Short", "Short", stop=shortStop, limit=shortTakeProfit)

// Plot EMAs
plot(fastEMA, title="Fast EMA", color=color.blue)
plot(slowEMA, title="Slow EMA", color=color.red)
```

> Detail

https://www.fmz.com/strategy/439190

> Last Modified

2024-01-18 11:37:10

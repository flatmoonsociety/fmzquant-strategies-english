
> Name

Short-term double filtering strategy SMA-RSI-Double-Filter-Short-term-Trading-Strategy based on SMA and RSI
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is designed based on two indicators, the Simple Moving Average (SMA) and the Relative Strength Index (RSI). It goes short when the RSI value breaks through the entry signal line and the closing price is below the SMA; it closes the position when the stop loss or take profit signal appears. This strategy combines double filtering conditions for entry, which can effectively avoid invalid transactions.
## Principle
This strategy mainly judges the market based on two indicators:
1. SMA: Calculate the simple moving average of the closing prices of the last 200 days, representing the medium and long-term trend direction.
2. RSI: Calculates the relative strength of the closing prices in the last 14 days, representing short-term overbought and oversold conditions.
When the RSI crosses 51 and enters the overbought zone, and is above the SMA line, it indicates a divergence between the short-term and medium-term trends, so go short.
Then set the stop loss and take profit lines. Take profit when RSI falls below 32; stop loss when RSI crosses 54 or the stop loss line is breached.
## Advantages
1. Dual indicator filtering increases entry accuracy. RSI determines short-term overbought signals, and SMA determines medium- and long-term short signals. The combination of the two is more reliable.
2. The trailing stop loss method can be used to lock in profits according to market trends and avoid profit taking.
3. The strategy logic is simple and clear, easy to understand and modify.
## Risk
1. Influencing factors such as trading volume and volatility are not considered.
2. RSI parameters are relatively fixed and may not be applicable to all varieties and periods.
3. Transaction costs such as transaction slippage and handling fees are not considered.
4. The strategy is relatively simple and the scalability space is limited.
## Optimization ideas
1. Test and optimize the parameters of RSI and SMA to find the best parameter combination.
2. Add stop-profit and stop-loss methods. Such as trailing stop loss, proportional stop loss, etc.
3. Combine trend indicators such as MACD for filtering to avoid counter-trend trading.
4. Consider adding trading volume indicators to filter out low-volume false breakthroughs.
## Summarize
The overall idea of ​​this strategy is clear and has certain practical value. However, its parameter settings are relatively fixed and do not take into account market changes. There are also some details that can be optimized. In summary, this strategy can be used as an example for beginners to understand the dual indicator filtering strategy, but it needs further testing and improvement in real trading.
||


## Overview

This strategy is based on the Simple Moving Average (SMA) and Relative Strength Index (RSI) indicators. It goes short when the RSI crosses above the entry level and the close price is below the SMA; It closes positions when stop loss or take profit signals appear. The double filter helps avoid ineffective trades.

## Principles 

The strategy judges the market mainly based on two indicators:

1. SMA: Calculated based on the simple moving average of closing prices in the past 200 days, representing mid-long term trends.

2. RSI: Calculated based on the relative strength of closing prices in the past 14 days, representing short-term overbought/oversold levels.

When RSI crosses above 51 into the overbought zone and is above the SMA line, it indicates that the short-term and mid-long term trends are diverging, so a short position is opened. 

After that, stop loss and take profit lines are set. Position is closed when RSI drops below 32 for take profit, or when RSI crosses above 54 or the stop loss is hit for stop loss.

## Strengths

1. The double filter of indicators increases the accuracy of entry signals. RSI determines short-term overbought levels and SMA determines mid-long term bearish signals, combining the two makes the signals more reliable.

2. The trailing stop locks in profits according to price action, avoiding giving back profits.

3. The logic is simple and straightforward, easy to understand and modify.

## Risks

1. Does not consider factors like trading volume or volatility. 

2. RSI parameters are fixed and may not suit all products and timeframes.

3. Does not consider trading costs like slippage and commissions. 

4. The strategy is very simple and has limited room for expansion.

## Improvement Areas

1. Test and optimize RSI and SMA parameters to find the best combination.

2. Add more types of stop loss/profit taking methods, like trailing stops, percentage-based stops.

3. Add trend filter indicators like MACD to avoid trading against the trend. 

4. Consider volume indicators to filter out false breakouts with low volume.

## Summary  

The strategy has clear logic and some practical value. But its parameters are fixed and don't adapt to market changes. There are also some details that can be improved. Overall, it can serve as an example for beginners to learn double indicator filtering strategies, but needs further testing and enhancement for actual trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|200|SMA Length|
|v_input_2|14|RSI Length|
|v_input_3|51|RSI Entry Level|
|v_input_4|54|RSI Stop Level|
|v_input_5|32|RSI Take Profit Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-07 00:00:00
end: 2023-10-07 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © abdllhatn

//@version=5
// strategy("Alpha Short SMA and RSI Strategy", overlay=true, initial_capital=10000, default_qty_value=100)

// Inputs
sma_length = input(200, title="SMA Length")
rsi_length = input(14, title="RSI Length")
rsi_entry = input(51, title="RSI Entry Level")
rsi_stop = input(54, title="RSI Stop Level")
rsi_take_profit = input(32, title="RSI Take Profit Level")

// Indicators
sma_value = ta.sma(close, sma_length)
rsi_value = ta.rsi(close, rsi_length)

var float trailingStop = na
var float lastLow = na

// Conditions
shortCondition = ta.crossover(rsi_value, rsi_entry) and close < sma_value
if (shortCondition)
    strategy.entry("Sell", strategy.short)
    trailingStop := na
    lastLow := na

if (strategy.position_size < 0)
    if (na(lastLow) or close < lastLow)
        lastLow := close
        trailingStop := close

if not na(trailingStop) and close > trailingStop
    strategy.close("Sell")

if (rsi_value >= rsi_stop)
    strategy.close("Sell")

if (rsi_value <= rsi_take_profit)
    strategy.close("Sell")

// Plot
plot(sma_value, color=color.red, linewidth=2)



```

> Detail

https://www.fmz.com/strategy/428682

> Last Modified

2023-10-08 12:14:36

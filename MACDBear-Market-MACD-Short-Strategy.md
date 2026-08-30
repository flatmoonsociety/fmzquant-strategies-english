
> Name

Bear-Market-MACD-Short-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

## Strategy Principle
This strategy focuses on short-selling in bear market declines while ensuring that the asset is in a large-cycle downward channel, and then exiting after further declines.
The main transaction logic is:
1. Calculate the fast line, slow line and column line of MACD indicator
2. When the MACD fast line crosses the slow line, it indicates that a downward trend has begun.
3. Price is below the 450-day moving average, confirming that it is in a downward long-term trend
4. When the above two conditions are met, enter the market short.
5. The take profit line is set below 8% of the entry price
6. The stop loss line is set above 4% of the entry price
This strategy makes full use of MACD to determine short-term trend reversal, and assists the long-term moving average to determine the general trend to avoid blind short selling. Take-profit and stop-loss strategies control risk.
## Strategic Advantages
- MACD determines short-term downward opportunities
- Long-term moving average filtering to avoid short reversals
- The stop-profit and stop-loss ratio is 2:1 to control risks
## Strategy Risk
- Need to optimize MACD parameters
- Long-term moving averages tend to lag behind and produce false signals
- Only short selling cannot take advantage of long opportunities
## Summarize
This strategy captures short-term falling opportunities and goes short while ensuring that the general trend is downward. Take profit and stop loss strategy Optimization and portfolio management are crucial to the effectiveness of the strategy.

||


## Strategy Logic

This short strategy focuses on downside moves during bear markets, while ensuring the asset trades within a long-term downtrend, exiting after further downside. 

The logic is:

1. Compute MACD short, long and histogram lines

2. Bearish MACD crossover signals potential downtrend

3. Price below 450-day MA confirms long-term downtrend

4. Enter short when both conditions met 

5. Take profit set at 8% below entry price 

6. Stop loss set at 4% above entry price

It utilizes MACD for short-term turns and long MA to avoid blind shorting. Profit/loss controls risk.

## Advantages

- MACD signals short-term downside potential

- Long MA filter avoids shorting reversals 

- 2:1 profit/loss ratio controls risk

## Risks

- Requires MACD parameter tuning

- Long MA prone to lagging signals

- SHORT only misses long opportunities 

## Summary

This strategy captures short-term down moves when ensured of a bear trend. Profit/loss tuning and position sizing are key for performance.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-14 00:00:00
end: 2023-09-13 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Coinrule

//@version=5
strategy("Shorting Bearish MACD Cross with Price Below EMA 450 (By Coinrule)", overlay=true, initial_capital = 10000, default_qty_value = 30, default_qty_type = strategy.percent_of_equity, commission_type=strategy.commission.percent, commission_value=0.1)

// EMAs 
slowEMA = ta.ema(close, 450)

// MACD
[macdLine, signalLine, histogramLine] = ta.macd(close, 11, 26, 9)

// Conditions
goShortCondition1 = ta.crossunder(macdLine, signalLine)
goShortCondition2 = slowEMA > close

timePeriod = time >= timestamp(syminfo.timezone, 2021, 12, 1, 0, 0)
notInTrade = strategy.position_size <= 0
strategyDirection = strategy.direction.short

if (goShortCondition1 and goShortCondition2 and timePeriod and notInTrade)
    stopLoss = high * 1.04
    takeProfit = low * 0.92
    strategy.entry("Short", strategy.short)
    strategy.exit("exit","Short", stop=stopLoss, limit=takeProfit)
    
plot(slowEMA, color=color.green)

```

> Detail

https://www.fmz.com/strategy/426836

> Last Modified

2023-09-14 18:04:28

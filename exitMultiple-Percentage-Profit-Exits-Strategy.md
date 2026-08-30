
> Name

Multiple-Percentage-Profit-Exits-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fe27b27583d529deaf.png)

[trans]

## Overview
This strategy implements the function of setting multiple percentage take-profit exits. The strategy first determines the long and short conditions and enters the market for long and short positions. Then convert the percentage into price points through a custom percentageAsPoints function. The program sets 4 exits according to the set take-profit percentages of 1%, 2%, 3% and 4%, and also sets a general 2% stop-loss exit. This achieves the effect of multiple percentage take-profits.
## Strategy Principle
This strategy mainly determines entry through the long and short crossover of the SMA moving average. Specifically, when the fast line sma (14) crosses the slow line sma (28), you will enter the market to go long; when the fast line sma (14) crosses below the slow line sma (28), you will enter the market to go short.
So the question is, how to set multiple percentage take-profit exits? Here, a custom percentageAsPoints function is used to convert the percentage into price points. The function logic is:
```
percentAsPoints(pcnt) => 
    strategy.position_size != 0 ? round(pcnt / 100 * strategy.position_avg_price / syminfo.mintick) : float(na)
```

If the position is not 0, this function uses the percentage multiplied by the average price of the position and divided by the minimum price tick to obtain the price points. If the position is 0, then na is returned.
With this function we can easily convert percentages to points. Then the program sets 4 exits according to the set 1%, 2%, 3% and 4% take profit:
```
lossPnt = percentAsPoints(2)

strategy.exit("x1", qty_percent = 25, profit = percentAsPoints(1), loss = lossPnt)  

strategy.exit("x2", qty_percent = 25, profit = percentAsPoints(2), loss = lossPnt)

strategy.exit("x3", qty_percent = 25, profit = percentAsPoints(3), loss = lossPnt)

strategy.exit("x4", profit = percentAsPoints(4), loss = lossPnt)  
```

At the same time, all exits use a common 2% stop loss. This achieves the effect of multiple percentage take-profits.
## Advantage Analysis
This multiple percentage take-profit strategy has the following advantages:
1. You can stop profits step by step to avoid missing opportunities for greater profits. Generally, the further back the position, the greater the take-profit range and the greater the risk. This strategy can balance risk and return.
2. Taking profit in batches can return the principal and reduce risks. For example, if you set a 25% batch size, you can get back 1/4 of your principal when the profit reaches 1%, and subsequent positions will be operated based on profits.
3. Prevent stop loss in abnormal market conditions. A 2% stop loss can avoid huge losses caused by extreme market conditions.
4. The code implementation is simple, clear, easy to understand, and easy to modify and optimize. A custom function converts percentages into points, and then multiple take-profits can be set with just a few lines of code.
## Risk Analysis
There are also some risks with this strategy:
1. Percentage take-profit is easy to cause sideways fluctuations, and the price oscillates back and forth near the take-profit price. At this time, stop-profit and stop-loss will be triggered frequently, increasing the frequency of transactions and the burden of handling fees.
2. Taking profit in batches increases the number of transactions and also increases the burden of handling fees. If the handling fee is too high, it will offset part of the take-profit profit.
3. Improper setting of profit stop points will also affect the rate of return. If the setting is too conservative, it will be difficult to obtain satisfactory returns; if the setting is too aggressive, the risk will be too great.
4. Fixed percentage take-profit does not take into account market volatility and trend. In a volatile market, the take-profit range should be lowered, while in a trending market, the take-profit range should be increased.
## Optimization direction
Considering the above risks, optimization can be continued from the following aspects:
1. Optimize the take-profit strategy so that it can automatically adjust according to market volatility and trends. For example, add ATR take-profit, tighten the take-profit during shocks, and relax the take-profit during the trend.
2. Optimize the proportion and range of profit taking in batches to achieve the optimal combination of risk and return. Add parameter optimization function to find the optimal parameters.
3. Reduce the number of take-profits and avoid too frequent transactions. For example, set a price buffer and take profit only when it exceeds a certain range.
4. Considering the handling fee, when the expected take-profit profit is lower than the handling fee, no profit will be taken. Or optimize the profit-taking range according to the handling fee.
5. Use book orders to take profit. Avoid moving the take profit price based on depth priority price priority offers.
## Summarize
This strategy achieves the effect of multiple percentage take-profits. It sets four take-profit exits of 1%, 2%, 3% and 4%, which can stop profits step by step. At the same time, a 2% stop-loss is used to prevent huge losses in abnormal market conditions. This strategy can balance risks and benefits and prevent missing greater profit opportunities. However, there are also certain risks, such as sideways shocks, increased trading frequency, etc. These suggestions are worth considering to add to the strategy for optimization so that it can operate stably in more markets.
||

## Overview

This strategy implements the functionality of setting multiple percentage profit exits. The strategy first judges the long and short conditions to enter positions. It then uses a custom percentAsPoints function to convert percentages into price ticks. The program sets 4 exits with profit percentages of 1%, 2%, 3% and 4% based on the configurations, and also sets a common 2% stop loss exit. This achieves the effect of multiple percentage profit exits.

## Strategy Logic

The core logic of this strategy is using SMA crossovers to determine entries. Specifically, when the fast SMA (14) crosses above the slow SMA (28), it will go long. When the fast SMA (14) crosses below the slow SMA (28), it will go short.

Then how to set multiple percentage profit exits? Here a custom percentAsPoints function is used to convert percentages into price ticks. The logic is:

```
percentAsPoints(pcnt) =>
    strategy.position_size != 0 ? round(pcnt / 100 * strategy.position_avg_price / syminfo.mintick) : float(na) 
```

If position size is not 0, it calculates the price ticks by percentage multiplied by average entry price and divided by minimum tick size. If position size is 0, it returns na.  

With this function, we can easily convert percentages into ticks. The program then sets 4 exits based on profit percentages of 1%, 2%, 3% and 4%:

```
lossPnt = percentAsPoints(2)

strategy.exit("x1", qty_percent = 25, profit = percentAsPoints(1), loss = lossPnt)   

strategy.exit("x2", qty_percent = 25, profit = percentAsPoints(2), loss = lossPnt)

strategy.exit("x3", qty_percent = 25, profit = percentAsPoints(3), loss = lossPnt)  

strategy.exit("x4", profit = percentAsPoints(4), loss = lossPnt)
```

Also a common 2% stop loss is used for all exits. This achieves the effect of multiple percentage profit exits.

## Advantage Analysis

This multiple percentage profit exit strategy has the following advantages:

1. It allows taking profits step-by-step, avoiding missing larger profits. Generally the later exits have larger profit targets and higher risks, and this strategy balances risks and returns.  

2. Exiting in batches allows capital retrieval, lowering risks. For example with 25% batch size, 1% profit can return 1/4 of the capital, and later positions are all by pure profits.

3. 2% stop loss prevents extreme losses in abnormal market moves.

4. The implementation is simple and clean, easy to understand and modify. The custom percentage conversion function enables setting multiple exits in a few lines of code.

## Risk Analysis

There are also some risks with this strategy:

1. Percentage exits may cause sideways choppiness, with prices oscillating around exit prices, triggering frequent exits. This increases trade frequency and commission costs.

2. Batch exits increase number of trades and commissions. High commissions could erase some of the exit profits.  

3. Improper exit positioning could also impact returns. Overly conservative exits may lead to insufficient profits, while too aggressive exits have higher risks.

4. Fixed percentage exits do not consider market volatility and trends. In choppy markets smaller exits should be used, while in trending markets larger exits should be targeted.

## Optimization Directions   

Considering above risks, further optimizations could be done in following aspects:

1. Optimize exits to adapt based on market volatility and strength using methods like ATR exits. Tighter exits in choppy markets and wider exits in strong trends.

2. Optimize batch percentages and ranges to find optimal risk-return combinations. Add parameter optimization for finding best parameters.  

3. Reduce number of exits to avoid over-trading. For example set a price buffer zone, only exit after exceeding certain price move.

4. Consider commission factors, avoid exits where projected profit is less than commission costs. Or optimize percentages based on commissions.
  
5. Use orderbook exits based on depth instead of moving exit prices. Exit using best bid/ask prices based on depth priority.

## Summary

This strategy achieves the effect of multiple percentage profit exits, with 4 exits at 1%, 2%, 3% and 4%, allowing gradual profitable exits, and using 2% stop loss to prevent huge losses in extreme moves. It balances risks and returns and prevents missing further profits. But some risks exist like choppiness and higher trade frequencies. The optimization suggestions provided can help improve performance in more market conditions when incorporated into the strategy.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-31 00:00:00
end: 2023-11-30 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © adolgov

//@version=4
strategy("Multiple %% profit exits example", overlay=false, default_qty_value = 10)

longCondition = crossover(sma(close, 14), sma(close, 28))
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

shortCondition = crossunder(sma(close, 14), sma(close, 28))
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short)

percentAsPoints(pcnt) =>
    strategy.position_size != 0 ? round(pcnt / 100 * strategy.position_avg_price / syminfo.mintick) : float(na)

lossPnt = percentAsPoints(2)

strategy.exit("x1", qty_percent = 25, profit = percentAsPoints(1), loss = lossPnt)
strategy.exit("x2", qty_percent = 25, profit = percentAsPoints(2), loss = lossPnt)
strategy.exit("x3", qty_percent = 25, profit = percentAsPoints(3), loss = lossPnt)
strategy.exit("x4", profit = percentAsPoints(4), loss = lossPnt)

profitPercent(price) =>
    posSign = strategy.position_size > 0 ? 1 : strategy.position_size < 0 ? -1 : 0
    (price - strategy.position_avg_price) / strategy.position_avg_price * posSign * 100

p1 = plot(profitPercent(high), style=plot.style_linebr, title = "open profit % upper bound")
p2 = plot(profitPercent(low), style=plot.style_linebr, title = "open profit % lower bound")
fill(p1, p2, color = color.red)
```

> Detail

https://www.fmz.com/strategy/433932

> Last Modified

2023-12-01 15:22:29

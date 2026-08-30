
> Name

Quantitative-Strategy-Based-on-Dual-Exponential-Moving-Average-Crossover
> Author

ChaoZhang

> Strategy Description


[trans]

This article will detail a quantitative strategy for a double exponential moving average crossover. This strategy sets two EMAs, fast and slow, to form trading signals based on their intersection.
1. Strategy Principle
The core of this strategy is to set two EMAs with different parameters, one fast and one slow, and generate buy and sell signals based on their cross relationship. Its specific logic is:
1. Set a small period EMA (such as 29 periods) to represent the short-term trend;
2. Set a large period EMA (such as 86 periods) to represent the long-term trend;
3. When the short-term EMA crosses above the long-term EMA, go long; when the short-term EMA crosses below the long-term EMA, go short;
4. The current strategy only sets the opening logic and does not set the stop-loss and take-profit logic;
5. Open a position with a fixed quota.
The fast EMA reflects short-term changes, and the slow EMA tracks the long-term trend. The intersection of the two forms a trading signal, which can capture the core direction of price changes.
2. Strategic advantages
The biggest advantage of this strategy is that it is simple to operate and easy to implement. The EMA indicator is easy to calculate and the cross signals are directly visible.
Secondly, the combination of fast and slow EMA can track short and long cycle trends at the same time. Fast EMA follows changes quickly, while slow EMA filters out noise.
Finally, fixed position management also reduces the difficulty of parameter optimization of the strategy.
3. Potential risks
Although this strategy is easy to implement, you should also pay attention to the following risks in real trading:
First of all, there is a certain lag in the EMA crossover, and the optimal entry point may be missed.
Secondly, no stop loss setting makes the loss of each order uncontrollable.
Finally, the lack of a profit stop setting also makes the profit margin difficult to control.
This requires further supplementing the exit logic and setting stop loss and profit conditions.
4. Content summary
This article introduces in detail a quantitative trading strategy of double EMA crossover. It uses a combination of fast EMA and slow EMA to determine the trend direction and form trading signals. The strategy is easy to implement, but there is also the problem that parameter optimization is not difficult. Overall, this strategy can be used as a smoothing trend trading strategy, but it needs to be properly optimized to control risks.
||

This article explains in detail a quantitative trading strategy based on dual EMA crossover. It sets up fast and slow EMAs and generates signals when they cross over.

I. Strategy Logic

The core of this strategy is setting up two EMAs with different parameters, one fast and one slow, and generating buy and sell signals based on their crossover relationship. The specific logic is:

1. Set up a short-period EMA (e.g. 29 periods) to represent the short-term trend.

2. Set up a long-period EMA (e.g. 86 periods) to represent the long-term trend.

3. Go long when the short EMA crosses above the long EMA, and go short when it crosses below.

4. Currently only entry logic is defined, with no stop loss or take profit. 

5. Trade fixed position sizing.

By using a fast EMA to react to short-term moves and a slow EMA to track the long-term trend, the crossover generates signals that capture the core direction of price changes.

II. Advantages of the Strategy

The biggest advantage of this strategy is its simplicity and ease of implementation. EMA is straightforward to calculate and crossover signals are visually clear.

Secondly, the fast and slow EMA complement each other to track both short and long-term trends simultaneously. The fast EMA moves nimbly while the slow EMA filters out noise.

Lastly, the fixed position sizing also reduces optimization difficulty.

III. Potential Weaknesses 

Despite being easy to implement, the following risks should be noted for live trading:

Firstly, EMA crossovers have a lag and may miss the optimal entry point. 

Secondly, the lack of a stop loss means losing trades cannot be controlled.

Finally, the lack of a take profit level also makes it hard to manage profit potential.

Additional exit logic needs to be added, with stop loss and take profit conditions.

IV. Summary

In summary, this article has explained a quantitative trading strategy based on dual EMA crossovers. It uses fast and slow EMA combinations to determine trend direction for trade signals. While easy to implement, the strategy also lacks sophistication in optimization. Overall, it can serve as a smoothing trend trading framework but requires proper enhancements to manage risks.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|29|Small EMA|
|v_input_2|86|Long EMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-14 00:00:00
end: 2023-09-13 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("EMA Cross Strategy", overlay=true, initial_capital=100, currency="USD", default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.075)

small_ema = input(29, title="Small EMA")
long_ema = input(86, title="Long EMA")

ema1 = ema(close, small_ema)
ema2 = ema(close, long_ema)

longCondition = ema1 > ema2
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = ema1 < ema2
if (shortCondition)
    strategy.entry("Short", strategy.short)
    
//strategy.close("Long", when=close < ema1)
//strategy.close("Short", when=close > ema1)
    
x1 = plot(ema(close, small_ema), title="EMA 1", color=longCondition?green:shortCondition?red:blue, transp=0, linewidth=0)
x2 = plot(ema(close, long_ema), title="EMA 2", color=longCondition?green:shortCondition?red:blue, transp=0, linewidth=0)

//bgcolor(longCondition?green:shortCondition?red:blue, transp=75)

fill(x1,x2,color=longCondition?green:shortCondition?red:blue)
```

> Detail

https://www.fmz.com/strategy/426844

> Last Modified

2023-09-14 19:51:37

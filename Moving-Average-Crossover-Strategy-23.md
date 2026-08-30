
> Name

Moving Average Golden Cross Strategy Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

## Strategy Principle
The Moving Average Golden Cross Strategy generates trading signals by calculating the intersection of two moving averages with different periods. When the short-period moving average crosses the long-period moving average, a buy signal is generated; when the short-period moving average crosses below the long-period moving average, a sell signal is generated.
For example, when the 5-day moving average crosses the 21-day moving average, go long; when the 5-day moving average crosses below the 21-day moving average, close the long position.
The specific trading logic of the strategy is:
1. Calculate two moving averages, one short-term, such as the 5th, and one long-term, such as the 21st.
2. When the 5-day moving average crosses the 21-day moving average from below, go long
3. When the 5-day moving average crosses the 21-day moving average from above, close the long position
4. In the same way, calculate a short-term moving average such as the 14th day and a long-term moving average such as the 28th day.
5. Go short when the 14-day moving average crosses the 28-day moving average
6. When the 14-day moving average crosses below the 28-day moving average, close the short position
By choosing different moving average cycle combinations, you can adapt to the long-term and short-term trends of the market.
## Strategic Advantages
- Simple, easy to implement
- Moving average has a certain trend filtering effect
- Parameters can be optimized by adjusting the cycle
## Strategy Risk
- Moving average lags, there is a time difference
- Long and short positions may be opened simultaneously
- Easy to stop losses in volatile market conditions
## Summarize
The moving average golden cross strategy uses moving average crossovers of different periods to generate trading signals and adapts to the market cycle through parameter adjustment. It is a simple and practical trend following strategy. However, its hysteresis and anti-shock ability are weak, so it needs to be used with caution. You can consider assisting other indicators for filtering optimization.


||


## Strategy Logic

The moving average crossover strategy generates buy and sell signals by calculating the crossover between two moving averages of different periods. A long signal is generated when the shorter period MA crosses above the longer period MA, while a short signal is generated on the downward crossover.

For example, going long when the 5-day MA crosses above the 21-day MA, and closing the long when the 5-day MA crosses back below the 21-day MA. 

The trading logic is:

1. Calculate two MAs, one short-term e.g. 5-day and one long-term e.g. 21-day
2. Go long when the 5-day MA crosses above the 21-day MA 
3. Close the long when the 5-day MA crosses back below the 21-day MA
4. Similarly calculate a 14-day and 28-day MA
5. Go short when the 14-day MA crosses below the 28-day MA
6. Close the short when the 14-day MA crosses back above the 28-day MA

Different MA period combinations can suit short or long term trends.

## Advantages

- Simple and easy to implement 
- MAs provide some trend filtering  
- Parameters can be optimized by adjusting periods

## Risks

- MAs lag price, time delay
- Longs and shorts can open simultaneously  
- Prone to whipsaws in choppy markets

## Summary

The MA crossover strategy uses MA crosses to generate signals, with adjustable periods to fit market cycles. A simple trend following approach, but lagging MAs and whipsaw risk need caution. Consider combining with other indicators for filtration and optimization.

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

//@version=3
strategy("My Strategy", overlay=true)

longCondition = crossover(sma(close, 5), sma(close, 21))
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

shortCondition = crossunder(sma(close, 14), sma(close, 28))
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short)
```

> Detail

https://www.fmz.com/strategy/426776

> Last Modified

2023-09-14 14:55:49

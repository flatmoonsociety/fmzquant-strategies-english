
> Name

Trend-Following-Strategy-Based-on-Moving-Average-Crossover
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/e107064a94dc2d0cb2.png)
 [trans]

## Overview
This strategy determines the market trend and follows the trend by calculating different types of moving averages (simple moving average SMA, exponential moving average EMA, Hull moving average HMA and volume weighted moving average VWMA) and finding their intersection points. A buy signal is generated when the shorter-term moving average crosses above the longer-term moving average from below; a sell signal is generated when the shorter-term moving average crosses below the longer-term moving average from above.
## Strategy Principle
This strategy mainly judges the market trend by comparing the relationship between two different moving averages. Specifically, set the type and length of the two moving averages by inputting parameters. The first moving average is longer and represents the long-term trend; the second moving average is shorter and represents the current short-term trend.
When the short-term moving average crosses the long-term moving average from below, it means that the short-term trend has become stronger and the market has entered an upward trend, so a buy signal is issued at this intersection. On the contrary, when the short-term moving average crosses the long-term moving average from above, it means that the short-term trend has weakened and the market has entered a downward trend, so a sell signal is issued at this intersection.
Use such moving average crossover judgments to follow the market trend and trade.
## Strategic Advantages
- Using moving average crossover to determine the main trend is a classic and practical technical indicator.
- Supports many different types of moving average combinations with high flexibility
- The strategy logic is simple and clear, easy to understand and implement, and is suitable for the automation of quantitative trading
- Flexible configurable parameters, suitable for different market environments
## Risk Analysis
- The moving average is lagging. When the cross signal is issued, the price movement may have already occurred or is close to the reversal point, and there is a certain risk of lagging and false alarms.
- Trend judgment may be misjudged, resulting in unnecessary losses
- It is necessary to configure the moving average parameters reasonably. Different parameters may lead to greatly different results.
**Risk Solutions:**
- Appropriately shorten the moving average period to increase sensitivity to market changes
- Verify in combination with other indicators to avoid misjudgment
- Parameter optimization methods: traversal, machine learning, genetic algorithm, etc.
- Properly control position size and stop loss points
## Strategy optimization direction
- Add other indicator filters and combine multiple indicator judgments to improve decision-making accuracy
- Automatically adjust moving average parameters according to market conditions
- Combined with machine learning algorithm to automatically optimize parameters
- Optimize stop loss strategy
## Summarize
This strategy is based on the classic idea of ​​judging the main trend by moving average crossover, and is flexibly applied through the combination of different moving averages. The strategy logic is simple, easy to implement, and suitable for automated trading. Overall, this strategy has certain practicability, but there is also some room for improvement and optimization. Through parameter optimization and adding other filter judgments, the strategy performance can be continuously improved.
||

## Overview

This strategy generates trading signals by calculating different types of moving averages (Simple Moving Average SMA, Exponential Moving Average EMA, Hull Moving Average HMA and Weighted Moving Average VWMA) and detecting crossover points between them, to determine the market trend and follow it. It generates buy signals when the shorter-term MA crosses above the longer-term MA from below, and sell signals when the opposite crossing happens.  

## Strategy Logic

The core idea of this strategy is to judge the market trend by comparing two moving averages. Specifically, it allows configuring two MAs with different types and lengths through input parameters. The first MA has a longer period to represent the major trend, while the second MA has a shorter period for the current short-term trend.  

When the short-term MA crosses over the long-term MA from below, it signals that the short-term trend is strengthening and the market is entering an upward trend. Thus a buy signal is generated at this crossover point. Conversely, when the short-term MA crosses below the long-term MA, it suggests the short-term trend is weakening and the market is reversing downwards. Accordingly a sell signal is generated then.

By detecting such MA crossovers, this strategy follows the market trend to trade.

## Advantages

- Utilizes classic and practical MA crossover method to determine major trends  
- Supports combinations of various MA types, providing flexibility
- Simple and clear logic, easy to understand and automate
- Configurable parameters adapt to different market conditions  

## Risk Analysis  

- MAs have lagging effect, signals may come at or near turning points when price action has already happened
- Trend judgements may be inaccurate, incurring unnecessary losses
- Results vary significantly with different MA parameter settings

**Solutions:**

- Use shorter MA periods for better sensitivity  
- Add other filters for cross-verification to avoid mistakes
- Parameter optimization methods e.g. brute force, machine learning, genetic algorithms
- Control position sizing and stop loss properly  

## Improvement Directions

- Add other indicators as filters to enhance accuracy
- Auto-adapt MA parameters based on changing market conditions
- Utilize machine learning for automated parameter optimization
- Refine stop loss strategy

## Conclusion

This strategy builds on the classic idea of using MA crossovers for major trend detection. With flexible MA combinations, it is simple to implement and suitable for algorithmic trading automation. Overall it is reasonably practical but leaves room for enhancements like parameter tuning, additional filters etc. to further improve performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|25|1st MA Length|
|v_input_3|0|1st MA Type: HMA|EMA|SMA|VWMA|
|v_input_4|7|2nd MA Length|
|v_input_5|0|2nd MA Type: HMA|EMA|SMA|VWMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-31 00:00:00
end: 2024-01-30 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
//study(title="MA Crossover Strategy", overlay = true)
strategy("MA Crossover Strategy", overlay=true)
src = input(close, title="Source")

price = request.security(syminfo.tickerid, timeframe.period, src)
ma1 = input(25, title="1st MA Length")
type1 = input("HMA", "1st MA Type", options=["SMA", "EMA", "HMA", "VWMA"])

ma2 = input(7, title="2nd MA Length")
type2 = input("HMA", "2nd MA Type", options=["SMA", "EMA", "HMA", "VWMA"])

f_hma(_src, _length)=>
    _return = wma((2*wma(_src, _length/2))-wma(_src, _length), round(sqrt(_length)))

price1 = if (type1 == "SMA")
    sma(price, ma1)
else
    if (type1 == "EMA")
        ema(price, ma1)
    else
        if (type1 == "VWMA")
            vwma(price, ma1)
        else
            f_hma(price, ma1)
    
price2 = if (type2 == "SMA")
    sma(price, ma2)
else
    if (type2 == "EMA")
        ema(price, ma2)
    else
        if (type2 == "VWMA")
            vwma(price, ma2)
        else
            f_hma(price, ma2)


//plot(series=price, style=line,  title="Price", color=black, linewidth=1, transp=0)
plot(series=price1, style=line,  title="1st MA", color=blue, linewidth=2, transp=0)
plot(series=price2, style=line, title="2nd MA", color=green, linewidth=2, transp=0)


longCondition = crossover(price1, price2)
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = crossunder(price1, price2)
if (shortCondition)
    strategy.entry("Short", strategy.short)

```

> Detail

https://www.fmz.com/strategy/440545

> Last Modified

2024-01-31 15:17:31

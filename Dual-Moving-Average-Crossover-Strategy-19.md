
> Name

Dual-Moving-Average-Crossover-Strategy based on the Dual-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1155b1ddb5d164aa192.png)
[trans]

## Overview
This strategy is a typical moving average crossover strategy, which uses two sets of moving averages at the same time, one set of fast moving averages and one set of slow moving averages. When the fast moving average crosses the slow moving average, a buy signal is generated; when the fast moving average crosses below the slow moving average, a sell signal is generated. This strategy uses both EMA and SMA to form two sets of fast and slow moving averages. The fast moving average is calculated using EMA, and the slow moving average is calculated using SMA. By confirming multiple sets of moving averages, some false signals can be filtered out and the reliability of the signals can be improved.
## Strategy Principle
The main logic of this strategy is to determine the timing of entry and exit based on the intersection of two sets of fast and slow moving averages.
First, calculate two sets of fast and slow moving averages respectively:
- The first set of quick EMA, with a length of 8 days
- The second set of quick EMA, with a length of 21 days
- The first set of slow SMA, the length is 50 days
- The second set of slow SMAs has a length of 200 days
Then, determine whether the fast EMA has crossed the golden cross or the slow SMA:
- If the 8-day EMA crosses the 50-day SMA, it is a golden cross signal
- If the 8-day EMA falls below the 50-day SMA, it is a dead cross signal
In order to filter out false signals, a second set of EMA and SMA confirmations is added:
- A trading signal will only be issued when the 21-day EMA has also crossed above or below the 50-day SMA
In this way, through the confirmation of two sets of fast and slow moving averages, many false signals can be filtered out, thereby improving the reliability of the signal.
When it is judged that a buy signal is generated, enter the market long; when it is judged that a sell signal is generated, enter the market short.
In addition, this strategy also sets up stop-profit and stop-loss logic. When holding a position, the take profit and stop loss prices will be tracked according to the set profit and loss ratio.
## Advantage Analysis
This strategy has several advantages:
1. Using a double moving average combination can effectively filter out false signals and improve signal accuracy.
2. Use a combination of EMA and SMA to combine the sensitivity of EMA to the latest price changes and the smoothness of SMA
3. Set up stop-profit and stop-loss to lock in profits and control risks.
4. Simple and clear principles, easy to understand and modify
5. Customizable parameters suitable for different market environments
## Risk Analysis
There are also some risks with this strategy:
1. The moving average strategy is prone to produce more shocks, small profits and losses.
2. When the trend changes drastically, large losses may occur
3. Improper parameter settings will also lead to poor profitability.
In order to control risks, it is recommended to:
1. Appropriately adjust the parameter combination to adapt to different market environments
2. Optimize parameters based on backtest results to make the strategy more suitable for the target market
3. Set a stop loss to control the size of a single loss
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Test more fast and slow moving average combinations to find the best parameter combination
2. Use machine learning or genetic algorithms to automatically optimize parameters
3. Add trend judgment indicators to avoid counter-trend trading
4. Add trailing stop or wandering stop to better lock in profits
5. Combine with trading volume or volatility indicators to enhance signal reliability
6. Multi-strategy/multi-variety combination, using non-correlation to spread risks
## Summarize
Generally speaking, this double moving average golden cross and dead cross strategy forms trading signals through the intersection of fast and slow moving averages, and sets stop-profit and stop-loss to control risks. It is simple, intuitive, and easy to implement. This strategy can optimize parameters according to the market and demand, and can also be used in combination with other technical indicators or strategies, making it very practical in quantitative trading.
||

## Overview
This strategy is a typical moving average crossover strategy that uses two sets of moving averages, one fast and one slow. When the fast moving average crosses over the slow moving average, a buy signal is generated. When the fast crosses below the slow, a sell signal is generated. The strategy uses both EMA and SMA for the moving averages, with EMAs as the fast lines and SMAs as the slow lines. Using multiple moving averages can help filter out false signals and improve reliability. 

## Strategy Logic

The core logic relies on crossovers between fast and slow moving average lines to determine entries and exits.

Specifically, two sets of fast and slow moving averages are calculated:

- 1st Fast EMA, length 8 days
- 2nd Fast EMA, length 21 days
- 1st Slow SMA, length 50 days 
- 2nd Slow SMA, length 200 days

Crossovers are then checked between the fast EMAs and slow SMAs:

- If 8-day EMA crosses over 50-day SMA, golden cross signal
- If 8-day EMA crosses below 50-day SMA, death cross signal

To filter false signals, a second EMA/SMA crossover is required for confirmation:

- Only when 21-day EMA also crosses over/under 50-day SMA, trading signal is triggered

By requiring two fast/slow MA crossovers, many false signals can be filtered out and reliability improved.

When buy signal triggers, go long. When sell signal triggers, go short.  

The strategy also sets profit taking and stop loss based on input percentage from entry price once in a position.

## Advantage Analysis

The advantages of this strategy include:

1. Dual MA design filters false signals and improves accuracy 
2. Combination of EMA and SMA utilizes EMA's sensitivity and SMA's smoothness
3. Take profit and stop loss lock in profits and control risks
4. Simple logic easy to understand and modify
5. Customizable parameters suit different market environments

## Risk Analysis

Risks of the strategy:

1. MA strats tend to produce lots of small wins/losses in choppy markets
2. Can face large losses in strong trending markets
3. Poor parameter tuning also leads to underperformance

To control risks:

1. Adjust parameters for different market conditions
2. Optimize based on backtests to fit target market
3. Use stop loss to limit loss size

## Improvement Directions

The strategy can be further optimized by:

1. Testing more fast/slow MA combinations to find best
2. Using machine learning or genetic algos to auto optimize
3. Adding trend filter to avoid counter-trend trades 
4. Adding trailing stop loss to lock in profits
5. Incorporating volume or volatility filters to confirm signals
6. Combining with other strats/products to utilize low correlation

## Conclusion
In summary, the dual MA crossover strategy generates signals with fast/slow MA crosses, sets take profit and stop loss to control risks, and is simple, intuitive and easy to implement. The parameters can be tuned and combined with other indicators for better performance. It has great utility in quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|8|Length|
|v_input_2|true|EMA|
|v_input_3|21|Length|
|v_input_4|true|EMA|
|v_input_5|50|Length|
|v_input_6|true|SMA|
|v_input_7|200|Length|
|v_input_8|true|SMA|
|v_input_9|8|Profit/lost %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-20 00:00:00
end: 2024-02-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © JMLSlop

//@version=4

src = close
strategy("Crossover moving averages", shorttitle="Cross MA-EMA", overlay=true, calc_on_order_fills=false)

// first fast EMA
len = input(8, "Length", type=input.integer, minval=1)
doma1 = input(true, title="EMA")
out1 = ema(src, len) 

//Second fast EMA
len2 = input(21, minval=1, title="Length")
doma2 = input(true, title="EMA")
out2 = ema(src, len2)

//First slow MA
len3 = input(50, minval=1, title="Length")
doma3 = input(true, title="SMA")
out3 = sma(src, len3)

//Second slow MA
len4 = input(200, minval=1, title="Length")
doma4 = input(true, title="SMA")
out4 = sma(src, len4)

// Profit
profit = input(8, "Profit/lost %", type=input.float, minval=1) * 0.01


plot(doma1 and out1 ? out1: na, color=color.blue, linewidth=1, title="1st EMA")
plot(doma2 and out2 ? out2: na, color=color.red, linewidth=1, title="2nd EMA")
plot(doma3 and out3 ? out3: na, color=color.green, linewidth=2, title="1st MA")
plot(doma4 and out4 ? out4: na, color=color.orange, linewidth=3, title="2nd MA")

// Orders config
takeProfitPrice =
     (strategy.position_size > 0) ? strategy.position_avg_price + open*profit : (strategy.position_size < 0) ? strategy.position_avg_price - (open*profit) : na

longStopPrice  = strategy.position_avg_price * (1 - profit)
shortStopPrice = strategy.position_avg_price * (1 + profit)

longCondition2 = (out2>out3 and (crossover(out1, out4) or crossover(out1[1], out4[1]) or crossover(out1[2], out4[2]) or (crossover(out1[3], out4[3]))) or (out2>out3 and (crossover(out1, out3) or crossover(out1[1], out3[1]) or crossover(out1[2], out3[2]) or crossover(out1[3], out3[3]))))
if (longCondition2)
    strategy.entry("Enter L", strategy.long)

shortCondition2 = (out2<out3 and (crossunder(out1, out4) or crossunder(out1[1], out4[1]) or crossunder(out1[2], out4[2]) or crossunder(out1[3], out4[3]))) or (out2<out3 and (crossunder(out1, out3) or crossunder(out1[1], out3[1]) or crossunder(out1[2], out3[2]) or crossunder(out1[3], out3[3])))
if (shortCondition2)
    strategy.entry("Enter S", strategy.short)


if (strategy.position_size > 0)
    strategy.exit("Exit L", limit=takeProfitPrice, stop=longStopPrice)

if (strategy.position_size < 0)
    strategy.exit("Exit S", limit=takeProfitPrice, stop=shortStopPrice)

```

> Detail

https://www.fmz.com/strategy/442957

> Last Modified

2024-02-27 16:21:02

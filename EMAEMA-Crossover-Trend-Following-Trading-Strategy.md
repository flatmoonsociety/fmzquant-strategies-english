
> Name

Trend following trading strategy EMA-Crossover-Trend-Following-Trading-Strategy based on EMA indicator
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/b053e832e7c826d35880f4f96d6b6d316e447129b0012ed0c7c67e0b536a2e53.png)
[trans]
## Overview
This strategy uses the golden cross and dead cross of the EMA fast and slow lines to determine the trend, and combines it with the preset take-profit ratio to implement trend following transactions. This strategy is suitable for any time period and can capture the trends of indexes and individual stocks.
## Strategy Principle
This strategy uses EMA lines of length 3 and 30 as trading signals. When the 3EMA crosses above the 30EMA, it indicates that the price has begun to rise and meets the buying conditions; when the 3EMA falls below the 30EMA, it indicates that the price has begun to fall and meets the selling conditions.
At the same time, the strategy also sets profit-taking conditions. When the price rises and reaches the strategy entry price according to the set take-profit ratio, EXIT will occur. This can lock in more profits and enable trend following trading.
## Advantage Analysis
1. Using the EMA indicator to determine the trend direction is simple and easy to master;
2. Combining trend indicators and profit-taking methods, you can effectively control risks and lock in profits;
3. It can be applied to any cycle and any variety, with strong flexibility.
## Risk Analysis
1. The EMA line itself has a lag in price changes, and misjudgments may occur;
2. If the take-profit ratio is set too large, it may result in failure to take profit in time and miss the opportunity for reversal;
3. If you stop tracking too early, you may not be able to capture all the trends.
## Optimization direction
1. You can test EMA with different parameter combinations to find the best parameters;
2. It can be combined with other indicators to verify the EMA signal and improve the accuracy;
3. Dynamically adjust the take-profit ratio, relax it appropriately in a bull market, and tighten it appropriately in a bear market.
## Summarize
This strategy is overall a very useful trend following strategy. It uses a simple EMA indicator to determine the trend direction and sets reasonable profit-taking rules, which can effectively control risks and is suitable for long-term tracking of the medium and long-term trends of stocks and indices. Through parameter optimization and supporting indicator verification, the stability and Profit Factor of the strategy can be further improved.
||

## Overview

This strategy uses the golden cross and death cross of fast and slow EMA lines to determine the trend and sets a profit percentage as the take profit rule to implement trend following trading. It is applicable to any timeframe and can capture trends in both indexes and stocks.

## Strategy Logic

The strategy employs 3 and 30 period EMAs as trading signals. When the 3EMA crosses above the 30EMA, it signals that price starts to rise which conforms to the buy condition. When the 3EMA crosses below the 30EMA, it signals that price starts to fall which conforms to the sell condition.  

In addition, a profit target is configured in the strategy. When price rises to the entry price multiplied by the profit percentage, the position will be closed to lock in more profits and achieve trend following trading.

## Advantage Analysis  

1. Using EMAs to determine trends is simple and easy to grasp. 
2. Combining trend indicators and take profit rules can effectively control risks and lock in profits.
3. Applicable to any timeframe and tradable, great flexibility.

## Risk Analysis

1. EMA itself has lagging effect on price changes, may cause misjudgments.  
2. Overly large profit target may lead to failure in timely profit-taking, missing reversal opportunities.
3. Stopping tracking too early may result in missing part of the trending move.

## Optimization Directions 

1. Different EMA combinations can be tested to find the optimal parameters.
2. Other indicators can be combined to verify the EMA signals and improve accuracy. 
3. The profit percentage can be dynamically tuned, relaxed during bull market and tightened during bear market.

## Conclusion

In conclusion, this is a very practical trend following strategy. It adopts simple EMA indicators to determine the trend direction and sets reasonable profit taking rules to effectively control risks, suitable for long term tracking of stock and index mid-to-long term trends. Further improvements on stability and profit factor can be achieved through parameter optimization and supplementary signal verification indicators.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|Fast EMA Length|
|v_input_2|30|Slow EMA Length|
|v_input_3|100|Profit Percentage|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-12 00:00:00
end: 2024-02-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA Crossover Strategy with Target", shorttitle="EMACross", overlay=true)

// Define input parameters
fastLength = input(3, title="Fast EMA Length")
slowLength = input(30, title="Slow EMA Length")
profitPercentage = input(100.0, title="Profit Percentage")

// Calculate EMAs
fastEMA = ta.ema(close, fastLength)
slowEMA = ta.ema(close, slowLength)

// Plot EMAs on the chart
plot(fastEMA, color=color.blue, title="Fast EMA")
plot(slowEMA, color=color.red, title="Slow EMA")

// Buy condition: 3EMA crosses above 30EMA
buyCondition = ta.crossover(fastEMA, slowEMA)

// Sell condition: 3EMA crosses below 30EMA or profit target is reached
sellCondition = ta.crossunder(fastEMA, slowEMA) or close >= (strategy.position_avg_price * (1 + profitPercentage / 100))

// Target condition: 50 points profit
//targetCondition = close >= (strategy.position_avg_price + 50)

// Execute orders
// strategy.entry("Buy", strategy.long, when=buyCondition)
// strategy.close("Buy", when=sellCondition )
if (buyCondition)
    strategy.entry("Buy", strategy.long)

if (sellCondition)
    strategy.close("Buy")

// // Execute sell orders
// strategy.entry("Sell", strategy.short, when=sellCondition)
// strategy.close("Sell", when=buyCondition)

// Plot buy and sell signals on the chart
plotshape(series=buyCondition, title="Buy Signal", color=color.green, style=shape.labelup, location=location.belowbar)
plotshape(series=sellCondition, title="Sell Signal", color=color.red, style=shape.labeldown, location=location.abovebar)

```

> Detail

https://www.fmz.com/strategy/442077

> Last Modified

2024-02-19 10:39:22

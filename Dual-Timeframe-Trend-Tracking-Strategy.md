
> Name

Dual-Timeframe-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13ddc56bc1ed43c3339.png)

[trans]

## Overview
This strategy uses double moving averages to configure on the daily and hourly lines, determines the direction of the general trend on the daily line, and makes specific market entries and exits on the hourly line. Go long when the daily line indicates an upward trend and a golden cross occurs on the hourly line; close the position when the daily line indicates an upward trend and a dead cross occurs on the hourly line. This configuration allows us to capture short- and medium-term opportunities in the general trend while avoiding the impact of short-term market fluctuations.
## Strategy Principle
1. Calculate fast EMA lines and slow EMA lines on the daily chart
2. When the fast EMA line crosses the slow EMA line, it is judged to be an upward trend.
3. Also calculate the fast and slow EMA lines on the hourly chart.
4. Go long when the fast EMA line of the hourly line crosses the slow EMA line
5. Close the position when the fast EMA line of the hourly line crosses the slow EMA line
## Advantage Analysis
The main advantages of this dual time frame configuration are:
1. Ability to capture short-term trading opportunities in general trends and enhance profit probability
2. Use double EMA filtering configuration to avoid arbitrage
3. Only open positions when the trend background is good to effectively control risks
4. Combine multi-time axis judgment to improve the accuracy of decision-making
## Risk Analysis
The main risks of this strategy are:
1. When there is an error in judging the general trend, the risk of stop loss is greater.
2. When the hourly line fluctuates violently, false signals will be generated
3. When parameters are set improperly, it is easy to over-trade and cause arbitrage.
These risks can be avoided and reduced by appropriately relaxing the stop loss range, optimizing parameter combinations, or adding filter conditions.
## Optimization direction
This strategy can be further optimized:
1. Add volume and energy indicators and other filters on daily or hourly lines to improve decision-making accuracy
2. Add an adaptive stop-loss mechanism to proactively avoid risks
3. Optimize the combination of moving average parameters and find the best configuration
4. Determine trends in higher time frames and implement multi-timeline nesting
## Summary
This strategy uses dual time frame analysis to capture short- and medium-term opportunities based on judgment of the general trend. Configure dual EMA to filter out noise. This configuration not only ensures the probability of profit, but also effectively controls risks. Through further optimization, the strategy can be made more robust and efficient, which is worthy of recommendation.
||


## Overview
This strategy uses double moving averages configured on the daily and hourly charts to determine the major trend direction on the daily chart and enter and exit trades on the hourly chart. It goes long when the daily chart indicates an upward trend and the hourly chart sees a golden cross, and closes the position when the daily chart shows an upward trend but the hourly chart sees a death cross. This configuration allows us to capture short-to-medium-term opportunities while avoiding the impacts of short-term market fluctuations.

## Strategy Logic
1. Calculate fast and slow EMA lines on the daily chart  
2. Determine an upward trend when the fast EMA line crosses above the slow EMA line
3. Also calculate fast and slow EMA lines on the hourly chart
4. Go long when the hourly fast EMA crosses above the slow EMA
5. Close the position when the hourly fast EMA crosses below the slow EMA  

## Advantage Analysis 
The main advantages of this dual timeframe configuration are:
1. Captures short-term trading opportunities in line with major trends, improving profitability  
2. The double EMA filter avoids whipsaws
3. Only trades when trend background is favorable, effectively controlling risk
4. Combining multiple timeframes improves decision accuracy  

## Risk Analysis
Main risks of this strategy are:
1. Incorrect major trend judgement leads to larger stop loss risk
2. Volatile hourly price action can generate false signals 
3. Improper parameter tuning causes overtrading and whipsaws

These risks can be mitigated by widening stop loss levels, optimizing parameters, or adding filters.

## Optimization Directions
This strategy can be further optimized by:
1. Adding additional indicators like volume to improve signal accuracy
2. Implementing adaptive stop loss mechanisms to actively manage risk
3. Finding optimal moving average parameter combinations  
4. Judging trends across even higher timeframes for robustness

## Conclusion
This strategy leverages a dual timeframe analysis to capture short-to-medium-term opportunities within major trends. The double EMA configuration filters out noise. This provides solid profitability while effectively managing risk. Further optimizations can make the strategy more robust and efficient for wider application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|20|Short EMA Length (Daily)|
|v_input_int_2|50|Long EMA Length (Daily)|
|v_input_int_3|10|Short EMA Length (Hourly)|
|v_input_int_4|30|Long EMA Length (Hourly)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-08 00:00:00
end: 2023-12-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Dual Time Frame Strategy", overlay=true)

// Define Daily Time Frame Inputs
lenShort = input.int(20, title="Short EMA Length (Daily)", minval=1)
lenLong = input.int(50, title="Long EMA Length (Daily)", minval=1)

// Calculate EMAs on Daily Time Frame
emaShort_D = ta.ema(close, lenShort)
emaLong_D = ta.ema(close, lenLong)

// Define Hourly Time Frame Inputs
lenShort_H = input.int(10, title="Short EMA Length (Hourly)", minval=1)
lenLong_H = input.int(30, title="Long EMA Length (Hourly)", minval=1)

// Calculate EMAs on Hourly Time Frame
emaShort_H = ta.ema(close, lenShort_H)
emaLong_H = ta.ema(close, lenLong_H)

// Daily Time Frame Condition
dailyUpTrend = emaShort_D > emaLong_D

// Hourly Time Frame Condition
hourlyBuy = ta.crossover(emaShort_H, emaLong_H)
hourlySell = ta.crossunder(emaShort_H, emaLong_H)

// Strategy Entry and Exit Conditions
if (dailyUpTrend and hourlyBuy)
    strategy.entry("Buy", strategy.long)
    
if (dailyUpTrend and hourlySell)
    strategy.close("Buy")

// Plot EMAs for Daily and Hourly Time Frames
plot(emaShort_D, color=color.blue, title="Short EMA (Daily)")
plot(emaLong_D, color=color.red, title="Long EMA (Daily)")

plot(emaShort_H, color=color.green, title="Short EMA (Hourly)")
plot(emaLong_H, color=color.orange, title="Long EMA (Hourly)")

```

> Detail

https://www.fmz.com/strategy/435492

> Last Modified

2023-12-15 13:46:47


> Name

Timed-Order-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The main idea of ​​the timed order strategy is to perform buying and selling operations at user-defined time points. This strategy allows users to set a precise time point at which they will first sell their current position and then make a limit buy at a price 1% lower than the current price. This allows for regular rebalancing at specific times every day.
## Strategy Principle
This strategy first obtains user-defined hours and minutes through the input function, and then uses the timestamp function to generate the order execution time. If the current time is after the specified time point, the sell and buy operations are triggered.
Specifically, the strategy first determines whether the current time is within the start and end date range specified by the user. If it is met, when the specified order execution time point is reached, the current position will be sold at the market price first, and then the limit price will be bought at 99% of the current price. In this way, positions can be re-adjusted at a price that is 1% lower than the current price at a specific time point.
## Advantage Analysis
The biggest advantage of this strategy is that positions can be re-adjusted regularly at specific points in time, without the need for manual operations and reducing labor costs. In addition, by buying at a price slightly lower than the current price every time you re-adjust positions, you can get a certain advantage of ultra-low buying.
Specific advantages include:
1. Completely automated operation, reducing labor costs.
2. Positions can be re-adjusted regularly at specific points in time.
3. Each time you re-adjust positions, you can get an ultra-low buying opportunity slightly lower than 1% of the current price.
4. The time point for position adjustment can be customized and adjusted flexibly.
5. The start and end dates of the position adjustment cycle can be customized to facilitate backtesting and optimization.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. If the time point for regular position adjustment is not chosen properly, you may miss a better buying opportunity or sell at an inappropriate time.
2. The buying price is only 1% lower than the selling price, and it may not be possible to obtain enough ultra-low buying price difference in each position adjustment cycle.
3. Both selling and buying are market orders, which may be affected by a certain degree of slippage.
4. If the strategy only operates at a specific point in time, the market cannot be managed between that point in time.
5. Frequent position adjustments will incur more transaction fees.
Corresponding solutions:
1. Choose an appropriate time point for position adjustment and judge based on other technical indicators.
2. The bid spread parameters can be added as appropriate.
3. Try to choose trading varieties with better depth and less volatility.
4. It can be used in conjunction with other strategies for risk management during non-positioning periods.
5. Appropriately control the frequency of position adjustment and balance the advantages of position adjustment and transaction costs.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize the selection of time points for position adjustment, and select the optimal time point based on the intraday cycle characteristics of trading varieties.
2. Add other technical indicator judgments to avoid adjusting positions at unfavorable times. For example, combined with trend judgment indicators such as moving averages.
3. Optimize ultra-low buying parameters to balance advantages and transaction costs.
4. Use trailing stop loss and stop profit to manage positions between positions.
5. Combine with machine learning algorithms to train historical data and automatically optimize the position adjustment time point.
6. Add the right-restoration function and adjust the position adjustment point according to stock splits, dividends and other time points.
## Summarize
Overall, the timed order strategy can automate the trading process and reduce manual operation costs by regularly adjusting positions. There is a lot of room for strategy optimization, which can be improved from aspects such as position selection time point, buying parameter setting, stop loss and profit, and algorithm optimization. At the same time, you also need to pay attention to certain transaction risks and take appropriate risk management measures. Overall, this strategy is suitable for quantitative traders who pursue efficient automated position adjustment.
||

## Overview

The main idea of the timed order strategy is to conduct buying and selling operations at user-defined time points. This strategy allows users to set an exact time point. At this time point, it will first sell the current position, and then place a limit buy order at 1% below the current price. This allows periodic rebalancing to be carried out at a specific time every day.

## Strategy Logic

The strategy first uses the input function to get the custom hour and minute defined by the user, and then generates the order execution time using the timestamp function. If the current time is after the specified time point, the selling and buying operations are triggered. 

Specifically, the strategy first checks if the current time is within the user-defined start and end date range. If yes, when the specified order execution time point is reached, it will first sell the current position at market price, and then place a limit buy order at 99% of the current price. This achieves rebalancing at a price 1% lower than the current price at the specific time point.

## Advantage Analysis

The biggest advantage of this strategy is that it can periodically rebalance positions at specific time points without manual intervention, reducing labor costs. In addition, each rebalancing buys at a slightly lower price than the current price, gaining some ultra-low buying advantage.

The specific advantages include:

1. Fully automated operation, reducing manual costs. 

2. Allows periodic rebalancing of positions at specific time points.

3. Gains ultra-low buying opportunities around 1% below current prices during each rebalancing. 

4. Customizable rebalancing time points, flexible adjustment.

5. Customizable start and end dates for rebalancing cycles, convenient for backtesting optimization.

## Risk Analysis

The strategy also has some risks to note:

1. If the periodic rebalancing time point is poorly chosen, it may miss better buying opportunities or sell out at inappropriate times.

2. The buy price is only 1% lower than the sell price, may not gain sufficient ultra-low buy price spread in each rebalancing cycle.

3. Both sell and buy are market orders, may suffer from some degree of slippage. 

4. If the strategy only operates at specific time points, the market cannot be managed between those time points.

5. Frequent rebalancing will incur relatively higher trading fees.

The corresponding solutions:

1. Choose appropriate rebalancing time points, also combine with other technical indicators.

2. Increase the buy price spread parameter as appropriate.

3. Choose products with good depth and low volatility. 

4. Combine with other strategies for risk management during non-rebalancing periods.

5. Control rebalancing frequency appropriately to balance advantages and trading costs.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Optimize rebalancing time point selection based on the intraday cycle characteristics of the trading products.

2. Add other technical indicators to avoid rebalancing at unfavorable times. For example, combining moving average trend indicators.

3. Optimize the ultra-low buy parameter to balance advantage and trading cost. 

4. Adopt trailing stop loss/take profit to manage positions between rebalancings. 

5. Use machine learning algorithms to train on historical data and automatically optimize rebalancing time points.

6. Add adjustments around stock splits, dividends etc. to follow timing changes.

## Summary  

In general, the timed order strategy can automate the trading process and reduce manual operation costs through periodic rebalancing. There is large room for optimization in areas like rebalancing time point selection, buy parameter setting, stop loss/take profit, and algorithm improvement. Also need to note certain trading risks and take appropriate risk management measures. Overall, this strategy suits quantitative traders looking for efficient automated rebalancing.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Hour for Order Execution|
|v_input_2|false|Minute for Order Execution|
|v_input_3|10|Start Day|
|v_input_4|2|Start Month|
|v_input_5|2021|Start Year|
|v_input_6|22|End Day|
|v_input_7|3|End Month|
|v_input_8|2021|End Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-28 00:00:00
end: 2023-09-27 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/








// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ytrevor

//@version=4
strategy("Order At Specified Time", overlay=true)


// -- These inputs are for customizing the times of your desired orders -- //
customHour = input(title="Hour for Order Execution", type=input.integer, defval=01, minval=00, maxval=24) //
customMinute = input(title="Minute for Order Execution", type=input.integer, defval=00, minval=00, maxval=59)
targetTime = timestamp("UTC", year, month, dayofmonth, customHour, customMinute, 00) //Order executes at this time

inDateRange = (time >= targetTime) and (time <= targetTime) //Orders are placed everyday at 01:00 UTC, or any other time specified via input


// -- These inputs are for back testing. Feel free to change the start and end dates via input -- // 
startDay = input(title="Start Day", type=input.integer, defval=10, minval=1, maxval=31) 
startMonth = input(title="Start Month", type=input.integer, defval=2, minval=1, maxval=12)
startYear = input(title="Start Year", type=input.integer, defval=2021)
endDay = input(title="End Day", type=input.integer, defval=22, minval=1, maxval=31)
endMonth = input(title="End Month", type=input.integer, defval=3, minval=1, maxval=12)
endYear = input(title="End Year", type=input.integer, defval=2021)

betweenDates = true


// -- Order execution --  //
if betweenDates
    buyPrice = close*0.99 //Buy at 1% lower than selling price
    strategy.entry("Sell", strategy.short, when=inDateRange) //Sell at 01:00 UTC, or at any other time specified via input
    strategy.entry("Buy", strategy.long, limit=buyPrice, when=inDateRange) //Buy limit order placed at the same time, 1% lower than selling price



```

> Detail

https://www.fmz.com/strategy/428087

> Last Modified

2023-09-28 15:26:20

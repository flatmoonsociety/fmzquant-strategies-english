
> Name

Daily-Close-Price-Comparison-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy determines the long and short direction by comparing the closing price of the current K-line with the closing price of the previous day. It is a simple trend following strategy, going long when the price rises and shorting when the price falls. There is no need to judge complex indicators, and the trend direction can be judged through the most basic price information.
## Strategy Principle
1. Calculate the difference ratio between the current K-line closing price and the previous day's closing price.
2. When the ratio is greater than the set threshold, it means that the price is rising, so go long.
3. When the ratio is less than the negative set threshold, it means that the price is falling and you are short.
4. The threshold is set to 0, that is, as long as it rises, go long, and as long as it falls, go short.
5. There is no stop-loss and stop-profit logic, and profits are achieved solely by the continuity of the trend.
## Advantage Analysis
1. A very simple and intuitive trend judgment method, easy to understand and implement.
2. No need to calculate any technical indicators, reducing computing resource usage.
3. Only focus on the core price information and reduce unnecessary indicator noise.
4. The backtest performance is excellent, but the actual performance is questionable.
## Risk Analysis
1. Without stop loss settings, there is the risk of unlimited losses.
2. Unable to effectively handle the consolidation and fluctuation of the market, and easy to be trapped.
3. There is a risk of over-fitting, and the actual effect needs to be verified.
4. Simply following the trend cannot lock in profits, and the profits achieved are limited.
## Optimization direction
1. Add a trailing stop loss strategy to make losses controllable.
2. Combined with volatility indicators, reduce the arbitrage rate of market consolidation.
3. Test cycle parameter settings for different days to improve stability.
4. Add trend judgment indicators to avoid irrational price fluctuations.
5. Optimize the profit-taking strategy, such as looking back at the highest price, to expand profit margins.
## Summarize
The core idea of ​​this strategy is simple, but the actual effect is questionable. It is necessary to strengthen the risk control mechanism and carry out parameter optimization testing to make it truly practical. But the basic ideas are worth learning from.
|| 

## Overview

This strategy determines direction by comparing the current bar's closing price to previous bar's closing price. It is a simple trend following strategy, going long when price rises and short when price drops. No complex indicators are needed, just the most basic price information is used to determine trend direction.

## Strategy Logic

1. Calculate percentage difference between current bar's closing price and previous bar's closing price.

2. If percentage is greater than the threshold, it indicates rising price, go long. 

3. If percentage is less than negative threshold, it indicates falling price, go short.

4. Threshold is set to 0, meaning go long on any rise and short on any drop.

5. No stop loss or take profit logic, relying solely on trend persistence for profitability.

## Advantage Analysis 

1. Very simple and intuitive trend determination method, easy to understand and implement.

2. No need to compute any technical indicators, reducing resource consumption. 

3. Only focuses on core price information, avoiding unnecessary indicator noise.

4. Excellent backtest results but live performance is questionable.

## Risk Analysis

1. No stop loss exposes unlimited loss risks.

2. Ineffective in range-bound choppy markets, prone to being trapped.

3. Overfitting risks exist, live performance yet to be validated. 

4. Pure trend following cannot lock in profits, realized profit is limited.

## Optimization Directions 

1. Add trailing stop loss for risk control.

2. Incorporate volatility measures to reduce whipsaws in choppy markets.

3. Test different period parameters for increased robustness.

4. Add trend determination indicators to avoid irrational price moves.

5. Optimize profit taking like lookback highest price to expand profit potential.

## Summary

The strategy's core idea is simple but its live performance is questionable. Stronger risk control mechanisms and parameter optimization testing are needed before real application. But the basic concept is worth learning from.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Price Difference Threshold|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-17 00:00:00
end: 2023-09-16 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Daily Close Comparison Strategy (by ChartArt)", shorttitle="CA_-_Daily_Close_Strat", overlay=false)

// ChartArt's Daily Close Comparison Strategy
//
// Version 1.0
// Idea by ChartArt on February 28, 2016.
//
// This strategy is equal to the very
// popular "ANN Strategy" coded by sirolf2009,
// but without the Artificial Neural Network (ANN).
//
// Main difference besides stripping out the ANN
// is that I use close prices instead of OHLC4 prices.
// And the default threshold is set to 0 instead of 0.0014
// with a step of 0.001 instead of 0.0001.
//
// This strategy goes long if the close of the current day
// is larger than the close price of the last day.
// If the inverse logic is true, the strategy
// goes short (last close larger current close).
//
// This simple strategy does not have any
// stop loss or take profit money management logic.
//
// List of my work: 
// https://www.tradingview.com/u/ChartArt/
// 
//  __             __  ___       __  ___ 
// /  ` |__|  /\  |__)  |   /\  |__)  |  
// \__, |  | /~~\ |  \  |  /~~\ |  \  |  
// 
// 

threshold = input(title="Price Difference Threshold", type=float, defval=0, step=0.001)

getDiff() =>
    yesterday=security(syminfo.tickerid, 'D', close[1])
    today=security(syminfo.tickerid, 'D', close)
    delta=today-yesterday
    percentage=delta/yesterday
    
closeDiff = getDiff()
 
buying = closeDiff > threshold ? true : closeDiff < -threshold ? false : buying[1]

hline(0, title="zero line")

bgcolor(buying ? green : red, transp=25)
plot(closeDiff, color=silver, style=area, transp=75)
plot(closeDiff, color=aqua, title="prediction")

longCondition = buying
if (longCondition)
    strategy.entry("Long", strategy.long)

shortCondition = buying != true
if (shortCondition)
    strategy.entry("Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/427066

> Last Modified

2023-09-17 18:28:31

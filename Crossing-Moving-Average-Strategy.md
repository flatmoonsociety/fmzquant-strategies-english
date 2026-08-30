
> Name

Crossing-Moving-Average-Strategy based on different periods
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1325cdb1618c44908ae.png)
[trans]

## Overview
The moving average crossover strategy is a quantitative trading strategy that uses exponential moving averages (EMA) of different periods to generate trading signals. This strategy uses the intersection of three EMAs of 5, 9 and 21 periods to determine market trends and generate buy and sell signals. At the same time, this strategy also combines the longer-period 100-period and 200-period EMA to determine the general trend.
## Strategy Principle
The core indicator of this strategy is the three-bar EMA of 5, 9 and 21 periods. Its trading logic is based on the following points:
1. When the 5-period EMA breaks through the 9-period EMA upwards, a buy signal is generated; when the 5-period EMA breaks through the 9-period EMA downwards, a sell signal is generated.
2. The 21-period EMA can be used to validate trading signals. That is, when the 5-period EMA and the 9-period EMA are both higher than the 21-period EMA, the buy signal is more effective; when both are lower than the 21-period EMA, the sell signal is more effective.
3. The 100-period and 200-period EMA are used to determine the mid- and long-term market trends. They can provide validation or warning of larger trends for short-term trading signals.
## Advantage Analysis
This strategy has the following advantages:
1. Simple operation and easy to implement. The calculation of EMA and the judgment of crossover situations are very simple.
2. Be responsive to the market. The 5-period and 9-period EMA are very sensitive to price changes and can quickly capture short-term trends.
3. Easy to set stop loss and take profit. The EMA itself acts as a trailing stop.
4. Good scalability. Other period EMAs or technical indicators can be easily introduced to enrich the system.
## Risk Analysis
This strategy also has the following main risks:
1. Risk of false signals. EMA crossovers are not 100% reliable and false breakouts may occur. It should be judged carefully in combination with other factors.
2. Trend reversal risk. A quick EMA crossover may only reflect a short-term correction and ignore a larger trend reversal. The mid to long term EMA should be referenced.
3. Parameter Tuning Risks. Parameter settings will vary greatly under different varieties and market conditions, and require full optimization and testing.
## Optimization direction
This strategy can be optimized from the following perspectives:
1. Introduce other indicators to filter signals, such as KD, MACD, etc., to reduce the probability of false signals.
2. Increase the stop loss range to reduce single loss. Or trailing stop and trailing stop to lock in profits.
3. Optimize the parameters and find the optimal combination of period parameters. Machine learning methods can also be used for dynamic optimization.
4. Combine with the quantitative framework to automate the entire transaction process.
## Summarize
This moving average crossover strategy has a clear overall idea, is easy to operate, and can effectively capture short-term trends. However, there are still certain blind spots in relying solely on the EMA cross to make decisions, and other factors need to be assisted to make decisions and reduce risks. This strategy has a large space for optimization, and it is expected to enrich the content of the strategy and improve stable profitability by introducing more indicators or technical means.
|| 

## Overview  

The crossing moving average strategy is a quantitative trading strategy that generates trading signals by using exponential moving averages (EMAs) of different time periods. This strategy employs the crossovers of three EMAs - 5-period, 9-period, and 21-period - to determine market trends and generate buy and sell signals. It also incorporates longer-period 100-period and 200-period EMAs to gauge the major trend.  

## Principles  

The core indicators of this strategy are the three EMAs of 5-period, 9-period and 21-period. Its trading logic is based on the following points:  

1. A buy signal is generated when the 5-period EMA crosses above the 9-period EMA, and a sell signal when it crosses below.  

2. The 21-period EMA can be used to validate the trading signals. Trading signals are more reliable when both 5 and 9 EMAs are above the 21 EMA for buy signals, and below it for sell signals.

3. The 100 and 200 EMAs serve to determine mid to long-term trends in the market. They can provide trend validation or warning for short-term trading signals.

## Advantage Analysis   

This strategy has the following advantages:

1. Simple to implement and operate. EMA calculation and crossover judgment is straightforward.  

2. Sensitive to market changes. The fast 5 & 9 EMAs can quickly capture short-term trends.

3. Easy to set stop loss/take profit. EMAs themselves can serve as moving stop loss lines.  

4. Extendable. Other EMAs or indicators can be easily introduced to enrich the system.

## Risk Analysis

The main risks of this strategy include:  

1. False signal risk. EMA crossovers are not 100% reliable and false breaks can occur. Other factors need careful review.

2. Trend reversal risk. Fast EMA crosses may just reflect short-term corrections, ignoring major trend reversals. Mid to long term EMAs should be checked.  

3. Parameter tuning risk. Parameters can vary greatly across different products and market regimes, requiring thorough optimization and testing.

## Optimization Directions  

This strategy can be optimized in the following aspects:

1. Introduce other filters like KD, MACD etc to screen signals and reduce false signals.  

2. Expand stop loss size to limit losses. Or adopt trailing stop to lock in profits.

3. Optimize parameters to find the optimal EMA period combinations. Machine learning can also be used to dynamically optimize the periods.  

4. Automate the entire trading workflow by integrating quantitative frameworks.  

## Summary  

The crossing moving average strategy has a clear logic and is easy to operate, capturing short-term trends effectively. But sole reliance on EMA crosses for decision making still has blind spots. Additional factors are required to reduce risks. This strategy has good potential for enhancements by introducing more technical indicators or techniques to improve its profitability and stability.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-12 00:00:00
end: 2023-12-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © nagversion

//@version=5
strategy("5/9/21 EMA Strategy with 200 and 100 EMA", overlay=true)

// Calculate EMAs
ema5 = ta.ema(close, 5)
ema9 = ta.ema(close, 9)
ema21 = ta.ema(close, 21)
ema100 = ta.ema(close, 100)
ema200 = ta.ema(close, 200)

// Plot EMAs
plot(ema5, title="5 EMA", color=color.blue)
plot(ema9, title="9 EMA", color=color.yellow)
plot(ema21, title="21 EMA", color=color.red)
plot(ema100, title="100 EMA", color=color.purple)
plot(ema200, title="200 EMA", color=color.green)

// Strategy conditions
longCondition = ta.crossover(ema5, ema9) and ta.crossover(ema9, ema21)
shortCondition = ta.crossunder(ema5, ema9) and ta.crossunder(ema9, ema21)

if (longCondition)
    strategy.entry("Long", strategy.long)

if (shortCondition)
    strategy.entry("Short", strategy.short)

// Set strategy properties if required (like stop loss, take profit, etc.)

```

> Detail

https://www.fmz.com/strategy/435863

> Last Modified

2023-12-19 13:34:30

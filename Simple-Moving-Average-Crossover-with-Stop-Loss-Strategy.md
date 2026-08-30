
> Name

Simple-Moving-Average-Crossover-with-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy generates trading signals through the intersection of the simple moving average and the volume-weighted price, and uses the exponential moving average as the stop loss level. It is a short-term trading trend following strategy.
## Strategy Principle
1. Calculate the 5-day simple moving average SMA and the volume-weighted price VWAP.
2. When SMA breaks through VWAP from below, a long signal is generated; when SMA falls below VWAP from above, a short signal is generated.
3. SMA is sensitive to price changes and can capture short-term trends; VWAP can reflect the latest price dynamics. The intersection of the two can determine short-term trend changes.
4. Set the 9-day exponential moving average EMA as the stop loss level. EMA responds slower than SMA and can provide a stop loss buffer.
5. Execute transactions based on long and short signals; exit the position when the price falls below the stop loss level to control risks.
This strategy mainly captures short-term price fluctuations through the intersection of the fast-responding SMA and the VWAP that responds to prices in real time. The EMA step-by-step stop loss is used to control risks, and the direction is simple and intuitive.
## Advantage Analysis
1. It is simple and practical to judge short-term trend changes by crossing SMA and VWAP.
2. The EMA stop loss method can provide a certain buffer to avoid being too sensitive.
3. The strategy signals are clear, the rules are simple, and easy to implement.
4. There is a large space for parameter optimization and can be adjusted to different market environments.
5. You can control a single loss by modifying the stop loss method.
6. Easy to expand, other technical indicators or risk control methods can be introduced.
## Risk Analysis
1. SMA and VWAP may have cross-lag or false signals.
2. If the stop loss range is too small, it can easily lead to over-optimization. When placing a firm offer, you need to pay attention to the breakdown of the stop loss.
3. It is only applicable within the short-term range and cannot track the long-term trend.
4. Improper selection of the backtest period may lead to curve fitting.
5. The impact of transaction costs on profitability needs to be considered.
## Optimization direction
1. Test different combinations of SMA and VWAP parameters.
2. Optimize the period parameters of EMA stop loss.
3. Try other types of moving average or indicator stop loss methods.
4. Increase positions and risk management strategies.
5. Introduce machine learning and other algorithms for parameter optimization.
6. Evaluate the effectiveness of regularly adjusting parameters to adapt to market changes.
## Summarize
This SMA and VWAP crossover strategy combines EMA moving stop loss to adapt to short-term fluctuations through parameter adjustment. It is simple to operate and is a typical short-term tracking strategy idea. Adding more indicators or algorithm extensions can improve stability, and can also be integrated into more complex multi-strategy systems as modules. Generally speaking, this strategy is easy to use and implement, and has strong inspirational significance.
|| 

## Overview

This strategy generates trading signals by crossover between Simple Moving Average and Volume Weighted Average Price, and uses Exponential Moving Average as stop loss, belonging to short-term trend following trading strategies.

## Strategy Logic

1. Calculate 5-day Simple Moving Average (SMA) and Volume Weighted Average Price (VWAP).

2. When SMA crosses above VWAP from below, generate long signal; when crossing below from above, generate short signal.

3. SMA is sensitive to price changes and can capture short-term trends. VWAP reflects latest price dynamics. Their crossover identifies short-term trend changes.

4. Set 9-day Exponential Moving Average (EMA) as stop loss. EMA reacts slower than SMA, providing stop loss buffer. 

5. Execute trades on long/short signals. Exit when price drops below stop loss to control risks.

The strategy mainly uses the crossover of the fast-reacting SMA and realtime VWAP to capture short-term price fluctuations, with EMA trailing stop to manage risks, simple and intuitive.

## Advantage Analysis  

1. SMA and VWAP crossover is simple and effective for short-term trend changes.

2. EMA stop loss provides buffer avoiding premature stop out.

3. Clear signals and simple rules, easy to execute.

4. Large optimization space, adjustable to different market environments. 

5. Can modify stop loss mechanism to control single trade loss amount.

6. Easy to expand, can introduce other technical indicators or risk management techniques.

## Risk Analysis

1. SMA and VWAP crossover may have lags or wrong signals.

2. Stop loss range too tight risks over-optimization. Real trading should watch for stop loss breaches.

3. Only applicable for short-term ranges, cannot track long-term trends.

4. Improper backtest period risks curve fitting.

5. Need to consider trading cost impact on profitability.

## Optimization Directions  

1. Test different parameter combinations for SMA and VWAP.

2. Optimize EMA stop loss period parameter.

3. Try other MA types or indicators for stop loss.

4. Add position sizing and risk management strategies.

5. Introduce machine learning algorithms for parameter optimization.

6. Evaluate periodically adjusting parameters to adapt to market changes.

## Summary

This SMA and VWAP crossover strategy with EMA trailing stop can be adjusted for short-term fluctuations via parameters, simple to operate, a typical short-term tracking strategy idea. Adding more indicators or algorithms can improve stability, also usable as a module integrated into more complex multi-strategy systems. Overall an easy to use strategy with great inspirational value for practical trading.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-19 00:00:00
end: 2023-09-18 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © realisticDove62527

//@version=5
strategy("ROoT", overlay=true, margin_long=1, margin_short=1)

longCondition = ta.crossover(ta.sma(close, 5), ta.vwap(hlc3))
if (longCondition)
    strategy.entry("BUY", strategy.long)

shortCondition = ta.crossunder(ta.sma(close, 5), ta.vwap(hlc3))
if (shortCondition)
    strategy.entry("SELL", strategy.short)
    

stoploss = ta.ema(close, 9)


```

> Detail

https://www.fmz.com/strategy/427307

> Last Modified

2023-09-19 21:42:30

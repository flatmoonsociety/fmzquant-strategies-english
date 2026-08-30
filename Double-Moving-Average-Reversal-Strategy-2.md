
> Name

Based on the simple double-moving average reversal strategy Double-Moving-Average-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f09efb4add3baf512a.png)

[trans]

### Overview
This strategy is a trend following and reversal trading strategy based on a simple moving average. It uses the moving average crossover of the 1-day and 4-day lines to determine the trend direction, and then generates buy and sell signals.
### Strategy Principles
When the 1-day line crosses the 4-day line from above, a sell signal is generated; when the 1-day line crosses the 4-day line from below, a buy signal is generated. In this way, the turning point of the market trend can be judged through the intersection of the fast moving average and the slow moving average, and then profits can be made.
Set stop loss and take profit points after entering the market. The stop-loss point is set to 10 points below the entry price, and the take-profit point is set to 100 points above the entry price. This limits losses and locks in profits.
### Advantage Analysis
- Use double moving averages to determine trend reversal points, simple and practical
- Set stop-loss and stop-profit points to limit risks
- Adjustable parameters to adapt to different market conditions
- Easy to understand and implement, suitable for beginners
### Risk Analysis
- Improper moving average parameters may lead to frequent trading or missing good opportunities
- If the stop-loss and stop-profit points are set improperly, the loss may be stopped prematurely or the stop-profit may be insufficient.
- The lag in judging trend turning by double moving averages may lead to losses
- If the parameters are not adjusted as the market environment changes, the effect will become worse.
These risks can be reduced by adjusting moving average parameters, setting up dynamic stop-loss and take-profit mechanisms, or adding other indicator judgments.
### Optimization direction
- You can consider adding MACD, KD and other indicators to verify trading signals and filter out false signals
- You can study the effects of moving averages with different periods
- Trend judgment indicators can be added to avoid counter-trend trading
- You can make the stop loss and take profit move proportionally instead of a fixed value
- Parameters can be dynamically adjusted in combination with volatility indicators
### Summarize
Overall, this strategy is a typical double moving average trading strategy. It uses fast and slow moving average crossovers to determine trend turning points, and sets stop loss and take profit to control risks. It is simple, practical, easy to understand, and suitable for beginners. Through parameter adjustment and optimization, it can adapt to different market environments, and other indicator filters can also be added to improve the effect. Overall, this strategy is very good as an introductory learning strategy.
||


### Overview

This is a trend following and reversal trading strategy based on simple moving averages. It uses the crossover of 1-day and 4-day moving averages to determine the trend direction and generate buy and sell signals.

### Strategy Logic

When the 1-day MA crosses below the 4-day MA, a sell signal is generated. When the 1-day MA crosses above the 4-day MA, a buy signal is generated. By using the crossover of a fast and slow moving average to identify trend reversal points, it aims to profit. 

After entering the market, stop loss and take profit points are set. The stop loss is set 10 points below the entry price. The take profit is set 100 points above the entry price. This can limit losses and lock in profits.

### Advantage Analysis 

- Uses double MAs to identify reversal points simply and practially
- Sets stop loss and take profit to limit risk
- adjustable parameters adaptable to different market conditions
- easy to understand and implement, suitable for beginners

### Risk Analysis

- Invalid MA parameters may cause overtrading or missing opportunities 
- Improper stop loss and take profit setting may cause premature exit
- The lagging of double MAs identifying reversals may cause losses
- Poor performance if parameters are not adjusted per market changes

Risks can be mitigated by tuning parameters, setting dynamic stops, incorporating other indicators for signal validation etc.

### Optimization Directions

- Adding MACD, KD to filter fake signals 
- Studying the effect of different MA periods  
- Adding trend filter to avoid counter-trend trades
- Using proportional stops instead of fixed values
- Dynamically adjusting parameters by volatility

### Summary
This is a typical double MA reversal strategy overall. It identifies reversals by fast and slow MA crossovers, controls risk with stops, simple and practical to understand for beginners. With parameter tuning and optimizations, it can be adaptive and adding filters can improve it further. It is a very good starter strategy to learn.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-19 00:00:00
end: 2023-12-19 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © cesarpieres72

//@version=5
strategy("300% STRATEGY", overlay=true, margin_long=10, margin_short=10)
 
var float lastLongOrderPrice = na
var float lastShortOrderPrice = na

longCondition = ta.crossover(ta.sma(close, 1), ta.sma(close, 4))
if (longCondition)
    strategy.entry("Long Entry", strategy.long)  // Enter long

shortCondition = ta.crossunder(ta.sma(close, 1), ta.sma(close, 4))
if (shortCondition)
    strategy.entry("Short Entry", strategy.short)  // Enter short

if (longCondition)
    lastLongOrderPrice := close

if (shortCondition)
    lastShortOrderPrice := close

// Calculate stop loss and take profit based on the last executed order's price
stopLossLong = lastLongOrderPrice - 170  // 10 USDT lower than the last long order price
takeProfitLong = lastLongOrderPrice + 150  // 100 USDT higher than the last long order price
stopLossShort = lastShortOrderPrice + 170  // 10 USDT higher than the last short order price
takeProfitShort = lastShortOrderPrice - 150  // 100 USDT lower than the last short order price

// Apply stop loss and take profit to long positions
strategy.exit("Long Exit", from_entry="Long Entry", stop=stopLossLong, limit=takeProfitLong)

// Apply stop loss and take profit to short positions
strategy.exit("Short Exit", from_entry="Short Entry", stop=stopLossShort, limit=takeProfitShort) 
```

> Detail

https://www.fmz.com/strategy/435968

> Last Modified

2023-12-20 14:43:41

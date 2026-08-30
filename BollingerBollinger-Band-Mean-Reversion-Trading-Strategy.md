
> Name

Bollinger-Band-Mean-Reversion-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/a66fd058fb1d46430f.png)
[trans]

## Overview
This strategy is a mean reversion trading strategy based on Bollinger Bands. It combines mean reversion trading and risk management mechanisms to capture short-term reversal opportunities in trending markets.
## Strategy Principle
This strategy uses the 20-day Bollinger Bands to identify overextended areas of price. When the price is close to the upper band, go short; when the price is close to the lower band, go long. This allows you to profit when prices reverse.
In addition, the strategy also sets stop loss and take profit levels based on ATR. The stop-loss position is set to the price when the price breaks through the moving average minus 2 times ATR; the stop-profit position is set to the price plus 3 times ATR. This can effectively control the risk of each transaction.
Specifically, the strategy includes the following steps:
1. Calculate the upper track, lower track and moving average of the Bollinger Band on the 20th
2. Calculate the 14-day ATR indicator
3. Go long when the price goes above and below the upper rail; go short when the price goes below the upper rail.
4. When going long, set the stop loss to the price minus 2 times ATR, and the take profit to the price plus 3 times ATR.
5. When selling short, set the stop loss to the price plus 2 times ATR, and the take profit to the price minus 3 times ATR.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Bollinger bands can be used to effectively determine the over-expansion area of ​​price.
2. Combined with mean reversion trading, you can make profits on reversals
3. Set ATR stop loss and take profit to strictly control risks
4. The backtesting effect is good, and profits have been made many times in historical data.
## Risk Analysis
There are also some risks with this strategy:
1. Reverse the risk of failure. Price fluctuations may not follow mean reversion and prices may continue to trend after a reversal signal is issued
2. Risk of stop loss being skipped. Market emergencies may cause prices to gap up, thus skipping pre-set stop loss levels
3. Parameter optimization risks. Under different market conditions, parameter settings need to be adjusted, otherwise it will affect the strategy effect.
Countermeasures:
1. Strictly follow stop loss rules and control single losses
2. Optimize parameters and adjust to current market conditions
3. Use options or other tools to hedge short-gap risks
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Test different moving average systems and find the best parameter combination
2. Add filter conditions, and then trade after the trend is accurately judged.
3. Adjust the multiple of ATR and optimize the range of stop loss and take profit.
4. Add a dynamic exit mechanism related to market structure
This will help further improve the stability and profitability of the strategy.
## Summarize
In general, the Bollinger band mean reversion strategy combines trend judgment and risk control, and is an effective short-term trading strategy. Through continuous optimization and enrichment, it is expected to obtain stable and high-quality excess returns.
||

## Overview

This is a mean reversion trading strategy based on Bollinger Bands. It combines mean reversion trading and risk management mechanisms to capture short-term reversal opportunities in trending markets.  

## Strategy Logic

The strategy uses 20-day Bollinger Bands to identify overextended price areas. It goes short when price nears the upper band and goes long when price nears the lower band, profiting from eventual reversals.

It also sets stop loss and take profit based on ATR. The stop loss is set at price breaking the moving average minus 2 times ATR. Take profit is set at price plus 3 times ATR. This effectively controls the risk per trade.  

Specifically, the strategy includes:

1. Calculate 20-day Bollinger Bands upper band, lower band and moving average  
2. Calculate 14-day ATR
3. Long when price crosses above lower band; Short when price crosses below upper band
4. Set stop loss at price minus 2 times ATR and take profit at price plus 3 times ATR when long
5. Set stop loss at price plus 2 times ATR and take profit at price minus 3 times ATR when short

## Advantage Analysis 

The main advantages are:

1. Bollinger Bands effectively identify overextended price areas
2. Profit from reversals through mean reversion  
3. ATR stops set risk controls  
4. Positive backtest results with multiple profitable trades

## Risk Analysis

Potential risks include:

1. Failed reversal risk if price continues trending 
2. Stop loss skipped risk from price gaps  
3. Parameter optimization required for changing markets

Solutions:

1. Strictly follow stop loss rules to limit loss per trade 
2. Optimize parameters to suit current markets
3. Use options or other tools to hedge gap risk

## Optimization Directions

The strategy can be further optimized by:  

1. Testing different moving averages for best parameters
2. Adding filters to improve trend determination   
3. Adjusting ATR multiples to fine tune stops and limits
4. Incorporating dynamic exit mechanisms based on market regimes

This will further enhance the stability and return profile.  

## Summary

In summary, the Bollinger Band mean reversion strategy with trend filters and risk management has demonstrated positive results. With continuous optimization and enhancements, it holds potential for steady and high-quality excess returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Bollinger Bands Length|
|v_input_2|2|Bollinger Bands Multiplier|
|v_input_3|2|Stop Loss ATR Multiplier|
|v_input_4|3|Take Profit ATR Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-20 00:00:00
end: 2023-08-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Mean Reversion with Risk Management", overlay=true)

// Inputs for Bollinger Bands and Risk Management
length = input(20, minval=1, title="Bollinger Bands Length")
mult = input(2.0, title="Bollinger Bands Multiplier")
stopLossATRMult = input(2.0, title="Stop Loss ATR Multiplier")
takeProfitATRMult = input(3.0, title="Take Profit ATR Multiplier")

// Bollinger Bands Calculation
src = close
basis = sma(src, length)
dev = mult * stdev(src, length)
upper = basis + dev
lower = basis - dev
plot(upper, "Upper Band", color=color.red)
plot(lower, "Lower Band", color=color.green)

// ATR for Stop Loss and Take Profit
atr = atr(14)

// Trading Conditions
longCondition = crossover(src, lower)
shortCondition = crossunder(src, upper)

// Order Execution with Stop Loss and Take Profit
if (longCondition)
    sl = src - stopLossATRMult * atr
    tp = src + takeProfitATRMult * atr
    strategy.entry("Long", strategy.long, stop=sl, limit=tp)

if (shortCondition)
    sl = src + stopLossATRMult * atr
    tp = src - takeProfitATRMult * atr
    strategy.entry("Short", strategy.short, stop=sl, limit=tp)

```

> Detail

https://www.fmz.com/strategy/436790

> Last Modified

2023-12-27 17:18:26

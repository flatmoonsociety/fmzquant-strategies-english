
> Name

Bitcoin-Trading-Strategy-Based-on-Ichimoku-Cloud
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/c28dfb00db82569befd3f43fc6d0b65098441ed749e0bf2fa16702eafa7d7017.png)
[trans]
## Overview
This strategy is a Bitcoin trading strategy designed based on the Ichimoku Balance Sheet indicator. It forms a balance table by calculating the average of the highest and lowest prices in different periods, and generates trading signals when the short-period line crosses the long-period line.
## Strategy Principle
This strategy uses the Ichimoku Balance Sheet indicator, and the specific calculation formula is as follows:
Lmax = the highest price within the period_max period
Smax = the lowest price in period_max period
Lmed = the highest price in period_med period
Smed = the lowest price in period_med period
Lmin = the highest price in the period_min period
Smin = the lowest price in period_min period
HL1 = (Lmax + Smax + Lmed + Smed)/4  

HL2 = (Lmed + Smed + Lmin + Smin)/4

That is, calculate the equilibrium prices of the long-period line HL1 and the short-period line HL2 respectively. When the short-period line HL2 crosses the long-period line HL1 above, go long; when the short-period line HL2 crosses below the long-period line HL1, close the position.
## Advantage Analysis
This strategy has the following advantages:
1. Using the Ichimoku Balance Sheet indicator can effectively filter market noise and identify trends.
2. Using the intersection of different period lines as trading signals can reduce false signals. 
3. The strategy logic is simple and clear, easy to understand and implement.
4. The cycle parameters can be customized to adapt to different market environments.
## Risk Analysis
There are also some risks with this strategy:
1. The Ichimoku Balance Sheet indicator lags behind and may miss short-term signals.
2. When the long and short cycle lines cross, it is easy to be arbitraged.
3. When the market fluctuates violently, the signals sent by the indicators may be unreliable.
These risks can be reduced by properly optimizing cycle parameters or combining them with other indicators.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the parameters of long and short cycles and adapt to market changes.
2. Add a stop loss strategy to control losses.
3. Combine with other indicators such as MACD to improve the accuracy of the signal. 
4. Suspend trading during periods of high volatility to avoid huge losses.
## Summarize
This strategy is based on the Ichimoku Balance Sheet indicator, which generates a trading signal when the short-term line breaks through the long-term line. Compared with a single indicator, it can effectively filter out false signals. Through parameter optimization and risk control, the stability and profitability of the strategy can be further improved.
||

## Overview  

This strategy is a bitcoin trading strategy designed based on the Ichimoku cloud indicator. It generates trading signals when the short-term line crosses over the long-term line by calculating the equilibrium prices over different periods.

## Strategy Logic  

The strategy uses the Ichimoku cloud indicator. The specific formulas are:  

Lmax = highest price over period_max  

Smax = lowest price over period_max

Lmed = highest price over period_med  

Smed = lowest price over period_med   

Lmin = highest price over period_min

Smin = lowest price over period_min

HL1 = (Lmax + Smax + Lmed + Smed)/4   

HL2 = (Lmed + Smed + Lmin + Smin)/4

It calculates the equilibrium prices for the long-term line HL1 and short-term line HL2. A long signal is generated when HL2 crosses over HL1. A close signal is generated when HL2 crosses below HL1.

## Advantage Analysis   

The advantages of this strategy include:

1. Using Ichimoku cloud filters market noise and identifies trends effectively.  
2. Crossover of different period lines generates trading signals and reduces false signals.
3. The logic is simple and easy to understand and implement.  
4. Customizable period parameters adapt to different market environments.

## Risk Analysis   

There are also some risks:   

1. Ichimoku cloud has lagging and may miss short-term signals.  
2. Crossover of long and short term lines can be vulnerable to arbitrage. 
3. Signals may become unreliable during high volatility.  

These risks can be reduced by optimizing parameters or incorporating other indicators.

## Optimization Directions   

The strategy can be optimized in the following aspects:

1. Optimize long and short term periods to adapt to market changes.  
2. Add stop loss to control losses.
3. Incorporate other indicators like MACD to improve accuracy.   
4. Suspend trading at high volatility periods to avoid huge losses.  

## Conclusion  

This strategy generates signals when short-term equilibrium line crosses over long-term line based on Ichimoku cloud. Compared to single indicators, it effectively filters out false signals. Further improvements on parameters and risk control can enhance its stability and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|period_max|
|v_input_2|10|period_med|
|v_input_3|16|period_min|
|v_input_4|2020|v_input_4|
|v_input_5|2025|v_input_5|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-31 00:00:00
end: 2024-01-30 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Alferow

//@version=4
strategy("BTC_ISHIMOKU", overlay=true)

period_max = input(20, minval = 1)
period_med = input(10, minval = 1)
period_min = input(16, minval = 1)

Lmax = highest(high, period_max)
Smax = lowest(low, period_max)

Lmed = highest(high, period_med)
Smed = lowest(low, period_med)

Lmin = highest(high, period_min)
Smin = lowest(low, period_min)

HL1 = (Lmax + Smax + Lmed + Smed)/4
HL2 = (Lmed + Smed + Lmin + Smin)/4

p1 = plot(HL1, color = color.red, linewidth = 2)
p2 = plot(HL2, color = color.green, linewidth = 2)

fill(p1, p2, color = HL1 < HL2 ? color.green : color.red, transp = 90)

start = timestamp(input(2020, minval=1), 01, 01, 00, 00)
finish = timestamp(input(2025, minval=1),01, 01, 00, 00)
trig = time > start and time < finish ? true : false

strategy.entry("Long", true, when = crossover(HL2, HL1) and trig)
// strategy.entry("Short", false, when = crossunder(HL2, HL1) and trig)
strategy.close("Long", when = crossunder(HL2, HL1) and trig)

```

> Detail

https://www.fmz.com/strategy/440510

> Last Modified

2024-01-31 11:06:02

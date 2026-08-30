
> Name

Intelligent-Trailing-Stop-Loss-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/4c4a356d6dc1fb68024034965d8ee3e857927284b12c9cb29ba1b85dd9814cbf.png)
[trans]
## Overview
Intelligent Trailing Stop Loss Strategy is a strategy that automatically adjusts the stop loss point according to price changes. It combines the logic of the SAR indicator. When the price reaches a new high or low, it tracks and adjusts the stop loss line to achieve maximum retracement control.
## Strategy Principle
The core logic of this strategy is to automatically adjust the stop loss line based on the SAR indicator. Specifically, it defines 4 variables:
- EP: extreme point
- SAR: current stop loss point
- AF: step factor, used to control the extent of stop loss line adjustment
- Uptrend sign: Determine whether the current trend is an uptrend or a downtrend
During an upward trend, the stop-loss line will continue to move upward to track the rising price; when the price turns downward, the stop-loss line remains unchanged until it changes to an upward trend again.
The magnitude of the stop loss line adjustment is controlled by the step factor AF. AF will increase when a new stop loss point is successfully set, thereby expanding the scope of the next adjustment.
## Strategic Advantages
The biggest advantage of this strategy is that it can intelligently adjust the stop loss point according to market fluctuations, ensuring sufficient profit margins while minimizing the maximum drawdown. Compared with traditional static stop loss methods, it can better capture price trends.
Specifically, it has the following main advantages:
1. Reduce the maximum retracement: Intelligently adjust the stop loss line to exit before the market reverses and protect the realized profits to the maximum extent.
2. Capture the trend: The stop loss line will be adjusted with new highs or new lows, and can automatically track the price trend.
3. Customizable parameters: Users can customize the step value and starting value of AF according to their own risk preferences, and control the sensitivity of stop loss adjustment.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. Too sensitive: If the step size of AF is adjusted too large or the starting value is too small, the stop loss line will be too sensitive and may be triggered by short-term market noise.
2. Missed opportunities: Stop loss being triggered too early may also lead to profit opportunities after losses continue to rise.
3. Parameter selection: Improper parameter setting will also affect the strategy effect. Parameters need to be adjusted for different markets.
## Optimization direction
This strategy can also be optimized from the following directions:
1. Combined with other indicators: You can pause the stop loss line adjustment when the large cycle indicator sends a signal to avoid premature stop loss before the trend reverses.
2. Added parameter adaptive module: can automatically optimize parameters based on historical data through machine learning algorithms
3. Multi-level stop loss: You can set multiple stop loss lines to track market fluctuations of different magnitudes.
## Summarize
The intelligent trailing stop loss strategy simulates the operating logic of the SAR indicator and adjusts the position of the stop loss line in real time to protect profits while minimizing the possibility of missing opportunities. It maximizes the value of the stop loss function itself.
Compared with the traditional fixed stop-loss strategy, this strategy can better adapt to market changes and is more flexible. Through custom parameter settings, users can choose a stop-loss mode that suits them according to their risk preferences.
Of course, this strategy also has a certain space for parameter optimization, and the improvement effect can be achieved by combining with other indicators. Overall, it finds a smarter balance between stop loss and take profit for investors.
||

## Overview

The Intelligent Trailing Stop Loss Strategy is a strategy that automatically adjusts the stop loss point based on price changes. It combines the logic of the SAR indicator and adjusts the trailing stop loss line when the price reaches new high or low points to achieve maximum drawdown control.

## Strategy Principle 

The core logic of this strategy is to automatically adjust the stop loss line based on the SAR indicator. Specifically, it defines four variables:

- EP: Extreme Point  
- SAR: Current Stop Loss Point
- AF: Step Factor, used to control the adjustment magnitude of stop loss line
- Uptrend Flag: To judge if it is currently an uptrend or a downtrend

During an uptrend, the stop loss line will continue to move up to trail the rising price. When the price turns into a downtrend, the stop loss line remains unchanged until the next uptrend.

The adjustment magnitude of the stop loss line is controlled by the Step Factor AF. AF will increase when a new stop loss point is successfully set, thereby expanding the next adjustment magnitude.

## Advantages

The biggest advantage of this strategy is that it can intelligently adjust the stop loss point according to market fluctuations, while ensuring sufficient profit space and minimizing the maximum drawdown as much as possible. Compared with the traditional static stop loss method, it can better capture the price trend. 

Specifically, there are main advantages:

1. Reduce Maximum Drawdown: Intelligent adjustment of stop loss line can exit before trend reversal to maximize protection of realized profit
2. Capture Trends: The stop loss line will adjust with new highs or lows and automatically trail price trends  
3. Customizable Parameters: Users can customize AF step value and initial value based on their own risk preference to control sensitivity of stop loss adjustments

## Risk Analysis

There are also some risks to note for this strategy:

1. Overly Sensitive: If the AF step adjustment is too large or the initial value is too small, the stop loss line will be too sensitive and may be triggered by short-term market noise
2. Missing Opportunities: Triggering stop loss too early may also result in missing profitable opportunities from continued upside
3. Parameter Selection: Improper parameter settings will also affect strategy performance and needs adjustment for different markets

## Optimization Directions

The strategy can also be optimized in the following aspects:

1. Combine With Other Indicators: Pause stop loss line adjustment when major cycle indicators issue signals to avoid premature stop loss before trend reversal  
2. Add Parameter Self-Adaptive Module: Automatically optimize parameters based on historical data using machine learning algorithms
3. Multi-Level Stop Loss: Set up multiple stop loss lines to trail different magnitudes of market fluctuations

## Conclusion

The Intelligent Trailing Stop Loss Strategy adjusts stop loss line positions in real-time by simulating the operating logic of the SAR indicator. While protecting profits, it also minimizes the possibility of missing opportunities as much as possible. It maximizes the inherent value of the stop loss function itself.

Compared with traditional fixed stop loss strategies, this strategy can better adapt to market changes and is more flexible. Through custom parameter settings, users can choose stop loss modes suitable for their own risk preferences.

Of course, there are also certain parameter optimization spaces for this strategy, and improved effects that can be achieved by combining other indicators. Overall, it finds a more intelligent balance between stop loss and profit taking for investors.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.02|AF_initial|
|v_input_2|0.02|AF_increment|
|v_input_3|0.2|AF_maximum|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-17 00:00:00
end: 2024-01-24 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Lucid SAR Strategy", shorttitle="Lucid SAR Strategy", overlay=true)

// Full credit to Sawcruhteez, Lucid Investment Strategies LLC and Casey Bowman.
// This is a strategy version of the Lucid SAR indicator created by the above-mentioned parties.
// Original version of the indicator: https://www.tradingview.com/script/OkACQQgL-Lucid-SAR/

// Branded under the name "Lucid SAR" 
// As agreed to with Lucid Investment Strategies LLC on July 9, 2019
// https://lucidinvestmentstrategies.com/


// Created by Casey Bowman on July 4, 2019

// MIT License

// Copyright (c) 2019 Casey Bowman

// Permission is hereby granted, free of charge, to any person obtaining a copy
// of this software and associated documentation files (the "Software"), to deal
// in the Software without restriction, including without limitation the rights
// to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
// copies of the Software, and to permit persons to whom the Software is
// furnished to do so, subject to the following conditions:

// The above copyright notice and this permission notice shall be included in all
// copies or substantial portions of the Software.

// THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
// IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
// FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
// AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
// LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
// OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
// SOFTWARE.


AF_initial = input(0.02)
AF_increment = input(0.02)
AF_maximum = input(0.2)


// start with uptrend
uptrend = true
newtrend = false
EP = high
SAR = low
AF = AF_initial

if not na(uptrend[1]) and not na(newtrend[1])
    if uptrend[1]
        EP := max(high, EP[1])
    else
        EP := min(low, EP[1])
    if newtrend[1]
        AF := AF_initial
    else
        if EP != EP[1]
            AF := min(AF_maximum, AF[1] + AF_increment)
        else
            AF := AF[1]
    SAR := SAR[1] + AF * (EP - SAR[1])
    if uptrend[1]
        if newtrend
            SAR := max(high, EP[1])
            EP := min(low, low[1])
        else
            SAR := min(SAR, low[1])
            if not na(low[2])
                SAR := min(SAR, low[2])
            if SAR > low
                uptrend := false
                newtrend := true
                SAR := max(high, EP[1])
                EP := min(low, low[1])
            else
                uptrend := true
                newtrend := false
    else
        if newtrend
            SAR := min(low, EP[1])
            EP := max(high, high[1])
        else
            SAR := max(SAR, high[1])
            if not na(high[2])
                SAR := max(SAR, high[2])
            if SAR < high
                uptrend := true
                newtrend := true
                SAR := min(low, EP[1])
                EP := max(high, high[1])
            else
                uptrend := false
                newtrend := false
            
        

plot(SAR, color = color.blue, style = plot.style_cross, linewidth = 2)

if (uptrend)
    strategy.entry("PBSARLE", strategy.long, comment="PBSARLE")
if (newtrend)
    strategy.entry("PBSARSE", strategy.short, comment="PBSARSE")
```

> Detail

https://www.fmz.com/strategy/439962

> Last Modified

2024-01-25 12:50:12

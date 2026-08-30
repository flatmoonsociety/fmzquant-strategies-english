
> Name

Aggressive-Bottom-Sniping-Quantitative-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/164cac8630574ff3351723860ee073b1c58692dc0a65f7190302754d3aa2d721.png)
[trans]
## Overview
This strategy locates the short-term bottom by judging the outstanding trading volume in the downward trend, and performs buying operations under oversold conditions. It is an active short-term trading strategy.
## Strategy Principle
When the trading volume exceeds 2 times the standard deviation of the average volume based on the SMA, it is considered to be outstanding trading volume, and when the RSI is below 30, it is considered to be an oversold state. When both conditions are met at the same time, it is judged to be a short-term bottom and go long immediately. After going long, the position will be closed and exited after a certain period of time (such as 10 K lines).
So the logic of this strategy only has the following steps:
1. Calculate the trading volume SMA of the last 20 K lines as the base volume
2. Calculate 2 times the standard deviation of the trading volume of the last 20 K lines as the criterion for judging the outstanding volume.
3. Calculate the RSI of the last 20 K lines to determine whether it is oversold.
4. When the trading volume exceeds the benchmark volume + 2 times the standard deviation and the RSI is lower than 30, it is judged to be a short-term bottom.
5. Go long immediately at short-term bottoms
6. Automatically close the position after 10 K lines
## Advantage Analysis
This strategy has the following advantages:
1. Simple logic, easy to understand and optimize
2. Use the characteristics of outstanding trading volume to determine short-term turning points
3. The RSI indicator ensures that you only go long in the oversold zone to avoid chasing the top.
4. Automatic stop loss to maximize the avoidance of tail risks
In general, the strategy makes full use of the characteristics of volume breakthroughs to determine short-term trend reversal, and at the same time strictly controls risks. It is an active long strategy with high reliability.
## Risk Analysis
This strategy mainly involves the following risks:
1. The trading signal composed of trading volume and RSI may have false breakthroughs, leading to wrong long losses;
2. The fixed stop loss time setting may fail to stop the loss or stop the loss too early when the market reverses sharply;
3. Inadequate parameter optimization may result in frequent or too few signals.
In view of the above risks, optimization can be carried out from the following aspects:
1. Add other indicator filters to avoid false breakthrough signals;
2. Set dynamic trailing stop loss instead of fixed Root K line stop loss;
3. Comprehensively test and optimize parameters to ensure they are robust.
## Optimization direction
This strategy can be further optimized from the following aspects:
1. Increase the reliability of the machine learning model’s judgment and avoid false signals
2. Add an adaptive stop loss mechanism instead of a simple fixed K-line setting
3. Cube optimization for protrusion parameters
4. Increase the accuracy of machine learning in screening oversold signals
5. Combined with sentiment analysis to increase the alpha of the strategy
By introducing more advanced technical indicators, machine learning and sentiment analysis, the stability, alpha and Sharpe ratio of the strategy can be significantly improved.
## Summarize
Overall, this strategy is a very simple, direct, and logical short-term breakthrough strategy. By rationally applying trading volume indicators to determine short-term trend reversal points and strictly controlling risks, good results can be achieved. However, there is still a certain risk of false signals and parameter robustness risks. These problems can be gradually improved and optimized by introducing more advanced technologies to make the effect of the strategy more significant.
||

## Overview

This strategy identifies short-term bottoms by detecting outstanding volume in a downtrend, and takes long positions during oversold conditions. It is an aggressive short-term trading strategy.  

## Strategy Principles  

When the volume exceeds 2 standard deviations above the SMA-based average volume, it is considered outstanding volume. Meanwhile, RSI below 30 indicates oversold status. When both conditions are met, it is judged as a short-term bottom and long position is taken immediately. The position will be closed after a certain period of time (e.g. 10 bars).

So the logic of this strategy is simple:  

1. Calculate 20-bar SMA of volume as benchmark  
2. Calculate 2 standard deviation of 20-bar volume as threshold for outstanding volume  
3. Calculate 20-bar RSI to judge oversold status  
4. When volume exceeds benchmark + 2 standard deviation and RSI < 30, judge as short-term bottom
5. Take long position immediately at bottom 
6. Close position after 10 bars automatically  

## Advantage Analysis

The advantages of this strategy include:

1. Simple logic, easy to understand and optimize  
2. Utilize outstanding volume to detect short-term turning points  
3. RSI ensures only taking longs in oversold zone, avoiding chasing tops  
4. Automatic stop loss maximizes risk evasion at bottoms  

In summary, this strategy takes advantage of volume breakouts to catch trend reversals, while strictly controlling risks. It is a reliable aggressive long strategy.

## Risk Analysis  

The main risks of this strategy include:

1. Volume and RSI may generate false breakout signals, causing wrong longs and losses.
2. Fixed stop loss time may fail to stop loss or stop loss too early during significant market reversal. 
3. Suboptimal parameter tuning may lead to too few or too many signals.

To address these risks, optimization can be done in the following aspects:

1. Add other indicators to filter false breakout signals.  
2. Set dynamic trailing stop loss instead of fixed number of bars.
3. Comprehensive parameter testing and tuning to ensure robustness.  

## Optimization Directions

This strategy can be further optimized in the following aspects:

1. Add ML model to judge reliability of volume breakouts to avoid false signals  
2. Add adaptive stop loss mechanism instead of fixed bars
3. Multi-dimensional dataset optimization for outstanding volume parameters   
4. Increase accuracy of oversold signals using ML screening
5. Incorporate sentiment analysis to improve alpha

By introducing more advanced techniques, significant improvement can be achieved on stability, alpha and Sharpe ratio.  

## Conclusion  

In summary, this is a very simple, straightforward and logical short-term breakout strategy. By properly leveraging volume to detect trend reversals, and strictly controlling risks, solid performance can be achieved. But risks of false signals and parameter robustness exist. These can be addressed incrementally by introducing more advanced techniques to further improve the strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Volume SMA Length|
|v_input_2|2|mult|
|v_input_3|20|RSI Length|
|v_input_4|30|Oversold|
|v_input_5|10|Close After|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-10 00:00:00
end: 2024-01-17 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © footlz

//@version=4
strategy("Bottom catch strategy", overlay=true)

v_len = input(20, title="Volume SMA Length")
mult = input(2)
rsi_len = input(20, title="RSI Length")
oversold = input(30, title="Oversold")
close_time = input(10, title="Close After")

v = volume
basis = sma(v, v_len)
dev = mult * stdev(v, v_len)
upper_volume = basis + dev

rsi = rsi(close, rsi_len)

long = v > upper_volume and rsi < oversold

strategy.entry("Long", true, when=long)

passed_time = 0.0
if strategy.position_size != 0
    passed_time := 1
else
    passed_time := 0

if strategy.position_size != 0 and strategy.position_size[1] != 0
    passed_time := passed_time[1] + 1

if passed_time >= close_time
    strategy.close_all()

// If want to enable plot, change overlay=false.
v_color = close >= close[1] ? color.new(#3eb370, 0) : color.new(#e9546b, 0)

// plot(v, title="volume", color=v_color, style=plot.style_columns)
// plot(upper_volume, title="Threshold", color=color.aqua)
```

> Detail

https://www.fmz.com/strategy/439270

> Last Modified

2024-01-18 16:25:33

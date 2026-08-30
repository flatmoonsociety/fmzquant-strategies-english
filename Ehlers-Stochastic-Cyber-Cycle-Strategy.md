
> Name

Ehlers-Stochastic-Cyber-Cycle-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b9580b66201c0a1539.png)

[trans]

## Overview
The Ehlers stochastic cycle strategy is a quantitative trading strategy that uses Ehlers' stochastic cycle indicator to generate trading signals. This strategy combines the advantages of stochastic indicators and cyclical indicators and aims to seize cyclical opportunities in the market.
## Strategy Principle
This strategy first builds a smoothed period indicator, and then builds a stochastic indicator value based on this indicator. Trading signals are generated based on the crossing of the moving average of this stochastic indicator value.
Specifically, the calculation method of the smoothed cycle indicator is:
```
smooth = (src + 2 * src[1] + 2 * src[2] + src[3]) / 6
```

where src is the input price data, such as the closing price. This indicator combines the current price with the prices of the previous 3 time periods to construct a smooth periodic signal.
Based on this smoothed indicator, the stochastic indicator cycle can then be calculated:
```
cycle := (1 - .5 * alpha) * (1 - .5 * alpha) * 
           (smooth - 2 * smooth[1] + smooth[2]) + 
           2 * (1 - alpha) * cycle[1] - 
           (1 - alpha) * (1 - alpha) * cycle[2]
```

The calculation formula includes the second-order difference term of the smoothed periodic signal and the values ​​of the previous two periods. α is the smoothing factor, which adjusts the weight of the old and new period values.
Finally, a random value value1 from 0-100 is calculated based on this cycle indicator. And construct the signal value signal based on the 10-day moving average of value1. A trading signal is issued when the signal's moving average crosses above or below.
## Strategic Advantages
This strategy combines stochastic indicators and periodic indicators, combining the advantages of both. Compared with simple moving average and other trend strategies, this strategy can better capture cyclical opportunities and achieve better results.
The main advantages are:
1. The cycle indicator can identify cycle patterns, and the stochastic indicator provides xFB trading opportunities.
2. Dual indicator design can effectively filter out false signals
3. Customizable parameters to adapt to different market environments
## Strategy Risk
This strategy mainly involves the following risks:
1. Improper parameter settings may lead to frequent transactions, increased transaction fees and slippage costs.
2. Inability to effectively handle markets with violent price fluctuations, which may result in larger losses
3. Periodic indicators are highly dependent on curve fitting, and improper fitting may produce erroneous signals.
Risks can be controlled by optimizing parameter settings, setting stop loss points, and combining other filtering indicators.
## Strategy optimization direction
This strategy can also be optimized from the following directions:
1. Combine with other technical indicators for signal filtering, such as Bollinger Bands, RSI, etc., to reduce false signals
2. Add an adaptive exit mechanism to dynamically adjust the stop loss point according to the degree of market fluctuations
3. Use machine learning methods to automatically optimize parameters so that they can dynamically adapt to the market
4. Optimize capital utilization and enhance capital utilization efficiency through leverage, compound interest and other means
## Summarize
Ehlers' stochastic cycle strategy comprehensively uses the advantages of stochastic indicators and periodic indicators, effectively controls risks through dual signal design, and can obtain better returns in highly cyclical markets. Through further optimization, this strategy can become a recommended quantitative trading strategy.
||

## Overview

The Ehlers Stochastic Cyber Cycle Strategy is a quantitative trading strategy that generates trading signals using Ehlers' stochastic cycle indicator. This strategy combines the advantages of stochastic indicators and cycle indicators, aiming to capture cyclical opportunities in the market.  

## Strategy Logic  

This strategy first constructs a smoothed cycle indicator, then builds a stochastic indicator value based on that indicator. The generation of trading signals is determined by the crossover of the moving average line of this stochastic indicator value.

Specifically, the smoothed cycle indicator is calculated as:  

```
smooth = (src + 2 * src[1] + 2 * src[2] + src[3]) / 6
```

Where src is the input price data, such as closing price. This indicator combines the current price and the prices of the previous 3 time periods to construct a smoothed cycle signal.  

Based on this smoothed indicator, the stochastic cycle cycle can then be calculated:  

```
cycle := (1 - .5 * alpha) * (1 - .5 * alpha) *  
           (smooth - 2 * smooth[1] + smooth[2]) +  
           2 * (1 - alpha) * cycle[1] -  
           (1 - alpha) * (1 - alpha) * cycle[2]
```

This calculation formula contains the second order difference of the smoothed periodic signal, and the values of the previous two cycles. α is a smoothing factor that adjusts the weight of new and old cycle values.

Finally, a 0-100 random value value1 is calculated based on this cycle indicator. And the signal value signal is constructed based on the 10-day moving average of value1. Trading signals are issued when the moving average line of signal crosses up or down.  

## Advantages of the Strategy  

This strategy combines stochastic indicators and cycle indicators to integrate the advantages of both. Compared to simple trend strategies such as moving averages, this strategy can better capture cyclical opportunities and thus achieve better results.

The main advantages are:

1. Cycle indicators can identify cyclic patterns, stochastic indicators provide trading opportunities  
2. Dual indicator design can effectively filter false signals  
3. Customizable parameters suit different market environments

## Risks of the Strategy

The main risks of this strategy are:  

1. Improper parameter settings may lead to frequent trading, increasing trading costs and slippage costs  
2. Cannot effectively handle markets with violent price fluctuations, which may lead to large losses  
3. Cycle indicators rely heavily on curve fitting, improper fitting may generate wrong signals  

Risks can be controlled by optimizing parameter settings, setting stop loss points, combining other filtering indicators, etc.  

## Optimization Directions  

This strategy can also be optimized in the following aspects:  

1. Combine with other technical indicators for signal filtering, such as Bollinger Bands, RSI, etc., to reduce false signals  
2. Add adaptive exit mechanisms, dynamically adjust stop loss points according to market volatility  
3. Use machine learning methods to automatically optimize parameters to dynamically adapt to the market  
4. Optimize capital utilization through leverage, compounding and other means  

## Conclusion  

The Ehlers Stochastic Cyber Cycle Strategy integrates the advantages of stochastic and cycle indicators through dual signal design to effectively control risks, and can achieve good returns in markets with strong cyclicality. With further optimization, this strategy can become a worthwhile quantitative trading strategy to recommend.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_hl2|0|Source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_2|0.07|Alpha|
|v_input_3|9|Lag|
|v_input_4|8|Stochastic len|
|v_input_5|true|oppositeTrade|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-09 00:00:00
end: 2024-01-16 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Ehlers Stochastic Cyber Cycle Strategy",overlay=false, default_qty_type = strategy.percent_of_equity, default_qty_value = 100.0, pyramiding = 1, commission_type = strategy.commission.percent, commission_value = 0.1)
src = input(hl2, title = "Source") 
alpha = input(.07, title = "Alpha")
lag = input(9, title = "Lag")
smooth = (src + 2 * src[1] + 2 * src[2] + src[3]) / 6
len = input(8, title = "Stochastic len")
cycle = na
if na(cycle[7])
    cycle := (src - 2 * src[1] + src[2]) / 4
else
    cycle := (1 - .5 * alpha) * (1 - .5 * alpha) * (smooth - 2 * smooth[1] + smooth[2]) + 2 * (1 - alpha) * cycle[1] - (1 - alpha) * (1 - alpha) * cycle[2]

value1 = stoch(cycle, cycle, cycle, len) / 100
value2 = 2 * ((4 * value1 + 3 * value1[1] + 2 * value1[2] + value1[3]) / 10 - 0.5)

signal = value2
oppositeTrade = input(true)
barsSinceEntry = 0
barsSinceEntry := nz(barsSinceEntry[1]) + 1
if strategy.position_size == 0
    barsSinceEntry := 0
if (crossover(signal, signal[1]) and not oppositeTrade) or (oppositeTrade and crossunder(signal, signal[1]))
    strategy.entry("Long", strategy.long)
    barsSinceEntry := 0
if (crossunder(signal, signal[1]) and not oppositeTrade) or (oppositeTrade and crossover(signal, signal[1]))
    strategy.entry("Short", strategy.short)
    barsSinceEntry := 0
if strategy.openprofit < 0 and barsSinceEntry > 8
    strategy.close_all()
    barsSinceEntry := 0
    
    
plot(0, title="ZeroLine", color=gray) 
plotSrc = signal
cyclePlot = plot(plotSrc, title = "CyberCycle", color = blue)
triggerPlot = plot(plotSrc[1], title = "Trigger", color = green)
fill(cyclePlot, triggerPlot, color = plotSrc < plotSrc[1] ? red : lime, transp = 50)
```

> Detail

https://www.fmz.com/strategy/439084

> Last Modified

2024-01-17 16:03:30

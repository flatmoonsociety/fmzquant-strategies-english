
> Name

Peak-to-Peak-Pattern-Based-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/8926b2ec34d9421aa662c652aba459c8e3c05cd38114938ba2fcbcb20777cd60.png)
[trans]
## Overview
The name of this strategy is "Trading strategy based on peak-peak pattern", which mainly uses the peak-peak pattern of K-line to determine the timing of buying and selling. This strategy belongs to the technical analysis strategy.
## Strategy Principle
This strategy determines the peak-to-peak shape of the K-line graph by defining the rising peak (upFractal) and falling peak (downFractal).
Specifically, the judgment logic of the rising peak is: the high point of the current K line is the highest point of the last n K lines, and the high points of subsequent K lines will not exceed the high point of the current K line.
The judgment logic of the falling peak is: the low point of the current K line is the lowest point of the last n K lines, and the low point of the subsequent K line is not lower than the low point of the current K line.
Here, Boolean variables and loops are used to determine the relationship between the high and low points of the first n and last n K-lines and the current K-line, and finally determine the rising peak and falling peak.
Therefore, the core logic of this strategy is:
1. Determine the rising peak value and falling peak value
2. Go long when the peak rises and go short when the peak falls.
## Advantage Analysis
This strategy has the following advantages:
1. The peak shape is easy to identify and the operation is simple
2. Utilize technical forms and not be affected by fundamentals
3. The retracement may be relatively small
## Risk Analysis
There are also some risks with this strategy:
1. Inaccurate judgment of peak-to-peak patterns may result in missing the best entry opportunity
2. When the market changes drastically, it may be difficult to determine the stop loss.
3. Rely only on form and ignore other factors
Countermeasures:
1. Adjust the parameters of the peak shape and optimize the judgment logic
2. Combine with other indicators to determine stop loss position
3. Use in combination with fundamental analysis or other strategies
## Optimization direction
This strategy can also be optimized from the following directions:
1. Increase parameter adjustment space and optimize peak morphology judgment
2. Add stop loss logic
3. Consider other indicators such as trading volume or volatility
4. Combine analysis with different time periods
## Summarize
This strategy is simple and easy to operate based on the principle of peak-peak morphology, and the retracement may be small. However, there are certain risks and it needs to be used in combination with other analysis methods to achieve maximum effect. The next step will be to improve judgment accuracy, stop loss, indicator optimization, etc.
||

## Overview

The strategy is named "Peak-to-Peak Pattern Based Trading Strategy". It mainly uses the peak-to-peak pattern in candlestick charts to determine entries and exits. This is a technical analysis based strategy.   

## Strategy Principle  

The strategy defines rising peak (upFractal) and falling peak (downFractal) to identify the peak-to-peak pattern in candlestick charts.   

Specifically, the judgment logic for rising peak is: the high of current candlestick is the highest of recent n candlesticks, and the high of subsequent candlesticks does not exceed the current one.

The judgment logic for falling peak is: the low of current candlestick is the lowest of recent n candlesticks, and the low of subsequent candlesticks does not break below the current one.

Boolean variables and loops are used here to determine the relationship between previous n and later n candlesticks' high/low and that of the current one, and eventually identify rising and falling peaks.   

Therefore, the core logic of this strategy is:  

1. Identify rising peaks and falling peaks  
2. Long on rising peaks and short on falling peaks

## Advantage Analysis   

The advantages of this strategy include:

1. Peak-to-peak pattern is easy to identify, simple to operate  
2. Based on technical pattern, not affected by fundamentals
3. Possible smaller drawdowns

## Risk Analysis  

There are also some risks with this strategy:   

1. Inaccurate peak-to-peak pattern judgment, may miss best entry timing
2. Hard to set stop loss when market moves violently  
3. Only relies on pattern, ignores other factors  

Counter measures:

1. Adjust parameters of peak-to-peak pattern to optimize the logic
2. Combine with other indicators to determine stop loss position  
3. Use together with fundamental or other analysis

## Optimization Directions   

Some directions to optimize the strategy:

1. Increase parameter tuning options to better identify peak-to-peak patterns
2. Add stop loss logic  
3. Consider trading volume, volatility and other indicators
4. Combine different timeframe analysis  

## Summary

This strategy is simple to operate with possibly smaller drawdowns based on the peak-to-peak pattern principle. But still has some risks and needs to be combined with other analysis methods to maximize its performance. Next step is to improve on accuracy of pattern judgment, stop loss, indicator optimizations etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|2|Periods|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("sanju parmar", shorttitle="sanju trading empire", overlay=true)

// Define "n" as the number of periods and keep a minimum value of 2 for error handling.
n = input.int(title="Periods", defval=2, minval=2)

// UpFractal
bool upflagDownFrontier = true
bool upflagUpFrontier0 = true
bool upflagUpFrontier1 = true
bool upflagUpFrontier2 = true
bool upflagUpFrontier3 = true
bool upflagUpFrontier4 = true

for i = 1 to n
    upflagDownFrontier := upflagDownFrontier and (high[n-i] < high[n])
    upflagUpFrontier0 := upflagUpFrontier0 and (high[n+i] < high[n])
    upflagUpFrontier1 := upflagUpFrontier1 and (high[n+1] <= high[n] and high[n+i + 1] < high[n])
    upflagUpFrontier2 := upflagUpFrontier2 and (high[n+1] <= high[n] and high[n+2] <= high[n] and high[n+i + 2] < high[n])
    upflagUpFrontier3 := upflagUpFrontier3 and (high[n+1] <= high[n] and high[n+2] <= high[n] and high[n+3] <= high[n] and high[n+i + 3] < high[n])
    upflagUpFrontier4 := upflagUpFrontier4 and (high[n+1] <= high[n] and high[n+2] <= high[n] and high[n+3] <= high[n] and high[n+4] <= high[n] and high[n+i + 4] < high[n])
flagUpFrontier = upflagUpFrontier0 or upflagUpFrontier1 or upflagUpFrontier2 or upflagUpFrontier3 or upflagUpFrontier4

upFractal = (upflagDownFrontier and flagUpFrontier)


// downFractal
bool downflagDownFrontier = true
bool downflagUpFrontier0 = true
bool downflagUpFrontier1 = true
bool downflagUpFrontier2 = true
bool downflagUpFrontier3 = true
bool downflagUpFrontier4 = true

for i = 1 to n
    downflagDownFrontier := downflagDownFrontier and (low[n-i] > low[n])
    downflagUpFrontier0 := downflagUpFrontier0 and (low[n+i] > low[n])
    downflagUpFrontier1 := downflagUpFrontier1 and (low[n+1] >= low[n] and low[n+i + 1] > low[n])
    downflagUpFrontier2 := downflagUpFrontier2 and (low[n+1] >= low[n] and low[n+2] >= low[n] and low[n+i + 2] > low[n])
    downflagUpFrontier3 := downflagUpFrontier3 and (low[n+1] >= low[n] and low[n+2] >= low[n] and low[n+3] >= low[n] and low[n+i + 3] > low[n])
    downflagUpFrontier4 := downflagUpFrontier4 and (low[n+1] >= low[n] and low[n+2] >= low[n] and low[n+3] >= low[n] and low[n+4] >= low[n] and low[n+i + 4] > low[n])
flagDownFrontier = downflagUpFrontier0 or downflagUpFrontier1 or downflagUpFrontier2 or downflagUpFrontier3 or downflagUpFrontier4

downFractal = (downflagDownFrontier and flagDownFrontier)

plotshape(downFractal, style=shape.triangleup, location=location.belowbar, offset=-n, color=#18f523, size = size.small)
plotshape(upFractal, style=shape.triangledown, location=location.abovebar, offset=-n, color=#cf3d11, size = size.small)

// Strategy Conditions
longCondition = upFractal
shortCondition = downFractal

// Strategy Entry and Exit
if (longCondition)
    strategy.entry("Buy", strategy.long)
if (shortCondition)
    strategy.entry("Sell", strategy.short)

```

> Detail

https://www.fmz.com/strategy/442255

> Last Modified

2024-02-20 15:40:58

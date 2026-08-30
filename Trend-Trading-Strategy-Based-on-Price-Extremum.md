
> Name

Trend-Trading-Strategy-Based-on-Price-Extremum
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ca8a4a8d1fe2d34118.png)

[trans]

## Overview
This strategy forms an upper and lower track by calculating the maximum and minimum price points within a certain period, and determines whether the current price is above the upper track or below the lower track, and then carries out long or short positions. The strategy mainly determines the trend of prices and trades when the trend strengthens.
## Strategy Principle
The core indicator of this strategy is to calculate the maximum and minimum price points within a certain period. The specific calculation method is:
Upper track: Scan the K lines within the period from left to right to find a maximum high point, and then determine whether the first K line on the left to the leftmost end and the right to the last K line are all lower than the maximum high point. If so, confirm that this point is the apex of the interval.
Lower track: Scan the K lines within the period from left to right, find a minimum low point, and then determine whether the first K line on the left to the leftmost end and the right to the last K line are all higher than the minimum low point. If so, confirm that point as the low point of the interval.
By repeating this calculation, you can get the upper and lower price rails within a certain period. Go long when the price goes above the upper track, and go short when it goes below the lower track. This forms a trading strategy that determines trend based on price extreme points.
## Advantage Analysis
This strategy's way of judging the trend is relatively primitive and direct. It uses price extremes to judge the part where the trend is increasing, which can effectively filter out shock scenarios and avoid trading in shocks. The location where strategic trading signals are generated is more advantageous and easy to form trend following. In addition, the way the strategy takes signals is relatively strict, which can reduce false signals.
## Risk Analysis
This strategy is relatively strict in signal acquisition and may miss more trading opportunities. In addition, the extreme points require a certain amount of time to accumulate and form, which will lag behind, and the parameters need to be appropriately optimized. When parameters are inappropriate, error signals are likely to be generated.
The strictness of extreme point judgment can be appropriately reduced and a certain degree of fluctuation can be allowed, which can reduce the risk of misjudgment. In addition, it can be combined with other indicators for confirmation to avoid false signals.
## Optimization direction
The strategy's judgment of the period of the upper and lower rails can be appropriately optimized so that it can better capture the trend. In addition, the scanning interval when judging extreme points can also be adjusted.
In order to reduce the possibility of missing trading opportunities, the judgment conditions for extreme points can be appropriately relaxed and a certain range of fluctuations allowed.
You can try to confirm by combining other indicators, such as energy indicators, moving averages, etc., to avoid the risk of false signals caused by the judgment of a single indicator.

## Summarize
This strategy is relatively direct and effective in judging price trend characteristics through price extreme points. It can effectively filter shocks and determine the timing of trend enhancement, thereby conducting trend trading. The advantage of the strategy is that the signal is generated in a good position and can chase the trend. The disadvantage is that the signal may be lagging behind, making it difficult to catch the turning point. Through the optimization of parameters and conditions, this strategy can become a more reliable trend judgment tool.
||

## Overview

This strategy calculates the maximum and minimum price points over a certain period to form upper and lower bands. When the current price breaks through the upper or lower band, long or short positions are taken. The strategy mainly judges the trend of prices and trades when the trend strengthens.

## Strategy Logic

The core indicator of this strategy is to calculate the maximum and minimum price points over a period. The specific calculation methods are:

Upper Band: Scan the K-line in the period from left to right to find a maximum high point, and then determine whether the 1st K-line on its left to the utmost left and the 1st K-line on its right to the utmost right are both lower than this maximum high point. If so, this point is confirmed as the top of the range.

Lower Band: Scan the K-line in the period from left to right to find a minimum low point, and then determine whether the 1st K-line on its left to the utmost left and the 1st K-line on its right to the utmost right are both higher than this minimum low point. If so, this point is confirmed as the bottom of the range.

By repeating this calculation, the upper and lower bands of prices over a period can be obtained. Take long positions when prices break through the upper band and take short positions when prices break through the lower band. This forms a trend trading strategy based on determining trend by price extremum points.


## Advantage Analysis

The way this strategy judges the trend is quite straightforward by determining the strengthening part of the trend through price extremum points, which can effectively filter out consolidation scenarios and avoid trading in consolidations. The signal generation position of the strategy has advantages and can easily form trend tracking. In addition, the strategy takes signals in a relatively strict way, which can reduce erroneous signals.

## Risk Analysis  

The strategy takes signals quite strictly, which may miss more trading opportunities. In addition, extremum points need some time to accumulate and form, which will be relatively lagging. The parameters need proper optimization. When the parameters are improper, erroneous signals are also very likely to occur.

The strictness of judging the extremum points can be moderately reduced to allow some fluctuations to reduce the risk of misjudgment. In addition, confirmation can be made with other indicators to avoid wrong signals.

## Optimization Directions

The cycle for determining the upper and lower bands can be properly optimized to better capture the trend. In addition, the scanning range for judging extremum points can also be adjusted.

To reduce the possibility of missing trading opportunities, the conditions for determining extremum points can be moderately loosened to allow some fluctuation.

Attempts can be made to confirm with other indicators such as volume indicators, moving averages, etc. to avoid the risk of wrong signals resulting from single indicator judgment.

## Conclusion  

The way this strategy judges trend characteristics by price extremum points is quite straightforward and effective. It can effectively filter out consolidation and determine the strengthening time of trends for trend trading. The advantage of the strategy lies in good signal generation position to chase trends. The shortcoming is that the signals may have some lag and it is difficult to capture turns. Through the optimization of parameters and conditions, this strategy can become a relatively reliable trend judging tool.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Pattern|
|v_input_2|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-05 00:00:00
end: 2023-12-11 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 19/02/2018
//  Stock market moves in a highly chaotic way, but at a larger scale, the movements 
// follow a certain pattern that can be applied to shorter or longer periods of time 
// and we can use Fractal Chaos Bands Indicator to identify those patterns. Basically, 
// the Fractal Chaos Bands Indicator helps us to identify whether the stock market is 
// trending or not. When a market is trending, the bands will have a slope and if market 
// is not trending the bands will flatten out. As the slope of the bands decreases, it 
// signifies that the market is choppy, insecure and variable. As the graph becomes more 
// and more abrupt, be it going up or down, the significance is that the market becomes 
// trendy, or stable. Fractal Chaos Bands Indicator is used similarly to other bands-indicator 
// (Bollinger bands for instance), offering trading opportunities when price moves above or 
// under the fractal lines.
//
// The FCB indicator looks back in time depending on the number of time periods trader selected 
// to plot the indicator. The upper fractal line is made by plotting stock price highs and the 
// lower fractal line is made by plotting stock price lows. Essentially, the Fractal Chaos Bands 
// show an overall panorama of the price movement, as they filter out the insignificant fluctuations 
// of the stock price.
//
// You can change long to short in the Input Settings
// WARNING:
//  - For purpose educate only
//  - This script to change bars colors.
////////////////////////////////////////////////////////////
fractalUp(pattern) =>
    p = high[pattern+1]
    okl = 1
    okr = 1
	for i = pattern to 1
		okl := iff(high[i] < high[i+1] and okl == 1 , 1, 0)
	for i = pattern+2 to pattern*2+1
		okr := iff(high[i] < high[i-1] and okr == 1, 1, 0)
	res = iff(okl == 1 and okr == 1, p, res[1])
    res

fractalDn(pattern) =>
    p = low[pattern+1]
    okl = 1
    okr = 1
	for i = pattern to 1
		okl := iff(low[i] > low[i+1] and okl == 1 , 1, 0)
	for i = pattern+2 to pattern*2+1
		okr := iff(low[i] > low[i-1] and okr == 1, 1, 0)
	res = iff(okl == 1 and okr == 1, p, res[1])
    res

strategy(title="Fractal Chaos Bands", overlay = true)
Pattern = input(1, minval=1)
reverse = input(false, title="Trade reverse")
xUpper = fractalUp(Pattern)
xLower = fractalDn(Pattern)
pos = iff(close > xUpper, 1,
       iff(close < xLower, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )  
plot(xUpper, color=red, title="FCBUp")
plot(xLower, color=green, title="FCBDn")
```

> Detail

https://www.fmz.com/strategy/435123

> Last Modified

2023-12-12 14:36:14


> Name

Quantitative-Trading-Strategy-Based-on-Trend-Analysis-Index Quantitative-Trading-Strategy-Based-on-Trend-Analysis-Index
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fe39b0418efb31439d.png)
[trans]

## Overview
The core idea of ​​this strategy is to use the slope of the moving average to determine the market trend and construct a Trend Analysis Index (TAI) as a trading signal. When the price is moving in a trend, the slope of the moving average increases; when the price fluctuates within a range without a clear trend, the slope of the moving average decreases. An increase in the trend analysis index indicates the entry of a trend, and a decrease in the trend analysis index indicates the end of the trend.
## Strategy Principle
The strategy starts by calculating a simple moving average of the price (X-day moving average). Then calculate the highest and lowest values ​​of the moving average in the past Y days, and calculate the fluctuation range of the moving average in the past Y days through these two extrema values. Finally, by comparing the Y-day fluctuation range with the price, it is converted into a standardized indicator between 0 and 1, that is, the trend analysis index is constructed. Go long when the index is above a certain threshold and go short when it is below a certain threshold.
## Advantage Analysis
This strategy has the following advantages:
1. Determine the trend operation through the slope of the moving average, which can effectively capture the medium and long-term trend.
2. Combined with the standardization of fluctuation range, construct index indicators to make trading signals clearer
3. The moving average parameters and trend judgment parameters can be customized to adapt to different market environments.
4. Optional reverse trading, which can be used to track or hedge other strategies
## Risk Analysis
This strategy also has certain risks:
1. In the shock and consolidation, it is easy to generate false signals
2. Improper setting of moving average parameters may miss the trend transition point
3. Improper setting of normalization parameters may miss weaker trends
4. When trading in the opposite direction, losses may increase
Corresponding solutions:
1. Filter signals in combination with other indicators
2. Optimize parameters and find the best parameter combination
3. Adjust the upper and lower thresholds of the normalized parameters
4. Use the reverse trading function with caution
## Optimization direction
This strategy can be optimized from the following aspects:
1. Combine with other indicators to determine trends, such as BOLL channels, etc., to make trading signals more reliable
2. Add a stop-loss strategy to control single losses
3. Optimize the daily parameters of the moving average to make it more consistent with the market characteristics of different cycles.
4. Train the optimal standardized parameters and find the optimal parameter thresholds
5. Add machine learning model to predict trend probability and assist trading
## Summarize
Generally speaking, this strategy is a medium- and long-term strategy that determines the trend through the slope of the moving average. It can effectively capture the trend, but there is also a certain risk of false signals. By combining it with other indicators, adding stop loss, parameter optimization and other means, the strategy can be made more robust and reliable. In essence, it is still a relatively simple trend following strategy.
||

## Overview

The core idea of this strategy is to use the slope of moving average to judge market trend and construct a Trend Analysis Index (TAI) as trading signal. When price is trending, the slope of moving average increases. When price is ranging in a trendless zone, the slope of moving average decreases. The increase of Trend Analysis Index indicates the start of a trend while the decrease means the end of the trend.

## Strategy Logic

The strategy first calculates the Simple Moving Average (X-day MA) of price. Then it computes the highest and lowest value of this moving average in the last Y days to get the fluctuation range. Finally, by comparing this Y-day range with price, it converts to a standardized indicator between 0-1, namely the Trend Analysis Index. Taking long position when index is above a threshold and short position when below another threshold.

## Advantage Analysis  

The advantages of this strategy are:

1. Effectively catching mid- to long-term trends by judging slope of MA  
2. Constructing standardized index for clearer trading signal
3. Customizable MA and trend judgment parameters for different market environments 
4. Choosable reverse trading for tracking or hedging other strategies

## Risk Analysis

There are also some risks:

1. Prone to wrong signals during range-bound market
2. Missing trend reversal points if MA parameters set inappropriately
3. Missing weak trends if standardization parameters set inappropriately 
4. Increased loss on reverse trading 

Solutions:

1. Filter signals with other indicators
2. Optimize parameters to find best combination
3. Adjust threshold of standardization parameters
4. Carefully use reverse trading 

## Optimization Directions

The strategy can be optimized in following aspects:

1. Combine other indicators like BOLL to make signals more reliable
2. Add stop loss to control single loss
3. Optimize MA days to fit characteristics in different timeframes 
4. Train optimal threshold parameters  
5. Add ML model for trend probability to assist trading

## Conclusion

In summary, this is a mid- to long-term trend following strategy based on the slope of moving average. It can effectively capture trends but also has some false signal risks. By combining with other indicators, adding stop loss, parameter optimization etc, the strategy can be more robust. Essentially it is still a simple trend tracking strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|28|AvgLen|
|v_input_2|5|TAILen|
|v_input_3|0.11|TopBand|
|v_input_4|0.02|LowBand|
|v_input_5|false|Trade reverse|


> Source (PineScript)

``` pinescript
//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 21/12/2017
// In essence, it is simply the standard deviation of the last x bars of a 
// y-bar moving average. Thus, the TAI is a simple trend indicator when prices 
// trend with authority, the slope of the moving average increases, and when 
// prices meander in a trendless range, the slope of the moving average decreases.
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Trend Analysis Index", shorttitle="TAI")
AvgLen = input(28, minval=1)
TAILen = input(5, minval=1)
TopBand = input(0.11, step=0.01)
LowBand = input(0.02, step=0.01)
reverse = input(false, title="Trade reverse")
hline(TopBand, color=red, linestyle=line)
hline(LowBand, color=green, linestyle=line)
xPrice = close
xSMA = sma(xPrice, AvgLen)
xHH = highest(xSMA, TAILen)
xLL = lowest(xSMA, TAILen)
nRes = (xHH - xLL) * 100 / xPrice
pos = iff(nRes > TopBand, 1,
       iff(nRes < LowBand, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(nRes, color=blue, title="TAI")

```

> Detail

https://www.fmz.com/strategy/435084

> Last Modified

2023-12-12 10:40:52

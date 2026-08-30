
> Name

Short-term-Trading-Strategy-Based-on-Momentum-Indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b176d126530061f913.png)
[trans]
## Overview
The name of this strategy is "Short-term trading strategy based on momentum indicators". This strategy uses the momentum indicator Mass Index to identify turning points in market trends to capture short-term trading opportunities.
## Strategy Principle
This strategy uses two sets of exponential moving averages EMA with different parameters to smooth the difference between the highest price and the lowest price of the price to obtain the indicator Mass Index. Go short when the Mass Index crosses a certain threshold; go long when the Mass Index falls below a certain threshold.
Specifically, first calculate the difference xPrice between the highest price and the lowest price. Then calculate the 9-period and 25-period EMAs of xPrice, named xEMA and xSmoothXAvg respectively. Then calculate the sum of the ratios of these two EMAs to get the Mass Index. When the Mass Index is greater than a certain threshold, go short, and when it is less than a certain threshold, go long.
This strategy uses the upper and lower breakthroughs of the Mass Index to determine the trend turning point for short-term trading. When market volatility intensifies, the Mass Index will rise; when market volatility weakens, the Mass Index will fall. Monitoring its breakout of a certain level can effectively capture short-term trading opportunities.
## Strategic Advantages
This strategy has the following advantages:
1. Use the momentum indicator Mass Index to effectively identify short-term fluctuations and trend turns.
2. Position the timing of buying and selling more accurately to avoid chasing highs and selling lows.
3. Trading strategies and parameters are simple, clear and easy to implement
4. Parameters can be flexibly adjusted to suit different market environments
## Strategic risks and solutions
There are also some risks with this strategy:
1. False breakthroughs may occur, leading to unnecessary transactions. Parameters can be adjusted appropriately to reduce the false alarm rate.
2. Failure to consider long-term trend judgment may deviate from the main trend. Trend indicators can be combined to avoid counter-trend operations.  
3. Risks of data curve fitting. The sample interval can be appropriately expanded to test the robustness of the parameters.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Combine with stock fundamental analysis to avoid trading low-quality stocks with excessive fluctuations
2. Add a stop-loss mechanism and strictly control single losses
3. Combine with volatility indicators to reduce position size when market volatility intensifies
4. Add conditional order function to optimize entry and exit timings
## Summarize
This strategy designs a relatively simple short-term trading strategy based on the Mass Index indicator, which can effectively identify the turning point of the market, thereby accurately doing long and short positions. The trading strategy and parameter settings of this strategy are simple and intuitive, easy to implement, and can be adjusted and optimized according to different market environments, making it highly practical. However, we should also pay attention to the risks of data overfitting and indicator failure, and we need to combine trend judgment and stop-loss measures to deal with market uncertainty.
||

## Overview

The strategy is named "Short-term Trading Strategy Based on Momentum Indicator". It utilizes the momentum indicator Mass Index to identify turning points in market trends and capture short-term trading opportunities.

## Strategy Logic

The strategy uses two exponential moving averages (EMA) with different parameters to smooth the difference between the highest and lowest prices and obtains the Mass Index indicator. It goes short when the Mass Index crosses above a threshold and goes long when crossing below a threshold. 

Specifically, it first calculates the difference between the highest and lowest prices xPrice. Then it calculates the 9-period and 25-period EMA of xPrice, named xEMA and xSmoothXAvg respectively. After that, it sums the ratios of these two EMAs to get the Mass Index. When the Mass Index is greater than a threshold, it goes short. When less than a threshold, it goes long.

The strategy identifies trend reversal points by the crossover of Mass Index and thus conducts short-term trading. As market volatility intensifies, Mass Index will rise. As market volatility subsides, Mass Index will fall. Monitoring its breakthrough of certain level can effectively capture short-term trading opportunities.


## Advantages

The strategy has the following advantages:

1. Using momentum indicator Mass Index can effectively identify fluctuations and turning points in the short term
2. Relatively accurate in positioning entry and exit points, avoiding chasing tops and bottoms
3. Simple and clear trading strategy and parameters, easy to implement 
4. Flexible parameter adjustment for different market environments

## Risks and Solutions

There are also some risks with this strategy:

1. False breakouts may occur, resulting in unnecessary trades. Fine tuning parameters could reduce false signals.
2. Long term trends are not considered, which may conflict with the main trend. Combine with trend indicators to avoid counter-trend trades.
3. Curve fitting risk. Expand sample periods reasonably to test robustness of parameters.

## Optimization Directions 

The strategy can be optimized in the following aspects:

1. Combine with fundamental analysis to avoid trading highly volatile low quality stocks
2. Add stop loss mechanisms to strictly control single loss
3. Combine with volatility indicators to reduce position sizing when market volatility rises  
4. Add conditional orders to optimize entry and exit timing

## Conclusion  

This strategy designs a simple short-term trading strategy based on the Mass Index indicator, which can effectively identify turning points in the market for precise long and short trades. The trading strategy and parameter settings are simple and intuitive, easy to implement, and adjustable for different market environments, making it highly practical. But risks of overfitting and failure of indicators should also be noticed. Trend analysis and stop loss should be combined to cope with market uncertainty.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Length1|
|v_input_2|25|Length2|
|v_input_3|26.5|Trigger|
|v_input_4|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-20 00:00:00
end: 2024-02-26 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 12/09/2017
// The Mass Index was designed to identify trend reversals by measuring 
// the narrowing and widening of the range between the high and low prices. 
// As this range widens, the Mass Index increases; as the range narrows 
// the Mass Index decreases.
// The Mass Index was developed by Donald Dorsey. 
//
// You can change long to short in the Input Settings
// WARNING:
//   - For purpose educate only
//   - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="MASS Index", shorttitle="MASS Index")
Length1 = input(9, minval=1)
Length2 = input(25, minval=1)
Trigger = input(26.5, step = 0.01)
reverse = input(false, title="Trade reverse")
hline(27, color=blue, linestyle=line, title = "Setup")
hline(Trigger, color=red, linestyle=line, title = "Trigger")
xPrice = high - low
xEMA = ema(xPrice, Length1)
xSmoothXAvg = ema(xEMA, Length1)
nRes = sum(iff(xSmoothXAvg != 0, xEMA / xSmoothXAvg, 0), Length2)
pos = iff(nRes > Trigger, -1,
	   iff(nRes < Trigger, 1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )  
plot(nRes, color=red, title="MASS Index")
```

> Detail

https://www.fmz.com/strategy/442924

> Last Modified

2024-02-27 14:07:09


> Name

Dynamic-Momentum-Oscillator-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/5b24ea6c2d232440136484557b34aa9bce54f3d83910c542859773a649b35136.png)

[trans]

## Overview
The Dynamic Momentum Oscillator Trading Strategy is based on the Dynamo indicator proposed by E. Marshall Wall in an article published in "Futures" magazine in July 1996. It normalizes the standard oscillator to eliminate the influence of the trend.
## Strategy Principle
This strategy first calculates a Stochastic Oscillator with a length of 10 days, then calculates the 10-day simple moving average of the index, and then calculates the 20-day moving average based on this moving average. This forms the basis for the calculation of the dynamic momentum oscillator.
Strategy then calculated the highest and lowest values ​​of the index, and then calculated the middle value. It takes the difference between the 20-day moving average and the original index, and then subtracts this difference from the middle value to form the normalized oscillator value. Go long when the normalized value is above 77 and go short when it is below 23.
## Advantage Analysis
The main advantages of this strategy are:
1. Use the dynamic momentum oscillator indicator to eliminate the influence of the trend, making trading signals more reliable.
2. Combined with overbought and oversold areas, more accurate trading signals can be generated at reversal points.
3. The rules are simple, clear and easy to implement.
## Risk Analysis
The main risks of this strategy are:
1. When the market crashes, the probability of indicators sending out wrong signals will be greater. Stop losses can be set to control risk.
2. In a volatile market, false signals will frequently occur. Parameters can be adjusted appropriately to filter out some noise.
3. The frequency of transactions may be high, and transaction costs will have a certain impact on profits.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test data from different markets to find the best contract and optimal parameter combination.
2. Add filtering conditions to judge the strength of the trend before sending a signal to avoid being trapped in volatile market conditions.
3. Add a stop loss mechanism. When the price breaks through a certain threshold in an adverse direction, choose stop loss and exit.
4. Based on this strategy, more complex trading systems can be developed and combined with multiple other indicators to make decisions.
## Summarize
The dynamic momentum oscillator trading strategy sends more accurate trading signals in overbought and oversold areas by eliminating the influence of trends. This strategy is simple and easy to implement, but it also has certain risks. Through parameter and rule optimization, system stability and profitability can be further improved.
||

## Overview

The Dynamic Momentum Oscillator Trading Strategy is based on the Dynamo indicator proposed by E. Marshall Wall in an article published in Futures magazine in July 1996. It normalizes a standard oscillator to eliminate the impact of trends.

## Strategy Logic

The strategy first calculates a 10-day Stochastic Oscillator, then calculates its 10-day simple moving average, and further calculates a 20-day moving average based on that. This forms the foundation for the Dynamo calculation.

The strategy then calculates the highest and lowest values of the oscillator and computes the midpoint. It takes the difference between the 20-day average and the original oscillator and subtracts that difference from the midpoint to form a normalized oscillator value. It goes long when this normalized value is above 77 and goes short when it's below 23.

## Advantage Analysis 

The main advantages of this strategy are:

1. By utilizing the Dynamo indicator, it eliminates the impact of trends and generates more reliable trading signals. 

2. By combining overbought/oversold areas, it can produce relatively accurate signals at turning points.

3. The rules are simple and clear, easy to implement.

## Risk Analysis

The main risks of this strategy are:

1. At market shocks, the probability of wrong signals from the indicator will be higher. Stop loss can be used to control the risk.

2. In oscillating markets, frequent false signals may occur. Parameters can be adjusted to filter out some noise. 

3. High trading frequency may lead to considerable trading costs that eat into profits.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Test data from different markets to find the optimal contract and parameter combinations.

2. Add filters to judge the strength of the trend before signals to avoid being trapped in oscillating markets. 

3. Incorporate stop loss mechanisms. Exit trades when prices breach certain thresholds in unfavorable directions.

4. Develop more complex trading systems based on this strategy by combining signals from multiple other indicators.

## Summary

The Dynamic Momentum Oscillator Trading Strategy generates relatively accurate trading signals by eliminating trend impact and using overbought/oversold areas. The strategy is simple and easy to implement but also has some risks. Further improvements to stability and profitability can be achieved by optimizing parameters and rules.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|OscLen|
|v_input_2|20|MALen|
|v_input_3|77|HiBand|
|v_input_4|23|LowBand|
|v_input_5|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-15 00:00:00
end: 2024-01-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 10/04/2017
// In July 1996 Futures magazine, E. Marshall Wall introduces the 
// Dynamic Momentum Oscillator (Dynamo). Please refer to this article 
// for interpretation.
// The Dynamo oscillator is a normalizing function which adjusts the 
// values of a standard oscillator for trendiness by taking the difference 
// between the value of the oscillator and a moving average of the oscillator 
// and then subtracting that value from the oscillator midpoint.
//
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading
////////////////////////////////////////////////////////////
strategy(title="Dynamo", shorttitle="Dynamo")
OscLen = input(10, minval=1)
MALen = input(20, minval=1)
HiBand = input(77, minval=1)
LowBand = input(23)
reverse = input(false, title="Trade reverse")
hline(HiBand, color=red, linestyle=line)
hline(LowBand, color=green, linestyle=line)
xOscK = stoch(close, high, low, OscLen)
xOscAvg = sma(xOscK, OscLen)
xMAVal = sma(xOscAvg, MALen)
maxNum = 9999999
LowestSoFar = iff(xOscAvg < nz(LowestSoFar[1], maxNum), xOscAvg, nz(LowestSoFar[1], maxNum))
HighestSoFar = iff(xOscAvg > nz(HighestSoFar[1]), xOscAvg, nz(HighestSoFar[1]))
MidPnt = (LowestSoFar + HighestSoFar) / 2
nRes = MidPnt - (xMAVal - xOscAvg)
pos = iff(nRes > HiBand, 1,
	     iff(nRes < LowBand, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
plot(nRes, color=blue, title="Dynamo")
```

> Detail

https://www.fmz.com/strategy/439649

> Last Modified

2024-01-22 17:28:39

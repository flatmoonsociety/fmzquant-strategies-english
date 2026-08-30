
> Name

Statistical-Volatility-Backtest-Strategy-Based-on-Extreme-Value-Method
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/d9d4643aa10dd85481fb0851ac20ba74b847cb4fb2a7312d7119adc02044872d.png)
[trans]

### Overview
This strategy uses the extreme value method to calculate statistical volatility, also known as historical volatility. It calculates the statistical volatility based on the extreme values ​​of the highest price, lowest price, and closing price, combined with time factors. This volatility reflects the volatility of an asset's price. The strategy will make corresponding long or short trades when volatility is above or below a set threshold.
### Strategy Principles
1. Calculate the extreme values of the highest price, lowest price, and closing price within a certain period of time
2. Apply the extreme value method formula to calculate the statistical volatility   
```
   SqrTime = sqrt(253 / Length)  
   Vol = ((0.6 * log(xMaxC / xMinC) * SqrTime) + (0.6 * log(xMaxH / xMinL) * SqrTime)) * 0.5
   
```
3. Compare the volatility with the set upper and lower thresholds to generate trading signals   
```
   pos = iff(nRes > TopBand, 1, 
             iff(nRes < LowBand, -1, nz(pos[1], 0)))
   
```
4. Go long or short based on trading signals
### Advantage Analysis
The main advantages of this strategy are:
1. Using statistical volatility indicators can effectively capture market hot spots and reversal opportunities.
2. The extreme value method calculates volatility, which is not sensitive to extreme prices, and the results are more stable and reliable.
3. You can adjust parameters to adapt to transactions in different volatility environments
### Risk Analysis
This strategy mainly involves the following risks:
1. Statistical volatility itself has a certain lag and cannot accurately grasp market turning points.
2. The volatility indicator responds slowly to emergencies and may miss short-term trading opportunities.
3. There is a certain risk of wrong transactions and stop loss risks
Countermeasures and solutions:
1. Appropriately shorten the statistical period and increase sensitivity to market changes
2. Combine with other indicators as auxiliary to improve the accuracy of the signal
3. Set a stop loss point to control single loss
### Optimization direction
Optimization direction of this strategy:
1. Test different statistical period parameters and find the optimal parameters
2. Add a position management module to adjust positions according to volatility
3. Combine with indicators such as moving averages and set filter conditions to reduce mistaken transactions.
### Summarize
This strategy uses the extreme value method to calculate statistical volatility and generates trading signals by capturing changes in volatility. Compared with indicators such as simple moving averages, it can better reflect market volatility and capture reversals. At the same time, the extreme value method algorithm also makes the results more stable and reliable. Through parameter adjustment and optimization, this strategy can be adapted to different market conditions, and its trading ideas and statistical volatility indicators are worthy of further research and application.
||

### Overview

This strategy uses the extreme value method to calculate the statistical volatility, also known as historical volatility. It measures the volatility based on the extreme values of highest price, lowest price and close price, combined with the time factor. The volatility reflects the fluctuation of the asset price. The strategy will make corresponding long or short trades when the volatility is higher or lower than the threshold.  

### Strategy Principle

1. Calculate the extreme values of highest price, lowest price and close price in a certain time period
2. Apply the extreme value method formula to calculate the statistical volatility
   
```
   SqrTime = sqrt(253 / Length)
   Vol = ((0.6 * log(xMaxC / xMinC) * SqrTime) + (0.6 * log(xMaxH / xMinL) * SqrTime)) * 0.5
   
```
3. Compare the volatility with the upper and lower thresholds to generate trading signals
   
```
   pos = iff(nRes > TopBand, 1,  
             iff(nRes < LowBand, -1, nz(pos[1], 0)))
   ``` 
4. Make long or short trades based on the trading signals

### Advantage Analysis 

The main advantages of this strategy are:

1. Using the statistical volatility indicator can effectively capture market hotspots and reversal opportunities  
2. The extreme value method for calculating volatility is not sensitive to extreme prices, resulting in more stable and reliable results
3. Parameters can be adjusted to adapt to trading in different volatility environments

### Risk Analysis

The main risks of this strategy are:

1. The statistical volatility itself has some lag, and cannot accurately grasp market turning points
2. The volatility indicator reacts slowly to sudden events, possibly missing short-term trading opportunities  
3. There are some risks of wrong trades and stop loss

Countermeasures and solutions:

1. Appropriately shorten the statistical cycle to increase sensitivity to market changes
2. Use other indicators as an aid to improve signal accuracy 
3. Set stop loss points to control single loss

### Optimization Directions

The optimization directions for this strategy:

1. Test different statistical period parameters to find the optimal parameters
2. Add a position management module to adjust positions based on volatility
3. Add filter conditions like moving average lines to reduce wrong trades

### Summary  

This strategy uses the extreme value method to calculate statistical volatility, and generates trading signals by capturing volatility anomalies. Compared to simple indicators like moving average lines, it better reflects market volatility and captures reversals. Meanwhile, the extreme value method algorithm also makes the results more stable and reliable. Through parameter adjustment and optimization, this strategy can adapt to different market conditions, and its trading logic and statistical volatility indicator are worth further research and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|30|Length|
|v_input_2|0.005|TopBand|
|v_input_3|0.0016|LowBand|
|v_input_4|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-19 00:00:00
end: 2023-12-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 22/11/2014
// This indicator used to calculate the statistical volatility, sometime 
// called historical volatility, based on the Extreme Value Method.
// Please use this link to get more information about Volatility. 
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Statistical Volatility - Extreme Value Method ", shorttitle="Statistical Volatility Backtest")
Length = input(30, minval=1)
TopBand = input(0.005, step=0.001)
LowBand = input(0.0016, step=0.001)
reverse = input(false, title="Trade reverse")
hline(TopBand, color=red, linestyle=line)
hline(LowBand, color=green, linestyle=line)
xMaxC = highest(close, Length)
xMaxH = highest(high, Length)
xMinC = lowest(close, Length)
xMinL = lowest(low, Length)
SqrTime = sqrt(253 / Length)
Vol = ((0.6 * log(xMaxC / xMinC) * SqrTime) + (0.6 * log(xMaxH / xMinL) * SqrTime)) * 0.5
nRes = iff(Vol < 0,  0, iff(Vol > 2.99, 2.99, Vol))
pos = iff(nRes > TopBand, 1,
	   iff(nRes < LowBand, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )  
plot(nRes, color=blue, title="Statistical Volatility")

```

> Detail

https://www.fmz.com/strategy/436598

> Last Modified

2023-12-26 10:24:53

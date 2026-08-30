
> Name

Polarized-Fractal-Efficiency-PFE-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/d552e0373cec4fa25b.png)
 [trans]

### Overview
The Polarized Fractal Efficiency (PFE) trading strategy measures the efficiency of price movement by applying the concepts of fractal geometry and chaos theory. The more linear and efficient the price movement is, the shorter the distance between two points and the higher the efficiency of the price movement.
### Strategy Principles
The core indicator of the PFE trading strategy is Polarized Fractal Efficiency (PFE). The indicator is calculated based on the following formula:
```
PFE = sqrt(pow(close - close[Length], 2) + 100)
```

Among them, Length is the lookback window period, and this parameter is set through input. PFE actually measures the "length" of price movement during the Length period, which is approximated using Euclidean distance (straight-line distance).
In order to evaluate the efficiency of price movements, we need a benchmark for comparison. This benchmark is the length of the path formed by connecting prices in actual order during the Length period, which is called C2C (Close to Close). The calculation formula is as follows:
```
C2C = sum(sqrt(pow((close - close[1]), 2) + 1), Length)  
```

In this way, we can calculate the fractal efficiency xFracEff of the price movement:
```
xFracEff = iff(close - close[Length] > 0, round((PFE / C2C) * 100) , round(-(PFE / C2C) * 100))
```

If the price rises, the score is positive, if it falls, it is negative. The larger the absolute value, the less efficient the movement.
To generate trading signals, we calculate xEMA, the exponential moving average of xFracEff. And set the buying and selling channels:
```
xEMA = ema(xFracEff, LengthEMA) 

BuyBand = input(50)  
SellBand = input(-50)
```

When xEMA crosses above the BuyBand, a buy signal is generated; when xEMA crosses below the SellBand, a sell signal is generated.
### Advantage Analysis
The PFE trading strategy has the following advantages:
1. Apply unique fractal geometry and chaos theory methods to measure price movement efficiency from another angle
2. Avoid some problems with conventional technical indicators, such as curve fitting
3. You can find settings suitable for different market environments by adjusting parameters
4. The trading rules are simple, clear and easy to implement
### Risk Analysis
PFE trading strategies also have the following risks:
1. Like all indicator strategies, parameter optimization is difficult and easy to over-optimize.
2. When the market fluctuates violently, buy and sell signals may be unreliable
3. Extreme values need to be handled with caution, such as a sudden gap in the price
4. It needs to endure a certain time lag, and the best entry point may have been missed when the signal is generated.
### Optimization direction
PFE trading strategies can be optimized from the following aspects:
1. Try different combinations of Length parameters to find the best balance point
2. Optimize buying and selling channel parameters to reduce the probability of wrong transactions
3. Add a stop-loss mechanism to control single losses
4. Combine with other indicators to improve signal quality
5. Dynamically adjust parameters to adapt to changes in the market environment
### Summarize
PFE trading strategy is based on the perspective of fractal geometry and chaos theory, and proposes a novel method to measure the efficiency of price movement. Compared with conventional technical indicators, this method has its unique advantages, but it also faces a certain degree of time lag, parameter optimization, and signal quality problems. Through continuous testing and optimization, the PFE strategy is expected to become a reliable quantitative trading strategy choice.

|| 

### Overview  

The Polarized Fractal Efficiency (PFE) trading strategy measures the efficiency of price movements by applying concepts from fractal geometry and chaos theory. The more linear and efficient the price movement, the shorter the distance prices travel between two points, and the higher the efficiency.
  
### Strategy Logic

The core indicator of PFE trading strategy is Polarized Fractal Efficiency (PFE). It is calculated based on the following formula:  

```
PFE = sqrt(pow(close - close[Length], 2) + 100)
```

Where Length is the lookback window, adjustable through input parameters. PFE essentially measures the "length" of price movement over the Length period, using Euclidean distance (straight-line distance) as an approximation.

 To evaluate the efficiency of price movement, we need a benchmark for comparison. This benchmark is the length of the path connecting prices over Length period according to the actual sequence, called C2C (Close to Close), and is calculated as:

```
C2C = sum(sqrt(pow((close - close[1]), 2) + 1), Length)
```

Thus we can calculate fractal efficiency of price movement xFracEff:  

``` 
xFracEff = iff(close - close[Length] > 0, round((PFE / C2C) * 100) , round(-(PFE / C2C) * 100))
```

Positive value when price rises and negative value when price falls. The larger the absolute number, the less efficient the movement.  

To generate trading signals, we calculate the exponential moving average of xFracEff, called xEMA. Buy and sell bands are defined:   

```
xEMA = ema(xFracEff, LengthEMA)

BuyBand = input(50)
SellBand = input(-50)  
```

When xEMA crosses above BuyBand, it generates buy signal. When crossing below SellBand, it generates sell signal.


### Advantage Analysis   

The PFE trading strategy has the following advantages:

1. Applies unique concepts from fractal geometry and chaos theory to measure price movement efficiency from a different angle  
2. Avoids some problems of conventional technical indicators like curve fitting
3. Parameters can be adjusted to find suitable settings for different market environments  
4. Simple and clear trading rules, easy to implement
   
### Risk Analysis

The PFE trading strategy also has the following risks:   

1. Difficult parameter optimization, prone to overfitting like all indicator strategies  
2. Unreliable signals during extreme market turbulence
3. Need to cautiously handle extremes like price gaps  
4. Bear some time lag, may have missed best entry point when signal triggers  

### Optimization Directions  

The PFE strategy can be optimized from the following aspects:  

1. Try different combinations of Length parameter to find optimal balance   
2. Optimize buy and sell bands to reduce erroneous trades  
3. Add stop loss to control single trade loss size
4. Combine other indicators to improve signal quality   
5. Dynamically adjust parameters to adapt to changing market environments

### Summary   

The PFE trading strategy proposes a novel approach based on fractal geometry and chaos theory concepts to measure the efficiency of price movements. Compared to conventional technical indicators, this method has its unique advantages but also faces problems like time lag, parameter optimization, signal quality to some extent. With continuous testing and optimization, PFE strategy shows promise to become a reliable quantitative trading strategy choice.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Length|
|v_input_2|5|LengthEMA|
|v_input_3|50|BuyBand|
|v_input_4|-50|SellBand|
|v_input_5|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-07 00:00:00
end: 2024-01-14 00:00:00
period: 3m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 29/09/2017
// The Polarized Fractal Efficiency (PFE) indicator measures the efficiency 
// of price movements by drawing on concepts from fractal geometry and chaos 
// theory. The more linear and efficient the price movement, the shorter the 
// distance the prices must travel between two points and thus the more efficient 
// the price movement.
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="PFE (Polarized Fractal Efficiency)", shorttitle="PFE (Polarized Fractal Efficiency)")
Length = input(9, minval=1)
LengthEMA = input(5, minval=1)
BuyBand = input(50, step = 0.1)
SellBand = input(-50, step = 0.1)
reverse = input(false, title="Trade reverse")
hline(BuyBand, color=green, linestyle=line, title = "TopBand")
hline(SellBand, color=red, linestyle=line, title = "LowBand")
PFE = sqrt(pow(close - close[Length], 2) + 100)
C2C = sum(sqrt(pow((close - close[1]), 2) + 1), Length)
xFracEff = iff(close - close[Length] > 0,  round((PFE / C2C) * 100) , round(-(PFE / C2C) * 100))
xEMA = ema(xFracEff, LengthEMA)
pos = iff(xEMA < SellBand, -1,
	   iff(xEMA > BuyBand, 1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(xEMA, color=blue, title="PFE")
```

> Detail

https://www.fmz.com/strategy/438792

> Last Modified

2024-01-15 14:01:25

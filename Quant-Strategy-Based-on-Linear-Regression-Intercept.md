
> Name

Quant-Strategy-Based-on-Linear-Regression-Intercept based on linear regression intercept point
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/7c501e0247b46b487f3b0f509e8078c35b1140b226fbc83ae70d9b0f904f9381.png)
[trans]

## Overview
This strategy uses linear regression technology to calculate the linear regression intercept point and uses it as a buy and sell signal to construct a quantitative trading strategy. This strategy generates trading signals by analyzing stock price time series, fitting a linear regression trend line, and using linear regression intercept points to determine whether the price is overvalued or undervalued.
## Strategy Principle
The linear regression intercept point represents the predicted value of the Y value (usually price) when the time series X value is 0. This strategy pre-sets the parameter Length, uses the closing price as the source sequence, and calculates the linear regression intercept point (xLRI) of the recent Length day. When the closing price is higher than xLRI, go long; when the closing price is lower than xLRI, go short.
The specific calculation formula is as follows:
```
xX = Length *(Length - 1)* 0.5  
xDivisor = xX *xX - Length* Length *(Length - 1) *(2 * Length - 1) / 6
xXY = Σ(i *收盘价[i]),i从0到Length-1  
xSlope = (Length *xXY - xX* Σ(收盘价, Length))/ xDivisor
xLRI = (Σ(收盘价, Length) - xSlope * xX) / Length
```
Through such calculation, the linear regression intercept point xLRI of the nearest Length day can be obtained. The strategy uses it to determine the price level and generate trading signals.
## Strategic Advantages
This strategy has the following advantages:
1. Using linear regression technology, it has a certain ability to predict prices and judge trends.
2. There are fewer parameters, the model is simple, and it is easy to understand and implement.
3. The parameter Length adaptive can be customized to adjust the strategy flexibility.
## Risks and Solutions
This strategy also has some risks:
1. Linear regression fitting is only a statistical fitting based on historical data, and its ability to predict future price trends is limited.
2. If the company's fundamentals change significantly, the results of linear regression fitting may be invalid.
3. Improper setting of parameter Length may lead to overfitting.
Countermeasures:
1. Appropriately shorten the parameter Length to prevent overfitting.
2. Pay attention to changes in the company's fundamentals and manually intervene to close positions when necessary.
3. Adopt the adaptive parameter Length and dynamically adjust it according to market conditions.
## Strategy optimization direction
This strategy can also be optimized from the following aspects:
1. Add a stop-loss mechanism to control single losses.
2. Combine with other indicators to form a combination strategy to improve stability.
3. Add a parameter adaptive optimization module to allow the Length parameter to change dynamically.
4. Add a position control module to prevent excessive trading.
## Summarize
This strategy builds a simple quantitative trading strategy based on linear regression interception points. Overall, this strategy has certain economic value, but there are also some risks that need to be noted. Through continuous optimization, it is expected to further improve the stability and profitability of the strategy.
||

## Overview

This strategy uses linear regression techniques to calculate the linear regression intercept and uses it as a trading signal to construct a quantitative trading strategy. By analyzing the price time series of stocks, this strategy fits a linear regression trend line and uses the linear regression intercept to judge whether prices are overestimated or underestimated, thereby generating trading signals.

## Strategy Principle  

The linear regression intercept indicates the predicted value of Y (usually the price) when the time series value X is 0. This strategy presets the parameter Length, takes the closing price as the source sequence, and calculates the linear regression intercept (xLRI) of the most recent Length days. When the closing price is higher than xLRI, go long; when the closing price is lower than xLRI, go short.

The specific calculation formula is as follows:
```
xX = Length *(Length - 1)* 0.5
xDivisor = xX *xX - Length* Length *(Length - 1) *(2 * Length - 1) / 6  
xXY = Σ(i *Closing Price[i]), i from 0 to Length-1
xSlope = (Length *xXY - xX* Σ(Closing Price, Length))/ xDivisor 
xLRI = (Σ(Closing Price, Length) - xSlope * xX) / Length
```
Through such calculations, the linear regression intercept xLRI for the most recent Length days can be obtained. The strategy judges the price highs and lows based on it to generate trading signals.

## Advantages

This strategy has the following advantages:

1. Using linear regression techniques, it has certain predictive and trend judgment capabilities for prices.
2. Fewer parameters, simpler model, easy to understand and implement.  
3. Customizable parameter Length to adjust strategy flexibility.

## Risks and Solutions

This strategy also has some risks:

1. Linear regression fitting is merely a statistical fitting based on historical data, with limited ability to predict future price trends.  
2. If the company's fundamentals undergo major changes, the results of linear regression fitting may become invalid.
3. Improper setting of the parameter Length may lead to overfitting.

Countermeasures:  

1. Appropriately shorten the parameter Length to prevent overfitting.
2. Pay attention to changes in the company's fundamentals and intervene manually to close positions when necessary.
3. Adopt adaptive parameter Length to dynamically adjust according to market conditions.

## Optimization Directions

This strategy can also be optimized in the following aspects:  

1. Add a stop loss mechanism to control single loss.
2. Combine with other indicators to form a combination strategy to improve stability. 
3. Add parameter self-adaptive optimization module to make Length parameter change dynamically.
4. Add a position control module to prevent over-trading.   

## Summary  

This strategy constructs a simple quantitative trading strategy based on the linear regression intercept. Overall, the strategy has some economic value, but there are also some risks to note. Through continuous optimization, it is expected to further improve the stability and profitability of the strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-28 00:00:00
end: 2023-12-28 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 21/03/2018
// Linear Regression Intercept is one of the indicators calculated by using the 
// Linear Regression technique. Linear regression indicates the value of the Y 
// (generally the price) when the value of X (the time series) is 0. Linear 
// Regression Intercept is used along with the Linear Regression Slope to create 
// the Linear Regression Line. The Linear Regression Intercept along with the Slope 
// creates the Regression line.
//
// You can change long to short in the Input Settings
// WARNING:
//  - For purpose educate only
//  - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Line Regression Intercept Backtest", overlay = true)
Length = input(14, minval=1)
xSeria = input(title="Source", defval=close)
reverse = input(false, title="Trade reverse")
xX = Length * (Length - 1) * 0.5
xDivisor = xX * xX - Length * Length * (Length - 1) * (2 * Length - 1) / 6
xXY = 0
for i = 0 to Length-1
	xXY := xXY + (i * xSeria[i])
xSlope = (Length * xXY - xX * sum(xSeria, Length)) / xDivisor
xLRI = (sum(xSeria, Length) - xSlope * xX) / Length
pos = iff(close > xLRI, 1,
       iff(close < xLRI, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(xLRI, color=blue, title="LRI")
```

> Detail

https://www.fmz.com/strategy/436997

> Last Modified

2023-12-29 11:45:20

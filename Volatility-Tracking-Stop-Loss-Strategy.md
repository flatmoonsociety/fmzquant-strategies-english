
> Name

Volatility-Tracking-Stop-Loss-Strategy based on price volatility
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy reflects the volatility of the market by calculating the moving average of the true fluctuation range, and determines the trend direction based on the relationship between the volatility and its moving average. When volatility crosses above the moving average, go short and when it crosses below, go long, and set a trailing stop.
### Strategy Principles
Use the ATR function to calculate the true fluctuation range within the specified period. A simple moving average of ATR is then calculated as a moving average of volatility. When ATR crosses its moving average, it is believed that market volatility has increased, and a bearish strategy is adopted; when ATR crosses below its moving average, it is believed that market volatility has decreased, and a bullish strategy is adopted.
When holding a position, a fixed proportion of the trailing stop loss position will be set, and the stop loss position will be dynamically adjusted according to price changes to prevent the stop loss from being trapped while protecting profits.
### Advantage Analysis
This strategy uses volatility indicators to determine market trends and avoid being misled by noise. When volatility rises, it is bearish and when volatility falls, it is bullish, thus achieving hedging operations. Trailing stop loss can adjust the stop loss position according to real-time price changes, which can protect profits while reducing unnecessary stop losses.
### Risk Analysis
This strategy is based on only one volatility indicator and there is some lag. Moreover, trailing stop loss only considers price changes in the unfavorable direction and cannot prevent profit taking. When prices fluctuate violently, the stop loss line may be breached, resulting in large losses.
The period parameters of ATR and moving average can be appropriately optimized, and other indicators can also be added for comprehensive judgment. The stop loss method can also be changed to dynamic stop loss, and the stop loss range can be adjusted according to the degree of market fluctuations.
### Optimization direction
1. Test different ATR and moving average cycle parameter combinations to find the optimal parameters.
2. Add other indicator judgments to form a strategy combination and improve the accuracy of the strategy.
3. Set up a dynamic stop loss strategy and adjust the stop loss range according to the degree of market fluctuations.
4. Optimize the fund management strategy, and different position sizes can be set for different varieties.
5. Apply machine learning technology to assist in determining the turning point of market volatility.
6. Combine with high-level moving average indicators to identify larger-level trend directions.
### Summarize
This strategy uses volatility indicators to judge market trends, which is relatively simple and direct, but relying on a single indicator is easily limited. Properly introducing multiple indicators to judge and optimize parameters can improve the stability of the strategy. Overall, this strategy provides an idea for trading based on market volatility.
||

### Overview

This strategy calculates the moving average of true range to reflect market volatility. It determines the trend direction based on the relationship between volatility and its moving average. It goes short when volatility crosses above the moving average, and goes long when crossing below, with a trailing stop loss.

### Strategy Logic

The ATR function is used to calculate the true range over a specified period. The simple moving average of ATR is then calculated as the moving average line of volatility. When ATR crosses above its moving average, market volatility is considered as increasing and a short strategy is adopted. When ATR crosses below its moving average, market volatility is considered as decreasing and a long strategy is adopted.

When in a position, a fixed percentage trailing stop loss is set to adjust the stop loss dynamically based on price changes, in order to protect profits while avoiding being stopped out prematurely. 

### Advantage Analysis

This strategy judges market trends via the volatility indicator, avoiding noise interference. It goes short when volatility rises and goes long when volatility falls, realizing hedged operations. The trailing stop loss adjusts stop loss positions according to real-time price changes, balancing profit protection and unnecessary stop loss.

### Risk Analysis

The strategy relies solely on one volatility indicator, with some lagging. The trailing stop loss only considers adverse price moves, unable to prevent profit retracements. If prices fluctuate violently, the stop loss may be hit, incurring large losses.

Parameter tuning on ATR and moving average periods could help, as could incorporating other indicators for comprehensive judgements. The stop loss method could also switch to dynamic stops, adjusting stop loss percentage based on market volatility.

### Optimization Directions

1. Test different parameter combinations of ATR and moving averages to find optimal parameters.

2. Incorporate other indicators for judgement to form a strategy ensemble, improving accuracy.

3. Adopt dynamic stop loss strategies, adjusting stop loss percentage based on market volatility. 

4. Optimize position sizing models for different products.

5. Apply machine learning to aid in identifying volatility turning points.

6. Combine with higher timeframe moving averages to determine larger trend direction.

### Summary

The strategy judges market trends simply and directly via volatility, but a single indicator has limitations. Introducing multiple indicators and parameter optimization can improve robustness. Overall, the strategy provides a volatility-based trading idea.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Length|
|v_input_2|26|LengthMA|
|v_input_3|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-20 00:00:00
end: 2023-09-19 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 20/08/2018
// The Volatility function measures the market volatility by plotting a 
// smoothed average of the True Range. It returns an average of the TrueRange 
// over a specific number of bars, giving higher weight to the TrueRange of 
// the most recent bar.
//
// You can change long to short in the Input Settings
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
strategy(title="Volatility Backtest", shorttitle="Volatility")
Length = input(10, minval=1)
LengthMA = input(26, minval=1)
reverse = input(false, title="Trade reverse")
xATR = atr(Length)
nRes = ((Length - 1) * nz(nRes[1], 0) + xATR) / Length
xMARes = sma(nRes, LengthMA)
pos = iff(nRes < xMARes, 1,
       iff(nRes > xMARes, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue ) 
plot(nRes, color=blue, title="Volatility")
plot(xMARes, color=red, title="MA")
```

> Detail

https://www.fmz.com/strategy/427346

> Last Modified

2023-09-20 11:31:12

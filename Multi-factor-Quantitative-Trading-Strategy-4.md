
> Name

Multi-factor reversal quantitative trading strategyMulti-factor-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1001827e928503709c0.png)
[trans]

## Overview
This strategy combines the 123 reversal strategy and the psychological line strategy to form a multi-factor quantitative trading strategy. This strategy comprehensively considers multiple dimensions such as technical form and market psychology, and can make more accurate decisions when judging market trends.
## Principle
### 123 Reversal Strategy
The 123 reversal strategy determines that if the closing price of the day rises compared with the previous day and the slow K line is below 50, go long; if it falls and the fast K line is above 50, go short. This strategy takes advantage of short-term reversal characteristics to profit.
### Psychological line strategy
The psychological line strategy counts the rise and fall ratios within a certain period. If the rise is greater than 50%, it means bulls control the market; if the rise is less than 50%, it means bears control the market.根据涨跌比例来判断市场心理面。
This strategy combines the signals of the above two strategies. When they give signals in the same direction, open a position and close the position when they give signals in different directions.
## Advantages
This strategy combines multiple factors to more accurately judge market trends and avoid misjudgments caused by a single technical indicator. At the same time, combined with market psychological factors, it also makes the strategy more resilient and able to cope with more complex market conditions.
## Risks and Solutions
The setting of each factor parameter in this strategy will have a great impact on the performance of the strategy. Unreasonable parameter combinations may greatly reduce the effectiveness of the strategy. In addition, if the market changes drastically, the strategy will fail. In order to reduce risks, we need to conduct a large number of backtests on various market conditions to find the optimal parameters; at the same time, we need to control the position size to ensure that a single loss is not too large.
## Optimization direction
We can continue to add other judgment factors on the existing basis, such as volatility, trading volume and other indicators, to form a more three-dimensional strategy logic; or add machine learning algorithms to achieve adaptive optimization of the parameters of the strategy.这都将是本策略进一步优化的方向。
## Summarize
This strategy comprehensively considers multiple factors such as technical form and market psychology, and ensures the validity of the signal through verification between different factors. At the same time, there is a lot of room for optimization, which is expected to achieve better performance. This is a high-quality quantitative strategy worthy of long-term tracking, accumulation and optimization.
||

## Overview

This strategy combines the 123 reversal strategy and psychological line strategy to form a multi-factor quantitative trading strategy. By comprehensively considering technical patterns, market psychology and other factors, the strategy can make more accurate judgments when determining market trends.  

## Principle

### 123 Reversal Strategy

The 123 reversal strategy judges that if the closing price of the day rises compared to the previous day, and the slow K line is below 50, go long; if it falls, and the fast K line is above 50, go short. The strategy takes advantage of the characteristics of short-term reversals to profit.

### Psychological Line Strategy

The psychological line strategy counts the ratio of rises and falls over a certain cycle. If the rise is greater than 50%, it indicates that bulls control the market; if the rise is less than 50%, it indicates that bears control the market. Make judgments about market psychology based on the ratio of rises and falls.

This strategy combines the signals from the above two strategies. Open positions when the two strategies give signals in the same direction, and close positions when giving signals in different directions.

## Advantages

The strategy combines multiple factors and can make more accurate judgments about market trends, avoiding misjudgments caused by a single technical indicator. At the same time, the combination of market psychology makes the strategy more resilient to cope with complex trend changes.  

## Risks and Solutions

The setting of parameters for each factor in the strategy will have a greater impact on strategy performance. Unreasonable parameter combinations may greatly reduce the effectiveness of the strategy. In addition, drastic changes in trends can also cause the strategy to fail. To reduce risks, we need to backtest various market conditions to find the optimal parameter settings; also control position sizing to ensure that a single loss will not be too large.

## Optimization Directions 

On the existing basis, we can continue to add other judgment factors such as volatility and volume to form a more three-dimensional strategy logic; or add machine learning algorithms to achieve automatic parameter adaptive optimization. These will be further optimization directions for this strategy.  

## Summary  

This strategy comprehensively considers multiple factors such as technical patterns and market psychology. Validation between different factors ensures the validity of signals. At the same time, it leaves ample room for optimization and is expected to achieve superior performance. This is a high-quality quantitative strategy worth long-term tracking, accumulation and optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- Psychological line ----|
|v_input_7|20|LengthPLine|
|v_input_8|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-20 00:00:00
end: 2023-12-26 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 30/04/2021
// This is combo strategies for get a cumulative signal. 
//
// First strategy
// This System was created from the Book "How I Tripled My Money In The 
// Futures Market" by Ulf Jensen, Page 183. This is reverse type of strategies.
// The strategy buys at market, if close price is higher than the previous close 
// during 2 days and the meaning of 9-days Stochastic Slow Oscillator is lower than 50. 
// The strategy sells at market, if close price is lower than the previous close price 
// during 2 days and the meaning of 9-days Stochastic Fast Oscillator is higher than 50.
//
// Second strategy
// Psychological line (PSY), as an indicator, is the ratio of the number of 
// rising periods over the total number of periods. It reflects the buying 
// power in relation to the selling power.
// If PSY is above 50%, it indicates that buyers are in control. Likewise, 
// if it is below 50%, it indicates the sellers are in control. If the PSY 
// moves along the 50% area, it indicates balance between the buyers and 
// sellers and therefore there is no direction movement for the market.
//
// WARNING:
// - For purpose educate only
// - This script to change bars colors.
////////////////////////////////////////////////////////////
Reversal123(Length, KSmoothing, DLength, Level) =>
    vFast = sma(stoch(close, high, low, Length), KSmoothing) 
    vSlow = sma(vFast, DLength)
    pos = 0.0
    pos := iff(close[2] < close[1] and close > close[1] and vFast < vSlow and vFast > Level, 1,
	         iff(close[2] > close[1] and close < close[1] and vFast > vSlow and vFast < Level, -1, nz(pos[1], 0))) 
	pos


PLine(Length) =>
    pos = 0.0
    cof = close > close[1]? 1:0
    xPSY = sum(cof,Length) / Length * 100
    pos:= iff(xPSY > 50, 1,
           iff(xPSY < 50, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & Psychological line", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- Psychological line ----")
LengthPLine = input(20, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posPLine = PLine(LengthPLine)
pos = iff(posReversal123 == 1 and posPLine == 1 , 1,
	   iff(posReversal123 == -1 and posPLine == -1, -1, 0)) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1 , 1, pos))	   
if (possig == 1 ) 
    strategy.entry("Long", strategy.long)
if (possig == -1 )
    strategy.entry("Short", strategy.short)	 
if (possig == 0) 
    strategy.close_all()
barcolor(possig == -1 ? #b50404: possig == 1 ? #079605 : #0536b3 )
```

> Detail

https://www.fmz.com/strategy/436770

> Last Modified

2023-12-27 15:46:27

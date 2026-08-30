
> Name

Dual-Factor-Combo-Reversal-and-Mass-Index-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12ae8468696c2cc6b1a.png)
[trans]

## Overview
This strategy is a portfolio reversal trading strategy based on the dual factor model. It integrates the two factors of 123 pattern reversal and incremental index to achieve the additive effect of strategic signals. When two factors send out buy or sell signals at the same time, the strategy will perform corresponding long or short operations.
## Strategy Principle
### 123 reversal factor
This factor operates based on the 123 pattern of price. When the closing price relationship of the previous two days is "low-high" and the Stoch indicator is lower than 50, it is judged to be a bottom reversal signal, and you go long; when the closing price relationship of the previous two days is "high-low" and the Stoch indicator is higher than 50, it is judged to be a top reversal signal, and you go short.
### Incremental exponential factor
This factor identifies trend reversals based on an increase or decrease in the price range. When the fluctuation range increases, the index rises; when the fluctuation range decreases, the index falls. When the index crosses a certain threshold, a short signal is generated, and when the index crosses below a certain threshold, a long signal is generated.
Only signals from two factors in the same direction will open a position, achieve strategic profitability, and avoid the risk of false signals caused by a single factor.
## Advantage Analysis
- Two-factor model, combining price patterns and volatility indicators to improve signal accuracy
- 123 form judgment local extremum, incremental index captures the global trend reversal point, complementary advantages
- Only open positions when the two factors send signals in the same direction, effectively filtering out false signals and improving strategy stability
## Risk Analysis
- There is a probability that two factors will send out wrong signals at the same time, bringing the risk of loss.
- There is a probability of reversal failure, and stop loss needs to be set to control losses.
- Improper parameter optimization may lead to overfitting
Risks can be reduced by expanding the training set, strict stop loss, and multi-factor combination filtering.
## Optimization direction
- Test more combinations of price and volatility indicators
- Add machine learning model to judge signal quality and dynamically adjust positions
- Combine trading volume, Bollinger Bands and other factors to discover more Alpha
- Use walk forward method for rolling optimization to improve robustness
## Summarize
This strategy combines two factors, price form and volatility indicator, and only opens a position when the two factors send signals in the same direction, avoiding the risk of false signals caused by a single factor, thereby improving the overall stability of the strategy. However, there is also a risk that two factors may send out wrong signals at the same time with a certain probability. We can further improve strategy performance and risk-adjusted returns by expanding the training set, setting stop losses, and optimizing factor combinations.
||

## Overview

This strategy is a combo reversal trading strategy based on a dual-factor model. It integrates the 123 reversal pattern and the Mass Index factors to achieve a cumulative effect for the strategy signals. It will only go long or short when both factors emit a buy or sell signal simultaneously.

## Strategy Logic

### 123 Reversal Factor

This factor operates based on the 123 price pattern. When the closing price relationship over the past two days is "low-high" and the Stoch indicator is below 50, it signals a bottom reversal and goes long. When the closing price relationship is “high-low” and Stoch is above 50, it signals a top reversal and goes short.

### Mass Index Factor

This factor judges trend reversals based on the expansion or contraction of the price fluctuation range. As the range expands, the index rises and as the range narrows, the index falls. It generates a sell signal when the index crosses above a threshold and a buy signal when crossing below a threshold.

The strategy only opens positions when the two factors emit signals in the same direction, achieving profitable trades while avoiding false signals from a single factor.

## Advantage Analysis

- Dual-factor model combines price pattern and volatility indicator for better signal accuracy
- 123 pattern catches local extremums, Mass Index captures global trend reversal points, complementary strengths  
- Only taking signals when two factors agree avoids false signals and enhances stability

## Risk Analysis

- Probability exists for both factors to emit wrong signals concurrently, causing losses
- Failure rate of reversals exists, need to set stop loss to control downside
- Improper parameter tuning may lead to overfitting

Risks can be reduced via expanding training set, strict stop loss, multi-factor filtering etc.

## Optimization Directions

- Test more price and volatility indicator combinations
- Add ML model to judge signal quality and dynamically size positions
- Incorporate volume, Bollinger Bands etc. to discover more alpha
- Employ walk forward optimization for robustness

## Conclusion

This strategy combines two factors, price pattern and volatility indicator, to only take signals when they agree, avoiding false signals from a single factor and improving stability. But risks remain for concurrent wrong signals. We can further enhance performance and risk-adjusted returns by expanding dataset, setting stop loss, optimizing factor combinations and more.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- MASS Index ----|
|v_input_7|9|Length1|
|v_input_8|25|Length2|
|v_input_9|26.5|Trigger|
|v_input_10|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-25 00:00:00
end: 2023-12-25 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 22/02/2021
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
// The Mass Index was designed to identify trend reversals by measuring 
// the narrowing and widening of the range between the high and low prices. 
// As this range widens, the Mass Index increases; as the range narrows 
// the Mass Index decreases.
// The Mass Index was developed by Donald Dorsey. 
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


MASS(Length1,Length2,Trigger) =>
    pos = 0.0
    xPrice = high - low
    xEMA = ema(xPrice, Length1)
    xSmoothXAvg = ema(xEMA, Length1)
    nRes = sum(iff(xSmoothXAvg != 0, xEMA / xSmoothXAvg, 0), Length2)
    pos := iff(nRes > Trigger, -1,
	         iff(nRes < Trigger, 1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & MASS Index", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- MASS Index ----")
Length1 = input(9, minval=1)
Length2 = input(25, minval=1)
Trigger = input(26.5, step = 0.01)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posMASS = MASS(Length1,Length2,Trigger)
pos = iff(posReversal123 == 1 and posMASS == 1 , 1,
	   iff(posReversal123 == -1 and posMASS == -1, -1, 0)) 
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

https://www.fmz.com/strategy/436623

> Last Modified

2023-12-26 12:20:57

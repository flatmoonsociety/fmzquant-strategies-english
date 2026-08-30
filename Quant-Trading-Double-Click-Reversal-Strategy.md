
> Name

Quant-Trading-Double-Click-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11a6542951866ba488d.png)

[trans]

## Overview
This strategy first uses the 123 pattern to determine the reversal signal, and then combines it with the Klinger quantitative oscillator as a filter to achieve a quantitative double-click profit strategy that efficiently captures reversal opportunities.
## Strategy Principle
The strategy consists of two parts:
1. 123 pattern judgment reversal signal part: when the closing price closes positive on the 3rd day after falling for 2 consecutive days, and the stoch indicator is low, for long; when the closing price closes negative on the 3rd day after rising for 2 consecutive days, and the stoch indicator is high, for short.
2. Klinger quantitative oscillator part: Klinger quantitative oscillator combines the price fluctuation range and trading volume changes to determine the inflow and outflow of funds. When the Quantitative Oscillator crosses above its average value, it is a long signal; when it crosses below its average value, it is a short signal.
Finally, the strategy combines the above two parts of signals and double-clicks profit to determine the final entry.
## Advantage Analysis
The biggest advantage of this strategy is that it can effectively capture reversal opportunities by combining reversal patterns and volume indicators. In addition, the stoch indicator can be used to avoid false breakthroughs and the Klinger quantitative oscillator can be used to determine the true capital flow to ensure accurate entry timing.
## Risk Analysis
The main risks of this strategy lie in reversal pattern judgment and parameter setting issues. Since there is a certain lag in the reversal signal, it is necessary to ensure that the parameter settings are reasonable to avoid missing the best reversal opportunity. In addition, the reversal pattern itself may also have failures.
In order to reduce risks, parameters can be appropriately optimized to make the reversal signal more sensitive and timely. You can also add other filter conditions to ensure that the number of reversals is sufficient and the amplitude is sufficient to avoid expansion of retracement.
## Optimization direction
This strategy can mainly optimize the space in parameter adjustment and add other auxiliary judgments. Specifically, the stoch indicator parameters can be appropriately shortened to optimize the sensitivity of 123 morphological judgment. You can also add current mainstream indicators and patterns for combination, such as MACD, golden cross, or double top / bottom multiple bottoms and other judgments.
In addition, you can consider dynamically adjusting stop loss and take profit conditions to make the strategy more adaptable to market changes. It can also be combined with machine learning to optimize parameters in real time.
## Summary
This strategy comprehensively uses classic reversal theory and quantitative technical indicators to achieve efficient capture of reversal opportunities. The optimization space is large and has the potential to further improve the effect, which is worthy of real-time verification and continuous optimization.
||
## Overview
This strategy first uses the 123 pattern to determine the reversal signal, and then combines the Klinger Volume Oscillator as a filter to implement the double-click quantitative profit strategy to efficiently capture reversal opportunities.

## Principle  
The strategy consists of two parts:

1. 123 pattern to determine reversal signals: when the closing price falls continuously for 2 consecutive days and the 3rd day closes positive, and the stoch indicator is at a low level for long; when the closing price rises continuously for 2 consecutive days and the 3rd day closes negative, and the stoch indicator is at a high level for short.

2. Klinger Volume Oscillator section: Klinger Volume Oscillator combines price fluctuation range and trading volume changes to determine capital inflows and outflows. When the volume oscillator crosses above its average value, it is a long signal; when it crosses below its average value, it is a short signal.

Finally, the strategy combines the signals from the above two parts and double clicks to determine the final entry.


## Advantage Analysis  
The biggest advantage of this strategy is that it combines reversal patterns and volume indicators to efficiently capture reversal opportunities. In addition, with the help of stoch indicator, avoid false breakouts, and the Klinger Volume Oscillator to determine real money flow direction, accurate entry timing can be ensured.

## Risk Analysis
The main risks of this strategy lie in the problem of reversal pattern judgment and parameter setting. Due to the delay in reversal signals, it needs to ensure that the parameters are set reasonably to avoid missing the best reversal timing. In addition, the reversal patterns themselves may fail.

To reduce risks, you can optimize parameters to make reversal signals more responsive and timely. Other filters can also be added to ensure a sufficient number and amplitude of reversals to avoid widening declines.

## Optimization direction
The main optimization space for this strategy is in parameter adjustment and addition of other auxiliary judgments. Specifically, it's possible to appropriately shorten the stoch indicator parameters to optimize the sensitivity of 123 pattern discrimination. It is also feasible to combine with mainstream indicators and patterns currently, such as adding MACD golden crosses and deadly crosses, or double top/bottom multiple bottoms and other judgments.

In addition, consider dynamically adjusting stop loss and take profit conditions to make the strategy more adaptable to market changes. It is also possible to combine machine learning to optimize parameters in real time.

## Summary  
This strategy integrates the application of classical reversal theories and volume technical indicators to efficiently capture reversal opportunities. The space for optimization is large and has the potential to further improve the effect, which is worth validating and continuously optimizing in real trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|13|TrigLen|
|v_input_6|34|FastX|
|v_input_7|55|SlowX|
|v_input_8|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-22 00:00:00
end: 2023-11-21 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 23/12/2020
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
// The Klinger Oscillator (KO) was developed by Stephen J. Klinger. Learning 
// from prior research on volume by such well-known technicians as Joseph Granville, 
// Larry Williams, and Marc Chaikin, Mr. Klinger set out to develop a volume-based 
// indicator to help in both short- and long-term analysis.
// The KO was developed with two seemingly opposite goals in mind: to be sensitive 
// enough to signal short-term tops and bottoms, yet accurate enough to reflect the 
// long-term flow of money into and out of a security.
// The KO is based on the following tenets:
// Price range (i.e. High - Low) is a measure of movement and volume is the force behind 
// the movement. The sum of High + Low + Close defines a trend. Accumulation occurs when 
// today's sum is greater than the previous day's. Conversely, distribution occurs when 
// today's sum is less than the previous day's. When the sums are equal, the existing trend 
// is maintained.
// Volume produces continuous intra-day changes in price reflecting buying and selling pressure. 
// The KO quantifies the difference between the number of shares being accumulated and distributed 
// each day as "volume force". A strong, rising volume force should accompany an uptrend and then 
// gradually contract over time during the latter stages of the uptrend and the early stages of 
// the following downtrend. This should be followed by a rising volume force reflecting some 
// accumulation before a bottom develops.
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

KVO(TrigLen,FastX,SlowX) =>
    pos = 0.0
    xTrend = iff(hlc3 > hlc3[1], volume * 100, -volume * 100)
    xFast = ema(xTrend, FastX)
    xSlow = ema(xTrend, SlowX)
    xKVO = xFast - xSlow
    xTrigger = ema(xKVO, TrigLen)
    pos := iff(xKVO > xTrigger, 1,
    	     iff(xKVO < xTrigger, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & Klinger Volume Oscillator", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
TrigLen = input(13, minval=1)
FastX = input(34, minval=1)
SlowX = input(55, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posKVO = KVO(TrigLen,FastX,SlowX)
pos = iff(posReversal123 == 1 and posKVO == 1 , 1,
	   iff(posReversal123 == -1 and posKVO == -1, -1, 0)) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1 , 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	 
if (possig == 0) 
    strategy.close_all()
barcolor(possig == -1 ? #b50404: possig == 1 ? #079605 : #0536b3 )
```

> Detail

https://www.fmz.com/strategy/432845

> Last Modified

2023-11-22 10:03:04

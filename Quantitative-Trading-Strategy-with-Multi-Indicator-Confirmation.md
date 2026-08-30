
> Name

Quantitative-Trading-Strategy-with-Multi-Indicator-Confirmation based on multi-indicator verification
> Author

ChaoZhang

> Strategy Description


[trans]

This article will introduce in detail a quantitative strategy that forms trading signals through multi-indicator verification. This strategy comprehensively uses a variety of indicator judgments to improve the reliability of the signal.
1. Strategy Principle
This strategy set uses two trading techniques:
(1) 123 pattern reversal strategy
1. Calculate the closing price relationship of the K line and determine the possible bottom and top patterns;
2. Combine with stochastic indicators to determine reversal signals and avoid false signals;
(2) Smoothed long and short volume indicator
1. Calculate the long and short volume indicators and their moving averages;
2. Determine the trend based on the divergence between indicators and moving averages;
3. Only when the judgments of the two technologies are consistent, the final trading signal is generated.
In this way, through multi-index verification, certain false signals can be filtered out and signal accuracy improved.
2. Strategic advantages
The biggest advantage of this strategy is the multi-indicator combination verification, which avoids the limitations of a single indicator and enhances the stability of the signal.
Another advantage is the combined use of two different types of techniques, which further improves the comprehensiveness of the judgment.
Finally, combined use also provides more parameter space for optimization testing.
3. Potential risks
But this strategy also has the following problems:
First, the combination of multiple indicators increases the difficulty of parameter optimization, and improper settings may lead to over-optimization.
Secondly, there may be differences between the two technical signals, and clear judgment rules need to be set.
Finally, some indicators such as stochastic indicators still have lagging problems.
4. Content summary
This article details a strategy for quantitative trading with multi-indicator validation. It improves signal quality by using a combination of indicators, but it also needs to pay attention to issues such as difficulty in parameter optimization and indicator lag. Overall, this strategy provides a relatively robust trading approach.
||

This article explains in detail a quantitative trading strategy that utilizes multi-indicator confirmation to generate signals. It combines different techniques to improve reliability.

I. Strategy Logic

The strategy synthesizes two techniques:

(1) 123 Reversal Pattern

1. Identify potential bottoms and tops based on candle close relationships.

2. Use stochastic to validate reversal signals and avoid false signals.

(2) Smoothed Accumulation/Distribution 

1. Calculate Accumulation/Distribution and moving average.

2. Determine trends based on divergences between the indicator and MA.

3. Only agreeable signals from both techniques are taken.

By requiring multiple confirmations, certain false signals can be filtered out and accuracy improved.

II. Advantages of the Strategy

The biggest advantage is multi-indicator confirmation, which overcomes single indicator limitations and enhances robustness.

Another advantage is combining two different technique types for greater comprehensiveness.

Finally, the combinations also provide more tuning options.

III. Potential Risks

However, some risks exist:

Firstly, multi-indicator combinations increase optimization difficulty and overfitting risks.

Secondly, discrepancies between indicators require clear judgment rules.

Finally, some indicators still have lagging issues.

IV. Summary

In summary, this article has explained a quantitative trading strategy utilizing multi-indicator confirmations. It improves signals through synthesis but requires managing optimization difficulty and indicator lags. Overall it provides a relatively robust approach.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- Smoothed Williams AD ----|
|v_input_7|14|LengthWillAD|
|v_input_8|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-15 00:00:00
end: 2023-09-14 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 21/07/2021
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
// Accumulation is a term used to describe a market controlled by buyers;
// whereas distribution is defined by a market controlled by sellers.
// Williams recommends trading this indicator based on divergences:
//  Distribution of the security is indicated when the security is making 
//  a new high and the A/D indicator is failing to make a new high. Sell.
//  Accumulation of the security is indicated when the security is making 
//  a new low and the A/D indicator is failing to make a new low. Buy. 
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


SWAD(Length) =>
    pos = 0.0
    xWAD = 0.0
    xPrice = close
    xWAD:= iff(close > nz(close[1], 0), nz(xWAD[1],0) + close - low[1], 
             iff(close < nz(close[1],0), nz(xWAD[1],0) + close - high[1],0))
    xWADMA = sma(xWAD, Length)
    pos:= iff(xWAD > xWADMA, 1,
             iff(xWAD < xWADMA, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & Smoothed Williams AD", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- Smoothed Williams AD ----")
LengthWillAD = input(14, step = 1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posSWAD = SWAD(LengthWillAD)
pos = iff(posReversal123 == 1 and posSWAD == 1 , 1,
	   iff(posReversal123 == -1 and posSWAD == -1, -1, 0)) 
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

https://www.fmz.com/strategy/426888

> Last Modified

2023-09-15 11:55:04


> Name

Multi-factor-Combined-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

This strategy combines the use of multiple different types of technical indicators to form a comprehensive quantitative trading strategy. This strategy brings together the advantages of multiple factors to improve the accuracy of trading decisions.
Strategy principle:
1. Calculate the 123 reversal indicator to determine whether the price has a three-day reversal pattern.
2. Calculate the Elder Bear Power indicator to determine whether the price is oversold.
3. When both of them send out buy signals at the same time, perform long operations. When both issue sell signals at the same time, short selling is performed.
4. Through the verification of indicator factors, some noise trading signals can be effectively filtered out.
5. The combination of different types of indicators can improve the judgment of market conditions.
Advantages of this strategy:
1. Multi-factor combination verification can reduce the probability of wrong transactions.
2. Improved the ability to identify complex market situations.
3. Combination strategy parameter optimization is difficult and has certain advantages.
Risks of this strategy:
1. Multi-index combination requires time-consuming optimization of parameters to achieve the best match.
2. There may be signal inconsistencies between different indicators.
3. The overall stability of the combination strategy may be lower than that of a single indicator strategy.
In short, this strategy can improve the accuracy of decision-making to a certain extent by bringing together the advantages of multiple factors for trading. However, we need to pay attention to the matching problem between different indicators and obtain stable excess returns through strict parameter optimization.
||

This strategy combines multiple technical indicators into an integrated quantitative system, harnessing the strengths of different factors to improve trade decision accuracy.

Strategy Logic: 

1. Calculate 123 Reversal indicator to identify potential 3-day reversals.

2. Calculate Elder Bear Power for oversold conditions.

3. Go long when both indicators give buy signals, and short when both give sell signals.

4. Requiring factor verification reduces false signal trades.

5. Combining different indicator types improves situational awareness.

Advantages:

1. Multi-factor verification reduces probability of bad trades.

2. Improves recognition of complex market conditions.

3. Optimization difficulty gives advantage over single strategies.

Risks:

1. Time-consuming to optimize parameters for ideal combination.

2. Potential for signal conflicts between indicators.

3. Overall stability lower than single indicator strategies.

In summary, this strategy aims to improve accuracy by combining multiple factors, but requires tuning to match indicators appropriately for steady outperformance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|13|LengthBP|
|v_input_6|false|Trigger|
|v_input_7|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-05 00:00:00
end: 2023-02-03 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 27/05/2020
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
// Developed by Dr Alexander Elder, the Elder-ray indicator measures buying 
// and selling pressure in the market. The Elder-ray is often used as part 
// of the Triple Screen trading system but may also be used on its own.
// Dr Elder uses a 13-day exponential moving average (EMA) to indicate the 
// market consensus of value. Bull Power measures the ability of buyers to 
// drive prices above the consensus of value. Bear Power reflects the ability 
// of sellers to drive prices below the average consensus of value.
// Bull Power is calculated by subtracting the 13-day EMA from the day's High. 
// Bear power subtracts the 13-day EMA from the day's Low.
// You can use in the xPrice any series: Open, High, Low, Close, HL2, HLC3, OHLC4 and ect...
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

BP(Trigger,Length) =>
    pos = 0
    DayHigh = 0.0
    xPrice = close
    xMA = ema(xPrice,Length)
    DayHigh := iff(dayofmonth != dayofmonth[1], high, max(high, nz(DayHigh[1])))
    nRes = DayHigh - xMA
    pos := iff(nRes > Trigger, 1,
    	     iff(nRes < Trigger, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & Elder Ray (Bear Power) ", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
LengthBP = input(13, minval=1)
Trigger = input(0)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posBP = BP(Trigger,LengthBP)
pos = iff(posReversal123 == 1 and posBP == 1 , 1,
	   iff(posReversal123 == -1 and posBP == -1, -1, 0)) 
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

https://www.fmz.com/strategy/426498

> Last Modified

2023-09-12 16:05:10

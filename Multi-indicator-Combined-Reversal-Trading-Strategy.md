
> Name

Multi-indicator-Combined-Reversal-Trading-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]
The name of this strategy is "Multi-Indicator Fusion Reversal Trading Strategy". This strategy comprehensively uses a variety of technical indicators to identify opportunities for price reversal in the short term and conduct reverse trades to make profits.
First, this strategy uses the 123 reversal pattern to identify short-term price reversals. The 123 reversal pattern refers to a pattern in which the price closes with a clear high-low gap for three consecutive days, and the third day's closing reverses the trend of the previous two days. According to statistics, the profit rate of continuing the 123 reversal pattern to signal is higher.
Secondly, this strategy adds the stochastic indicator RSI to determine the reliability of the reversal signal. An RSI below 50 indicates an oversold condition, and an RSI above 50 indicates an overbought condition. Combined with the RSI indicator, you can avoid too many unreliable signals from the 123 reversal pattern alone.
Finally, this strategy introduces the multi-period cross difference determination of the CMO indicator. The CMO cross difference is combined with exponential moving averages of different periods to determine the reversal of price momentum. Its signal once again confirms the 123 reversal trading timing.
The comprehensive use of the above multiple indicators can improve the success rate of price reversal capture and avoid too many uncertain signals. When both RSI and CMO support the 123 pattern, it sends a strong reversal trading signal.
This strategy is suitable for consolidating volatile markets and capturing short-term price fluctuations. However, multi-index combinations are also prone to different indicators hedging each other, and parameter optimization is required. Stop loss strategies also need to be used in conjunction to control the maximum loss in a single transaction.
In general, multi-indicator fusion reversal trading strategies combine various tools to improve the accuracy of judgment on market reversal timing. However, any single strategy is difficult to perfect and requires traders to conduct detailed verification and adjustments based on the current market conditions and always maintain the flexibility of trading awareness.

||

This strategy is named “Multi-indicator Combined Reversal Trading Strategy”. It integrates various technical indicators to identify opportunities for short-term price reversals and trade against the previous trend for profits.

Firstly, the strategy uses the 123 reversal pattern to determine short-term trend reversals. The 123 pattern is when prices gap significantly over three consecutive days and the third day closes in the opposite direction of the previous two days. Statistically, trading with 123 reversal signals has a higher win rate.

Secondly, the RSI indicator is incorporated to evaluate the reliability of reversal signals. RSI below 50 represents oversold conditions, while above 50 is overbought. Using RSI avoids generating excessive unreliable signals purely based on the 123 pattern.

Thirdly, the CMO indicator’s multi-period crossover is introduced. The CMO crossover combining different period exponential moving averages judges momentum reversals. Its signals provide further confirmation of the 123 reversal timing.

The combined application of multiple indicators increases the success rate of capturing price reversals by avoiding excessive uncertain signals. Only when RSI and CMO both support the 123 pattern will a strong reversal trade signal emerge.

This strategy suits ranging, oscillating markets to capture short-term price fluctuations. However, combining too many indicators can also lead to conflicts. Parameter optimization is needed. Stop loss should also be used to limit maximum loss per trade.

In conclusion, the multi-indicator combined reversal trading strategy integrates various tools to improve judgment accuracy of market reversals. But no single strategy is perfect. Traders need to validate and adjust based on current market conditions, maintaining flexible trading mindset.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|50|LengthFirst|
|v_input_6|25|LengthSecond|
|v_input_7|10|LengthThird|
|v_input_8|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-03-11 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 25/02/2020
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
// The related CMOaDisparity Index article is copyrighted material from Stocks & Commodities Dec 2009
// My strategy modification.
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

CMOD(LengthFirst, LengthSecond, LengthThird) =>
    pos = 0.0
    xEMAFirst = ema(close,LengthFirst)
    xEMASecond  = ema(close,LengthSecond)
    xEMAThird  = ema(close,LengthThird)
    xResFirst = 100 * (close - xEMAFirst) / close
    xResSecond = 100 * (close - xEMASecond) / close
    xResThird = 100 * (close - xEMAThird) / close
    pos := iff(xResThird > xResFirst, -1,
             iff(xResThird < xResSecond, 1, nz(pos[1], 0)))     
    pos

strategy(title="Combo Backtest 123 Reversal & CMOaDisparity Index", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
LengthFirst = input(50, minval=1)
LengthSecond = input(25, minval=1)
LengthThird = input(10, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posCMOD = CMOD(LengthFirst, LengthSecond, LengthThird)
pos = iff(posReversal123 == 1 and posCMOD == 1 , 1,
	   iff(posReversal123 == -1 and posCMOD == -1, -1, 0)) 
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

https://www.fmz.com/strategy/426587

> Last Modified

2023-09-13 15:04:40

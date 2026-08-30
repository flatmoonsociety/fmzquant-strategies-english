
> Name

Double-Reversal-RSI-Momentum-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy combines the 123 pattern reversal strategy and the RSI momentum strategy to achieve dual signal filtering and achieve high probability entries at trend reversal points.
## Principle analysis
### 123 Pattern Reversal Strategy
This strategy comes from page 183 of Ulf Jensen's book "How I Tripled My Gains in the Futures Market". The principle is to identify potential trend reversal opportunities during the consolidation phase.
Specifically, when the closing price is higher than the closing price of the previous day for 2 consecutive days, and the 9-day Slow K-line is lower than 50, go long; when the closing price is lower than the previous day's closing price for 2 consecutive days, and the 9-day Fast K-line is higher than 50, go short.
Therefore, this strategy essentially uses the fast and slow lines of the Stochastic indicator to determine potential reversal opportunities.
### RSI Momentum Strategy
This strategy uses the ROC function to calculate the price change rate, and then constructs the RSI indicator based on the price change rate to determine the momentum trend.
When the RSI is below the buy zone, it indicates that the upward momentum of the price is accelerating, so go long; when the RSI is above the sell zone, it indicates that the downward momentum of the price is accelerating, so go short.
### Advantages
- 123 pattern reversal strategy can determine potential reversal points after consolidation
- RSI momentum strategy can effectively filter out false breakouts
- The signals from the two strategies accumulate to form a strong entry signal
### Risk
- The 123 pattern is prone to overlapping heads or false breakthroughs, and needs to be filtered with other indicators.
- RSI itself is still based on price, so it cannot completely avoid being trapped.
- You may miss better entry points when dual signals accumulate
Consider the following points to reduce risk:
1. Adjust the parameters of the Stochastic indicator and use a longer period to determine the trend
2. Adjust the parameters of RSI and use the lower zone to buy and the higher zone to sell.
3. Consider entering using only a single signal
## Optimization direction
- Can test ROC cycle parameters to find parameters that are more suitable for specific varieties
- Can test 123 form judgment logic, such as adjusting K line speed and slow line parameters
- You can test RSI section parameters to determine more suitable buying and selling areas
- You can try other indicators such as MACD instead of Stochastic
- Possibility to test the effect of using only a single strategy signal
## Summarize
Through the verification of double reversal signals, this strategy can improve the accuracy of entry before the trend reverses. The 123 pattern determines reversal opportunities, and the RSI momentum indicator further verifies the effectiveness of the reversal. The strategy is easy to optimize and adjust parameters, and users can test it according to different varieties and trading preferences. However, we should also pay attention to the risk that dual signals may miss the entry point. Overall, this strategy provides an idea and framework for effectively judging reversal trends.
|| 

## Overview

This strategy combines the 123 reversal pattern and RSI momentum strategies to filter signals for high-probability entries at trend reversal points.

## Principles

### 123 Reversal Strategy 

This strategy is from the book "How I Tripled My Money in the Futures Market" by Ulf Jensen, Page 183. It identifies potential trend reversals during consolidations.

Specifically, it goes long when the close is higher than the previous close for 2 consecutive days and the 9-period Slow K line is below 50; it goes short when the close is lower than the previous close for 2 consecutive days and the 9-period Fast K line is above 50.

So essentially it uses the stochastic indicator's golden cross and death cross to determine potential reversals.

### RSI Momentum Strategy

This strategy uses the ROC function to calculate price rate of change, and constructs a RSI indicator based on the price rate of change to determine momentum trends. 

It goes long when RSI is below the buy zone, indicating accelerating upside momentum; it goes short when RSI is above the sell zone, indicating accelerating downside momentum.

### Advantages

- 123 reversal pattern identifies potential reversal points after consolidations
- RSI momentum filters out false breakouts effectively 
- Accumulation of signals from both strategies gives high-conviction entries

### Risks

- 123 pattern prone to bull traps or false breakouts, needs filtering 
- RSI still based on price, cannot fully avoid whipsaws
- Double signal accumulation may miss better entry points

Possible ways to reduce risks:

1. Tune Stochastic parameters to use longer period to define trend
2. Adjust RSI parameters to use wider buy/sell zones
3. Consider using just one signal for entries

## Optimization Directions

- Test ROC periods to find optimal values for specific products
- Test 123 pattern logic, e.g. adjust fast/slow K lines
- Test RSI zone values to find optimal buy/sell ranges
- Try other indicators like MACD to replace Stochastic
- Test effect of using just one strategy signal

## Conclusion

This strategy improves entry accuracy at trend reversals by requiring two confirming reversal signals. 123 pattern identifies reversals and RSI momentum verifies validity. Easy to optimize parameters for different products and preferences. But beware of missing entries from dual signal accumulation. Overall an effective framework for identifying reversal trends.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- RSI based on ROC ----|
|v_input_7|20|RSILength|
|v_input_8|20|ROCLength|
|v_input_9|30|BuyZone|
|v_input_10|70|SellZone|
|v_input_11|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-26 00:00:00
end: 2023-09-25 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 17/06/2021
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
// This is the new-age indicator which is version of RSI calculated upon 
// the Rate-of-change indicator.
// The name "Relative Strength Index" is slightly misleading as the RSI 
// does not compare the relative strength of two securities, but rather 
// the internal strength of a single security. A more appropriate name 
// might be "Internal Strength Index." Relative strength charts that compare 
// two market indices, which are often referred to as Comparative Relative Strength.
// And in its turn, the Rate-of-Change ("ROC") indicator displays the difference 
// between the current price and the price x-time periods ago. The difference can 
// be displayed in either points or as a percentage. The Momentum indicator displays 
// the same information, but expresses it as a ratio.
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


RSI_ROC(RSILength,ROCLength,BuyZone,SellZone) =>
    pos = 0.0
    xPrice = close
    nRes = rsi(roc(xPrice,ROCLength),RSILength)
    pos := iff(nRes < BuyZone, -1,
	         iff(nRes > SellZone, 1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & RSI based on ROC", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- RSI based on ROC ----")
RSILength = input(20, minval=1)
ROCLength = input(20, minval=1)
BuyZone = input(30, minval=1)
SellZone = input(70, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posRSI_ROC = RSI_ROC(RSILength,ROCLength,BuyZone,SellZone)
pos = iff(posReversal123 == 1 and posRSI_ROC == 1 , 1,
	   iff(posReversal123 == -1 and posRSI_ROC == -1, -1, 0)) 
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

https://www.fmz.com/strategy/427883

> Last Modified

2023-09-26 15:42:48

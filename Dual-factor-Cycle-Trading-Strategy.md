
> Name

Dual-factor-Cycle-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/8fbc976d6b1399a2da44a69c5ba319112cec09d3d1019a3d5c7f5ce7c73a7b26.png)

[trans]

## Overview
The two-factor cycle trading strategy is a quantitative trading strategy. It combines two different types of technical indicators to generate trading signals to track market trends and obtain excess returns.
The advantage of this strategy is that it can look for trading opportunities by combining different factors. Double confirmation can improve the reliability of the signal and reduce the probability of wrong transactions. At the same time, the strategy makes full use of the advantages of cycle trading, that is, timely stop loss and reverse opening of positions, which can effectively control risks.
## Strategy Principle
The strategy consists of two parts:
1. 123 reversal strategy
This strategy comes from the book "How I Tripled My Money in the Futures Market" by Ulf Jensen. Its trading logic is: go long when the closing price is higher than the closing price of the previous day for two consecutive days, and the 9-day slow K-line is lower than 50; go short when the closing price is lower than the closing price of the previous day for two consecutive days, and the 9-day fast K-line is higher than 50.
2. Bullish/Bearish Support and Resistance Strategy
This strategy generates signals by determining if price breaks key support or resistance. It is bullish when the price breaks through the highest price of the previous trading day, and bearish when the price falls below the lowest price of the previous trading day.
Based on the signals of the above two strategies, the position will be entered when the signals from both parties are consistent, otherwise the position will be cleared. At the same time, a reverse position opening mode is set up to stop losses and reverse transactions in time when the market changes, so as to realize the circular operation of funds.
## Advantage Analysis
This two-factor cycle trading strategy offers the following advantages:
1. Multi-factor design ensures high signal reliability. 123 The reversal strategy and the support and resistance strategy verify each other and can reduce false signals.
2. The circular trading mechanism allows the strategy to adapt to market changes and effectively control unilateral losses.
3. Using the 9-day stochastics indicator can filter out the noise in the market and make the signal clearer.
4. Lower risk and smaller drawdown than single factor strategy. Multiple factors can form a combined force to suppress the impact of irrational fluctuations on strategies.
## Risk Analysis
There are also some risks with this strategy:
1. It is unable to capture the trend well in a volatile market, and will frequently stop losses and open reverse positions, thereby increasing transaction costs. The stop loss line can be appropriately relaxed to deal with it.
2. Stochastics parameter settings will affect signal quality. Improper parameters may lead to signal misalignment and quality degradation. Parameters need to be repeatedly tested and optimized.
3. Although the two-factor design improves signal quality, it also increases the impact of market "noise" on the strategy. This requires us to be more careful when constructing and validating strategies.
## Optimization direction
We can further optimize this strategy from the following aspects:
1. Test Stochastics with different length periods to find the best parameter combination to eliminate market noise
2. Add a trend filter to filter out volatile market conditions and only open positions under clear trends.
3. Optimize the stop loss line setting algorithm to reduce transaction costs while ensuring that the stop loss is effective.
4. Test different factor combinations and find factor combinations with clearer trading signals and more stable strategies.
## Summary
This strategy achieves higher signal quality and risk-adjusted returns through a two-factor design. At the same time, the circular trading mechanism is used to effectively control losses in unilateral market conditions. This strategy can be described as a good balance between risk and return. We still need to conduct in-depth research on parameter optimization, risk control settings, etc. to obtain better strategy performance.
||


## Overview
The dual-factor cycle trading strategy is a quantitative trading strategy. It combines two different types of technical indicators to generate trading signals and track market trends for excess returns.  

The advantage of this strategy is that it can find trading opportunities by combining different factors and dual confirmation can improve signal reliability and reduce the probability of erroneous trades. At the same time, the strategy takes full advantage of cycle trading, namely timely stop loss and reverse opening positions, which can effectively control risks.

## Strategy Principles 
The strategy consists of two parts:

1. 123 Reversal Strategy
This strategy comes from the book "How I Tripled My Money in the Futures Market" by Ulf Jensen. Its trading logic is: when the closing price is higher than the previous closing price for two consecutive days, and the 9-day slow K-line is lower than 50, go long; when the closing price is lower than the previous closing price for two consecutive days, and the 9-day fast K-line is higher than 50, go short.

2. Support/Resistance Lookback Strategy  
This strategy generates signals by judging whether prices break through key support or resistance levels. When the price breaks through the highest price of the previous trading day, it indicates a bullish signal; when the price breaks below the lowest price of the previous trading day, it indicates a bearish signal.

By combining the signals of the above two strategies, open positions when both signals are consistent, otherwise clear positions. A reverse opening mode is also set to stop loss and reverse trade in a timely manner when the market changes, so as to achieve a cyclic operation of funds.


## Advantage Analysis
This dual-factor cycle trading strategy has the following advantages:

1. The multi-factor design ensures high signal reliability. The 123 reversal strategy and the support/resistance strategy verify each other and can reduce erroneous signals.

2. The cycling mechanism enables the strategy to adapt to market changes and effectively control one-sided losses.  

3. The use of the 9-day Stochastics indicator can filter out market noise and make clearer signals.

4. It is less risky than single-factor strategies and has smaller drawdowns. Multiple factors can form a combined force to curb the impact of irrational fluctuations on the strategy.


## Risk Analysis 
This strategy also poses some risks:

1. It is difficult to capture trends well in sideways markets, and frequent stop losses and reverse openings will increase transaction costs. Appropiate expansion of stop loss lines can address this.

2. The parameter settings of Stochastics will affect signal quality. Improper parameters may lead to signal misplacement and quality degradation. Parameters need to be repeatedly tested and optimized.

3. Although dual-factor design improves signal quality, it also increases the impact of market "noise" on the strategy. This requires us to be more cautious when constructing and verifying strategies.

## Optimization Directions
We can further optimize this strategy from the following aspects:

1. Test Stochastics of different cycle lengths to find the optimal parameter combination to eliminate market noise

2. Add a trend filter to filter out sideways markets and only open positions in clear trends  

3. Optimize the stop loss line setting algorithm to reduce transaction costs while ensuring effective stop loss

4. Test different combinations of factors to find factor combinations with clearer trading signals and more stable strategies

## Summary 
Through dual-factor design, this strategy has obtained higher signal quality and risk-adjusted returns. At the same time, the use of cycle trading effectively controls the losses in unilateral market. The strategy has struck a good balance between risk and return. More in-depth research is still needed on parameter optimization, risk control settings, etc. to achieve better strategy performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|true|To Line  From Line|
|v_input_6|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-04 00:00:00
end: 2023-12-04 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 13/11/2019
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
// Cueing Off Support And Resistance Levels, by Thom Hartle 
// modified by HPotter for trade signals.
// The related article is copyrighted material from Stocks & Commodities.
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

COSRL(SigVal) =>
    pos = 0.0
    xLow = low
    xHigh = high
    xHighD = security(syminfo.tickerid,"W", high[1])
    xLowD  = security(syminfo.tickerid,"W", low[1])
    sigpre1 = iff(xHigh <= xLowD, -1,
                 iff(xLow >= xHighD, 1, nz(pos[1], 0))) 
    sigpre2 = iff( xHigh <= xHighD, -1,
                 iff(xLow >= xLowD, 1, nz(pos[1], 0))) 
    pos := SigVal ? sigpre1 : sigpre2
    pos

strategy(title="Combo Backtest 123 Reversal & Cueing Off Support And Resistance Levels", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
SigVal = input(true, title="To Line \ From Line")
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posCOSRL = COSRL(SigVal)
pos = iff(posReversal123 == 1 and posCOSRL == 1 , 1,
	   iff(posReversal123 == -1 and posCOSRL == -1, -1, 0)) 
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

https://www.fmz.com/strategy/434344

> Last Modified

2023-12-05 17:56:27

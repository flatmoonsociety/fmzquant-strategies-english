
> Name

Double-Momentum-Index-and-Reversal-Hybrid-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/a196e528d62db7d1c7f5de1ecb308ae7abc645a99cc8f6b132783ac1d45f3873.png)
[trans]
### Overview
The Dual Momentum Index and Reversal Composite Strategy is a composite strategy that combines a reversal strategy and a momentum strategy. It comprehensively uses two sub-strategies, the 123 reversal strategy and the Commodity Selection Index (CSI), to determine the entry opportunity based on dual signals. This strategy is designed to increase the accuracy of trading signals.
### Strategy Principles
This strategy consists of two sub-strategies:
1. 123 reversal strategy. It goes long when the closing price rises for two consecutive days and the stoch indicator is below 50; it goes short when the closing price falls for two consecutive days and the stoch indicator is above 50. It is a reversal strategy.
2. Commodity Selection Index (CSI) strategy. It combines the Average True Range indicator (ATR) with the Average Directional Movement indicator (ADX). ATR reflects market volatility, and ADX reflects trend strength. The higher the CSI value, the stronger the market trend and volatility. It is a momentum tracking strategy.
The entire strategy is based on the 123 reversal strategy and the CSI strategy is the auxiliary confirmation. A trading signal is issued only when the two signals are consistent. When going long, the closing price rises for two consecutive days and stoch is below 50, while CSI crosses its moving average; when going short, the closing price falls for two consecutive days and stoch is above 50, while CSI falls below its moving average.
This not only ensures the reversal properties of the trading signal, but also adds CSI indicator filtering to reduce false signals.
### Advantage Analysis
This strategy has the following advantages:
1. Combine reversal and momentum to improve signal accuracy. As the main signal, the 123 reversal strategy can capture sudden and violent market reversals. The CSI indicator serves as a secondary confirmation and can filter out some noise.
2. Using composite filtering can significantly reduce net positions. Even if the sub-strategy itself has a certain proportion of false signals, the final signals must be consistent in both directions, so that most of the false signals can be filtered out, thereby minimizing unnecessary repeated opening and closing of positions.
3. Sub-strategy parameters can be optimized individually. 123 The respective parameters of the inversion strategy and the CSI strategy can be tested and optimized separately without interfering with each other. This facilitates finding the best parameter combination.
4. Sub-policies can be enabled individually. This strategy supports trading alone using only the 123 reversal strategy or the CSI strategy. This provides flexibility in strategy.
### Risk Analysis
Although this strategy significantly reduces false signals through compound filtering, there are still the following major risks:
1. The frequency of strategic signals is relatively low. Using the double confirmation method will inevitably filter out a certain proportion of trading opportunities. This is an inevitable payment to achieve a high winning rate.
2. If the parameters of the two sub-strategies are inappropriate, it may result in few or even no signals. It is necessary to conduct rigorous testing and optimization of parameters to find the best parameter combination.
3. 123 reversal is a counter-market operation. If the market experiences continuous and violent unilateral price breakthroughs, this strategy will face greater risks. Consider adding a stop loss to control risk.
### Optimization direction
The main optimization space of this strategy lies in the following aspects:
1. Optimize the internal parameters of each sub-strategy and find the best parameter combination. Including stoch indicator parameters, CSI indicator parameters, etc.
2. Test adding different market status filters. For example, only use the CSI strategy when the trend is prevailing, and only use the 123 reversal strategy in volatile markets. This can overcome the disadvantages of sub-strategies to a certain extent.
3. Develop parameter adaptation and dynamic optimization modules. Allow the strategy to automatically adjust parameters based on real-time market status and statistical data, and track the optimal parameter combination in real time.
4. Test different stop loss mechanisms. Appropriate stop loss can not only effectively control risks, but also reduce unnecessary repeated opening and closing of positions.
### Summarize
The dual momentum index and reversal composite strategy uses multi-signal confirmation and combination ideas to effectively utilize the respective advantages of the reversal strategy and the momentum strategy. At the same time, it alleviates the disadvantages of both parties through mutual filtering, achieving high efficiency and high stability. It is one of the typical quantitative strategies available.
||

### Overview

The Double Momentum Index and Reversal Hybrid Strategy is a composite strategy combining reversal and momentum strategies. It integrates the 123 Reversal Strategy and the Commodity Selection Index (CSI) as sub-strategies to determine entry signals based on dual confirmation. The strategy aims to improve the accuracy of trading signals.  

### Strategy Logic   

The strategy consists of two sub-strategies:   

1. 123 Reversal Strategy. It goes long when the closing price rises for two consecutive days and Stoch is below 50; it goes short when the closing price falls for two consecutive days and Stoch is above 50. It’s a reversal-type strategy.  

2. Commodity Selection Index (CSI) Strategy. It combines the Average True Range (ATR) and the Average Directional Movement Index (ADX). ATR reflects market volatility and ADX reflects trend strength. The higher the CSI value, the stronger the market trend and volatility. It’s a momentum tracking strategy.   

The whole strategy takes the 123 Reversal strategy as the main body and CSI as an assistant confirmation. Trading signals are generated only when the signals of both strategies are consistent. It goes long when the closing price rises for two consecutive days and Stoch is below 50, and at the same time when CSI crosses above its moving average; it goes short when the closing price falls for two consecutive days and Stoch is above 50, and at the same time when CSI crosses below its moving average.  

This ensures the reversal attribute of trading signals, while adding CSI to filter can reduce false signals.  

### Advantages  

The strategy has the following advantages:  

1. Combining reversal and momentum improves signal accuracy. The 123 Reversal as the main signal can capture sudden and violent reversals. CSI as confirmation can filter out some noise.  

2. Adopting composite filtering can greatly reduce net positions. Even if the sub-strategies themselves have some false signals, the final signal must be double confirmed, which can filter out most false signals and minimize unnecessary opening and closing of positions.
  
3. The parameters of sub-strategies can be optimized separately without interference with each other. This facilitates finding the optimal parameter combination.  

4. Sub-strategies can be enabled separately. The strategy supports using only 123 Reversal or CSI for trading alone. This provides flexibility.

### Risk Analysis   

Although the strategy significantly reduces false signals through composite filtering, there are still the following main risks:  

1. The frequency of strategy signal generation is relatively low. By adopting double confirmation, a certain proportion of trading opportunities will inevitably be filtered out. This is the inevitable cost to achieve high win rate.  

2. If the parameters of the two sub-strategies are improper, it may result in rare or even no signals. Strict testing and optimization of the parameters are needed to find the optimal parameter combination.  

3. 123 Reversal belongs to counter-trend operations. In case of consecutive and violent one-way price breakthroughs, the strategy will face greater risks. It’s advisable to add in stop loss to control risk.  

### Optimization Direction  

The main optimization possibilities of this strategy are in the following areas:  

1. Optimize the intrinsic parameters of each sub-strategy to find the optimal parameter combinations, including the parameters of Stoch, CSI, etc.  

2. Test adding in different market condition filters, like using CSI only when trend prevails, using 123 Reversal only in range-bound markets, etc. This can overcome the disadvantages of sub-strategies to some extent.

3. Develop parameter self-adaptation and dynamic optimization modules, allowing the strategy to automatically adjust parameters and track optimal parameter combinations according to market conditions and statistics in real time.
  
4. Test different stop loss mechanisms. Proper stop loss can both effectively control risks and reduce unnecessary opening and closing of positions.

### Summary  

The Double Momentum Index and Reversal Hybrid Strategy utilizes the ideas of multi-signal confirmation and combination, making good use of the respective strengths of reversal and momentum strategies, while overcoming their shortcomings by mutual filtering, to achieve high efficiency and stability. It serves as a typical quantitative strategy to be considered for adoption.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|50|PointValue|
|v_input_6|3000|Margin|
|v_input_7|10|Commission|
|v_input_8|14|LengthCSI|
|v_input_9|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-06 00:00:00
end: 2024-02-05 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 25/10/2019
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
// The Commodity Selection Index ("CSI") is a momentum indicator. It was 
// developed by Welles Wilder and is presented in his book New Concepts in 
// Technical Trading Systems. The name of the index reflects its primary purpose. 
// That is, to help select commodities suitable for short-term trading.
// A high CSI rating indicates that the commodity has strong trending and volatility 
// characteristics. The trending characteristics are brought out by the Directional 
// Movement factor in the calculation--the volatility characteristic by the Average 
// True Range factor.
// Wilder's approach is to trade commodities with high CSI values (relative to other 
// commodities). Because these commodities are highly volatile, they have the potential 
// to make the "most money in the shortest period of time." High CSI values imply 
// trending characteristics which make it easier to trade the security.
// The Commodity Selection Index is designed for short-term traders who can handle 
// the risks associated with highly volatile markets.
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

fADX(Len) =>
    up = change(high)
    down = -change(low)
    trur = rma(tr, Len)
    plus = fixnan(100 * rma(up > down and up > 0 ? up : 0, Len) / trur)
    minus = fixnan(100 * rma(down > up and down > 0 ? down : 0, Len) / trur)
    sum = plus + minus 
    100 * rma(abs(plus - minus) / (sum == 0 ? 1 : sum), Len)

CSI(Length, Commission, Margin, PointValue) =>
    pos = 0.0
    K = 100 * ((PointValue / sqrt(Margin) / (150 + Commission)))
    xATR = atr(Length)
    xADX = fADX(Length)
    nADXR = (xADX + xADX[Length]) * 0.5
    xCSI = K * xATR * nADXR
    xMACSI = sma(xCSI, Length)
    pos := iff(xCSI < xMACSI, 1,
    	     iff(xCSI > xMACSI, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Strategy 123 Reversal & Commodity Selection Index", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
PointValue = input(50)
Margin = input(3000)
Commission = input(10)
LengthCSI = input(14)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posCSI = CSI(LengthCSI, Commission, Margin, PointValue)
pos = iff(posReversal123 == 1 and posCSI == 1 , 1,
	   iff(posReversal123 == -1 and posCSI == -1, -1, 0)) 
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

https://www.fmz.com/strategy/441164

> Last Modified

2024-02-06 12:22:32

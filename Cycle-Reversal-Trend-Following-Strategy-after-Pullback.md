
> Name

Cycle-Reversal-Trend-Following-Strategy-after-Pullback
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c760c51271c87b663f.png)
[trans]

## Overview
This strategy comprehensively uses two indicators: moving average reversal and price oscillator to form trading signals and achieve a trend trading strategy of seizing the rebound after the cycle reversal occurs.
## Principle
This strategy mainly uses the following two technical indicators to judge trading signals:
1. Moving average reversal
This part determines whether a reversal signal occurs by calculating the rise and fall of the closing price in the past two days and combining it with the K value of the fast line. When the price continues to rise in the past two days, and the fast line K value is lower than the slow line K value, a buy signal is generated; when the price continues to fall in the past two days, and the fast line K value is higher than the slow line K value, a sell signal is generated.
2. Price Disengagement Indicator
The Detrend Price Oscillator indicator identifies price cycles by plotting a horizontal moving average and based on price's relationship to that line. It filters out trends that are longer than the calculation period, so it can identify short-period fluctuations hidden by moving averages. When the price is above the average line, it is a buy signal, and when it is below the average line, it is a sell signal.
This strategy combines the signals of the two indicators, that is, when the moving average reversal signal appears, and the price deviation indicator also gives a confirmed reversal signal, a trading order will be generated. This can filter out some invalid reversal signals and seize the rebound trend opportunity after the reversal.
## Advantages
The biggest advantage of this strategy is that it makes reasonable use of the advantages of the two indicators for complementary confirmation, which can effectively filter out invalid signals and enhance the reliability of the signals.
The moving average reversal indicator itself is prone to produce false signals. If you rely solely on it to judge, it is easy to chase highs and sell lows. The introduction of price disengagement indicators for combination can avoid reversal operations in non-ideal shock ranges.
The parameter setting of the price departure indicator also determines that it only identifies fluctuations in shorter periods, which is very consistent with the judgment of moving average reversal and can identify reasonable reversal opportunities.
## Risk
This strategy mainly involves the following risks:
1. Insufficient rebound strength makes it easy to get stuck
Moving average reversals tend to occur in consolidation and shock ranges. If the rebound is not strong enough, it is easy to pull back again and hit the stop loss line, making it impossible to make a profit.
2. Improper parameter settings
If the parameter setting of the price deviation indicator is too large, medium and long-term cyclical trends will be identified; if it is too small, it will increase the risk of misjudgment. Careful testing of different varieties is required.
3. Unexpected events lead to reversal failure
The intervention of major breaking news events will disrupt the original trend judgment and cause the reversal signal to fail. This requires paying attention to fundamental news and avoiding blind trading when news events occur.
## Optimization direction
This strategy can be further optimized from the following points:
1. Add stop loss mechanism
Properly setting trailing stop loss or time stop loss can control single losses.
2. Combined with trading volume indicators
Increasing the confirmation of trading volume, such as sending a signal only when the average trading volume is exceeded, can avoid invalid breakthroughs due to insufficient volume and energy.
3. Dynamic parameter optimization
Dynamically optimize the parameters according to the market stage, appropriately relax the parameters when the trend is obvious, and tighten the parameters during shocks.
4. Use machine learning methods for dynamic optimization
Use machine learning methods such as random forest to evaluate and select parameter combinations to achieve dynamic intelligent optimization.
## Summarize
This strategy better combines the advantages of the two indicators and seizes the rebound trend at the reversal point. Although there are still problems such as quilt cover and parameter optimization, the overall idea is clear and the logic is reasonable, which is worthy of further testing and optimization to achieve stable profits.
||

## Overview

This strategy combines two indicators: moving average reversal and price detrend oscillator to generate trading signals and catch the rebound trend after cycle reversals.

## Principles 

This strategy mainly utilizes the following two technical indicators for trading signal judgment:

1. Moving Average Reversal

    It calculates the price uptrend or downtrend in the past two days combined with the fast line K value to determine if a reversal signal occurs. When the price keeps rising in the past two days and the fast line K value is lower than the slow line K value, a buy signal is generated. When the price keeps falling in the past two days and the fast line K value is higher than the slow line K value, a sell signal is generated.

2. Price Detrend Oscillator

    The Detrend Price Oscillator draws a horizontal moving average line and identifies price cycles based on the relationship between the price and the line. It filters out trends longer than the calculation period, thus revealing hidden short-term fluctuations. When the price is above the moving average line, it is a buy signal. When the price is below the line, it is a sell signal.

This strategy combines the signals of the two indicators. That is, when a moving average reversal signal appears and the price detrend oscillator also gives a confirming reversal signal, a trading order is generated. This can filter out some invalid reversal signals and catch the rebound trend after reversals.

## Advantages

The biggest advantage of this strategy is that it makes good use of the strengths of the two indicators for complementary confirmation, which can effectively filter out invalid signals and increase signal reliability.

The moving average reversal indicator itself tends to generate false signals. Relying solely on it for judgments tends to chase tops and hit bottoms. The introduction of the price detrend oscillator for combination can avoid reversal operations in non-ideal oscillation zones. 

The parameter settings of the price detrend oscillator also determine that it only identifies short-term fluctuations, which matches very well with the judgment of the moving average reversal and can identify reasonable reversal timing.

## Risks

The main risks of this strategy include:

1. Insufficient rebound momentum, tends to be trapped

Moving average reversals tend to occur in sideways ranges. If the rebound momentum is insufficient, it is likely to callback and touch the stop loss again, failing to profit.

2. Improper parameter settings  

If the parameters of the price detrend oscillator are set too large, it will identify medium- and long-term trends; if too small, it will increase misjudgment risks. Parameters need to be carefully tested for different products.

3. Reversal failures due to sudden events

Major news events can disrupt existing trend judgments, resulting in failure of reversal signals. It is necessary to pay attention to fundamentals and avoid trading blindly when news events occur.

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Add stop loss mechanisms

Reasonably set stop loss or time stop loss to control single loss.

2. Combine with volume indicators

Add volume confirmation, such as issuing signals only when breaking through the average volume, to avoid ineffective breakthroughs due to insufficient momentum.

3. Dynamic parameter optimization

Dynamically optimize parameters according to market conditions, relax parameters appropriately during obvious trends, and tighten parameters during consolidations.

4. Use machine learning methods for dynamic optimization

Use machine learning methods like random forest to evaluate and select parameter combinations to achieve dynamic intelligent optimization.

## Summary

This strategy combines the strengths of two indicators reasonably to catch the rebound trend at reversal points. Although problems like being trapped and parameter optimization remain, the overall idea is clear and logical. It is worth further testing and optimization to achieve stable profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|14|LengthDPO|
|v_input_6|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-15 00:00:00
end: 2023-11-14 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 30/12/2019
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
// The Detrend Price Osc indicator is similar to a moving average, 
// in that it filters out trends in prices to more easily identify 
// cycles. The indicator is an attempt to define cycles in a trend 
// by drawing a moving average as a horizontal straight line and 
// placing prices along the line according to their relation to a 
// moving average. It provides a means of identifying underlying 
// cycles not apparent when the moving average is viewed within a 
// price chart. Cycles of a longer duration than the Length (number 
// of bars used to calculate the Detrend Price Osc) are effectively 
// filtered or removed by the oscillator.
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

DPO(Length) =>
    pos = 0.0
    xPrice = close
    xsma = sma(xPrice, Length)
    nRes = xPrice - xsma
    pos := iff(nRes > 0, 1,
    	     iff(nRes < 0, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Detrended Price Oscillator", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
LengthDPO = input(14, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posDPO = DPO(LengthDPO)
pos = iff(posReversal123 == 1 and posDPO == 1 , 1,
	   iff(posReversal123 == -1 and posDPO == -1, -1, 0)) 
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

https://www.fmz.com/strategy/432231

> Last Modified

2023-11-15 17:13:18

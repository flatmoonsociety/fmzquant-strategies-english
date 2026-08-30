
> Name

Multi-indicator-Collision-Reversal-Strategy Multi-indicator-Collision-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/6f88f18cd243b479b160d3afb40f871f7f7407b364323b92d87c7d324a526201.png)
[trans]

## Overview
This strategy designs an efficient reversal strategy by combining dual indicator signals. First, it integrates a reversal signal based on the stochastic indicator and a system that tracks the number of consecutive rising days. The strategy will only place an order when both signals trigger a buy or sell at the same time. This multiple indicator collision mechanism can effectively filter out some invalid signals, thereby improving the strategy winning rate.
## Strategy Principle
This strategy consists of two parts of indicator signals. The first part is the 123 reversal system, which observes the closing price changes of the last two days, as well as the slow stochastic value with a standard deviation of 3. Specifically, when the closing price of the current day is lower than the previous two days, today's closing price is higher than yesterday's closing price, and the 9-day slow stochastic is below 50, go long; conversely, when today's closing price is lower than yesterday and the fast stochastic is above 50, go short.
The second part of the indicator tracks the number of consecutive rising days in the last n days. If the last n days have been rising, output 1, otherwise output 0. This indicator is used to identify trend formation.
Finally, this strategy will only execute a trade if the 123 reversal signal and the number of consecutive rising days are both buy or sell. This multi-index collision weighting method can filter out some invalid signals, thereby improving the overall stability of the strategy.
## Advantage Analysis
The biggest advantage of this multi-index combination strategy is that it can improve the reliability of signals and filter out some invalid signals. Specifically, it has the following main advantages:
1. 123 reversal itself has a certain screening function, which can avoid being confused by noise. Combined with tracking the rising days indicator, you can further identify trends and avoid reversal rebounds.
2. The stochastic indicator parameters are set to compare the fast and slow lines on the 9th and 3rd, which can smooth parameter changes, avoid being confused by short-term fluctuations, and enhance stability.
3. Customizable parameters, including stoch indicator parameters, rising days, etc., can be adjusted for different markets to improve adaptability.
4. You can choose to reverse the trading direction, there are many short-selling opportunities, and you can make profits through reverse operations.
## Risk Analysis
This strategy also has some risks, mainly focusing on the following aspects:
1. Although the combination of multiple indicators can improve signal accuracy, it may also miss some opportunities and reduce the upper limit of strategy income.
2. The reversal signal itself has the risk of being trapped, and stop loss needs to be set to control the risk.
3. Improper parameter settings will also affect strategy performance, and parameters need to be adjusted according to different markets.
4. Holding for a long time without stopping losses in time, or chasing stock reversals will also bring certain risks.
Correspondingly, the following measures can be taken to control risks:
1. Relax parameter conditions appropriately to retain more trading opportunities.
2. Set a stop loss point to control a single loss.
3. Optimize parameters and formulate parameter rules for different markets.
4. Avoid holding a single stock for a long time and maintain capital liquidity.
## Optimization direction
This multi-index reversal strategy still has a lot of room for optimization, which can mainly start from the following aspects:
1. Test more indicator combinations and find more matching indicator matching strategies.
2. Use machine learning algorithms to automatically optimize indicator parameters.
3. Add stop loss and take profit conditions to make the strategy more robust.
4. In the trend indicator section, you can test indicators of different time periods.
5. Evaluate the suitability of different markets such as stock indices, foreign exchange, precious metals, cryptocurrencies, etc.
6. Design compound strategies, evaluate multiple markets at the same time, and dynamically adjust positions.
## Summarize
This strategy uses a clever combination of multiple indicators to design a reversal trading strategy with both high efficiency and stability. Compared with a single indicator, this multiple indicator collision mechanism can effectively filter false signals. At the same time, this strategy also updates the traditional reversal strategy and adds new trend indicators as signal confirmation. Through a series of optimization measures such as parameter optimization, stop loss setting, and adaptation to different markets, this strategy can become a powerful tool for quantitative trading.
||

## Overview  

This strategy is designed as an efficient reversal strategy by combining dual-indicator signals. It integrates a reversal signal based on stochastic indicators and a system that tracks the number of consecutive up days. The strategy will only place orders when both signals trigger buy or sell concurrently. This multi-indicator collision mechanism can effectively filter out some invalid signals and improve the win rate.  

## Principle  

The strategy consists of two parts. The first part is the 123 reversal system, which observes the change in closing prices over the past two days, as well as the value of a 3-period slow stochastic indicator. Specifically, when yesterday's close is lower than the previous 2 days and today's close is higher than yesterday's, and the 9-period slow stochastic is below 50, go long; conversely, when today's close is below yesterday's and the fast stochastic is above 50, go short.  

The second indicator tracks the number of consecutive up days recently over n days. If the last n days are all rising, it outputs 1, otherwise 0. This indicator is used to identify trend formation.

Finally, the strategy will only execute trades when the 123 reversal signal and the number of consecutive up days both show buy or sell status concurrently. This multi-indicator collision weighted approach can filter out some invalid signals and improve the overall stability of the strategy.   

## Advantage Analysis

The biggest advantage of this multi-indicator combo strategy is that it can improve the reliability of signals by filtering out some invalid ones. Specifically, there are main advantages:

1. The 123 reversal itself has some screening capability to avoid noise interference. Combined with the consecutive day counter, it can further identify trends and avoid reversal bounces.  

2. The stochastic parameters of 9-day and 3-day fast and slow lines comparison can smooth parameter changes and avoid short-term fluctuations and enhance stability.

3. Customizable parameters including stoch, number of rising days parameters allows adaptation to different markets.  

4. Tradable both ways providing more shorting opportunities.

## Risk Analysis   

There are also some risks to this strategy:   

1. The multi-indicator combo, while enhancing signal accuracy, may also miss some opportunities and limit profits.

2. Reversal signals have inherent risks of being trapped, requiring stop losses to control risk.  

3. Improper parameter settings can affect performance requiring adjustment between markets.  

4. Holding long-term positions without timely stop loss or chasing stock reversals also carries risks.

Accordingly, the following measures can be taken to mitigate risks:

1. Relax parameter conditions appropriately to retain more trading opportunities.  

2. Set stop loss points to limit per trade loss.

3. Optimize parameters and set parameter rules for different markets.  

4. Avoid holding single stocks long-term and maintain liquidity.

## Optimization Directions   

There is still great potential to optimize this multi-indicator reversal strategy, mainly from the following aspects:  

1. Test more indicator combinations to find better matches.  

2. Use machine learning algorithms to auto optimize parameters.

3. Add stop loss and take profit conditions for more robustness.  

4. Test different timeframes in the trend indicator part.  

5. Evaluate applicability across stock indices, forex, commodities,cryptocurrencies.  

6. Design compounding strategies that dynamically adjust allocations across multiple markets concurrently.  

## Summary  

This strategy skillfully combines multiple indicators to design an efficient yet stable reversal trading strategy. Compared to single indicators, the multi-indicator collision mechanism effectively filters false signals. Meanwhile, this strategy also updates traditional reversal methods by adding new trend indicators for signal confirmation. With parameter optimization, stop losses, adaptation across markets, and more, this becomes a powerful quantitative trading toolkit.  
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- N Bars Up ----|
|v_input_7|4|nLength|
|v_input_8|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-28 00:00:00
end: 2024-01-03 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 26/03/2021
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
// Evaluates for n number of consecutive higher closes. Returns a value 
// of 1 when the condition is true or 0 when false.
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


NBU(nLength) =>
    pos = 0.0
    nCounter = 0
    nCounter :=  iff(close[1] >= open[1], nz(nCounter[1],0)+1,
                  iff(close[1] < open[1], 0, nCounter))
    C1 = iff(nCounter >= nLength, 1, 0)
    posprice = 0.0
    posprice := iff(C1== 1, close, nz(posprice[1], 0)) 
    pos := iff(posprice > 0, 1, 0)
    pos

strategy(title="Combo Backtest 123 Reversal & N Bars Up", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- N Bars Up ----")
nLength = input(4, minval=1)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posNBU = NBU(nLength)
pos = iff(posReversal123 == 1 and posNBU == 1 , 1,
	   iff(posReversal123 == -1 and posNBU == -1, -1, 0)) 
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

https://www.fmz.com/strategy/437694

> Last Modified

2024-01-04 18:02:12

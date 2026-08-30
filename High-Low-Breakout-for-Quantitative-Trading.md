
> Name

High-Low-Breakout-for-Quantitative-Trading
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/195f8a278bf14e17775.png)

[trans]

## Overview
Fusion strategy is a quantitative trading strategy that combines the 123 pattern reversal strategy and the high and low breakthrough strategy. This strategy realizes the combination of capital advantages in multiple time periods through comprehensive judgment of indicator signals in different time periods, and achieves the goal of obtaining excess returns in the medium and long term.
## Strategy Principle
The fusion strategy consists of two parts:
1. 123 reversal strategy
This strategy comes from the ideas on page 183 of Ulf Jensen's book "How I Tripled My Gains in the Futures Market". It determines the relationship between the price's closing price for two consecutive days and the closing price of the previous day, combined with the Stochastic indicator to determine the overbought and oversold conditions of the market, and generates buy and sell signals. Specifically, when the closing price for 2 consecutive days is higher than the closing price of the previous day, and the Stochastic Slow indicator is lower than 50, a buy signal is generated; when the closing price for 2 consecutive days is lower than the closing price of the previous day, and the Stochastic Fast indicator is higher than 50, a sell signal is generated. This strategy uses the Stochastic indicator to determine the overbought and oversold conditions of the market and avoid buying at high levels and selling at low levels.
2. High and low breakthrough strategy
This strategy determines trading signals by determining whether price breaks through the high and low levels of different cycles. It calculates the highest and lowest prices of the current period and past periods, and generates a buy signal when the price breaks through the highest price, and a sell signal when it breaks through the lowest price. The advantage of this strategy is that it can identify the morphological characteristics of different periodic lines and enter the market earlier when the trend is formed.
The fusion strategy combines the above two strategies. When the signal directions of the two strategies are consistent, an actual trading signal is generated. This can filter out some invalid signals caused by errors in the judgment of a single strategy and improve the reliability of the signal.
## Strategic Advantages
1. Comprehensive judgment in multiple time periods to improve signal accuracy
This strategy integrates the morphological characteristics of the daily line and higher time periods, which can improve the accuracy of judgment of trading signals and avoid being misled by short-term market fluctuations.
2. Make full use of the overbought and oversold judgment of the Stochastic indicator
The application of the StochasticSlow indicator avoids the rush to buy in the overbought area, and the application of the StochasticFast indicator avoids the rush to sell in the oversold area, reducing unnecessary losses.
3. Capture trend characteristics in time to reduce the probability of missing opportunities
The high-low breakthrough strategy can identify key price breakthrough areas in longer-term cycles, enter the trend earlier, and reduce the probability of missing opportunities.
4. Multi-strategy combination, flexible optimization
The strategy consists of multiple sub-strategies and has a large optimization space. It can be optimized by adjusting the sub-strategy parameters or introducing new sub-strategies to make the strategy more stable and reliable.
5. The strategy logic is clear and easy to understand
The strategy structure is simple and clear, easy to understand and modify, and also convenient for later maintenance.
## Strategy Risk
1. Multiple time periods comprehensively increase signal lag
Although comprehensive judgment in multiple time periods can improve the accuracy of signals, it will also increase the lag of signals to a certain extent, and short-term trading opportunities may be missed.
2. The 123 pattern cannot identify longer-term trend reversals.
The 123 reversal strategy only bases its judgment on the market conditions of recent days and cannot identify key trend reversal points in a longer period of time.
3. Improper setting of period parameters may lead to false signals
Stochastic indicators, high and low breakouts, and improperly set cycle parameters may result in too many false trading signals.
4. Based only on technical indicators, poor adaptability to special market conditions
This strategy is only based on technical indicators, does not consider fundamental information, and has poor adaptability when major black swan events occur.
Solutions corresponding to risks:
1. Appropriately shorten the calculation cycle and reduce signal lag.
2. Try to introduce longer period indicators or patterns as filters.
3. Optimize parameter settings and test parameter robustness in backtesting.
4. Consider filtering signals based on fundamental factors.
## Strategy optimization direction
1. Test and optimize the parameters of each sub-strategy to make it more robust.
2. Add other auxiliary decision-making logic, such as fundamentals, capital flow and other indicators for combination.
3. Introduce a stop-loss strategy to control the maximum loss in a single transaction.
4. Refine parameters for specific varieties to improve the suitability of the strategy for that variety.
5. Add machine learning models to assist decision-making.
## Summarize
To sum up, the fusion strategy integrates the advantages of technical indicators on multiple time scales and aims to improve the accuracy and timeliness of signal judgment. Compared with a single technical indicator strategy, it has a sharper trend judgment ability and more robust signal generation. However, this strategy also has certain hysteresis and weak adaptability to special market conditions. In the future, more auxiliary tools can be introduced to optimize parameter settings and improve the stability and profitability of the strategy.
||
## Overview

The Fusion strategy combines a 123 reversal pattern strategy and a high low breakout strategy into a quantitative trading system. By synthesizing indicator signals across different timeframes, it aims to achieve multi-timeframe capital advantage and generate excess returns in the medium to long term.

## Strategy Logic

The Fusion strategy consists of two components:

1. 123 Reversal Strategy
This strategy originates from the idea on p183 of the book "How I Tripled My Money in the Futures Market" by Ulf Jensen. It generates trading signals by examining the relationship between the closing prices of the past two days and the previous day, together with the Stochastic indicator to gauge overbought and oversold market conditions. Specifically, a buy signal is generated when the closing prices of two consecutive days are higher than the previous day, and the Stochastic Slow indicator is below 50. A sell signal is generated when the closing prices of two consecutive days are lower than the previous day, and the Stochastic Fast indicator is above 50. By incorporating the Stochastic indicator, this strategy avoids buying at market tops and selling at bottoms.

2. High Low Breakout Strategy 
This strategy identifies trading signals by detecting price breakouts beyond previous high/low levels over different time periods. It calculates the highest high and lowest low over the current and previous periods and generates buy signals when price breaks above the high, and sell signals when price breaks below the low. The advantage of this strategy is its ability to identify trend pattern changes in higher timeframes, allowing earlier entry.

The Fusion strategy combines the signals from the above two strategies, and generates actual trading signals only when the signal directions align. This filters out some false signals caused by errors in a single strategy and improves signal reliability.

## Advantages of the Strategy

1. Multi-timeframe synthesis improves signal accuracy
The integration of daily and higher timeframe patterns enhances accuracy of trading signal generation, avoiding distraction from short-term market noises.

2. Fully utilizes the overbought/oversold judgement of Stochastic 
The use of Stochastic Slow indicator prevents eager buying at overbought zones. The Stochastic Fast indicator prevents eager selling at oversold zones. Unnecessary losses are reduced.

3. Timely catches trend patterns, lowering missing out opportunities
The high low breakout strategy identifies trend initiation in higher timeframes earlier, reducing missed trading opportunities.

4. Flexible optimization with multiple sub-strategies
With multiple sub-strategies, huge optimization space allows parameter tuning of sub-strategies or introducing new ones to make the strategy more stable and reliable.

5. Simple and clear logic
The straightforward structure and logic make the strategy easy to understand, modify and maintain in the future.

## Risks of the Strategy

1. Multi-timeframe synthesis causes signal lag
Although accuracy is improved, combining signals across timeframes induces a lag and may miss short-term trading chances.

2. 123 patterns cannot identify longer timeframe trend reversals
The 123 reversal strategy only looks at recent days and misses key reversal points in longer timeframes. 

3. Wrong parameter settings may cause false signals
Bad parameter tuning of the Stochastic and breakout periods could result in excessive false signals.

4. Purely technical, weak adaptivity to extreme events
Without considering fundamentals, the strategy adapts poorly to black swan events.

Corresponding solutions:

1. Shorten calculation periods properly to reduce lag.

2. Try introducing longer-term indicators or patterns as filters.

3. Optimize parameters and test robustness thoroughly in backtests. 

4. Consider incorporating fundamental factors for signal filtering.

## Directions for Optimization

1. Test and optimize parameters of sub-strategies for robustness.

2. Incorporate additional signals like fundamentals, money flow etc. 

3. Introduce stop loss to limit max loss per trade.

4. Fine tune parameters for specific products to improve adaptiveness.

5. Assist with machine learning models.

## Conclusion

In summary, the Fusion strategy combines the advantages of multi-timeframe technical indicators, aiming for more accurate and timely signal generation. Compared to single indicator strategies, it has superior trend sensing ability and more robust signal production. But it also suffers from lags and inadequate adaptivity to extreme events. Future improvements could come from more auxiliary tools, better parameter optimization and upgrading stability and profitability.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|D|Resolution|
|v_input_6|true|LookBack|
|v_input_7|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-10 00:00:00
end: 2023-11-09 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 25/11/2020
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
// This script shows a high and low period value.
//    Width - width of lines
//    SelectPeriod - Day or Week or Month and etc.
//    LookBack - Shift levels 0 - current period, 1 - previous and etc. 
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

    
HLL(LookBack, SelectPeriod) =>
    pos = 0.0
    xHigh  = security(syminfo.tickerid, SelectPeriod, high[LookBack])
    xLow   = security(syminfo.tickerid, SelectPeriod, low[LookBack])
    vS1 = xHigh
    vR1 = xLow
    pos := iff(close > vR1, 1,
             iff(close < vS1, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & High and Low Levels", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
SelectPeriod = input(title="Resolution", type=input.resolution, defval="D")
LookBack = input(1,  minval=0)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posHLL = HLL(LookBack, SelectPeriod)
pos = iff(posReversal123 == 1 and posHLL == 1 , 1,
	   iff(posReversal123 == -1 and posHLL == -1, -1, 0)) 
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

https://www.fmz.com/strategy/431662

> Last Modified

2023-11-10 11:09:28

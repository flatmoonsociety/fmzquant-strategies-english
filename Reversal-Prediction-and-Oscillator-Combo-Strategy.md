
> Name

Reversal-Prediction-and-Oscillator-Combo-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a combination of a reversal strategy and an oscillator strategy, aiming to obtain more reliable trading signals. It combines the reversal prediction strategy and the Chande prediction oscillator strategy, and executes trades when both strategies send out buy or sell signals at the same time.
## Strategy Principle
1. Reversal of prediction strategy
- Use the Stochastic oscillator indicator to determine overbought and oversold conditions
- When the price reverses at the closing price of two consecutive bars and the Stochastic oscillator indicator shows an overbought or oversold signal, perform reverse operations.
2. Chande Prediction Oscillator Strategy    
- Predict prices using linear regression analysis
- The oscillator curve is equal to the difference between the closing price and the predicted price
- When the actual price deviates significantly from the predicted price, a trading signal is generated
3. Strategy logic
- Simultaneously calculate signals for reversal prediction strategies and Chande prediction oscillator strategies
- Only when the signals of the two strategies are consistent, that is, both are buy signals or sell signals, the actual trading signal is generated
- Filter out false signals that may appear with a single strategy through combination to improve signal reliability
## Strategic advantage analysis
1. Combine multiple strategies to comprehensively judge the market with higher reliability
2. Filter out false signals that may appear in a single technical indicator
3. The reversal prediction strategy can capture short-term reversal opportunities.
4. The Chande forecast oscillator accurately determines the long-term trend.
5. Stochastic oscillator indicator parameters are adjustable and highly adaptable.
6. Integrate multiple analysis methods to seize trading opportunities in different dimensions
## Risk Analysis
1. Although the combination strategy improves reliability, the frequency of signal generation decreases.
2. Each strategy parameter needs to be optimized at the same time, which is relatively complicated.
3. It is difficult to grasp the timing of reversal, and there is a risk of loss
4. Linear regression prediction is not suitable for markets with violent price fluctuations.
5. Pay attention to whether the stock price deviates from the Stochastic oscillator
6. Insufficient backtest data and doubtful results of real offer
## Strategy optimization direction
1. Optimize the Stochastic oscillator parameters and shorten the K-line and D-line cycles
2. Adjust the linear regression period and test more period parameters
3. Add stop loss strategy to reduce single loss
4. Modify the position opening logic and wait for the Stochastic oscillator indicator to completely enter the overbought and oversold zone.
5. Add statistical feature analysis of trading varieties
6. Combine with more indicators, such as MACD, etc., to provide more dimensional judgments
## Summarize
This strategy comprehensively uses a variety of analysis methods to improve signal quality through combination, while taking into account both the discovery of short-term reversals and the judgment of general trends, so as to seize more comprehensive trading opportunities. However, you need to pay attention to the actual effect and adjust the parameters appropriately. This strategy idea can be extended to more combinations of indicators and strategies, and can also be used to guide actual trading operations. Overall, this strategy has certain innovation and reference value.
|| 

## Overview

This strategy combines reversal and oscillator strategies to obtain more reliable trading signals. It incorporates the reversal prediction strategy and Chande Forecast Oscillator strategy, executing trades when both strategies generate concurrent buy or sell signals.

## Strategy Logic

1. Reversal Prediction Strategy

    - Use Stochastic oscillator to identify overbought and oversold conditions
    
    - Take counter directional trades when price closes reversal over 2 bars while Stochastic oscillator reaches overbought or oversold levels

2. Chande Forecast Oscillator Strategy

    - Use linear regression analysis to forecast prices
    
    - Oscillator plots the percentage difference between closing price and forecast price

    - Generate trading signals when actual price deviates significantly from forecast price
    
3. Strategy Rules

    - Concurrently compute signals from both strategies

    - Only generate actual trading signals when both strategies agree on buy or sell

    - Combination filters false signals from individual strategies, improving reliability
    
## Advantage Analysis 

1. Combining multiple strategies provides more robust market assessment

2. Filters out false signals that may occur in single indicators

3. Reversal strategy captures short-term reversal opportunities

4. Chande oscillator accurately judges long-term trends

5. Flexible Stochastic oscillator parameters adaptable to changing markets

6. Blends analysis techniques to capitalize on diverse trading prospects

## Risk Analysis

1. Although more reliable, combo strategies reduce signal frequency 

2. Requires complex optimization of multiple strategy parameters

3. Difficult to time reversals, risks of losses exist

4. Linear regression forecast ineffective when prices are volatile

5. Watch for price divergence from Stochastic oscillator 

6. Backtest data insufficient, live performance uncertain

## Improvement Opportunities

1. Optimize Stochastic oscillator by reducing K and D periods

2. Test more linear regression periods to find optimal

3. Add stop loss to limit losses

4. Tweak logic to await Stochastic oscillator reaches extremes

5. Analyze statistical properties of trading instruments 

6. Incorporate more indicators like MACD for robustness

## Summary

This strategy synthesizes multiple analytical techniques and improves signal quality through combination, capturing both short-term reversals and long-term trends. But live performance needs to be validated and parameters tuned accordingly. The conceptual framework can be extended to more indicators and strategies, providing practical trading guidance. Overall the strategy offers meaningful innovations and references.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|Length|
|v_input_2|true|KSmoothing|
|v_input_3|3|DLength|
|v_input_4|50|Level|
|v_input_5|14|LengthCFO|
|v_input_6|false|Offset|
|v_input_7|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-09 00:00:00
end: 2023-10-09 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 08/08/2019
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
// The Chande Forecast Oscillator developed by Tushar Chande The Forecast 
// Oscillator plots the percentage difference between the closing price and 
// the n-period linear regression forecasted price. The oscillator is above 
// zero when the forecast price is greater than the closing price and less 
// than zero if it is below.
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

ChandeForecastOscillator(Length, Offset) =>
    pos = 0
    xLG = linreg(close, Length, Offset)
    xCFO = ((close -xLG) * 100) / close
    pos := iff(xCFO > 0, 1,
           iff(xCFO < 0, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & Chande Forecast Oscillator", shorttitle="Combo", overlay = true)
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
LengthCFO = input(14, minval=1)
Offset = input(0)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posChandeForecastOscillator = ChandeForecastOscillator(LengthCFO, Offset)
pos = iff(posReversal123 == 1 and posChandeForecastOscillator == 1 , 1,
	   iff(posReversal123 == -1 and posChandeForecastOscillator == -1, -1, 0)) 
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

https://www.fmz.com/strategy/428855

> Last Modified

2023-10-10 10:39:44

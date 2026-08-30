
> Name

Multi-Timeframe-Stochastic-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/75b950b619508c6927d26f1a67778d375f3669ec5995af76498e1bf342813dfb.png)
[trans]
## Overview
The multi-time frame stochastic strategy (MTF Stochastic Strategy) is a quantitative trading strategy based on the stochastic index. It uses both the current time frame and the stochastic exponential moving average of higher time frames to achieve combination trading of trend following and trend reversal.
## Strategy Principle
The core indicators of this strategy are the stochastic index K-line and D-line. The K line reflects recent price momentum, and the D line is the moving average of the K line. Their relative position and direction can determine price trends and possible reversals.
Specifically, when the short-term K line breaks through the mid-term D line from bottom to top, it means that the price has the momentum to break upward in the short term; when the short-term K line breaks through the mid-term D line from top to bottom, it means that the price has downward pressure to break through in the short term.
This strategy uses the stochastic index indicator of two time frames to realize the confirmation and filtering of trading signals. Stochastics on higher time frames are used to confirm trend direction, while stochastics on the current time frame are used to find short-term breakout points for trading entry.
When the stochastic indicator of the higher time frame confirms that it is in an upward trend, and the stochastic indicator of the current time frame shows that the price has an upward breakthrough, go long; when the stochastic indicator of the higher time frame confirms a downward trend, and the stochastic indicator of the current time frame shows that the price has a downward breakthrough, go short.
## Advantage Analysis
This strategy combines multi-time frame indicators and current breakthroughs to effectively filter out market noise and lock in profitable trades with a higher probability. The specific advantages are as follows:
1. A higher time frame ensures that you only trade in the direction of the trend, which can reduce the frequency of unnecessary switching and the number of losses;
2. The current time frame ensures that short-term reversals in trends can be captured with lower risk, allowing for more accurate and timely trading entry and exit.
3. The combination of double stochastic indicators increases the accuracy of signals and reduces the probability of false signals.
## Risk Analysis
This strategy also has some risks, mainly reflected in the following aspects:
1. When the market suddenly reverses, indicators with a higher time frame may delay identifying the new trend, causing the strategy to delay switching directions and increase losses. Time frame parameters need to be optimized to ensure that sufficient and timely market information can be obtained.
2. The current time frame indicator is too sensitive and may increase strategy trading frequency and transaction costs. Parameters need to be adjusted appropriately to ensure that unimportant market noise is filtered out.  
3. Although the double stochastic indicator combination increases the signal accuracy, it also delays the reaction speed. If the market fluctuates violently, you may miss the best entry point.
## Optimization direction
The main optimization directions of this strategy include:
1. Optimize the smoothing factors of higher time frame indicators so that they can reflect new trend directions in a timely manner;
2. Adjust the current time frame indicator parameters and set a reasonable breakthrough threshold to filter out noise signals;
3. Test the effects of different time frame combinations and find the best balance point;
4. Add a stop-loss strategy to control the risk of single loss.
## Summarize
The multi-time frame stochastic exponential moving average strategy is a typical trend following strategy. It simultaneously uses the stochastic index indicator under two time scales to achieve accurate grasp of the market. Through parameter optimization, the stability and profitability of the strategy can be further enhanced.
||

## Overview

The Multi-Timeframe Stochastic Strategy is a quantitative trading strategy based on the Stochastic oscillator indicator. It utilizes stochastic moving averages across both the current and higher timeframes to combine trend following and mean reversion trading.  

## Strategy Logic

The core indicators of this strategy are the Stochastic K and D lines. The K line reflects recent price momentum while the D line is a moving average of the K line. Their relative position and direction can determine price trends and potential reversals. 

Specifically, when the short-term K line crosses above the mid-term D line from below, it signals upward momentum in prices short-term. And when the K line crosses below the D line from above, it signals downside breakdown pressure short-term.

This strategy employs stochastic indicators across two timeframes to confirm signals and filter noise. The higher timeframe stochastic defines the overall trend while the current timeframe stochastic identifies short-term inflection points to time entries.

When the higher timeframe stochastic confirms an uptrend and the current timeframe stochastic shows an upside breakout, a long position is taken. When the higher timeframe stochastic indicates a downtrend and the current stochastic signals a downside breakdown, a short position is initiated.

## Advantage Analysis 

By combining multi-timeframe indicators and current momentum, this strategy can effectively filter out market noise and capture high-probability profitable trades. The main advantages are:

1. Higher timeframe ensures trading with the trend to minimize unnecessary whipaws and losing trades.
2. Current timeframe allows low-risk entries to capture short-term reversals within the trend.  
3. Dual stochastic indicators improve signal accuracy and reduce false signals.

## Risk Analysis

There are some risks to consider with this strategy:

1. Sudden trend reversals may not be captured early by the higher timeframe indicator, increasing losses from late directional switches. Timeframe parameters need to be optimized to get sufficiently timely market data.
2. The current timeframe indicator can be too sensitive, increasing trade frequency and costs. Parameters need calibration to filter insignificant noise.
3. Although the dual stochastic enhances accuracy, it also slows down reaction time. Fast market moves could lead to missing optimal entry points.  

## Optimization Directions

The main optimization directions include:

1. Optimizing the higher timeframe stochastic smoothers to adapt faster to new trends. 
2. Adjusting the current timeframe parameters and breakout thresholds to reduce false signals.
3. Testing timeframe combinations to find the optimal balance.
4. Incorporating stop-loss strategies to control downside risk per trade.


## Conclusion

The Multi-Timeframe Stochastic Strategy is a typical trend following system. By utilizing stochastic indicators across two timescales, it aims to precisely capture market movements. Further optimizations can enhance stability and profitability.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|11|Length for Main Stochastic|
|v_input_2|3|SmoothK for Main Stochastic|
|v_input_3|3|SmoothD for Main Stochastic|
|v_input_4|80|Upper Line Value?|
|v_input_5|20|Lower Line Value?|
|v_input_6|50|Trialing step value|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-22 00:00:00
end: 2024-02-28 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("MTF stochastic strategy", overlay=false,pyramiding=3,default_qty_type=strategy.percent_of_equity,default_qty_value=100,currency=currency.USD)
//
//this strategy is inspired to bobby thread in forexfactory forum
//
len = input(11, minval=1, title="Length for Main Stochastic") 
smoothK = input(3, minval=1, title="SmoothK for Main Stochastic")
smoothD = input(3, minval=1, title="SmoothD for Main Stochastic")
upLine = input(80, minval=50, maxval=90, title="Upper Line Value?")
lowLine = input(20, minval=10, maxval=50, title="Lower Line Value?")
trailStep=input(50,minval=10,title="Trialing step value")

// current stochastic calculation
k = sma(stoch(close, high, low, len), smoothK)
d = sma(k, smoothD)

//mtf stochastic calculation smoothed with period

mtfK= sma(stoch(close, high, low, len), smoothK*3)
mtfD= sma(k, smoothD*3)

plot(k,"current TF k",black,style=linebr)
plot(d,"current TF d",gray,style=linebr)
plot(mtfK,"MTF TF k",red,style=line)
plot(mtfD,"Multi TF d",green,style=line)
hline(upLine)
hline(50)
hline(lowLine)

longCondition = crossover(mtfK, 50) and k>50 and change(k,1)>0 and k>d and mtfK>mtfD
if (longCondition)
    strategy.entry("Lungo", strategy.long)

shortCondition = crossunder(mtfD, 50) and k<50 and change(k,1)<0 and k<d and mtfK<mtfD
if (shortCondition)
    strategy.entry("Corto", strategy.short)
    
exitlong=crossunder(mtfD, upLine)
exitshort=crossover(mtfK, lowLine)

if (exitlong)
    strategy.exit("Esci lungo","Lungo",trail_points=trailStep)
if (exitshort)
    strategy.exit("Esci corto","Corto",trail_points=trailStep)
    


```

> Detail

https://www.fmz.com/strategy/443110

> Last Modified

2024-02-29 12:11:23

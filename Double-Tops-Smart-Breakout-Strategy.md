
> Name

Double-Tops-Smart-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The Double Joint Smart Breakout Strategy is a combo strategy that combines the 123 Reversal Strategy and the Pivot Detector Oscillator Strategy. This strategy mainly uses the double-joint pattern to determine potential trend reversal points, and combines pivot detection indicators to filter out false breakthrough operations to achieve breakthrough operations that capture trend turning points at important technical positions.
## Principle
The strategy consists of two parts:
1. 123 reversal strategy
The 123 reversal strategy comes from page 183 of Ulf Jensen's book "How I Twice the Value in the Futures Market". This strategy is a reversal strategy.
The specific logic is: when the closing price is higher than the closing price of the previous day for 2 consecutive days, and the 9-day stochastic slow line is lower than 50, go long; when the closing price is lower than the previous day's closing price for 2 consecutive days, and the 9-day stochastic fast line is higher than 50, go short.
2. Pivot Detector Oscillator Strategy
The pivot detection oscillator strategy was proposed by Giorgos E. Siligardos, and the related article was published in Stocks & Commodities magazine in September 2009.
This strategy uses a combination of moving averages and RSI indicators to determine the oscillations when prices are close to the upper and lower rails and generate trading signals. The specific calculation formula is as follows:
    
```
    当价格 > 移动均线时:
        指标值 = (RSI值 - 35) / (85 - 35) 
    当价格 <= 移动均线时:
        指标值 = (RSI值 - 20) / (70 - 20)

    如果指标值 > 50, 做多
    如果指标值 < 50, 做空
    
```

Combining the two strategies, in the double-joint form, if the indicators send signals in the same direction, a breakthrough operation will be performed. In this way, new trends can be discovered at important technical positions while false breakthroughs in the shock range can be avoided.
## Advantage Analysis
- Comprehensive use of dual indicators to filter signals, with high reliability
- Capture the explosion of new trends in key technology positions
- Breakthrough operations can obtain greater profit potential
- Combined with reversal patterns and indicator filtering, you can avoid repeated losses in the shock range
- Suitable for a variety of varieties and highly flexible
## Risk Analysis
- The double-joint pattern cannot completely rule out the possibility of a false breakout
- Indicator setting requires experience. Improper parameters can easily produce false signals.
- Requires effective stop-loss strategies to control single losses
- Failure to break through may result in larger losses
- The effect depends on parameter optimization, and parameters need to be adjusted for different varieties
Risk control and optimization methods:
- Optimize indicator parameters and reduce false signal rate
- Use trailing stop loss or trailing stop strategy to control single loss
- Assess the persistence of breakthroughs and avoid reversals after expected breakthrough failures
- Adjust parameter settings according to the characteristics of different varieties
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test different moving average systems and find the best parameter combination
2. Optimize RSI parameter settings and reduce false alarm rate
3. Increase trading volume filtering to ensure effective breakthroughs
4. Combine trend judgment indicators to avoid counter-trend breakthroughs
5. Use machine learning methods to automatically optimize parameter tuning
6. Add stop loss strategies to control risks
7. Assess the sustainability of breakthroughs and set target profits
8. Analyze the characteristics of different varieties and adjust parameter settings
Through parameter optimization, evaluation of breakthrough effects, and adjustment of stop loss strategies, the strategy can be continuously improved and stable returns can be obtained in different market environments.
## Summarize
The double-joint smart breakthrough strategy comprehensively uses reversal patterns and indicator filtering confirmation mechanisms to capture potential trend conversion points at important technical positions. Compared with the strategy of purely tracking breakthroughs, the timing of implementing breakthrough operations is more precise and avoids the trouble of repeated losses in the shock range. At the same time, this strategy emphasizes risk control and needs to be used in conjunction with the stop-loss mechanism. Through parameter optimization and technical indicator combination, you can obtain stable breakthrough trading signals, capture market outbreak nodes, and achieve the effect of obtaining greater profits at trend transition points. Generally speaking, this strategy has accurate time node selection and good risk control. After mastering it, you can become skilled and obtain excellent trading performance.
|| 

## Overview

The Double Tops Smart Breakout Strategy is a combination strategy that incorporates the 123 Reversal Strategy and the Pivot Detector Oscillator Strategy. It mainly utilizes double top patterns to identify potential trend reversal points and uses the pivot detector indicator to filter out false breakouts, in order to capture trend reversals at critical technical levels.

## Principles 

The strategy consists of two parts:

1. 123 Reversal Strategy

   The 123 Reversal Strategy originates from the book "How I Tripled My Money in the Futures Market" by Ulf Jensen, page 183. It is a counter-trend reversal strategy.

   The logic is: when the closing price is higher than the previous closing price for 2 consecutive days, and the 9-day Stochastic Slow line is below 50, go long; when the closing price is lower than the previous closing price for 2 consecutive days, and the 9-day Stochastic Fast line is above 50, go short.

2. Pivot Detector Oscillator Strategy

   The Pivot Detector Oscillator Strategy was proposed by Giorgos E. Siligardos. The related article was published in the September 2009 issue of Stocks & Commodities magazine.

   This strategy uses a combination of moving averages and the RSI indicator to gauge oscillation when price approaches upper or lower bands. The specific calculation formula is as follows:

   
```
   When price > moving average:
       Indicator value = (RSI value - 35) / (85 - 35)
   When price <= moving average: 
       Indicator value = (RSI value - 20) / (70 - 20)

   If indicator value > 50, go long
   If indicator value < 50, go short
   
```

By combining the two strategies, when a double top pattern emerges, if the indicator issues a signal in the same direction, a breakout operation is executed. This allows capturing new trends at critical technical levels while avoiding false breakouts within consolidation ranges.

## Advantage Analysis

- Utilizes double indicators for more reliable signals
- Captures new trend outbreaks at key technical levels  
- Breakout operations allow larger profit potential
- Combining reversals and indicator filters avoids whipsaws in ranges
- Applicable to multiple products with flexibility

## Risk Analysis

- Double tops cannot fully eliminate false breakout risks
- Indicator settings require experience, improper parameters may cause wrong signals 
- Effective stop loss strategies are needed to control single loss
- Failed breakouts can lead to large losses
- Performance relies on parameter tuning for different products

Risk management and optimization:

- Optimize indicator parameters to lower false signals
- Adopt moving or trailing stops to limit losses
- Evaluate sustainability of breakouts to avoid reversals
- Adjust parameters based on different product characteristics

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Test different moving average systems to find optimal parameter combinations

2. Optimize RSI parameters to reduce false signals

3. Add volume filter to ensure valid breakouts 

4. Incorporate trend-determining indicators to avoid counter-trend breaks

5. Use machine learning for automatic parameter tuning

6. Add stop loss strategies to control risks

7. Evaluate breakout sustainability and set profit targets

8. Analyze different product characteristics for parameter adjustments

Through parameter optimization, evaluating breakout effects, adjusting stop loss strategies etc, the strategy can be continuously improved to obtain steady profits in different market environments. 

## Conclusion

The Double Tops Smart Breakout Strategy combines reversal patterns and indicator confirmation mechanisms to capture potential trend reversal points at critical technical levels. Compared to purely chasing breakouts, its execution timing is more precise, avoiding whipsaws in ranging markets. Meanwhile, the strategy emphasizes risk control and should be used with stop loss mechanisms. Through parameter optimization and combining technical indicators, steady breakout signals can be obtained to capture outbreaks and achieve large profits at trend reversal points. In summary, the strategy has precise timing selection and sound risk control. With proficiency, it can achieve excellent trading performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|---- 123 Reversal ----|
|v_input_2|14|Length|
|v_input_3|true|KSmoothing|
|v_input_4|3|DLength|
|v_input_5|50|Level|
|v_input_6|true|---- Pivot Detector Oscillator ----|
|v_input_7|200|Length_MA|
|v_input_8|14|Length_RSI|
|v_input_9|100|UpBand|
|v_input_10|false|DownBand|
|v_input_11|50|MidlleBand|
|v_input_12|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-30 00:00:00
end: 2023-10-03 00:00:00
period: 45m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 20/04/2021
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
// The Pivot Detector Oscillator, by Giorgos E. Siligardos
// The related article is copyrighted material from Stocks & Commodities 2009 Sep
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


PDO(Length_MA,Length_RSI,UpBand,DownBand,MidlleBand) =>
    pos = 0.0
    xMA = sma(close, Length_MA)
    xRSI = rsi(close, Length_RSI)
    nRes = iff(close > xMA, (xRSI - 35) / (85-35), 
             iff(close <= xMA, (xRSI - 20) / (70 - 20), 0))
    pos:= iff(nRes * 100 > 50, 1,
    	   iff(nRes * 100 < 50, -1, nz(pos[1], 0))) 
    pos

strategy(title="Combo Backtest 123 Reversal & Pivot Detector Oscillator)", shorttitle="Combo", overlay = true)
line1 = input(true, "---- 123 Reversal ----")
Length = input(14, minval=1)
KSmoothing = input(1, minval=1)
DLength = input(3, minval=1)
Level = input(50, minval=1)
//-------------------------
line2 = input(true, "---- Pivot Detector Oscillator ----")
Length_MA = input(200, minval=1)
Length_RSI = input(14, minval=1)
UpBand = input(100, minval=1)
DownBand = input(0)
MidlleBand = input(50)
reverse = input(false, title="Trade reverse")
posReversal123 = Reversal123(Length, KSmoothing, DLength, Level)
posPDO = PDO(Length_MA,Length_RSI,UpBand,DownBand,MidlleBand)
pos = iff(posReversal123 == 1 and posPDO == 1 , 1,
	   iff(posReversal123 == -1 and posPDO == -1, -1, 0)) 
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

https://www.fmz.com/strategy/428708

> Last Modified

2023-10-08 15:17:51

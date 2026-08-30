
> Name

Moving Average Conversion-Divergence Indicator Trading Strategy CMO-Oscillator-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy is based on the moving average conversion-divergence indicator (CMO) for trading judgment. The absolute value of CMO represents the degree of price divergence. The strategy uses the average of the absolute values ​​of the three periods of CMO to determine overbought and oversold, which is a typical oscillator trading strategy.
## Strategy Principle
This strategy mainly uses the following logic:
1. Calculate the absolute values of the CMO index in three different periods
2. Average the absolute values of the three-period CMO index
3. When the average is higher than the upper threshold, go short.
4. When the average value is lower than the lower threshold, go long and go long
5. When the CMO index returns to normal levels, close the position
The CMO index reflects the momentum of price changes. Its absolute value represents the degree of price divergence. If it exceeds a certain range, it will enter the overbought and oversold area. This strategy takes advantage of this characteristic of CMO, uses multi-period averages to smooth the curve, and determines overbought and oversold conditions. It is a typical shock trading strategy.
## Strategic Advantages
- Use the CMO index to determine overbought and oversold areas
- Three-period average creates a smooth curve to avoid false signals
- According to the CMO theory, there is a strong basis for judging overbought and oversold.
- Customizable parameter thresholds to adapt to market changes
- Easy to implement reversal strategies
## Strategic risks and responses
- CMO indicators may send false signals
- Parameter thresholds require continuous testing and optimization
- Continuous overbought and oversold conditions under trending conditions may cause losses
How to deal with it:
1. Cooperate with trend indicators to avoid counter-trend trading
2. Optimize parameters and improve indicator sensitivity
3. Use trailing stop loss to control single loss
## Strategy optimization direction
This strategy can be expanded from the following dimensions:
1. Increase the confirmation of trading volume indicators to avoid false breakthroughs in trend reversal
2. Integrate trailing stop loss strategy and optimize risk management
3. Use machine learning and other methods to automatically optimize parameters
4. Adjust position size based on volatility indicators
5. Combine other strategies to diversify risks and increase overall returns
## Summarize
This strategy uses CMO to determine overbought and oversold for reversal trading. Due to the use of multi-period averages, it can effectively smooth the curve and avoid false signals. The CMO index itself has a solid theoretical foundation and can reliably determine price divergence. Through parameter optimization, stop loss strategy and other expansions, it can be optimized into a more stable oscillator trading strategy.
|| 

## Overview 

This strategy uses the Chande Momentum Oscillator (CMO) to determine overbought and oversold levels for trading signals. The absolute CMO values over 3 periods are averaged to smooth the oscillator for identifying extremes. A typical mean reversion oscillator trading strategy.

## Strategy Logic

The key logic includes:

1. Calculating absolute CMO values over 3 different periods 
2. Taking the average of 3-period absolute CMO values
3. Going short when average value exceeds upper threshold 
4. Going long when average value drops below lower threshold
5. Closing positions when CMO returns to normal range

The CMO reflects the momentum of price changes. High absolute values represent price divergence entering overbought/oversold zones. The strategy utilizes this characteristic of CMO, using a multi-period average to smooth the curve for identifying extremes.

## Advantages  

- Uses CMO to identify overbought/oversold regions
- Multi-period averaging smooths curve and avoids false signals
- Sound theoretical basis for overbought/oversold detection
- Customizable parameter thresholds to adapt  
- Simple mean reversion implementation

## Risks and Mitigations

- Potential for false CMO signals 
- Requires ongoing threshold optimization
- Sustained extremes during trends can cause losses

Mitigations:

1. Adding trend filter to avoid counter-trend trades
2. Parameter optimization for better CMO sensitivity
3. Using stops to limit losses

## Enhancement Opportunities

The strategy can be enhanced through:

1. Volume confirmation to avoid false breakouts
2. Incorporating trailing stops for better risk management
3. Auto-optimization of parameters via machine learning
4. Volatility-based position sizing 
5. Combining with other strategies to diversify and improve returns

## Conclusion

This strategy uses CMO to identify overbought/oversold for mean reversion trading. Multi-period averaging helps avoid false signals. CMO itself has sound theoretical basis for gauging divergence. Enhancements through better parameters, stops, and filters can make it a stable oscillator trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|5|Length1|
|v_input_2|10|Length2|
|v_input_3|20|Length3|
|v_input_4|58|TopBand|
|v_input_5|5|LowBand|
|v_input_6|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-11 00:00:00
end: 2023-09-14 07:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////7////////////
//  Copyright by HPotter v1.0 21/02/2017
//    This indicator plots the absolute value of CMO averaged over three 
//    different lengths. This indicator plots a classical-looking oscillator, 
//    which is really an averaged value based on three different periods.
//
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
strategy(title="CMOabsav", shorttitle="CMOabsav")
Length1 = input(5, minval=1)
Length2 = input(10, minval=1)
Length3 = input(20, minval=1)
TopBand = input(58, minval=1)
LowBand = input(5, minval=0)
reverse = input(false, title="Trade reverse")
hline(0, color=green, linestyle=hline.style_dashed)
hline(TopBand, color=purple, linestyle=hline.style_solid)
hline(LowBand, color=red, linestyle=hline.style_solid)
xMom = close - close[1]
xMomabs = abs(close - close[1])
nSum1 = sum(xMom, Length1)
nSumAbs1 = sum(xMomabs, Length1)
nSum2 = sum(xMom, Length2)
nSumAbs2 = sum(xMomabs, Length2)
nSum3 = sum(xMom, Length3)
nSumAbs3 = sum(xMomabs, Length3)
nRes = abs(100 * (nSum1 / nSumAbs1 + nSum2 / nSumAbs2 + nSum3 / nSumAbs3 ) / 3)
pos = iff(nRes > TopBand, 1,
	     iff(nRes < LowBand, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
plot(nRes, color=blue, title="CMOabsav")
```

> Detail

https://www.fmz.com/strategy/427300

> Last Modified

2023-09-19 21:16:26


> Name

Trading-Strategy-Based-on-Faytterro-Estimator
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is a strategy for trading based on the trading signals of the Faytterro Estimator. Faytterro Estimator is an indicator that determines trends by calculating the convergence and dispersion rate of prices. This strategy combines the trading signals of Faytterro Estimator, as well as some additional conditions, to issue buy and sell signals of different sizes at ideal points.
## Strategy Principle
The core of this strategy is the Faytterro Estimator. Its calculation method is: first calculate the price convergence dispersion rate CR, and then construct a quadratic function. This quadratic function can reflect the curve characteristics of CR by setting different coefficients. By observing the inflection point of the quadratic function curve, we can judge changes in the price trend.
Specifically, the strategy first calculates the convergence dispersion rate CR of the price. Then construct an array dizi with a length of 2*len, and fill it with the quadratic function values ​​in turn. The coefficient of the quadratic function reflects the value of CR. After that, by observing the two values ​​with subscripts len+1+5 and len+1+4, it is judged whether there is an inflection point in the quadratic function. If an inflection point occurs, a buy or sell signal is issued.
On this basis, the strategy also sets some additional conditions, such as setting the minimum distance for price breakthroughs to avoid frequent transactions; setting entry signals of different sizes, etc. These conditions are all intended to filter out some undesirable trading points.
## Advantage Analysis
This strategy has the following advantages:
1. Use the Faytterro Estimator indicator to determine the trend. This indicator is sensitive to price fluctuations and can capture trend changes early.
2. Construct a quadratic function to reflect the characteristics of the CR curve, find the inflection point signal, and the judgment method is intuitive and effective.
3. Set entry signals of different sizes to conduct pyramid transactions at ideal points to increase profit margins.
4. Add minimum spacing settings to effectively filter signals and avoid frequent invalid transactions.
5. There are many adjustable parameters, which can be optimized for different varieties and have strong adaptability.
6. The strategic ideas are clear and easy to understand, and the code is highly readable, making it easy to learn and refer to.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. Faytterro Estimator has risks in curve fitting and may not be effective in some varieties.
2. Only relying on the inflection point of the quadratic function to judge the signal may be too extensive, leading to misjudgment.
3. Frequent pyramid transactions will increase the burden of handling fees.
4. A large number of adjustable parameters increase the difficulty of tuning.
5. Unable to effectively deal with misjudgment during price shock periods.
6. Without a stop-loss mechanism, losses may expand.
The solutions corresponding to the risks are as follows:
1. Optimize parameters for different varieties to improve robustness.
2. Add other indicator filters to avoid misjudgments caused by relying solely on inflection points.
3. Set stop loss reasonably to control single loss.
4. Automatically tune parameters through big data methods.
5. Add a shock identification mechanism to avoid the shock stage.
6. Set reasonable stop loss logic.
## Optimization direction
The optimization directions of this strategy include:
1. Add stop loss logic to control single loss. You can set a trailing stop or a time stop.
2. Add other indicator combinations to avoid the risk of misjudgment based on a single indicator of Faytterro Estimator. For example, filter by combining MACD, KDJ and other indicators.
3. Add a confirmation mechanism to avoid stop losses due to short-term price corrections. Secondary admission confirmation can be considered.
4. Optimize adjustable parameters and set reasonable parameters for different varieties. Methods such as genetic algorithm and Bayesian optimization can be used.
5. Increase the recognition of volatile market conditions and avoid trading during volatile periods. It can be identified using indicators such as ATR and DMI.
6. Optimize the pyramid logic to prevent chasing the rise and killing the fall. For example, dynamically adjust the increase in position according to the strength of the trend.
7. Test parameter settings for different time periods to find the best period.
## Summarize
This strategy makes decisions based on the trading signals of Faytterro Estimator, adds logical judgment on it, and sets entry signals of different sizes to form a trend following strategy with pyramid characteristics. This strategy is intuitive and easy to understand, and has strong trend capturing capabilities. However, there are also problems such as misjudgment of indicators, no stop loss, and difficulty in parameter tuning. Future optimization directions include adding filtering mechanisms, stop-loss logic, parameter optimization, etc. to improve the stability and adaptability of the strategy. Generally speaking, this strategy provides an idea of ​​using indicators to judge trend changes, which is worth learning and reference.
||


## Overview

This strategy trades based on the trading signals generated by the Faytterro Estimator. The Faytterro Estimator is an indicator that judges trends by calculating the convergence and divergence rate of prices. This strategy combines the trading signals of the Faytterro Estimator and some additional conditions to generate long and short signals of different sizes at ideal points.

## Strategy Logic

The core of this strategy is the Faytterro Estimator. Its calculation is: first calculate the convergence and divergence rate (CR) of prices, then construct a quadratic function, which can reflect the shape of the CR curve by setting different coefficients. By observing the inflection points of the quadratic curve, it judges the change of price trends. 

Specifically, the strategy first calculates the CR of prices. Then it constructs an array dizi of length 2*len, and fills it with quadratic function values sequentially. The coefficients of the quadratic function reflect the value of CR. After that, by observing the two values at index len+1+5 and len+1+4, it determines whether the quadratic function has an inflection point. If there is an inflection point, it generates buy or sell signals.

On this basis, the strategy also sets some additional conditions, such as setting the minimum distance between price breakthroughs to avoid frequent trading, generating signals of different sizes, etc. These conditions are used to filter out some undesirable trading points.

## Advantage Analysis

This strategy has the following advantages:

1. Using the Faytterro Estimator to judge trends, which is sensitive to price fluctuations and can capture trend changes early.

2. Constructing a quadratic function to reflect the shape of the CR curve and finding inflection points directly and effectively.

3. Generating signals of different sizes allows pyramid-trading at ideal points, increasing profit potential.  

4. Increasing the minimum distance setting effectively filters signals and avoids ineffective frequent trading.

5. Many adjustable parameters can be optimized for different trading products, improving adaptability. 

6. The strategy logic is clear and easy to understand, and the code is highly readable, making it easy to learn from.

## Risk Analysis

There are also some risks to note for this strategy:

1. Faytterro Estimator has the risk of curve fitting, and may underperform in some trading products.

2. Judging solely based on inflection points of the quadratic curve may be too crude, leading to misjudgements.

3. Frequent pyramid trading increases the cost of commissions.

4. A large number of adjustable parameters increases the difficulty of optimization.

5. It cannot effectively deal with misjudgements in period of price oscillation. 

6. Lack of stop loss mechanism may lead to greater losses.

The corresponding solutions are:

1. Optimize parameters for different products to improve robustness.

2. Add other indicators for filtration to avoid misjudgements relying solely on inflection points.

3. Set proper stop loss to control single loss.

4. Use big data methods to auto-optimize parameters. 

5. Add oscillation identification to avoid trading in oscillating periods.

6. Set reasonable stop loss logic.

## Optimization Directions

The optimization directions include:

1. Add stop loss logic to control single loss, such as trailing stop loss or time stop loss.

2. Add other indicators to avoid misjudgements relying solely on Faytterro Estimator. For example, combining with MACD, KDJ etc.

3. Add confirmation mechanisms to avoid being stopped out by short-term pullbacks. Consider re-entry confirmation.

4. Optimize adjustable parameters for different products using genetic algorithms, Bayesian optimization etc.

5. Identify oscillating markets using ATR, DMI etc and avoid trading during oscillation.

6. Optimize pyramid logic to prevent chasing trends. For example, dynamically adjust pyramiding positions based on trend strength. 

7. Test parameters on different timeframes to find the optimal timeframe.

## Conclusion

This strategy makes decisions based on the trading signals of Faytterro Estimator, and adds logic judgments and different sized entry signals on top of it to form a trend-following strategy with pyramid characteristics. The strategy is intuitive and easy to understand, with strong trend catching capabilities. But it also has problems like indicator misjudgements, no stop loss, difficulty in parameter optimization. Future optimizations include adding filtration mechanisms, stop loss logic, parameter optimization etc to improve robustness and adaptability. Overall, this strategy provides a way of using indicators to judge trend changes that is worth learning from.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_hlc3|0|source: hlc3|high|low|open|hl2|close|hlcc4|ohlc4|
|v_input_int_1|10|faytterro estimator lenght|
|v_input_float_1|500|minumum enrty-close gap (different direction)|
|v_input_float_2|500|minumum entry-entry gap (same direction)|
|v_input_int_2|10|strong entry size|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-21 00:00:00
end: 2023-08-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © faytterro

//@version=5
// strategy("Faytterro Estimator Strategy", overlay=true, pyramiding=100)

src=input(hlc3,title="source")
len=input.int(10,title="faytterro estimator lenght", maxval=500)
len2=100
len3=input.float(500,title="minumum enrty-close gap (different direction)")
len4=input.float(500,title="minumum entry-entry gap (same direction)")
cr(x, y) =>
    z = 0.0
    weight = 0.0
    for i = 0 to y-1
        z:=z + x[i]*((y-1)/2+1-math.abs(i-(y-1)/2))
    z/(((y+1)/2)*(y+1)/2)
cr= cr(src,2*len-1) 
width=input.int(10, title="strong entry size", minval=1)

dizi = array.new_float(500)
// var line=array.new_line()
//if barstate.islast
for i=0 to len*2
    array.set(dizi,i,(i*(i-1)*(cr-2*cr[1]+cr[2])/2+i*(cr[1]-cr[2])+cr[2]))

buy = array.get(dizi,len+1+5)>array.get(dizi,len+1+4) and array.get(dizi,len+1+5)<cr[len] 
sell = array.get(dizi,len+1+5)<array.get(dizi,len+1+4) and array.get(dizi,len+1+5)>cr[len]
bb=buy? hlc3 : na
ss=sell? hlc3 : na 
sbuy= buy and close<(close[ta.barssince(buy or sell)])[1]-len4 and close<ta.highest(fixnan(ss),len2)-len3*3
ssell= sell and close>(close[ta.barssince(buy or sell)])[1]+len4 and close>ta.lowest(fixnan(bb),len2)+len3*3

buy:= buy and close<(close[ta.barssince(buy or sell)])[1]-len4 and close<ta.highest(fixnan(ss),len2)-len3 //and close>ta.highest(fixnan(ss),len2)-len3*3
sell:=  sell and close>(close[ta.barssince(buy or sell)])[1]+len4 and close>ta.lowest(fixnan(bb),len2)+len3 //and close<ta.lowest(fixnan(bb),len2)+len3*3
alertcondition(buy or sell)


if (sbuy)
    strategy.entry("strong buy", strategy.long,width)
if (ssell)
    strategy.entry("strong sell", strategy.short,width)
if (buy)
    strategy.entry("buy", strategy.long)
if (sell)
    strategy.entry("sell", strategy.short)
```

> Detail

https://www.fmz.com/strategy/427588

> Last Modified

2023-09-22 14:12:27

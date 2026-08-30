
> Name

Trend-Following-Strategy-Based-on-Nadaraya-Watson-Regression-and-ATR-Channel
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1553f5a4df3305680ee.png)
[trans]
## Overview
This strategy is a trend following strategy that combines Nadaraya-Watson regression and ATR channels to identify trend directions and entry points. When the price breaks through the lower track, go long; when the price breaks through the upper track, close the position. At the same time, a stop-loss mechanism is set up.
## Strategy Principle
First, the strategy uses Nadaraya-Watson kernel regression to calculate regression curves for two different lag periods, and then compares the intersection of the two regression curves to determine the trend direction. Specifically, the regression curves of h period and h-lag period are calculated respectively. When the h-lag period curve crosses the h period curve above, it is judged to be bullish; when the h-lag period curve crosses below the h period curve, it is judged to be short.
Secondly, this strategy uses the ATR channel to determine entry points. The upper rail is the regression curve plus the multiplier of n-period ATR, and the lower rail is the regression curve minus the multiplier of n-period ATR. When the price breaks through the upper band, go short and enter the market; when the price breaks through the lower band, go long and enter the market.
Finally, a stop-loss mechanism is set up. If the price continuously stopLossBars K-line is lower than the entry price, stop loss exit.
## Strategic advantage analysis
This strategy combines regression analysis and channel breakthrough to more accurately grasp the direction and intensity of market trends. Compared with using indicators such as moving averages alone to identify trends, this method reduces false signals, thereby improving the stability of the strategy.
In addition, the ATR channel sets a reasonable entry point to avoid mistaken entry near the trend reversal point. The stop-loss mechanism also effectively controls single losses.
Therefore, this strategy has the advantages of strong ability to identify trends, accurate entry and exit, and controllable risk of single stop loss.
## Risk Analysis
The biggest risk of this strategy is that when the ATR channel is broken, the price may be reversing or consolidating, making it inappropriate to enter the market or stop loss and exit soon after entering the market.
In addition, both the regression curve and the ATR channel require certain parameter optimization. If the parameters are set improperly, the regression analysis effect is poor, or the ATR amplitude is too large or too small, it will affect the effectiveness of the strategy.
## Optimization direction
You can consider combining other indicators to determine trends and reversal signals, such as VOLUME, MACD, etc., to improve the stability and accuracy of the strategy.
The kernel function in regression analysis can also be adjusted, such as considering the Epanechnikov kernel, etc., to see if a better fitting effect can be obtained.
The ATR period and multiplier of the ATR channel also need to be repeatedly tested and optimized to find the best parameter combination.
## Summarize
This strategy comprehensively uses regression analysis and channel breakthrough methods to identify the direction and strength of the trend, enter the market at a reasonable point, and set a stop loss, thereby achieving a stable trend following strategy. There is still a lot of room for sub-strategy optimization, and it deserves further testing and improvement.
||

## Overview

This strategy is a trend following strategy that combines Nadaraya-Watson regression and ATR channel to identify trend direction and entry points. It goes long when price breaks through the lower rail and closes position when price breaks through the upper rail. A stop loss mechanism is also set.  

## Strategy Logic

Firstly, this strategy uses Nadaraya-Watson kernel regression to calculate two regression curves with different lags, and compares the crossover of the two curves to determine the trend direction. Specifically, it calculates the regression curves of h-period and h-lag-period respectively. When the h-lag-period curve crosses over the h-period curve, it indicates a long signal. When the h-lag-period curve crosses below the h-period curve, it indicates a short signal.

Secondly, this strategy uses ATR channel to determine entry points. The upper rail is the regression curve plus n-period ATR multiplier and the lower rail is the regression curve minus the n-period ATR multiplier. It goes long when price breaks through the lower rail and goes short when price breaks through the upper rail.  

Finally, a stop loss mechanism is set. If the price stays below the entry price for stopLossBars consecutive bars, the position will be closed by stop loss.

## Advantage Analysis 

This strategy combines regression analysis and channel breakthrough, which can capture the trend direction and momentum relatively accurately. Compared with using single indicators like moving average to identify trends, this method reduces false signals and thus improves the stability of the strategy.

In addition, the ATR channel sets reasonable entry points, avoiding wrong entries around trend reversal points. The stop loss mechanism also effectively controls the single loss.

Therefore, this strategy has advantages like strong ability to identify trends, relatively accurate entries and exits, controllable single stop loss risk, etc.

## Risk Analysis

The biggest risk of this strategy is that when price breaks through the ATR channel, it may just be making a reversal or consolidation, which leads to improper entry or quick stop loss after entry.

In addition, both the regression curves and ATR channels need some parameter optimization. Improper parameter settings may lead to poor regression analysis results or over-wide or over-narrow ATR ranges, which will affect the performance of the strategy.

## Optimization Directions 

We can consider combining other indicators to judge trend and reversal signals, such as VOLUME, MACD etc. to improve the stability and accuracy of the strategy.

The kernel function in the regression analysis can also be adjusted, such as trying Epanechnikov kernel, to see if better fitting effects can be obtained.

The ATR period and multiplier of the ATR channel also need repeated testing and optimization to find the best parameter combination.  

## Summary

This strategy combines the use of regression analysis and channel breakthrough to identify trend direction and strength, enters at reasonable points, and sets stop loss, thus realizing a stable trend following strategy. There is still a large room for further testing and improvement of this strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|10|Lookback Window|
|v_input_3|10|Relative Weighting|
|v_input_4|50|Start Regression at Bar|
|v_input_5|2|Lag|
|v_input_6|3|Stop Loss Bars|
|v_input_7|46|EMA Period|
|v_input_8|32|ATR Period|
|v_input_9|2.7|Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Custom Strategy with Stop Loss and EMA", overlay=true)

src = input(close, title='Source')
h = input(10, title='Lookback Window', tooltip='The number of bars used for the estimation.')
r = input(10, title='Relative Weighting', tooltip='Relative weighting of time frames.')
x_0 = input(50, title='Start Regression at Bar',  tooltip='Bar index on which to start regression.')
lag = input(2, title='Lag', tooltip='Lag for crossover detection.')
stopLossBars = input(3, title='Stop Loss Bars', tooltip='Number of bars to check for stop loss condition.')
emaPeriod = input(46, title='EMA Period',  tooltip='Period for Exponential Moving Averages.')

lenjeje = input(32, title='ATR Period', tooltip='Period to calculate upper and lower band')
coef = input(2.7, title='Multiplier', tooltip='Multiplier to calculate upper and lower band')

// Function for Nadaraya-Watson Kernel Regression
kernel_regression1(_src, _size, _h) =>
    _currentWeight = 0.0
    _cumulativeWeight = 0.0
    for i = 0 to _size + x_0
        y = _src[i] 
        w = math.pow(1 + (math.pow(i, 2) / ((math.pow(_h, 2) * 2 * r))), -r)
        _currentWeight += y * w
        _cumulativeWeight += w
    [_currentWeight, _cumulativeWeight]

// Calculate Nadaraya-Watson Regression
[currentWeight1, cumulativeWeight1] = kernel_regression1(src, h, h)
yhat1 = currentWeight1 / cumulativeWeight1
[currentWeight2, cumulativeWeight2] = kernel_regression1(src, h-lag, h-lag)
yhat2 = currentWeight2 / cumulativeWeight2

// Calculate Upper and Lower Bands
upperjeje = yhat1 + coef * ta.atr(lenjeje)
lowerjeje = yhat1 - coef * ta.atr(lenjeje)

// Plot Upper and Lower Bands
plot(upperjeje, color=color.rgb(0, 247, 8), title="Upper Band", linewidth=2)
plot(lowerjeje, color=color.rgb(255, 0, 0), title="Lower Band", linewidth=2)

// Calculate EMAs
emaLow = ta.ema(low, emaPeriod)
emaHigh = ta.ema(high, emaPeriod)

// Plot EMAs
plot(emaLow, color=color.rgb(33, 149, 243, 47), title="EMA (Low)", linewidth=2)
plot(emaHigh, color=color.rgb(255, 153, 0, 45), title="EMA (High)", linewidth=2)

// Long Entry Condition
longCondition = low < lowerjeje
strategy.entry("Long", strategy.long, when=longCondition)

// Stop Loss Condition
stopLossCondition = close[1] < strategy.position_avg_price and close[2] < strategy.position_avg_price and close[3] < strategy.position_avg_price
strategy.close("Long", when=stopLossCondition)

// Close and Reverse (Short) Condition
shortCondition = high > upperjeje
strategy.close("Long", when=shortCondition)
strategy.entry("Short", strategy.short, when=shortCondition)
```

> Detail

https://www.fmz.com/strategy/442511

> Last Modified

2024-02-22 15:15:03

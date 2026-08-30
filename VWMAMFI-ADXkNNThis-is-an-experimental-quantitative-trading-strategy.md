
> Name

kNN machine learning quantitative trading strategy based on VWMA and MFI-ADX This-is-an-experimental-quantitative-trading-strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/762c27c901eec54e22.png)
[trans]

## Overview
This strategy is an experimental quantitative trading strategy that combines moving average indicators and the kNN algorithm of machine learning to generate trading signals. This strategy uses the intersection of two VWMA moving averages of different periods to determine the trend direction, and combines the two indicators MFI and ADX to filter the signal through the kNN algorithm to improve the reliability of the signal.
## Strategy Principle
The core indicator of this strategy is two VWMA moving averages with different parameters, namely the fast line and the slow line. When the fast line crosses the slow line, a buy signal is generated, and when the fast line crosses below the slow line, a sell signal is generated. In addition, this strategy introduces two auxiliary indicators, MFI and ADX, and uses the kNN classification algorithm to judge the reliability of the signal under current market conditions.
The idea of ​​the kNN algorithm is to compare new data with historical data, determine the results corresponding to the k most similar historical data, and classify based on these k historical results by majority voting. This strategy uses MFI and ADX as the two input parameters of the kNN algorithm to determine the historical price trend (up or down) when these two indicators are combined, thereby filtering the current signal and improving the signal quality.
## Strategic Advantages
- Use the trend following ability of VWMA to generate buying and selling points in conjunction with moving average crossovers
- Use MFI and ADX indicators to extract multi-dimensional features to assist in determining the trend direction
- Dynamic optimization and filtering of trading signals with the help of kNN machine learning algorithm
- Experimental strategy with large development space and needs to be verified and optimized with more data
## Risks and Countermeasures
- VWMA moving average is prone to lagging problems
- MFI and ADX have a certain lag and may misjudge market conditions.
- kNN algorithm parameter settings (such as k value selection) will have a great impact on the results
- An experimental strategy that may not perform well in real trading
Countermeasures:
- Adjust moving average parameters to reduce lag
- Improve the indicator algorithm to improve the accuracy of trend judgment
- Optimize the parameters of kNN algorithm to improve the fitting effect
- Use backtesting and simulated real trading to verify strategies
## Optimization direction
This strategy still has a lot of room for optimization:
- Add more moving average indicators and build moving average combinations
- Try different auxiliary indicators, such as MACD, KDJ, etc.
- Improve kNN algorithm, such as using different distance measurement methods
- Try other machine learning algorithms such as SVM, random forest, etc.
- Carry out parameter optimization and find the best parameter combination
By introducing more indicators and machine learning algorithms, it is expected to further improve the stability and profitability of the strategy.
## Summarize
This strategy is an experimental quantitative trading strategy based on the VWMA moving average indicator and kNN machine learning algorithm. It has the characteristics of strong trend following ability and signal filtering through machine learning. This strategy has a broad space and is expected to produce better results by introducing more features and optimization algorithms. However, as a new strategy, there are also certain risks, which need to be further verified and improved. Overall, this strategy has great potential for innovation.
||

## Overview

This is an experimental quantitative trading strategy that combines moving average indicators and kNN machine learning algorithms to generate trading signals. It uses the crossovers of two VWMA lines with different periods to determine the trend direction, and uses MFI and ADX indicators to filter the signals through kNN algorithm to improve the reliability of the signals.

## Strategy Principles 

The core indicators of this strategy are two VWMA lines with different parameters, namely fast line and slow line. When the fast line crosses above the slow line, a buy signal is generated. When the fast line crosses below the slow line, a sell signal is generated. In addition, this strategy introduces two auxiliary indicators, MFI and ADX, to judge the reliability of the current signal under the current market conditions through the kNN classification algorithm.

The idea behind kNN algorithm is to compare new data with historical data to determine the results corresponding to the k most similar historical data, and categorize based on the majority vote of these k historical results. This strategy uses MFI and ADX as two input parameters of the kNN algorithm to determine the historical price movement (uptrend or downtrend) under this combination of indicators, thereby filtering the current signal to improve the signal quality.

## Advantages

- Utilize the trend following capability of VWMA and generate trading signals through moving average crossovers 
- Apply MFI and ADX indicators for multi-dimensional feature extraction to assist in determining trend direction
- Leverage kNN machine learning algorithm to dynamically optimize and filter trading signals  
- Experimental strategy with large room for improvement through more data verification and optimization

## Risks and Mitigations

- VWMA lines tend to lag 
- MFI and ADX have some lagging, which may misjudge market conditions
- kNN algorithm parameters (e.g. k value) can have significant impact on results
- Experimental strategy may underperform in live trading

Mitigations:

- Adjust MA parameters to reduce lag
- Improve indicators to judge trends more accurately  
- Optimize kNN parameters to improve fitness
- Verify strategy via backtest and paper trading

## Optimization Directions   

There is large room for optimizing this strategy:

- Add more MA indicators to construct MA combinations
- Try different auxiliary indicators like MACD, KDJ etc
- Improve kNN algorithm e.g. using different distance metrics
- Try other machine learning algorithms like SVM, Random Forest etc
- Parameter tuning to find optimal parameter sets

Introducing more indicators and machine learning algorithms may further improve the stability and profitability of the strategy.  

## Summary

This is an experimental quantitative trading strategy based on VWMA indicators and kNN machine learning algorithms. It has the advantage of strong trend following capability while filtering signals via machine learning. The strategy has large room for expansion by introducing more features and optimization algorithms for better results. But as a novel strategy there are also risks that require further verification and improvement. Overall this strategy has great innovation potential.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_open|0|Source: open|high|low|close|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|13|Fast Length|
|v_input_3|19|Slow Length|
|v_input_4|13|Filter Length|
|v_input_5|6|Filter Smoothing|
|v_input_6|23|kNN nearest neighbors (k)|
|v_input_7|false|Draw background|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-21 00:00:00
end: 2023-12-21 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © lastguru

//@version=4
strategy(title="VWMA with kNN Machine Learning: MFI/ADX", shorttitle="VWMA + kNN: MFI/ADX", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

/////////
// kNN //
/////////

// Define storage arrays for: parameter 1, parameter 2, price, result (up = 1; down = -1)
var knn1 = array.new_float(1, 0)
var knn2 = array.new_float(1, 0)
var knnp = array.new_float(1, 0)
var knnr = array.new_float(1, 0)

// Store the previous trade; buffer the current one until results are in
_knnStore (p1, p2, src) =>
    var prevp1 = 0.0
    var prevp2 = 0.0
    var prevsrc = 0.0
    
    array.push(knn1, prevp1)
    array.push(knn2, prevp2)
    array.push(knnp, prevsrc)
    array.push(knnr, src >= prevsrc ? 1 : -1)
    
    prevp1 := p1
    prevp2 := p2
    prevsrc := src

// Sort two arrays (MUST be of the same size) based on the first.
// In other words, when an element in the first is moved, the element in the second moves as well.
_knnGet(arr1, arr2, k) =>
    sarr = array.copy(arr1)
    array.sort(sarr)
    ss = array.slice(sarr, 0, min(k, array.size(sarr)))
    m = array.max(ss)
    out = array.new_float(0)
    for i = 0 to array.size(arr1) - 1
        if (array.get(arr1, i) <= m)
            array.push(out, array.get(arr2, i))
    out

// Create a distance array from the two given parameters
_knnDistance(p1, p2) =>
    dist = array.new_float(0)
    n = array.size(knn1) - 1
    for i = 0 to n
        d = sqrt( pow(p1 - array.get(knn1, i), 2) + pow(p2 - array.get(knn2, i), 2) )
        array.push(dist, d)
    dist

// Make a prediction, finding k nearest neighbours
_knn(p1, p2, k) =>
    slice = _knnGet(_knnDistance(p1, p2), array.copy(knnr), k)
    knn = array.sum(slice)

////////////
// Inputs //
////////////

SRC = input(title="Source", type=input.source, defval=open)
FAST = input(title="Fast Length", type=input.integer, defval=13)
SLOW = input(title="Slow Length", type=input.integer, defval=19)
FILTER = input(title="Filter Length", type=input.integer, defval=13)
SMOOTH = input(title="Filter Smoothing", type=input.integer, defval=6)
KNN = input(title="kNN nearest neighbors (k)", type=input.integer, defval=23)
BACKGROUND = input(false,title = "Draw background")

////////
// MA //
////////
fastMA = vwma(SRC, FAST)
slowMA = vwma(SRC, SLOW)

/////////
// DMI //
/////////

// Wilder's Smoothing (Running Moving Average)
_rma(src, length) =>
    out = 0.0
    out := ((length - 1) * nz(out[1]) + src) / length

// DMI (Directional Movement Index)
_dmi (len, smooth) =>
    up = change(high)
    down = -change(low)
    plusDM = na(up) ? na : (up > down and up > 0 ? up : 0)
    minusDM = na(down) ? na : (down > up and down > 0 ? down : 0)
    trur = _rma(tr, len)
    plus = fixnan(100 * _rma(plusDM, len) / trur)
    minus = fixnan(100 * _rma(minusDM, len) / trur)
    sum = plus + minus
    adx = 100 * _rma(abs(plus - minus) / (sum == 0 ? 1 : sum), smooth)
    [plus, minus, adx]

[diplus, diminus, adx] = _dmi(FILTER, SMOOTH)

/////////
// MFI //
/////////

// common RSI function
_rsi(upper, lower) =>
    if lower == 0
        100
    if upper == 0
        0
	100.0 - (100.0 / (1.0 + upper / lower))

mfiUp = sum(volume * (change(ohlc4) <= 0 ? 0 : ohlc4), FILTER)
mfiDown = sum(volume * (change(ohlc4) >= 0 ? 0 : ohlc4), FILTER)
mfi = _rsi(mfiUp, mfiDown)

////////////
// Filter //
////////////

longCondition = crossover(fastMA, slowMA)
shortCondition = crossunder(fastMA, slowMA)

if (longCondition or shortCondition)
    _knnStore(adx, mfi, SRC)
filter = _knn(adx, mfi, KNN)

/////////////
// Actions //
/////////////

bgcolor(BACKGROUND ? filter >= 0 ? color.green : color.red : na)
plot(fastMA, color=color.red)
plot(slowMA, color=color.green)

if (longCondition and filter >= 0)
    strategy.entry("Long", strategy.long)
if (shortCondition and filter < 0)
    strategy.entry("Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/436239

> Last Modified

2023-12-22 14:13:27

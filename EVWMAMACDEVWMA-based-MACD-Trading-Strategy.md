
> Name

EVWMA-based MACD-Trading-Strategy EVWMA-based-MACD-Trading-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](https://www.fmz.com/upload/asset/15eebe05504c636db4b.png)
 [trans]

### Overview
This strategy is a MACD trading strategy based on the Elastic Volume Weighted Moving Average (EVWMA). It uses the advantages of EVWMA to design a strategy with clear trading signals and strong practicality.
### Strategy Principles
The EVWMA indicator integrates trading volume information into the calculation of the moving average, so that the moving average can more accurately reflect price changes. The calculations of fast and slow lines constructed by this strategy are based on EVWMA. The parameter settings of the fast line are more sensitive and can capture short-term price changes; the parameter settings of the slow line are more robust and can filter out some noise. The MACD formed by the two EVWMAs cross over for long and short positions, and a histogram is designed to give trading tips with better visual effects.
### Advantage Analysis
The biggest advantage of this strategy is to use the power of the EVWMA indicator to make the MACD strategy parameter settings more stable and the trading signals clearer. Compared with the simple moving average, EVWMA can better grasp the market trend. This makes the strategy more adaptable and can work stably in various market environments.
### Risk Analysis
The main risk of this strategy is that MACD itself has a certain lag and cannot capture price reversals in time. In addition, the parameter settings of EVWMA will also affect the strategy performance. If the parameters of the fast and slow lines are set improperly, trading signals will be confused and profitability will be affected.
In order to reduce risks, parameters should be adjusted appropriately to make the gap between the fast line and the slow line moderate. Histogram can help determine whether parameter adjustment is needed. In addition, you can also design a stop-loss strategy to avoid excessive losses in a single transaction.
### Optimization direction
This strategy can mainly be optimized from the following aspects:
1. Using adaptive parameter setting technology, the parameters of EVWMA can be automatically adjusted according to the market environment to ensure the clarity of trading signals.
2. Add a stop-loss mechanism to effectively control single losses.
3. Combine with other indicators to filter false positive signals. For example, combined with trading volume, a signal is generated only when the price changes significantly.
4. Optimize entry point selection. The current strategy is to open a position when the MACD zero line crosses. You can test whether deep hip pull is more suitable.
### Summarize
This strategy takes advantage of the EVWMA indicator to build a simple and practical MACD strategy. It has better stability and wider adaptability. At the same time, there is also the lagging problem of MACD itself. We can make improvements from adaptive parameter optimization, stop loss design, signal filtering, etc. to make the strategy more robust.
||

### Overview

This strategy is a MACD trading strategy based on Elastic Volume Weighted Moving Average (EVWMA). It utilizes the advantages of EVWMA and designs a strategy with clear trading signals and strong practicality.  

### Principles

The EVWMA indicator incorporates volume information into the calculation of moving averages, allowing moving averages to more accurately reflect price changes. The calculations of the fast line and slow line in this strategy are both based on EVWMA. The parameter settings of the fast line are more sensitive to capture short-term price fluctuations; the parameter settings of the slow line are more robust to filter out some noise. The MACD formed by the two EVWMAs triggers long and short signals on crossover, and the histogram provides visually enhanced trading prompts.

### Advantage Analysis 

The biggest advantage of this strategy is that by leveraging the power of the EVWMA indicator, the parameters settings of the MACD strategy become more stable and trading signals become clearer. Compared with simple moving averages, EVWMA can better grasp market trend changes. This makes the strategy more adaptable to work stably across various market environments.

### Risk Analysis

The main risk of this strategy is that MACD itself has a certain lag and cannot promptly capture price reversals. In addition, the parameter settings of EVWMA also affect strategy performance. If the fast and slow line parameters are not set properly, the trading signals will be chaotic, affecting profitability.

To mitigate risks, parameters should be adjusted appropriately to have a moderate difference between the fast and slow lines. The histogram can assist in judging whether a parameter adjustment is needed. In addition, stop loss strategies can also be designed to avoid excessively large single losses.

### Optimization Directions

The main aspects for optimizing this strategy include:

1. Use adaptive parameter setting techniques to automatically adjust EVWMA parameters according to market conditions to ensure signal clarity.

2. Increase stop loss mechanisms to effectively control single losses.

3. Incorporate other indicators to filter false signals. For example, combine with volume to only trigger signals during significant price changes. 

4. Optimize entry point selections. Currently the strategy opens positions on MACD zero line crossovers. Testing if using divergence performs better can be examined.


### Conclusion
This strategy utilizes the advantages of the EVWMA indicator to build a simple and practical MACD strategy. It has better stability and adaptability. At the same time, it also has the lag problem inherent in MACD. We can improve the strategy's robustness through adaptive parameter optimization, stop loss design, signal filtering and other aspects.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Fast Sum Length|
|v_input_2|20|Slow Sum Length|
|v_input_3|9|Signal Smoothing|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-15 00:00:00
end: 2024-01-21 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("QuantNomad - EVWMA MACD Strategy", shorttitle = "EVWMA MACD", overlay = false)

// Inputs
fast_sum_length = input(10, title = "Fast Sum Length",  type = input.integer)
slow_sum_length = input(20, title = "Slow Sum Length",  type = input.integer)
signal_length   = input(9,  title = "Signal Smoothing", type = input.integer, minval = 1, maxval = 50)

// Calculate Volume Period
fast_vol_period = sum(volume, fast_sum_length)
slow_vol_period = sum(volume, slow_sum_length)

// Calculate EVWMA
fast_evwma = 0.0
fast_evwma := ((fast_vol_period - volume) * nz(fast_evwma[1], close) + volume * close) / (fast_vol_period)

// Calculate EVWMA
slow_evwma = 0.0
slow_evwma := ((slow_vol_period - volume) * nz(slow_evwma[1], close) + volume * close) / (slow_vol_period)

// Calculate MACD
macd   = fast_evwma - slow_evwma
signal = ema(macd, signal_length)
hist   = macd - signal

// Plot 
plot(hist,   title = "Histogram", style = plot.style_columns, color=(hist>=0 ? (hist[1] < hist ? #26A69A : #B2DFDB) : (hist[1] < hist ? #FFCDD2 : #EF5350) ), transp=0 )
plot(macd,   title = "MACD",      color = #0094ff, transp=0)
plot(signal, title = "Signal",    color = #ff6a00, transp=0)

// Strategy
strategy.entry("Long",   true, when = crossover(fast_evwma, slow_evwma))
strategy.entry("Short", false, when = crossunder(fast_evwma, slow_evwma))
```

> Detail

https://www.fmz.com/strategy/439609

> Last Modified

2024-01-22 10:50:25

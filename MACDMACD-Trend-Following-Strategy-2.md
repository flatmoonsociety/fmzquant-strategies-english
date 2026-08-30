
> Name

MACD Trend Following Strategy MACD-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/51123b04f9d1038872d1d4a82e3bef8d0ce4fd0afcb5a81c6be00621d68faf47.png)
[trans]
### Overview
The MACD trend following strategy determines the trend by calculating the golden cross of the MACD indicator and its signal line and realizes profits from following the trend.
### Strategy Principles
This strategy determines the trend direction based on the MACD indicator. The MACD indicator is a trend-following exponential smoothed moving average of convergence and divergence, consisting of a fast line (MACD), a slow line (Signal) and a histogram. The golden cross on the fast and slow lines indicates that the market may start a bull market, while the dead cross indicates that the market may start a bear market. Histogram represents the difference between the fast line and the slow line, and the distance and change speed of the two average lines can be judged through color changes.
When the Histogram rises from a negative number to a positive number, a golden cross signal is generated, indicating that the market may have just begun, and a long position can be established; when the Histogram turns from a positive number to a negative number, a dead cross signal is generated, indicating that the market may have peaked, and the long position can be closed or a short position can be established.
### Advantage Analysis
- Use the double smoothing average line golden and dead cross patterns to determine the trend, and the winning rate is higher
- Histogram can clearly judge the trend and speed of MACD indicator
- There is a large space for parameter optimization and can be adjusted to the best state
- Can be used with other indicators to filter out false signals
### Risk and Optimization
- There is a certain degree of hysteresis
- May send false signals
- You can try MA, KD and other indicators to confirm the trend
- Adjustable parameters to find the best configuration
### Summarize
The MACD trend following strategy is generally a more reliable method of trend judgment. By optimizing parameters and confirming with other indicators, the false signal rate can be greatly reduced, thereby obtaining higher strategic returns. The strategy idea is simple and easy to understand, and it is the first choice for getting started with automated quantitative trading.
||


### Overview

The MACD trend following strategy judges the trend by calculating the golden cross and dead cross of the MACD indicator and its signal line to follow the trend for profit.

### Strategy Principle  

This strategy is based on the MACD indicator to determine the trend direction. The MACD indicator is a trend-following momentum indicator, consisting of the MACD line, Signal line and Histogram. The golden cross of the MACD and Signal lines suggests a potential bull market, while the dead cross suggests a potential bear market. The Histogram represents the difference between the two lines, indicating their divergence and changing speed through color change.

When the Histogram rises from negative to positive, a golden cross signal is generated, indicating the uptrend may just begin, and long positions can be built. When the Histogram turns from positive to negative, a dead cross signal is generated, indicating the uptrend may be topping, and long positions can be exited or short positions can be built.

### Advantage Analysis

- Utilize golden/dead cross of double smoothing lines to judge trend with relatively high win rate
- Histogram clearly indicates the progress and speed of MACD indicator
- Large parameter tuning space for optimization
- Can be combined with other indicators to filter fake signals

### Risk and Optimization

- There is some degree of lagging  
- May generate fake signals
- Try confirming trends with MA, KD etc.
- Adjust parameters for best configuration

### Conclusion

The MACD trend following strategy overall is a relatively reliable way to determine trends. By optimizing parameters and confirming with other indicators, the fake signal rate can be largely reduced, resulting in higher strategy profit. The strategy logic is simple and easy to understand, making it the first choice for algorithmic trading starters.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|Fast Length|
|v_input_2|26|Slow Length|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_4|9|Signal Smoothing|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-17 00:00:00
end: 2023-11-23 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("MACD")

// Getting inputs
fastLength = input(title="Fast Length",  defval=12)
slowlength = input(title="Slow Length",  defval=26)
src = input(title="Source",  defval=close)
signalLength = input(title="Signal Smoothing",  minval = 1, maxval = 50, defval = 9)

// Calculating
macd = ema(close, fastLength) - ema(close, slowlength)
signal = ema(macd, signalLength)
delta = macd - signal

// Plot colors
col_grow_above = #26A69A
col_grow_below = #FFCDD2
col_fall_above = #B2DFDB
col_fall_below = #EF5350
col_macd = #0094ff
col_signal = #ff6a00

// Plot histogram
plot(delta, title="Histogram", style=columns, color=(delta>=0 ? (delta[1] < delta ? col_grow_above : col_fall_above) : (delta[1] < delta ? col_grow_below : col_fall_below) ), transp=0 )
plot(macd, title="MACD", color=col_macd, transp=0)
plot(signal, title="Signal", color=col_signal, transp=0)

// Plot orders
if (crossover(delta, 0))
    strategy.entry("buy", strategy.long)
if (crossunder(delta, 0))
    strategy.entry("sell", strategy.short)






```

> Detail

https://www.fmz.com/strategy/433124

> Last Modified

2023-11-24 15:51:39

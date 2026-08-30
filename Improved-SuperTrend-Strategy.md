
> Name

Improved Trend Following Momentum Breakout Trend Strategy Improved-SuperTrend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/117c59f19588c7f602a.png)
[trans]

## Overview
This article provides a detailed analysis of an improved trend following strategy that combines the SuperTrend indicator and the Stochastic RSI filter. The strategy is designed to generate buy and sell signals while taking into account market trends and reducing false signals. Stochastic RSI is used to avoid false signals in overbought and oversold conditions.
## Strategy Principle
### SuperTrend calculation
First, calculate the true range (TR) and average true range (ATR). Then use ATR to calculate the upper rail and lower rail:
Upper rail = SMA (closing price, ATR period) + ATR multiplier × ATR
Lower track = SMA(closing price, ATR period) - ATR multiplier × ATR
If the closing price is higher than the lower band, it is an uptrend; if the closing price is lower than the upper band, it is a downtrend. In an upward trend, SuperTrend is the lower track; in a downward trend, SuperTrend is the upper track.
### Filtering mechanism
In order to reduce false signals, a moving average of SuperTrend is performed to obtain the filtered SuperTrend.
### Stochastic RSI

Calculate the value of RSI and then apply the Stochastic indicator to generate the Stochastic RSI. It reflects whether the RSI is in overbought or oversold territory.
### Entry and exit conditions
Buy conditions: The closing price crosses the filtered SuperTrend and is in an upward trend, and Stochastic RSI < 80
Sell conditions: The closing price crosses the filtered SuperTrend and is in a downtrend, and Stochastic RSI > 20
Exit Buy: The closing price crosses the filtered SuperTrend and is in an uptrend
Exit Sell: The closing price crosses the filtered SuperTrend and is in a downtrend
## Strategic Advantages
This is an improved trend following strategy that has the following advantages over simple moving averages and other indicators:
1. SuperTrend itself has strong trend identification capabilities and the ability to filter false signals.
2. The application of filtering mechanism further reduces false signals and makes the signal more reliable.
3. Stochastic RSI avoids false signals generated in overbought and oversold situations, allowing the strategy to send signals near important support and resistance areas.
4. The strategy takes into account both the trend direction and the overbought and oversold conditions of Stochastic RSI, which better balances the relationship between tracking the trend and avoiding false signals.
5. Strategy parameters can be flexibly adjusted and suitable for different market environments.
## Strategy Risk and Optimization
### Possible risks
1. In a volatile market, stop loss may be breached.
2. Both SuperTrend and the filtering mechanism have lag and may miss recent price changes.  
3. Improper setting of Stochastic RSI parameters will also affect strategy performance.
### Risk Response
1. Adjust stop loss appropriately or use default stop loss.
2. Adjust the parameters ATR cycle and filter cycle to balance the hysteresis.
3. Test and optimize the parameters of Stochastic RSI.
### Optimization direction
1. Test different parameter combinations to find the best parameters.
2. Try different filtering mechanisms, such as EMA smoothing, etc.
3. Apply machine learning algorithms to automatically optimize parameters.
4. Combine with other indicators to supplement the basis for entry.
## Summarize
This strategy integrates the advantages of SuperTrend and Stochastic RSI indicators, which can effectively identify trends and send high-quality trading signals. At the same time, the filtering mechanism also makes it more robust to market noise. This strategy can obtain better strategy effects through parameter optimization, and can also be considered in combination with other indicators or models. In general, this strategy shows good trend tracking capabilities and has a certain risk control mechanism, making it suitable for investors who pursue stable returns.
|| 

## Overview

This article analyzes in depth a trend following strategy that combines the SuperTrend indicator with a Stochastic RSI filter for improved accuracy. It aims to generate buy and sell signals while considering the prevailing trend and reducing false signals. The Stochastic RSI filters out false signals during overbought and oversold conditions.

## Strategy Logic

### SuperTrend Calculation

First, True Range (TR) and Average True Range (ATR) are calculated. Then the upper and lower bands are computed using ATR:

Upper Band = SMA(Close, ATR Period) + ATR Multiplier * ATR 
Lower Band = SMA(Close, ATR Period) - ATR Multiplier * ATR

An uptrend is identified when close > lower band. A downtrend is identified when close < upper band. 

During uptrend, SuperTrend is set to lower band. During downtrend, SuperTrend is set to upper band.

### Filtering Mechanism  

To reduce false signals, the SuperTrend is smoothed using a moving average to obtain the filtered SuperTrend.

### Stochastic RSI

The RSI value is calculated, then Stochastic indicator is applied on it to generate Stochastic RSI. It shows whether RSI is overbought or oversold.

### Entry and Exit Conditions

Long entry: Close crosses above filtered SuperTrend in uptrend and Stochastic RSI < 80
Short entry: Close crosses below filtered SuperTrend in downtrend and Stochastic RSI > 20 

Long exit: Close crosses below filtered SuperTrend in uptrend  
Short exit: Close crosses above filtered SuperTrend in downtrend

## Advantages of the Strategy

This improved trend following strategy has the following edges over simple moving averages:

1. SuperTrend itself has good trend identification and false signal filtering abilities. 
2. The filtering mechanism further reduces false signals resulting in more reliable signals.
3. Stochastic RSI avoids false signals around important support/resistance levels during overbought/oversold conditions.  
4. The strategy considers both trend direction and overbought/oversold conditions leading to better balance between following the trend and avoiding false signals.
5. Flexible parameter adjustment allows adaptation to different market environments.

## Risks and Optimization

### Potential Risks 

1. Stop loss can be hit during high volatility moves. 
2. Lagging issues with SuperTrend and filtering causing missing recent price changes.
3. Incorrect Stochastic RSI parameter settings impacting strategy performance.

### Risk Management

1. Adjust stop loss appropriately or use trailing stop loss.   
2. Tune parameters like ATR period and filter period to balance lagging effect.
3. Test and optimize Stochastic RSI parameters.

### Optimization Opportunities

1. Test different parameter combinations to find optimal parameters.  
2. Try different filtering mechanisms like EMA smoothing etc. 
3. Apply machine learning to auto-optimize parameters.
4. Incorporate other indicators to supplement entry conditions.

## Conclusion  

This strategy combines the strengths of SuperTrend and Stochastic RSI for effective trend identification and quality trade signals, while also making the strategy robust to market noise through filtering mechanisms. Further performance improvement can be achieved through parameter optimization or combining with other indicators/models. Overall, this strategy demonstrates good trend following ability and some risk control for those seeking steady returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|14|ATR Length|
|v_input_2|1.5|ATR Multiplier|
|v_input_3|5|Filter Length|
|v_input_4|14|Stochastic RSI Length|
|v_input_5|3|Stochastic RSI %K Smoothing|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-09 00:00:00
end: 2024-01-16 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Improved SuperTrend Strategy with Stochastic RSI", shorttitle="IST+StochRSI", overlay=true)

// Input parameters
atr_length = input(14, title="ATR Length")
atr_multiplier = input(1.5, title="ATR Multiplier")
filter_length = input(5, title="Filter Length")
stoch_length = input(14, title="Stochastic RSI Length")
smooth_k = input(3, title="Stochastic RSI %K Smoothing")

// Calculate True Range (TR) and Average True Range (ATR)
tr = ta.rma(ta.tr, atr_length)
atr = ta.rma(tr, atr_length)

// Calculate SuperTrend
upper_band = ta.sma(close, atr_length) + atr_multiplier * atr
lower_band = ta.sma(close, atr_length) - atr_multiplier * atr

is_uptrend = close > lower_band
is_downtrend = close < upper_band

super_trend = is_uptrend ? lower_band : na
super_trend := is_downtrend ? upper_band : super_trend

// Filter for reducing false signals
filtered_super_trend = ta.sma(super_trend, filter_length)

// Calculate Stochastic RSI
rsi_value = ta.rsi(close, stoch_length)
stoch_rsi = ta.sma(ta.stoch(rsi_value, rsi_value, rsi_value, stoch_length), smooth_k)

// Entry conditions
long_condition = ta.crossover(close, filtered_super_trend) and is_uptrend and stoch_rsi < 80
short_condition = ta.crossunder(close, filtered_super_trend) and is_downtrend and stoch_rsi > 20

// Exit conditions
exit_long_condition = ta.crossunder(close, filtered_super_trend) and is_uptrend
exit_short_condition = ta.crossover(close, filtered_super_trend) and is_downtrend

// Plot SuperTrend and filtered SuperTrend
plot(super_trend, color=color.orange, title="SuperTrend", linewidth=2)
plot(filtered_super_trend, color=color.blue, title="Filtered SuperTrend", linewidth=2)

// Plot Buy and Sell signals
plotshape(series=long_condition, title="Buy Signal", color=color.green, style=shape.triangleup, location=location.belowbar)
plotshape(series=short_condition, title="Sell Signal", color=color.red, style=shape.triangledown, location=location.abovebar)

// Output signals to the console for analysis
plotchar(long_condition, "Long Signal", "▲", location.belowbar, color=color.green, size=size.small)
plotchar(short_condition, "Short Signal", "▼", location.abovebar, color=color.red, size=size.small)

// Strategy entry and exit
strategy.entry("Long", strategy.long, when=long_condition)
strategy.entry("Short", strategy.short, when=short_condition)
strategy.close("Long", when=exit_long_condition)
strategy.close("Short", when=exit_short_condition)

```

> Detail

https://www.fmz.com/strategy/439082

> Last Modified

2024-01-17 15:55:15

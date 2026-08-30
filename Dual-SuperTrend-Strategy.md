
> Name

Dual-SuperTrend-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/145cbf84b133a308352.png)

[trans]

### Overview
The double super trend strategy is a short-term quantitative trading strategy that integrates double super trend channels. This strategy calculates the true volatility range and builds a dual-channel system to monitor price breakthrough channels in real time to achieve trend tracking and reversal trading.
### Strategy Principles
The double supertrend strategy is based on the derivation of the supertrend indicator. The supertrend indicator consists of an upper band and a lower band and is used to determine price trends and key support and resistance levels. The double overtrend strategy builds two channels on this basis: a stabilization channel and a rupture channel.
- Stabilizing channel: composed of the basic upper band and lower band, used to judge the current price trend;
- Broken Channel: consists of heuristic upper and lower bands and is used to capture trend reversals.
The strategy first calculates the true volatility range, which is the difference between the highest price and the lowest price, and the average true volatility range. The base channel is then calculated based on the length parameter and the multiplier parameter. Then judge whether the price breaks through the basic channel to construct a rupture channel, completing the establishment of dual channels.
Under the dual-channel system, the strategy generates trading signals by judging price breakthroughs in different channels:
- When the price crosses the lower end of the stabilizing channel, a buy signal is generated;
- A sell signal is generated when the price crosses the upper band of the stabilizing channel.
Through dual-channel monitoring, trend tracking and reversal capture can be achieved.
### Advantage Analysis
The double super trend strategy combined with the dual channel system has the following advantages:
- Capture trend reversals and avoid false breakouts. The setting of the rupture channel can effectively identify the true trend reversal and prevent being misled by short-term noise.
- Strong transaction continuity. Compared with a single super trend, a double super trend can extend each trading cycle.
- There is a lot of room for parameter optimization. By adjusting channel parameters, you can adapt to the characteristics of different varieties and cycles.
- Achieve lower strategic neuroticism. The dual-channel mechanism enhances strategy stability.
- Easy to verify and optimize. Intuitive channel display facilitates quick evaluation of strategy effects.
### Risk Analysis
The double supertrend strategy also has the following risks:
- Dual channel range selection requires experience. If the channel is too narrow, it will easily lead to multiple invalid breakthroughs; if the channel is too wide, it will be impossible to catch the trend reversal in time.
- Impact of major off-site events. Non-technically driven events may lead to abnormal price fluctuations and failure of the breakthrough channel system.
- Transaction frequency is higher. The dual-channel structure tends to increase the frequency of transactions, and the position size needs to be controlled.
- Parameter optimization is difficult. It is not easy to optimize the parameters of dual channels at the same time, and it takes enough time to adjust.
- Stop loss is not guaranteed. This strategy cannot set a stop loss and there are certain risks.
The above risks can be avoided by adjusting parameter ranges, combining filtering conditions, and appropriately controlling positions.
### Optimization direction
The double super trend strategy can be optimized from the following aspects:
- Add filter conditions to avoid false breakthroughs. Filter signals such as trading volume or volatility indicators can be added to ensure effective breakthroughs.
- Combine with trend indicators to determine the direction of the general trend. The direction of the general trend is consistent to avoid counter-trend trading.
- Dynamically adjust channel parameters to adapt to market changes. Adaptive algorithms can be used to optimize channel parameters.
- Optimize the exit mechanism to achieve profit protection. You can set up trailing stop loss or time exit.
- Distinguish between long and short status, trade long and short separately. Different parameters are used for the long and short phases.
- Add quantitative risk control to control the maximum drawdown. Methods such as position control and overall stop loss can be set up.
Through further optimization, the strategies Parameter Fitting and Walk Forward Analysis can be made more effective, thereby obtaining more stable returns.
### Summarize
The double super trend strategy is based on the dual channel mechanism to achieve trend tracking and reversal capture, and a stable trading strategy can be obtained through parameter optimization. However, this strategy also has certain limitations, and auxiliary means need to be introduced for risk control. Generally speaking, the double super trend strategy provides a reliable model framework for short-term quantitative trading.
||

### Overview

The Dual SuperTrend strategy is a quantitative trading strategy that incorporates a dual SuperTrend channel system. It calculates true range volatility and constructs a two-band channel to monitor price breakthroughs, enabling trend following and reversal trading.

### Strategy Logic  

The Dual SuperTrend strategy derives from the SuperTrend indicator. SuperTrend consists of upper and lower bands to determine price trends and key support/resistance levels. The Dual SuperTrend builds two channels on top of it: the consolidating channel and the breaking channel.

- Consolidating Channel: made up of the basic upper and lower bands to judge the ongoing trend.
- Breaking Channel: formed by the heuristic upper and lower bands to capture trend reversals.

The strategy firstly computes the true range and average true range. It then calculates the basic bands based on the length and multiplier parameters. Next, it constructs the breaking channel if the price breaks through the basic bands. The dual-channel system is thus established.

Under the dual-channel structure, trading signals are generated when the price crosses different channels:

- A buy signal is triggered when the price crosses above the lower band of the consolidating channel. 
- A sell signal is triggered when the price crosses below the upper band of the consolidating channel.

The dual-channel monitoring enables both trend following and reversal capturing.

### Advantage Analysis

The Dual SuperTrend strategy with the dual-channel system has the following advantages:

- Capturing trend reversals and avoiding false breakouts. The breaking channel effectively identifies true reversals.
- Persistence in trades. The dual-channel prolongs each trade compared to the single SuperTrend.  
- Large parameter optimization space. The channels can be tuned for different products and timeframes.
- Reduced strategy whipsaws. The dual-channel enhances stability.
- Easy backtesting and optimization. The intuitive channels facilitate evaluating the strategy.

### Risk Analysis

The Dual SuperTrend strategy also has the following risks:

- Channel range selection requires expertise. Too narrow channels cause frequent invalid breakouts. Too wide channels fail to capture reversals timely.
- Impact from external events. Non-technical events may trigger abnormal price moves that invalidate the channel system.  
- High trading frequency. The dual-channel structure tends to increase trading frequency and position sizing needs control.
- Difficult parameter optimization. It is challenging to optimize both channels simultaneously. Sufficient time is required. 
- No stop loss guarantee. The strategy does not have a stop loss mechanism.

The risks can be mitigated by adjusting parameter range, adding filters, controlling position sizing, etc.

### Optimization Directions

The Dual SuperTrend strategy can be optimized in the following aspects:

- Adding filters to avoid false breakouts. Volume or volatility indicators can be used to confirm valid breakouts.
- Incorporating trend indicators to determine the macro trend. Trading along the major trend avoids counter-trend trades. 
- Dynamically adjusting channel parameters to adapt to changing markets. Adaptive algorithms can optimize parameters.
- Optimizing exit mechanisms for profit protection. Trailing stop or time-based exit can be incorporated.
- Separating long and short states for directional trading. Different parameters can be used for bullish and bearish stages. 
- Introducing quant risk control for maximum drawdown limit. Position sizing control and overall stop loss can be set.

Further optimizations can improve Parameter Fitting and Walk Forward Analysis for more robust performance.

### Conclusion

The Dual SuperTrend strategy leverages the dual-channel mechanism for trend following and reversal capturing. Stable trading strategies can be developed through parameter optimization, but limitations exist. Risk control addons are required. Overall, the Dual SuperTrend provides a solid framework for short-term quantitative trading strategies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Length|
|v_input_2|3|Multiplier|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-08 00:00:00
end: 2023-11-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


//@version=4
strategy("Double Supertrend Strategy", overlay=true)

// Define your parameters
length = input(10, title="Length")
multiplier = input(3, title="Multiplier")

// Calculate the True Range and Average True Range
trueRange = max(high - low, max(abs(high - close[1]), abs(low - close[1])))
averageTrueRange = sma(trueRange, length)

// Calculate the basic upper and lower bands
basicUpperBand = hl2 + (multiplier * averageTrueRange)
basicLowerBand = hl2 - (multiplier * averageTrueRange)

// Calculate the final upper and lower bands
finalUpperBand = basicUpperBand
finalLowerBand = basicLowerBand

finalUpperBand := close[1] > finalUpperBand[1] ? max(basicUpperBand, finalUpperBand[1]) : basicUpperBand
finalLowerBand := close[1] < finalLowerBand[1] ? min(basicLowerBand, finalLowerBand[1]) : basicLowerBand

// Determine if we're currently in an uptrend or downtrend
uptrend = close > finalLowerBand[1]
downtrend = close < finalUpperBand[1]

// Plot the bands
plot(uptrend ? finalUpperBand : na, color=color.green, linewidth=2)
plot(downtrend ? finalLowerBand : na, color=color.red, linewidth=2)

// Define your conditions for entering and exiting trades
if (uptrend)
    strategy.entry("Buy", strategy.long)
else if (downtrend)
    strategy.entry("Sell", strategy.short)


```

> Detail

https://www.fmz.com/strategy/432221

> Last Modified

2023-11-15 16:33:05

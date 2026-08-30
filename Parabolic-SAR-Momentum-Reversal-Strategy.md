
> Name

Momentum Tracking Parabolic Stop Reversal Strategy Parabolic-SAR-Momentum-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/efc7411f52f0ae1400.png)
[trans]

## Overview
This strategy is a Swing trading strategy that uses Parabolic SAR and K-line to perform cross operations to achieve momentum tracking and stop loss. The strategy will take long and short positions in bullish and bearish situations and close these positions with stops when the price reverses.
## Strategy Principle
This strategy mainly relies on the Parabolic SAR to determine whether the current price trend is upward or downward. When the Parabolic SAR indicator is below the K line, it means that the price is currently rising. At this time, the strategy will check whether the Parabolic SAR value crosses the lowest price of the K line at the closing of each K line. If it does not cross the lowest price of the K line, it means that the upward trend continues, and the strategy will establish a long position; if the Parabolic SAR crosses the lowest price of the K line, it means that the upward trend has reversed to a downward trend. At this time, the strategy will close the long position and stop the loss. On the contrary, when the Parabolic SAR indicator is above the K line, it indicates that the price is currently falling. At this time, the strategy will check whether the Parabolic SAR value crosses the highest price of the K line at the closing of each K line. If it does not cross, a short position will be established; if it crosses below, it means that the downward trend has reversed to an upward trend, and the short position will be closed to stop the loss.
Through this operating principle, this strategy can establish a position under the confirmed price trend and stop the loss as soon as possible, thereby locking in profits. At the same time, the parabola, as a momentum indicator, can more accurately determine whether the trend is reversing, which also makes stop loss more accurate.
## Strategic Advantages
1. Using parabolas to determine trends and reversal points is a relatively advanced and accurate technical indicator that can improve the accuracy of judgment.
2. Use momentum tracking and reversal stop loss operations to make full use of opportunities brought by price trends.
3. The reversal stop loss rules are relatively strict and the risk control ability is strong
4. The parameters of this strategy have been optimized and are particularly suitable for use on GBP/JPY, a currency pair with a strong 추세
## Strategy Risk
1. Like any other single indicator strategy, this strategy may misjudge the price trend and reversal point of the parabola. If the indicator fails, it may lead to unnecessary losses.
2. This strategy completely relies on the instructions of the parabola for operation. If the indicator parameters are not set properly and the stop loss point is set too loosely, the risk cannot be effectively controlled.
3. Any single strategy may gradually fail due to changes in market structure or environment, and strategies need to be tested and optimized in a timely manner.
Methods to improve the robustness of the strategy include: optimizing the stop loss setting to make it strict enough; combining judgment with other indicators as confirmation; adjusting indicator parameters to adapt to changes in the market environment; selecting the optimal parameter combination according to different varieties, etc.
## Strategy optimization direction
1. This strategy can test and optimize the parameter combination of the parabola to obtain better indicator performance
2. It can be combined with other judgment indicators, such as MACD, KD, etc., to form a multi-indicator confirmation system to improve the reliability of operating signals.
3. You can test the effects of different stop loss methods, such as net stop loss, time stop loss, price stop loss, etc.
4. Optimize parameters according to the characteristics of different varieties so that the strategy can obtain good returns on different varieties.
## Summarize
The parabolic Swing strategy is generally a short-term operation strategy with better effect. It uses the parabolic indicator to determine the trend direction and momentum changes in prices, and cooperates with the Swing trading method to repeatedly establish long and short positions during the rising and falling phases of the product. The strict stop-loss mechanism also makes this strategy stronger in risk control. However, as a single indicator strategy, the failure of the parabola will also have a greater impact on the strategy. Therefore, this is a strategy that has certain advantages and potential, but also has certain risks. It needs to be tested and continuously optimized according to the actual situation in order to generate sustained and stable excess returns.
||

## Overview

This strategy utilizes the crossover operation between the Parabolic SAR sliding value and candlestick to achieve momentum tracking and stop loss for swing trading. The strategy will establish long and short positions when the price is rising and falling. It will close out these positions to stop loss when the price reverses.

## Strategy Logic  

The core of this strategy relies on the Parabolic SAR indicator to determine whether the current price is in an upward or downward trend. When the Parabolic SAR indicator is below the candlestick, it means that the price is currently rising. In this case, the strategy will check at the close of each candlestick whether the Parabolic SAR value crosses above the low of the candlestick. If not, it means the upward trend continues and the strategy will establish a long position. If Parabolic SAR crosses above the low, it means the upside trend reverses downside, and the strategy will close the long position to stop loss. 

On the contrary, when Parabolic SAR is above the candlestick, it means the price is currently falling. In this case, the strategy will check at the close of each candlestick whether Parabolic SAR crosses below the high of the candlestick. If not, it will establish a short position. If Parabolic SAR crosses the high, it means the downside trend reverses upside, and the strategy will close the short position to stop loss.

Through this logic, the strategy can establish positions along the price trend and realize stop loss in the first time when trend reverses, locking in profits. Meanwhile, Parabolic SAR as a momentum indicator can more accurately determine whether the trend is reversed, making the stop loss more precise.

## Advantages

1. Parabolic SAR is an advanced and accurate technical indicator to determine trend and reversal points, improving judgment accuracy.
2. Taking advantage of momentum tracking and reversal stop loss methods can make full use of trending opportunities.  
3. The strict stop loss rules mean good risk control capability.
4. Optimized parameters make this strategy particularly suitable for GBP/JPY with strong trend.

## Risks

1. Like any single indicator strategies, this strategy may suffer from Parabolic SAR's misjudgement on trend and reversals. Invalid signals may lead to unnecessary losses.  
2. The strategy fully depends on Parabolic SAR for entries and exits. Improper parameter settings and loose stop loss points may fail to control risks effectively.
3. Any single strategy may gradually deteriorate due to changing market structure and environments. Regular backtests and optimizations are necessary.

Methods to enhance robustness include: optimizing stop loss points to make them strict enough; combining other indicators for confirmation; adjusting parameters to adapt to changing environments; selecting optimal parameter sets for different products, etc.

## Optimization Directions

1. Test and optimize combinations of Parabolic SAR parameters for better performance.
2. Combine other indicators like MACD, KD to form a multi-indicator confirmation system, improving signal reliability. 
3. Test effects of different stop loss methods like trail stop loss, time stop loss, price stop loss, etc.
4. Optimize parameters based on different product characteristics so that the strategy can achieve good returns across products.

## Conclusion

In general, this Parabolic SAR swing strategy is quite an effective short-term trading strategy. It takes advantage of Parabolic SAR to determine trend direction and momentum changes, together with swing trading methods, to repeatedly establish long and short positions during uptrends and downtrends. The strict stop loss mechanism also gives this strategy decent risk control capability. But as a single indicator strategy, the invalidity of Parabolic SAR will have a significant impact. So this is a strategy with some strength and potential, but also has some risks. It needs backtests, optimizations and enhancements to generate stable excess returns in live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.05|start|
|v_input_2|0.075|increment|
|v_input_3|true|maximum|
|v_input_4|true|From Day|
|v_input_5|true|From Month|
|v_input_6|2000|From Year|
|v_input_7|31|To Day|
|v_input_8|12|To Month|
|v_input_9|2020|To Year|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-14 00:00:00
end: 2023-12-21 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Parabolic SAR Strategy", overlay=true)
start = input(0.05)
increment = input(0.075)
maximum = input(1)

fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2000, title = "From Year", minval = 1970)
 //monday and session 
// To Date Inputs
toDay = input(defval = 31, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2020, title = "To Year", minval = 1970)

startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true

var bool uptrend = na
var float EP = na
var float SAR = na
var float AF = start
var float nextBarSAR = na
if bar_index > 0
	firstTrendBar = false
	SAR := nextBarSAR
	if bar_index == 1
		float prevSAR = na
		float prevEP = na
		lowPrev = low[1]
		highPrev = high[1]
		closeCur = close
		closePrev = close[1]
		if closeCur > closePrev
			uptrend := true
			EP := high
			prevSAR := lowPrev
			prevEP := high
		else
			uptrend := false
			EP := low
			prevSAR := highPrev
			prevEP := low
		firstTrendBar := true
		SAR := prevSAR + start * (prevEP - prevSAR)
	if uptrend
		if SAR > low
			firstTrendBar := true
			uptrend := false
			SAR := max(EP, high)
			EP := low
			AF := start
	else
		if SAR < high
			firstTrendBar := true
			uptrend := true
			SAR := min(EP, low)
			EP := high
			AF := start
	if not firstTrendBar
		if uptrend
			if high > EP
				EP := high
				AF := min(AF + increment, maximum)
		else
			if low < EP
				EP := low
				AF := min(AF + increment, maximum)
	if uptrend
		SAR := min(SAR, low[1])
		if bar_index > 1
			SAR := min(SAR, low[2])
	else
		SAR := max(SAR, high[1])
		if bar_index > 1
			SAR := max(SAR, high[2])
	nextBarSAR := SAR + AF * (EP - SAR)
	if barstate.isconfirmed and time_cond
		if uptrend
			strategy.entry("ParSE", strategy.short, stop=nextBarSAR, comment="ParSE")
			strategy.cancel("ParLE")
		else
			strategy.entry("ParLE", strategy.long, stop=nextBarSAR, comment="ParLE")
			strategy.cancel("ParSE")
plot(SAR, style=plot.style_cross, linewidth=3, color=color.orange)
plot(nextBarSAR, style=plot.style_cross, linewidth=3, color=color.aqua)
//plot(strategy.equity, title="equity", color=color.red, linewidth=2, style=plot.style_areabr)
```

> Detail

https://www.fmz.com/strategy/436247

> Last Modified

2023-12-22 14:45:12

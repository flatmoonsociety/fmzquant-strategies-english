
> Name

Trend Following Stop Loss Reversal Strategy-Parabolic-SAR-Trend-Tracking-Stop-Loss-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/56bccf837b3bbcb73c1edc4b6b8f7951fa056d3d20c31e0d2ed41d9ad5e10600.png)
[trans]

## Overview
The Trend Following Stop Reversal Strategy is a strategy that utilizes the Parabolic SAR indicator to identify trends and enter opposite positions when the trend reverses. This strategy combines both stop-loss and take-profit mechanisms to control risk.
## Strategy Principle
This strategy uses the Parabolic SAR indicator to determine current market trends. Parabolic SAR full name is "Parabolic Stop and Reverse", which means parabolic stop loss reversal. Its indicator lines resemble a series of parabolas on the price chart, and these parabolic points represent possible reversal points.
When the SAR points fall and are below the price, it represents a bullish trend; when the SAR points rise and are above the price, it represents a bearish trend. This strategy is to judge the current trend direction based on the SAR point position.
Specifically, the strategy takes a short position when the SAR point is trending up and above price, and takes a long position when the SAR point is trending down and below price. That is, enter a reverse position when the SAR point indicates a trend reversal.
In addition, this strategy also sets up stop-loss and take-profit mechanisms. When going long, it is possible to set a stop-loss price to limit losses; at the same time, it is possible to set a take-profit price to close the position after the price reaches a certain target profit. Short selling has a similar mechanism.
## Advantage Analysis
This strategy combines trend indicators and stop-loss/take-profit mechanisms and has the following main advantages:
1. Able to capture trend reversal opportunities in a timely manner and implement reverse operations.
2. After setting stop loss and take profit, you can actively control risks and profits.
3. Parabolic SAR is a very commonly used trend reversal indicator with good effect.
4. The policy rules are simple and clear, easy to understand and implement.
## Risk Analysis
There are also some risks to be aware of with this strategy:
1. The Parabolic SAR indicator is not perfect and sometimes sends out wrong signals.
2. The stop loss or take profit price needs to be reasonable, otherwise the stop loss or take profit may be premature. 
3. Transaction fees will also affect the final profit.
4. The lengthening of the new trend after the reversal may be relatively short-lived.
These risks can be solved by adjusting parameter optimization or filtering with other indicators.
## Optimization direction
This strategy can be optimized from the following directions:
1. Optimize the parameters of Parabolic SAR and find the best parameter combination.
2. Try different stop loss and take profit strategies, such as trailing stop loss, etc.
3. Add indicators or conditions to filter reversal trading signals.
4. Add position control to expand or reduce positions according to market conditions.
5. Adjust parameters for different trading varieties.
## Summarize
This trend tracking stop-loss reversal strategy is generally a more classic trading strategy idea. It has the function of identifying trend reversal, and at the same time, it is supplemented by stop loss and take profit means to control risks. Through optimization, it can become a strategic idea worthy of real offer.
||

## Overview  

The Parabolic SAR Trend Tracking Stop Loss Reversal Strategy is a strategy that uses the Parabolic SAR indicator to identify trends and enter counter trend positions when the trend reverses. The strategy also incorporates stop loss and take profit mechanisms to control risk.  

## Strategy Logic

The strategy uses the Parabolic SAR indicator to judge the current market trend. Parabolic SAR stands for "Parabolic Stop and Reverse". Its indicator lines form a series of parabolas on the price chart, and these parabola points represent potential reversal points.  

When the SAR points are falling and below the price, it represents a bullish trend; when the SAR points are rising and above the price, it represents a bearish trend. The strategy judges the current trend direction based on the SAR points' location.   

Specifically, when SAR points show an uptrend and are above prices, the strategy will go short; when SAR points show a downtrend and are below prices, the strategy will go long. That is entering counter trend positions when SAR points indicate trend reversal.  

In addition, the strategy also sets stop loss and take profit mechanisms. When going long, it may set a stop loss price to limit losses; at the same time, it may set a take profit price to close positions after reaching a certain target profit. Going short is similar.

## Advantage Analysis   

The main advantages combining the trend indicator and stop loss/take profit mechanisms are:  

1. Timely capture reverse trend opportunities for counter trend trading.  
2. Actively control risks and profits by setting stop loss and take profit.
3. Parabolic SAR is a widely used and effective reverse indicator.  
4. Simple and clear strategy rules, easy to understand and implement.

## Risk Analysis

There are also some risks to note for the strategy:   

1. Parabolic SAR indicator is not perfect, sometimes it generates wrong signals.  
2. The stop loss and take profit prices need to be set reasonably, otherwise it may stop out or take profit prematurely.  
3. Trading commissions also affect total profits. 
4. The new trend after reversal may be short-lived.  

These risks can be solved by parameter optimization, using other filter indicators etc.

## Optimization Directions   

The strategy can be optimized in the following aspects:

1. Optimize the Parabolic SAR parameters to find the best combination.  
2. Try different stop loss and take profit strategies like trailing stop loss. 
3. Add indicators or conditions to filter reverse trading signals. 
4. Add position control based on market conditions.
5. Adjust parameters for different trading instruments.  

## Conclusion  

In general, this is a rather classical trend tracking stop loss reversal strategy. It identifies trend reversals and also controls risks with stop loss and take profit means. After optimizations it can become a worthwhile strategy for live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.02|start|
|v_input_2|0.02|increment|
|v_input_3|0.2|maximum|
|v_input_4|false|(?Stop Loss and Take Profit)Short Stop Loss|
|v_input_5|5|(%)|
|v_input_6|false|Long Stop Loss|
|v_input_7|5|(%)|
|v_input_8|false|Short Take Profit|
|v_input_9|20|(%)|
|v_input_10|false|Long Take Profit|
|v_input_11|20|(%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-24 00:00:00
end: 2024-01-31 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Parabolic SAR Strategy", overlay=true)
start = input(0.02)
increment = input(0.02)
maximum = input(0.2)
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
	if barstate.isconfirmed
		if uptrend
			strategy.entry("ParSE", strategy.short, stop=nextBarSAR, comment="ParSE")
			strategy.cancel("ParLE")
		else
			strategy.entry("ParLE", strategy.long, stop=nextBarSAR, comment="ParLE")
			strategy.cancel("ParSE")
plot(SAR, style=plot.style_cross, linewidth=3, color=color.orange)
plot(nextBarSAR, style=plot.style_cross, linewidth=3, color=color.aqua)
//Stop Loss Inputs
use_short_stop_loss = input(false, title="Short Stop Loss", group="Stop Loss and Take Profit", inline="Short_SL")
short_stop_loss = input(title="(%)", type=input.float, minval=0.0, step=0.1, 
     defval=5, group="Stop Loss and Take Profit", inline="Short_SL") * 0.01
use_long_stop_loss = input(false, title="Long Stop Loss", group="Stop Loss and Take Profit", inline="Long_SL")
long_stop_loss = input(title="(%)", type=input.float, minval=0.0, step=0.1, 
     defval=5, group="Stop Loss and Take Profit", inline="Long_SL") * 0.01

//Take Profit Inputs     
use_short_take_profit = input(false, title="Short Take Profit", group="Stop Loss and Take Profit", inline="Short_TP")
short_take_profit = input(title="(%)", type=input.float, minval=0.0, step=0.1,
     defval = 20, group="Stop Loss and Take Profit", inline="Short_TP") * .01
use_long_take_profit = input(false, title="Long Take Profit", group="Stop Loss and Take Profit", inline="Long_TP")
long_take_profit = input(title="(%)", type=input.float, minval=0.0, step=0.1,
     defval = 20, group="Stop Loss and Take Profit", inline="Long_TP") * .01


longStopPrice  = strategy.position_avg_price * (1 - long_stop_loss)
shortStopPrice = strategy.position_avg_price * (1 + short_stop_loss)
longLimitPrice = strategy.position_avg_price * (1 + long_take_profit)
shortLimitPrice = strategy.position_avg_price * (1 - short_take_profit)


if (strategy.position_size > 0.0)
    if (use_long_stop_loss and not use_long_take_profit)
        strategy.exit("Long", stop = longStopPrice)
    if (use_long_take_profit and not use_long_stop_loss)
        strategy.exit("Long", limit = longLimitPrice)
    if (use_long_take_profit and use_long_stop_loss)
        strategy.exit("Long", stop = longStopPrice, limit=longLimitPrice)
if (strategy.position_size < 0.0)
    if (use_short_stop_loss and not use_short_take_profit)
        strategy.exit("Short", stop = shortStopPrice)
    if (use_short_take_profit and not use_short_stop_loss)
        strategy.exit("Short", limit = shortLimitPrice)
    if (use_short_take_profit and use_short_stop_loss)
        strategy.exit("Short", stop = shortStopPrice, limit = shortLimitPrice)

//plot(strategy.equity, title="equity", color=color.red, linewidth=2, style=plot.style_areabr)
```

> Detail

https://www.fmz.com/strategy/440722

> Last Modified

2024-02-01 14:54:09

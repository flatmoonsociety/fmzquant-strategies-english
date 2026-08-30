
> Name

An-Intraday-Trend-Following-Quantitative-Strategy-Based-on-Multi-indicator-Condition-Filtering
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/11476a635c4f5dec576.png)

[trans]

## Overview
This strategy comprehensively uses the PSAR indicator to determine the price trend, the ADX indicator to determine the strength of the trend, the RSI indicator to locate overbought and oversold areas, and the CMF indicator to determine the flow of funds, to build a cross-cycle trend-following quantitative trading strategy. This strategy quickly locates when it determines that the price has consolidated and broken through to form a new trend direction, and continues to track the subsequent trend. It ensures that the main trend returns are captured while also setting process filtering conditions to reduce position risks.
## Strategy Principle
The main judgment rules of this strategy are as follows:
1. Use the PSAR indicator to determine whether the price is in an upward trend. When PSAR crosses the price below, it is deemed to have ended the upward trend and turned into a downward trend;
2. The RSI indicator is required to be higher than the midline 50 to filter out false breakthroughs formed in the oversold area;
3. The ADX requirement is higher than its own EMA moving average, indicating that there is a continuous signal in the trend analysis results;
4. If the CMF requirement is greater than 0, it is judged as capital inflow;
A buy signal is generated when the above four conditions are met; a sell signal is generated when PSAR crosses above, RSI is below 50, ADX is below its own EMA moving average, and CMF is less than 0.
This strategy comprehensively considers the price trend direction, trend intensity, overbought and oversold status, and capital flow to set trading rules from multiple dimensions. It sets strict logical judgments when judging the generation of trading signals, which can effectively filter out false breakthroughs and ensure that high-probability sustainable trend directions are captured.
## Advantage Analysis
This strategy mainly has the following advantages:
1. Combining multiple indicators to set trading rules can effectively prevent false breakthroughs and ensure the quality of trading signals;
2. Quickly locate and track emerging trend directions to fully grasp the benefits of the trend process;
3. Set process tracking filter conditions to effectively control risks and ensure tracking effects;
4. Combined with the judgment of trend strength indicators, you can avoid falling into consolidation difficulties.
## Risk Analysis
This strategy mainly involves the following risks:
1. A single strategy can easily accumulate risks, and positions need to be appropriately adjusted to control overall risks;
2. During the tracking process, it is necessary to pay close attention to changes in filtering conditions to avoid loss cut after the conditions are cancelled;
3. This strategy is mainly medium and long-term, and is susceptible to fluctuations in the short term, resulting in stop loss risks.
Corresponding risk management measures include: optimizing position management rules, setting risk warning lines, appropriately relaxing the distance of stop loss lines, etc.
## Optimization direction
This strategy has the following room for optimization:
1. Optimize parameter settings. Currently, parameter settings are relatively subjective, and machine learning methods can be introduced for automatic optimization;
2. Add a position management module, which can dynamically adjust positions according to risk status;
3. Add stop loss mechanism optimization, such as trailing stop loss, time stop loss, breakthrough stop loss, etc.
## Summarize
This strategy combines a variety of indicator judgment rules to achieve rapid positioning and continuous tracking of emerging trends, and verifies the effect of quantitative trading combining multi-dimensional analysis such as trends and funds. This strategy can be used as a basic strategy for cross-cycle trend tracking for exponential use, or it can be constructed into a stable mid- and long-term quantitative strategy after parameter and module optimization.
||

## Overview  

This strategy combines PSAR to judge price trends, ADX to judge trend strength, RSI to locate overbought and oversold zones, and CMF to judge fund flows to construct an intraday trend-following quantitative trading strategy across cycles. It can quickly locate new trend directions when prices break out of consolidation and form new trends, and continues to track trends afterwards. While ensuring that main trend gains are captured, filtering conditions are also set during the process to reduce holding risks.

## Principles

The main judging rules of this strategy are:

1. Use the PSAR indicator to judge whether prices are in an uptrend. PSAR’s decline below prices indicates the end of the upward trend and the start of a downward trend.

2. Require RSI to be above the midpoint of 50 to filter out false breakouts occurring in oversold zones.  

3. Require ADX to be above its EMA line, indicating a sustainable signal in trend analysis.

4. Require CMF to be greater than 0, judging increased funds flowing in.

Buying signals are generated when all four conditions above are met. Selling conditions occur when PSAR rises above prices, RSI drops below 50, ADX drops below its EMA and CMF becomes less than 0.

This strategy comprehensively considers the price trend direction, trend strength, the overbought/oversold state and fund flows when setting up trading rules. By setting strict logical rules when generating trading signals, false breakouts can be effectively filtered and high probability sustainable trend directions can be captured.  

## Advantages

The main advantages of this strategy include:

1. Combining multiple indicators in setting up trading rules can effectively prevent false breakouts and ensures signal quality.

2. Rapidly locating budding trend directions and tracking enables capturing most trend profits.

3. Setting up process filtering conditions can effectively control risks and ensures tracking efficacy. 

4. Considering trend strength helps avoiding trading range congestions.

## Risk Analysis   

The main risks of this strategy include:

1. A single strategy accumulation poses portfolio risks, requiring appropriate position sizing.

2. Closely monitor filtering condition changes during tracking to avoid losses when cancelled.

3. This mid/long-term strategy can be disrupted short-term by fluctuations and incurs stop loss risks.

Corresponding risk management measures include: optimizing position sizing rules, setting risk alert lines and widening stop distances etc.

## Optimization Directions

Optimization spaces include:

1. Parameter optimization via machine learning given current subjective settings.

2. Add position sizing module that dynamically sizes based on risks. 

3. Enhance stop mechanisms e.g. trailing stops, time stops or breakout stops. 

## Conclusion

This strategy combining indicators proved effective in rapidly locating and tracking nascent trends, validating quantitative trading based on multiple dimensions like trends and funds. As a base, it can be indexed across cycles. With parameter tuning and modular enhancements, it can also become a stable mid/long-term strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|1.02|start|
|v_input_2|1.02|increment|
|v_input_3|1.2|maximum|
|v_input_4|50|length|
|v_input_5|49|middle_RSI|
|v_input_6|20|lengthCMF|
|v_input_7|14|ADX Smoothing|
|v_input_8|14|DI Length|
|v_input_9|10|ema_length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-14 00:00:00
end: 2023-12-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("psar+ adx + cmf + rsi Strategy", overlay=true,initial_capital = 1000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent , commission_value=0.1 )

start = input(1.02)
increment = input(1.02)
maximum = input(1.2)
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

//rsi strat
length = input( 50 )
middle_RSI=input(49)
price = close
vrsi = rsi(price, length)

//cmf
lengthCMF = input(20, minval=1)
ad = close==high and close==low or high==low ? 0 : ((2*close-low-high)/(high-low))*volume
mf = sum(ad, lengthCMF) / sum(volume, lengthCMF)

//ADX
adxlen = input(14, title="ADX Smoothing")
dilen = input(14, title="DI Length")
dirmov(len) =>
	up = change(high)
	down = -change(low)
	plusDM = na(up) ? na : (up > down and up > 0 ? up : 0)
	minusDM = na(down) ? na : (down > up and down > 0 ? down : 0)
	truerange = rma(tr, len)
	plus = fixnan(100 * rma(plusDM, len) / truerange)
	minus = fixnan(100 * rma(minusDM, len) / truerange)
	[plus, minus]
adx(dilen, adxlen) =>
	[plus, minus] = dirmov(dilen)
	sum = plus + minus
	adx = 100 * rma(abs(plus - minus) / (sum == 0 ? 1 : sum), adxlen)
sig = adx(dilen, adxlen)
ema_length=input(10)
ema_sig= ema(sig,ema_length)


long = not uptrend  and vrsi > middle_RSI and sig > ema_sig   and mf>0 
short= uptrend   and vrsi < middle_RSI and sig<ema_sig and mf<0

strategy.entry("long",1,when=long)
strategy.close('long',when=short)
```

> Detail

https://www.fmz.com/strategy/435509

> Last Modified

2023-12-15 15:59:37

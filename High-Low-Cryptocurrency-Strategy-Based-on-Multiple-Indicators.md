
> Name

High-Low-Cryptocurrency-Strategy-Based-on-Multiple-Indicators
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1c4fec07cef3c2a069e.png)
[trans]

## Overview
This strategy is a high-low strategy for the cryptocurrency market. It comprehensively uses multiple indicators such as MACD, PSAR, ATR, Elliott wave, etc. to conduct transactions in higher time periods such as 1 hour, 4 hours or 1 day. The advantage of the strategy is that the risk-return rate is high, and the average profit factor can reach 1.5-2.5.
## Strategy Principle
The trading signals of this strategy come from the comprehensive judgment of price high and low points and multiple indicators. The specific logic is:
1. Determine whether the K-line has a high or low price range, that is, the high points make consecutive new highs and the low points make consecutive new lows.
2. Check the MACD histogram levels.
3. Check the PSAR indicator to determine the trend direction.
4. Check the trend indicators made by ATR and MA to determine the trend direction.
5. Check the Elliott Wave indicator to confirm the trend direction.
If the above five conditions all point in the same direction, a long or short signal is generated.
## Strategic Advantages
1. The risk-reward ratio is high, up to 1:30.
2. The average profit factor is high, generally between 1.5-2.5.
3. Multiple indicator combinations can effectively filter out false breakthroughs.
## Strategy Risk
1. The winning rate is low, only 10%-20%.
2. There is a certain risk of retracement and seesawing.
3. The indicator effect will be affected by the market environment.
4. Requires strong mental endurance.
Countermeasures:
1. Increase the trading capital size to balance the winning rate.
2. Strictly control single stop loss.
3. Adjust indicator parameters according to different markets.
4. Do a good job in psychological construction and control the size of the location.
## Optimization direction
1. Test indicator parameters based on different cryptocurrencies and market environments.
2. Add stop-loss and take-profit strategies to optimize fund management.
3. Combine with machine learning methods to improve your winning rate.
4. Add social sentiment indicators to filter trading signals.
5. Consider multi-time period indicator confirmation.
## Summarize
Overall, this strategy is a high-risk, high-yield trading strategy suitable for cryptocurrency. Its advantage is that it has a high risk-return rate and can obtain a high average profit factor. The risk mainly lies in the low winning rate, which requires strong psychological endurance. The next step of optimization can be carried out from multiple dimensions such as adjusting parameters, optimizing fund management, and improving winning rate. Overall, this strategy has certain practical value for cryptocurrency traders looking for high returns.
|| 

## Overview  

This strategy is a high/low level strategy suitable for cryptocurrency markets. It integrates MACD, PSAR, ATR, Elliott Wave and other multiple indicators for trading at higher timeframes like 1 hour, 4 hours or 1 day. The advantage of this strategy lies in the high risk reward ratio with average profit factor ranging from 1.5 to 2.5.  

## Strategy Logic  

The trading signals of this strategy come from the price high/low levels and composite judgments of multiple indicators. The specific logic is:

1. Judge if there is a high/low level range formed by successive higher highs or lower lows on the price chart.  

2. Check the histogram level of MACD.

3. Check PSAR indicator for trend direction.

4. Check trend direction based on ATR and MA.  

5. Confirm trend direction with Elliott Wave indicator.

If all the 5 conditions point to the same direction,  long or short signals are generated.

## Advantages

1. High risk reward ratio up to 1:30.  

2. High average profit factor, usually between 1.5-2.5.

3. Combination of multiple indicators helps filter false breakouts effectively.

## Risks  

1. Relatively low win rate around 10%-20%.  

2. Potential drawdown and whipsaw risks exist.

3. Indicator performance could be impacted by market regimes.

4. Need decent psychological endurance.

Corresponding Measures:

1. Increase capital to balance the win rate.

2. Set strict stop loss for each trade.  

3. Adjust parameters based on different markets.

4. Strengthen psychology and control position sizing.

## Optimization Directions 

1. Test parameters based on different cryptos and markets.

2. Add stop loss and take profit to optimize money management. 

3. Increase win rate with machine learning methods. 

4. Add social sentiment filter for trading signals.

5. Consider confirmation across multiple timeframes.

## Conclusion  

In conclusion, this is an aggressive high risk high return cryptocurrency trading strategy. Its advantage lies in the high risk reward ratio and profit factor. The main risks come from the relatively low win rate which requires strong psychology. The future optimization directions could be parameter tuning, money management, increasing win rate and so on. Overall this strategy has practical value for cryptocurrency traders seeking high profits.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|Fast Length|
|v_input_2|26|Slow Length|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_4|9|Signal Smoothing|
|v_input_5|true|Simple MA(Oscillator)|
|v_input_6|false|Simple MA(Signal Line)|
|v_input_7|0.02|start|
|v_input_8|0.02|increment|
|v_input_9|0.2|maximum|
|v_input_10|20|CCI|
|v_input_11|5|ATR|
|v_input_12|true|ATR Multiplier|
|v_input_13|true|original coloring|
|v_input_14_close|0|source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_15|5|sma1length|
|v_input_16|35|sma2length|
|v_input_17|true|Show Dif as percent of current Candle|
|v_input_18|0.15|tp|
|v_input_19|0.005|sl|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-21 00:00:00
end: 2023-12-28 00:00:00
period: 45m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © SoftKill21

//@version=4
strategy("Crypto strategy high/low", overlay=true)
fast_length = input(title="Fast Length", type=input.integer, defval=12)
slow_length = input(title="Slow Length", type=input.integer, defval=26)
src = input(title="Source", type=input.source, defval=close)
signal_length = input(title="Signal Smoothing", type=input.integer, minval = 1, maxval = 50, defval = 9)
sma_source = input(title="Simple MA(Oscillator)", type=input.bool, defval=true)
sma_signal = input(title="Simple MA(Signal Line)", type=input.bool, defval=false)
//sar
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


// Calculating
fast_ma = sma_source ? sma(src, fast_length) : ema(src, fast_length)
slow_ma = sma_source ? sma(src, slow_length) : ema(src, slow_length)
macd = fast_ma - slow_ma
signal = sma_signal ? sma(macd, signal_length) : ema(macd, signal_length)
hist = macd - signal

CCI = input(20)
ATR = input(5)
Multiplier=input(1,title='ATR Multiplier')
original=input(true,title='original coloring')
thisCCI = cci(close, CCI)
lastCCI = nz(thisCCI[1])
bufferDn= high + Multiplier * sma(tr,ATR)
bufferUp= low - Multiplier * sma(tr,ATR)
if (thisCCI >= 0 and lastCCI < 0) 
    bufferUp := bufferDn[1]
if (thisCCI <= 0 and lastCCI > 0) 
    bufferDn := bufferUp[1]

if (thisCCI >= 0)
    if (bufferUp < bufferUp[1])
        bufferUp := bufferUp[1]
else
    if (thisCCI <= 0)
        if (bufferDn > bufferDn[1])
            bufferDn := bufferDn[1]
x=0.0
x:=thisCCI >= 0 ?bufferUp:thisCCI <= 0 ?bufferDn:x[1]
swap=0.0

swap:=x>x[1]?1:x<x[1]?-1:swap[1]

swap2=swap==1?color.lime:color.red
swap3=thisCCI >=0 ?color.lime:color.red
swap4=original?swap3:swap2

//elliot wave
srce = input(close, title="source")
sma1length = input(5)
sma2length = input(35)
UsePercent = input(title="Show Dif as percent of current Candle", type=input.bool, defval=true)
smadif=iff(UsePercent,(sma(srce, sma1length) - sma(srce, sma2length)) / srce * 100, sma(srce, sma1length) - sma(srce, sma2length))
col=smadif <= 0 ? color.red : color.green

longC = high > high[1] and high[1] > high[2] and close[2] > high[3] and hist > 0 and uptrend and smadif < 0 and swap4==color.lime 
//longC = high > high[1] and high[1] > high[2] and high[2] > high[3] and high[3] > high[4] and close[4] > high[5]
shortC = low < low[1] and low[1] < low[2] and close[2] < low[3] and hist < 0 and not uptrend and  smadif > 0 and swap4==color.red 
//shortC = low < low[1] and low[1] < low[2] and low[2] < low[3] and low[3] < low[4] and close[4] < low[5]

tp=input(0.15, title="tp")
sl=input(0.005, title="sl")


strategy.entry("long",1,when=longC)
strategy.entry("short",0,when=shortC)

strategy.exit("x_long", "long" ,loss = close * sl / syminfo.mintick, profit = close * tp / syminfo.mintick , alert_message = "closelong")
//strategy.entry("short",0, when= loss = close * sl / syminfo.mintick)

strategy.exit("x_short", "short" , loss = close * sl / syminfo.mintick, profit  = close * tp / syminfo.mintick,alert_message = "closeshort")
//strategy.entry("long",1, when = loss = close * sl / syminfo.mintick)

//strategy.close("long",when= hist < 0)
//strategy.close("short", when= hist > 0)
```

> Detail

https://www.fmz.com/strategy/437004

> Last Modified

2023-12-29 14:16:16

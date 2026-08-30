
> Name

Comprehensive technical indicator strategyMulti-indicator-Combination-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses a variety of technical indicators to judge price trends and issue buy and sell signals.
## Strategy Principle
This strategy mainly judges price trends based on the following technical indicators:
1. Super Trend Indicator (SuperTrend): Calculate the upper and lower rails based on ATR. If the price breaks through the upper rail, go long, and when the price breaks through the lower rail, go short;
2. Simple Moving Average (SMA): When the price crosses the SMA above, go long, and when the price crosses the SMA below, go short;
3. Momentum indicator (Momentum): If the price momentum is positive, go long, if the price momentum is negative, go short;
4. MACD: DIFF goes long when it breaks through the DEA line upwards, and goes short when it breaks through the DEA line downwards;
5. Bull and Bear: If the bull’s power is greater than the bear’s power, go long, otherwise go short;
6. RSI: RSI goes long when it crosses the 30 line above, and short when it crosses the 70 line below;
7. Yang lines and Yin lines: go short on N consecutive Yin lines and go long on N consecutive Yin lines;
8. CCI: Go long when CCI is greater than 100, go short when less than -100;
9. DMI: If the DMI long line is greater than the short line, go long, otherwise go short;
10. Market waves: judge whether the price is going long when the price is rising, or short when the price is falling;
11. Stochastic indicator: The stochastic indicator goes long when it crosses the 20 line above, and short when it crosses the 80 line below.
The results calculated by these Indicators give a point number of 1 or -1 depending on the upward or downward direction. Add up the points of all Indicators to get the total points. When the total points cross the 0 line, a buy signal is generated; when the total points cross the 0 line, a sell signal is generated.
## Advantage Analysis
The biggest advantage of this multi-Indicator combination strategy is its high reliability. Due to the comprehensive use of multiple Indicators to determine the trend direction, false signals can be effectively reduced and the signals are more reliable. Compared with a single Indicator, this combination strategy will have better reliability and stability.
Another advantage is the flexibility and customizability of the strategy. Indicator types and parameter settings can be adjusted according to different markets, making the strategy more adaptable to different market environments. You can also adjust the weight of the Indicator based on the backtest results.
## Risk Analysis
This type of combination strategy also has some risks that need to be noted:
1. If the correlation between the selected Indicators is too high, there will be a risk of repeated signals. This requires selecting indicators with low correlation for combination according to different market environments.
2. If there are too many Indicators and the calculation time is too long, it will affect the timeliness of signal sending. There is a trade-off between the number of Indicators and timeliness.
3. Improper setting of Indicator parameters will also affect the strategy effect, and full backtesting is required to find the best parameters.
4. In different market stages, the effect of Indicator will be different. Its effectiveness needs to be constantly checked through rolling backtesting.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the type and quantity of Indicators and select the best combination;
2. Optimize the parameter settings of each Indicator;
3. Adjust the weight ratio of Indicators and increase the weight of key Indicators;
4. Add conditional filtering, such as a surge in trading volume, to avoid false breakthroughs;
5. Use model combination method to automatically find the optimal strategy combination through machine learning algorithm.
## Summarize
To sum up, this multi-Indicator combination strategy uses the advantages of various Indicators to determine the trend direction, which can reduce false signals and improve the reliability of signals. By optimizing the selection of Indicators, parameter settings, weight distribution, etc., the stability of the strategy can be continuously improved. This type of combination strategy is suitable for strategic traders who have high requirements for the stability of indicator signals.
||


## Overview

This strategy combines multiple technical indicators to judge the price trend and generate buy and sell signals.

## Strategy Principle 

The strategy mainly uses the following indicators to determine the price trend:

1. SuperTrend: Buy when price breaks above the upper band, sell when breaks below the lower band.

2. SMA: Buy when price crosses above SMA, sell when crosses below SMA.

3. Momentum: Go long when momentum is positive, go short when negative.

4. MACD: Buy when DIFF crosses above DEA, sell when crosses below.

5. Bull and Bear: Go long when bull power > bear power, vice versa.

6. RSI: Buy when RSI crosses above 30, sell when crosses below 70. 

7. Candlesticks: Go long after N bullish bars, go short after N bearish bars.

8. CCI: Buy when CCI > 100, sell when CCI < -100.

9. DMI: Go long when DMI+ > DMI-, else go short.

10. Market Waves: Go long in upward waves, go short in downward waves.

11. Stochastics: Buy when %K crosses above 20, sell when crosses below 80.

The indicator signals are quantified as 1 or -1 depending on up or down direction. The total points are summed up. Buy when total points cross above 0, sell when cross below 0.

## Advantage Analysis

The biggest advantage of this multi-indicator strategy is higher reliability by combining signals from various indicators to filter out false signals. It is more robust than single indicator strategies.

Another advantage is the flexibility to customize indicators and parameters for different market conditions. The indicator weights can also be adjusted based on backtest results.

## Risk Analysis

Some risks to note in such combo strategies:

1. High correlation between indicators may generate duplicated signals. Indicators should be selected to have low correlation.

2. Too many indicators leads to delayed signals. There is a tradeoff between indicator quantity and timeliness.

3. Inappropriate indicator parameters impact strategy performance. Optimal parameters need to be found through thorough backtesting. 

4. Indicator efficiency varies across market regimes. Rolling backtests should check indicator validity.

## Optimization Directions 

This strategy can be improved in several ways:

1. Optimize indicator selection and number to find best combination.

2. Optimize parameters for each indicator. 

3. Adjust indicator weights to emphasize key indicators.  

4. Add filters like volume spike to avoid false breakouts.

5. Use machine learning models to automatically find optimal combinations.

## Conclusion

In summary, this multi-indicator strategy combines the strengths of various indicators to improve signal reliability and reduce false signals. Fine-tuning the indicator selection, parameters, and weights can further enhance the stability. It suits traders who require stable indicator signals.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|════════ Test Period ═══════|
|v_input_2|2017|Backtest Start Year|
|v_input_3|true|Backtest Start Month|
|v_input_4|true|Backtest Start Day|
|v_input_5|2019|Backtest Stop Year|
|v_input_6|12|Backtest Stop Month|
|v_input_7|31|Backtest Stop Day|
|v_input_8_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_9|true|piz|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-10-06 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Super indicator ", overlay=true, precision=2, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.075)

/////////////// Time Frame ///////////////
_0 = input(false,  "════════ Test Period ═══════")
testStartYear = input(2017, "Backtest Start Year") 
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay, 0, 0)

testStopYear = input(2019, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay, 0, 0)

testPeriod() =>true


hilow = ((high - low)*100)
openclose = ((close - open)*100)
vol1 = (volume / hilow)
spreadvol = (openclose * vol1)
VPT = spreadvol + cum(spreadvol)
window_len = 28

v_len = 14
price_spread = stdev(high-low, window_len)

vp =  spreadvol + cum(spreadvol)
smooth = sma(vp, v_len)
v_spread = stdev(vp - smooth, window_len)
shadow = (vp - smooth) / v_spread * price_spread

out1 = shadow > 0 ? high + shadow : low + shadow

//plot(out, style=line,linewidth=3, color=color)
len=5
vpt=ema(out1,len)


// INPUTS //
st_mult   =3
st_period = 7

// CALCULATIONS //
up_lev = vpt - (st_mult * atr(st_period))
dn_lev = vpt + (st_mult * atr(st_period))

up_trend   = 0.0
up_trend   := close[1] > up_trend[1]   ? max(up_lev, up_trend[1])   : up_lev

down_trend = 0.0
down_trend := close[1] < down_trend[1] ? min(dn_lev, down_trend[1]) : dn_lev

// Calculate trend var
trend10 = 0
trend10 := close > down_trend[1] ? 1: close < up_trend[1] ? -1 : nz(trend10[1], 1)

// Calculate SuperTrend Line
st_line = trend10 ==1 ? up_trend : down_trend

//
src = input(close, title="Source")
//sma
sma20 = sma(src, 20)
smapoint = 0
smapoint := src > sma20 ? smapoint + 1 : smapoint - 1


//AO
ao = sma(hl2,5) - sma(hl2,34)
aopoint = ao > 0 ? 1 : ao < 0 ? -1 : 0
//momentum
mom = src - src[14]
mompoint = mom > 0 ? 1 : mom < 0 ? -1 : 0
//MACD
fast_ma = ema(src, 12)
slow_ma = ema(src, 26)
macd = fast_ma - slow_ma
signal = ema(macd, 9)
hist = macd - signal
histpoint = hist > hist[1] ? 3 : -3

//Bull bear
Length = 30
r1=iff(close[1]<open,max(open-close[1],high-low),high-low)
r2=iff(close[1]>open,max(close[1]-open,high-low),high-low)
bull=iff(close==open,iff(high-close==close-low,iff(close[1]>open,max(high-open,close-low),r1),iff(high-close>close-low,iff(close[1]<open, max(high-close[1],close-low), high-open),r1)),iff(close<open,iff(close[1]<open,max(high-close[1],close-low), max(high-open,close-low)),r1))
bear=iff(close==open,iff(high-close==close-low,iff(close[1]<open,max(open-low,high-close),r2),iff(high-close>close-low,r2,iff(close[1]>open,max(close[1]-low,high-close), open-low))),iff(close<open,r2,iff(close[1]>open,max(close[1]-low,high-close),max(open-low,high-close))))
colors=iff(sma(bull-bear,Length)>0, color.green, color.red)
// barcolor(colors)
bbpoint = sma(bull-bear,Length)>0 ? 1 : -1
//UO
length7 = 7,
length14 = 14,
length28 = 28
average(bp, tr_, length) => sum(bp, length) / sum(tr_, length)
high_ = max(high, src[1])
low_ = min(low, src[1])
bp = src - low_
tr_ = high_ - low_
avg7 = average(bp, tr_, length7)
avg14 = average(bp, tr_, length14)
avg28 = average(bp, tr_, length28)
uoout = 100 * (4*avg7 + 2*avg14 + avg28)/7
uopoint = uoout > 70 ? 1 : uoout < 30 ? -1 : 0
//IC
conversionPeriods = 9
basePeriods = 26
laggingSpan2Periods = 52
displacement = 26
donchian(len) => avg(lowest(len), highest(len))
baseLine = donchian(basePeriods)
icpoint = src > baseLine ? 1 : -1

//HMA
hullma = wma(2*wma(src, 9/2)-wma(src, 21), round(sqrt(21)))
hmapoint = src > hullma ? 2 : -2
//
//
trendDetectionLength =4
float trend = na
float wave = na
float vol = na
mov = close>close[1] ? 1 : close<close[1] ? -1 : 0
trend := (mov != 0) and (mov != mov[1]) ? mov : nz(trend[1])
isTrending = rising(close, trendDetectionLength) or falling(close, trendDetectionLength)
wave := (trend != nz(wave[1])) and isTrending ? trend : nz(wave[1])
vol := wave == wave[1] ? (nz(vol[1])+volume) : volume
up1 = wave == 1 ? vol : 0
dn1 = wave == 1 ? 0 : vol
Weis= up1 > dn1 ? 2 : -2


//

roclen =20
ccilen =21
dilen = 5
dirmov(len) =>
	up = change(high)
	down = -change(low)
	truerange = rma(tr, len)
	plus = fixnan(100 * rma(up > down and up > 0 ? up : 0, len) / truerange)
	minus = fixnan(100 * rma(down > up and down > 0 ? down : 0, len) / truerange)
	[plus, minus]

f_draw_infopanel(_x, _y, _line, _text, _color)=>
    _rep_text = ""
    for _l = 0 to _line
        _rep_text := _rep_text + "\n"
    _rep_text := _rep_text + _text
    var label _la = na
    label.delete(_la)
    _la := label.new(
         x=_x, y=_y, 
         text=_rep_text, xloc=xloc.bar_time, yloc=yloc.price, 
         color=color.black, style=label.style_labelup, textcolor=_color, size=size.normal)

TD = 0
TS = 0
TD := close > close[4] ? nz(TD[1]) + 1 : 0
TS := close < close[4] ? nz(TS[1]) + 1 : 0
TDUp = TD - valuewhen(TD < TD[1], TD , 1 )
TDDn = TS - valuewhen(TS < TS[1], TS , 1 )
td = TDUp > 0 ? 2 : TDDn > 0 ? -2 : 0
roc = roc(close, roclen)
Roc=roc > 0 ? 1 : -1
cci = cci(close, ccilen)
CCI=cci > 0? 2 : -2
[plus, minus] = dirmov(dilen)
dmi = plus - minus
DMI= dmi >= 0? 2 : -2
//
STT=trend10 == 1 ? 1 : -1
//
periods = 2
smooth1 =  14
price = close
fn(src, length) => 
    MA_s= 0.0
    MA_s:=(src + nz(MA_s[1] * (length-1)))/length
    MA_s
r11 = ema( price, periods ) 
r22 = iff( price > r11, price - r11, 0 ) 
r3 = iff( price < r11, r11 - price, 0 ) 
r4 = fn( r22, smooth1 ) 
r5 = fn( r3, smooth1 ) 
rr = iff( r5 == 0, 100, 100 - ( 100 / ( 1 + ( r4 / r5 ) ) ) ) 

length = 20,fast = 7,slow = 13
//
src10 = rr
er = abs(change(src,length))/sum(abs(change(src10)),length)
dev = er*stdev(src10*2,fast) + (1-er)*stdev(src10*2,slow)
a = 0.
a := bar_index < 9 ? src10 : src10 > a[1] + dev ? src10 : src10 < a[1] - dev ? src10 : a[1]
//

rsi=fixnan(a > a[1] ? 3 : a < a[1] ?-3 : na)
//
totalpoints =rsi+td+STT+Roc+DMI+ CCI+Weis+smapoint  + aopoint + mompoint + histpoint  + bbpoint  + icpoint  + hmapoint
//
piz=input(1)
tt=sma(totalpoints,piz)

//

zero=0
down = crossunder(tt, 0) 
up = crossover(tt, -0) 

//Alerts
/////// Alerts /////
alertcondition(down,title="sell")
alertcondition(up,title="buy")
//
/////////////// Strategy /////////////// 
long = up
short = down

strategy.entry("Long", strategy.long, when = long) 
strategy.entry("Short", strategy.short, when = short) 

```

> Detail

https://www.fmz.com/strategy/428617

> Last Modified

2023-10-07 15:34:33

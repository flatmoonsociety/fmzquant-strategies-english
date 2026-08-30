
> Name

RSI indicator divergence trading strategy RSI-Divergence-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1ece2731905214f3ae2.png)

[trans]

## Overview
The RSI Divergence trading strategy gives buy and sell signals by identifying divergences between the RSI indicator and price action. This strategy also has functions such as stop loss, take profit, and trailing stop loss, which can effectively control risks.
## Principle
This strategy is primarily based on divergence of the RSI indicator to identify trading opportunities. Specifically, the strategy first calculates the RSI value within a certain period, and then draws the trend line of the RSI indicator. At the same time, the strategy also draws a trend line for the price. When the RSI line deviates from the price line, that is, the RSI rises and the price falls, or the RSI falls and the price rises, the strategic judgment may turn and generate a trading signal.
If it is recognized that the RSI line is rising at the low point and the price line is falling at the high point, a buy signal is given. If a falling high point of the RSI line and an rising low point of the price line are recognized, a sell signal is given. Once a trading signal is formed, the strategy can conduct appropriate transactions based on the RSI value.
In addition, the strategy also sets stop loss, take profit and trailing stop functions. Stop loss can control the risk of loss, take profit can lock in profits, and trailing stop loss can allow profits to continue running. These settings effectively manage risk on every trade.
## Advantages
This RSI divergence trading strategy offers the following advantages:
1. By capturing the divergence of the RSI indicator, price turning points can be discovered early.
2. The RSI indicator is widely used, and most trading software has built-in RSI indicators. This strategy is highly applicable.
3. The RSI indicator parameter setting is flexible, and the observation period can be adjusted according to the market to adapt to different market conditions.
4. Combined with stop loss, take profit and trailing stop loss settings, the risk of each transaction can be effectively controlled.
5. The frequency of strategic trading signals is moderate to avoid too intensive trading.
6. The strategic ideas are clear and easy to understand, making it easy to implement computer programs.
## Risk
There are also some risks with this strategy:
1. RSI divergence is not 100% reliable and false signals may appear. Signals need to be filtered in combination with other indicators.
2. In trending markets, RSI divergence signals may be invalid and should be avoided.
3. Improper setting of RSI parameters will also affect the strategy effect. Setting the period too short will increase trading frequency and risk.
4. If the stop loss point is set too small, the loss may be stopped prematurely; if the stop loss point is too large, the risk cannot be effectively controlled. There are trade-offs to the setup.
5. Trailing stop loss may stop loss prematurely when prices fluctuate violently. It is necessary to set a reasonable trailing stop distance based on market volatility.
The corresponding risks can be mitigated through the following measures:
1. Add other indicators, such as MACD, Bollinger Bands, etc., to filter signals and reduce false signals.
2. Only use this strategy in consolidation and shock markets, and avoid obvious trend markets.
3. Optimize RSI parameter settings and select the best cycle length. Simultaneously test the parameter preferences of different markets.
4. Set reasonable stop loss and take profit positions based on historical backtest data.
5. Adjust the width of the trailing stop based on market volatility and risk appetite.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Add other indicator judgments to filter trading signals and improve the reliability of signals.
2. Use machine learning technology to automatically optimize RSI parameter settings.
3. Design dynamic stop loss algorithms based on different market conditions. For example, expand the stop loss position in a volatile market and reduce the stop loss position in a trending market.
4. Design a dynamic position management algorithm to adjust the position size of each transaction based on factors such as market volatility.
5. Introduce the concept of volatility into trailing stop loss, and set the trailing stop loss distance according to the intensity of price fluctuations.
6. Try to deploy the strategy to other markets such as foreign exchange and cryptocurrency.
7. Build a quantitative trading system to realize automated trading of strategies.
## Summarize
This RSI Divergence trading strategy generates trading signals by capturing the divergence between the RSI indicator and price action. The advantage of the strategy is that it is simple, clear and easy to automate. At the same time, stop loss, take profit and trailing stop settings can also effectively control risks. However, the strategy also has some limitations. It requires a combination of multiple indicators to verify the signal, and is not suitable for strong trend markets. The strategy can be improved by optimizing parameter settings, adding signal filtering, and dynamic stop loss. If implemented systematically, this strategy can be used as one of the auxiliary strategies during consolidation and shock market conditions.
||

## Overview

The RSI Divergence trading strategy generates buy and sell signals by identifying divergences between the RSI indicator and price movement. The strategy also incorporates stop loss, take profit and trailing stop loss to effectively manage risks. 

## Principle 

This strategy mainly uses divergences in the RSI indicator to identify trading opportunities. Specifically, the strategy first calculates the RSI values over a certain period, then plots the trendlines for both the RSI indicator and price. When the RSI line diverges from the price line, i.e. RSI rises while price falls, or RSI falls while price rises, the strategy takes it as a sign of impending trend reversal and generates trading signals.

If the strategy detects the RSI line bottoming while the price line topping, a buy signal is generated. If the RSI line tops while the price line bottoms, a sell signal is generated. Once a trading signal occurs, the strategy can trade according to the RSI value size.

In addition, the strategy has stop loss, take profit and trailing stop loss features. Stop loss controls downside risks, take profit locks in profits, and trailing stop allows profits to run. These settings effectively manage the risks for each trade.

## Advantages

The RSI divergence trading strategy has the following advantages:

1. Capturing RSI divergences can early detect trend reversals.

2. RSI is widely used and available in most trading platforms. The strategy has high applicability. 

3. RSI parameters are flexible and can be adjusted for different market conditions.

4. The stop loss, take profit and trailing stop loss controls risk effectively.

5. The strategy has a moderate signal frequency, avoiding over-trading. 

6. The logic is simple and easy to program for automation.

## Risks

The strategy also has some risks:

1. RSI divergences are not completely reliable and may generate false signals. Other filters are needed.

2. Divergences may fail in strong trending markets, which should be avoided.

3. Improper RSI parameters can affect performance. Too short periods increase frequency and risk.

4. Stop loss set too tight cuts profits short; too loose fails to limit risk. Fine tuning is needed.

5. Trailing stop may stop out prematurely during volatile markets. Reasonable trailing width is required considering volatility.

The risks can be mitigated through:

1. Adding other indicators like MACD, Bollinger Bands to filter signals and reduce false signals.

2. Using the strategy only during range-bound sideways markets, avoiding strong trends.

3. Optimizing RSI parameters, selecting optimal lookback periods. Testing parameters for different markets.

4. Setting reasonable stop loss and take profit levels based on historical backtesting. 

5. Adjusting trailing stop distance based on market volatility and risk appetite.

## Optimization

The strategy can be improved in the following aspects:

1. Incorporate other indicators to filter signals and improve reliability. 

2. Utilize machine learning to auto optimize RSI parameters.

3. Design dynamic stop loss algorithms according to market regimes. Wider stops for ranging, tighter stops for trending markets.

4. Build dynamic position sizing model based on volatility to adjust position sizes.

5. Introduce volatility in trailing stop to set trail distance based on price swings.

6. Deploy strategy to other markets like forex and crypto currencies.

7. Develop a quantitative trading system for automation.

## Conclusion

The RSI divergence trading strategy generates signals by identifying divergences between RSI and price. The logic is simple and easy to automate. The stop loss, take profit and trailing stop effectively controls risks. However, the strategy has limitations in accuracy and trending markets. Improvements can be made through optimizing parameters, adding filters and dynamic stops. As a technical strategy, it can serve as a complement during range-bound markets when systemized.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|14|rsi length|
|v_input_1_close|0|source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_2|14|RSI Divergence length|
|v_input_int_3|false|zoom|
|v_input_float_1|25|(?buy)take profit|
|v_input_float_2|5|stop|
|v_input_float_3|0.25|trailing stop|
|v_input_float_4|25|(?sell)take profit|
|v_input_float_5|5|stop|
|v_input_float_6|0.25|trailing stop|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-24 00:00:00
end: 2023-10-24 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © faytterro

//@version=5
// strategy("RSI Divergence Strategy", overlay=true, scale = scale.none)
rsilen=input.int(14, title="rsi length")
rsisrc=input(close, title="source")
x=ta.rsi(rsisrc,rsilen)
len=input.int(14, title="RSI Divergence length", maxval=500)
tpb = input.float(25, title="take profit", group = "buy", step = 0.5)
sb = input.float(5, title="stop", group = "buy", step = 0.5)
tsb = input.float(0.25, title="trailing stop", group = "buy", step = 0.5)
tps = input.float(25, title="take profit", group = "sell", step = 0.5)
ss =input.float(5, title="stop", group = "sell", step = 0.5)
tss = input.float(0.25, title="trailing stop", group = "sell", step = 0.5)
src=close
extrapolation=0
zoom=input.int(0, title="zoom", maxval=27, minval=-27)
hline(300-zoom*10, color=color.rgb(54, 58, 69, 100))
hline(10, color=color.rgb(54, 58, 69, 100))
// for ax+b
xo=0.0
yo=0.0
xyo=0.0
xxo=0.0
for i=0 to len-1
    xo:= xo + i/(len)
    yo:= yo + x[len-1-i]/(len)
    xyo:= xyo + i*x[len-1-i]/(len)
    xxo:= xxo + i*i/(len)
dnm=ta.lowest(low,200)
dizi=array.new_float(len*2+1+extrapolation)
// linedizi=array.new_line()
a=(xo*yo-xyo)/(xo*xo-xxo)
b=yo-a*xo
for i=0 to len-1+extrapolation
    array.set(dizi,i,a*i+b)
//// for src
// for ax+b
xo2=0.0
yo2=0.0
xyo2=0.0
xxo2=0.0
for i=0 to len-1
    xo2:= xo2 + i/(len)
    yo2:= yo2 + src[len-1-i]/(len)
    xyo2:= xyo2 + i*src[len-1-i]/(len)
    xxo2:= xxo2 + i*i/(len)

dizi2=array.new_float(len*2+1+extrapolation)
// linedizi2=array.new_line()
a2=(xo2*yo2-xyo2)/(xo2*xo2-xxo2)
b2=yo2-a*xo2
for i=0 to len-1+extrapolation
    array.set(dizi2,i,a2*i+b2)
ttk=((array.get(dizi,0)<array.get(dizi,1)) and (array.get(dizi2,0)>array.get(dizi2,1)))? 1 : 
 ((array.get(dizi,0)>array.get(dizi,1)) and (array.get(dizi2,0)<array.get(dizi2,1)))? -1 : 0
cg=((array.get(dizi,0)<array.get(dizi,1)) and (array.get(dizi2,0)>array.get(dizi2,1)))// and ta.highest(ttk[1],len/2)<1)
cr=((array.get(dizi,0)>array.get(dizi,1)) and (array.get(dizi2,0)<array.get(dizi2,1)))// and ta.lowest(ttk[1],len/2)>-1)
bgcolor(color=(cg and ta.highest(ttk[1],len/2)<1)? color.rgb(76, 175, 79, 50) : 
 (cr and ta.lowest(ttk[1],len/2)>-1)? color.rgb(255, 82, 82, 50) : na, offset=0, display=display.none)
plot(x)

// for ax+b
xo3=0.0
yo3=0.0
xyo3=0.0
xxo3=0.0
for i=0 to len-1
    xo3:= xo3 + i/(len)
    yo3:= yo3 + x[len-1-i+(ta.barssince(cg))]/(len)
    xyo3:= xyo3 + i*x[len-1-i+(ta.barssince(cg))]/(len)
    xxo3:= xxo3 + i*i/(len)

dizi3=array.new_float(len*2+1+extrapolation)
// linedizi3=array.new_line()
a3=(xo3*yo3-xyo3)/(xo3*xo3-xxo3)
b3=yo3-a3*xo3
for i=0 to len-1+extrapolation
    array.set(dizi3,i,a3*i+b3)

// for ax+b
xo4=0.0
yo4=0.0
xyo4=0.0
xxo4=0.0
for i=0 to len-1
    xo4:= xo4 + i/(len)
    yo4:= yo4 + x[len-1-i+(ta.barssince(cr))]/(len)
    xyo4:= xyo4 + i*x[len-1-i+(ta.barssince(cr))]/(len)
    xxo4:= xxo4 + i*i/(len)

dizi4=array.new_float(len*2+1+extrapolation)
// linedizi4=array.new_line()
a4=(xo4*yo4-xyo4)/(xo4*xo4-xxo4)
b4=yo4-a4*xo4
for i=0 to len-1+extrapolation
    array.set(dizi4,i,a4*i+b4)

// line=line.new((last_bar_index-ta.barssince(cg)-len),
//  array.get(dizi3,0), 
//  last_bar_index-ta.barssince(cg),
//  array.get(dizi3,len-1), color=color.rgb(0,255,0), width=2)
// line2=line.new((last_bar_index-ta.barssince(cr)-len),
//  array.get(dizi4,0), 
//  last_bar_index-ta.barssince(cr),
//  array.get(dizi4,len-1), color=color.rgb(255, 0, 0, 0), width=2)
// line.delete(line[1])
// line.delete(line2[1])

alert=((array.get(dizi,0)<array.get(dizi,1)) and (array.get(dizi2,0)>array.get(dizi2,1)) and ta.highest(ttk[1],len/2)<1)
 or ((array.get(dizi,0)>array.get(dizi,1)) and (array.get(dizi2,0)<array.get(dizi2,1)) and ta.lowest(ttk[1],len/2)>-1)
alertcondition(alert)
hline(50)
rs=hline(30)
rss=hline(70)
fill(rs, rss, color=color.rgb(126, 87, 194, 90), title="RSI Background Fill")

longCondition = cg and ta.highest(ttk[1],len/2)<1 
if (longCondition)
    strategy.entry("Long", strategy.long)
    strategy.exit("exit long", "Long", limit = close*(100+tpb)/100 , stop =close*(100-sb)/100 , trail_price = close , trail_offset = close*tsb)

shortCondition = cr and ta.lowest(ttk[1],len/2)>-1 
if (shortCondition)
    strategy.entry("Short", strategy.short)
    strategy.exit("exit short", "Short", limit = close*(100-tps)/100, stop = close*(100+ss)/100, trail_price = close , trail_offset = close*tss)

```

> Detail

https://www.fmz.com/strategy/430162

> Last Modified

2023-10-25 16:47:14

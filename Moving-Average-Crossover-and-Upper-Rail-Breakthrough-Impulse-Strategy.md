
> Name

Moving-Average-Crossover-and-Upper-Rail-Breakthrough-Impulse-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/3728d86feb8d11afaa7cbc2ac2c5fd9eb140b0782d0cc1a77cf90cb1582a34c5.png)

[trans]

## Overview
This strategy uses the cross signals of the fast and slow lines of the indicator MACD, combined with other indicators to make comprehensive judgments, captures the breakthrough signal of the exponential moving average at an instantaneous time, and makes a buying or selling decision. It is a short-term trading strategy.
## Strategy Principle
1. Use MACD’s fast and slow crosses as primary trading signals. When the fast line crosses the slow line, the entry is bullish, and when the fast line crosses below the slow line, the entry is bearish.
2. Use the RSI indicator to determine whether it is overbought or oversold. It is bullish when the RSI is below the midline, and bearish when the RSI is above the midline.
3. Calculate the current closing price and compare it with the SMA moving average within a certain period. When the closing price is lower than the SMA, it is bullish, and when the closing price is higher than the SMA, it is bearish.
4. Calculate the 0.5 Fibonacci level of the Highest value within a certain period as a bullish resistance level. Calculate the 0.5 Fibonacci level of the Lowest value within a certain period as a bearish support level.
5. When the fast line crosses and the price is below the support level, the bullish entry is made. When the fast line crosses below and the price is above the resistance level, the bearish entry is made.
6. Use a gradual trailing stop method. After entering the market, the stop loss position is fixed at a certain percentage of the opening price at the beginning. When the loss reaches a certain proportion, it is changed to a small and gradual trailing stop loss.
## Strategic Advantages
1. The strategy makes full use of the MACD crossover signal, which is a classic and effective technical indicator trading signal.
2. Combined with multiple indicators such as RSI and SMA for confirmation, false signals can be filtered and the reliability of the signal can be improved.
3. Calculate dynamic support and resistance levels and conduct breakthrough transactions to capture larger market trends.
4. Using the gradual moving stop method can not only lock in most of the profits, but also control risks.
5. The strategic trading logic is clear and simple, easy to understand and master, and is suitable for novices to learn.
## Strategy Risk
1. The MACD indicator has a lag problem and may miss the best buying and selling points in the market.
2. Multi-indicator combination judgment increases the complexity of the strategy and is prone to indicator conflicts.
3. There is a risk of false breakthrough in dynamic calculation of support and resistance levels.
4. The trailing stop loss may stop the loss too early in the big market and fail to make sustained profits.
5. Strategy parameters need to be repeatedly tested and optimized. Inappropriate parameters will affect the strategy effect.
## Strategy optimization direction
1. You can test different parameter combinations and optimize MACD cycle parameters.
2. More indicators can be introduced, such as Bollinger Bands, KDJ, etc., for multi-dimensional analysis.
3. More factors can be combined to judge the rationality of the support resistance level.
4. More advanced trailing stop loss mechanisms can be studied, such as time stop loss, oscillation stop loss, etc.
5. The automatic parameter optimization module can be added to realize automatic optimization of parameters.
## Summarize
This strategy comprehensively uses multiple indicators such as MACD, RSI, SMA, etc. to capture the breakthrough signal of the exponential moving average at an instant time. It is a typical short-term breakthrough trading strategy. There is a certain lag in strategy signal generation, but the accuracy can be improved through parameter optimization. Generally speaking, the trading logic of this strategy is simple and clear, easy to master, and its performance is robust. It is suitable for most people to learn and use, and is worthy of further testing and optimization.
||


## Overview

This strategy utilizes the crossover signals of the MACD fast line and slow line, combined with judgments based on multiple other indicators, to capture the breakthrough signals of the moving average index line in a timely manner and make buy or sell decisions. It belongs to a short-term trading strategy.

## Strategy Logic

1. Use the crossover of the MACD fast line and slow line as the primary trading signal. When the fast line crosses above the slow line, take a long position. When the fast line crosses below the slow line, take a short position.

2. Incorporate the RSI indicator to determine overbought and oversold conditions. Below the centerline suggests long, while above suggests short.

3. Compare the current closing price to the SMA line of a certain period. Closing price below SMA suggests long, while above suggests short. 

4. Calculate the 0.5 Fibonacci level of the Highest value of a certain period as the resistance for long. Calculate the 0.5 Fibonacci level of the Lowest value of a certain period as the support for short.

5. Take long when the fast line crosses above and the price is below support. Take short when the fast line crosses below and the price is above resistance.

6. Adopt a trailing stop loss mechanism. The stop loss is fixed at a certain percentage of the entry price initially. When the loss reaches a certain level, switch to a gradual trailing stop loss.

## Advantages

1. The strategy makes full use of the MACD crossover signals, which is a classic and effective technical indicator trading signal.

2. Incorporating confirmations from multiple indicators like RSI and SMA can filter false signals and improve reliability.

3. Calculating dynamic support and resistance levels for breakout trading can capture larger trends.

4. The trailing stop loss can lock in most profits while controlling risk.

5. The strategy logic is clear and simple, easy to understand and master for beginners.

## Risks

1. The MACD indicator has lagging issues and may miss the optimal entry and exit points.

2. Combining multiple indicators increases complexity and risks of conflicting signals.

3. There are risks of incorrect breakouts when dynamically calculating support and resistance. 

4. Trailing stop loss may exit prematurely in strong trends, failing to ride trends.

5. Parameters require repetitive testing and optimization, improper parameters negatively impact performance.

## Optimization Directions

1. Test different parameter combinations to optimize MACD periods.

2. Introduce more indicators like Bollinger Bands, KDJ for multidimensional analysis. 

3. Incorporate more factors to judge the reasonableness of support and resistance.

4. Research more advanced stop loss mechanisms like time-based or volatility-based stops. 

5. Add an auto-optimization module for automatic parameter optimization.

## Summary 

This strategy combines MACD, RSI, SMA and other indicators to capture moving average breakthrough signals opportunistically. It belongs to typical short-term breakout trading strategies. There is some lag in its signal generation, but accuracy can be improved through parameter optimization. Overall, this is a strategy with simple and clear logic, easy to grasp for most, and worth further testing and optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_2|60|Strategy Decision Time Frame|
|v_input_1|BINANCE:BTCUSDT|(?SYMBOL)Symbol|
|v_input_3|14|(?ADX)ADX Smoothing|
|v_input_4|14|ADX DI Length|
|v_input_5|30|ADX EMA|
|v_input_6|19|ADX CONSTANT|
|v_input_7|50|(?FIBO MACD SMA)Fibo Look Back Canles|
|v_input_8|30|SMA Look Back Candles|
|v_input_9|15|MACD Fast Lenght|
|v_input_10|30|MACD Slow Lenght|
|v_input_11|9|MACD Signal Smoothing|
|v_input_12|100|MACD Look Back Candles|
|v_input_13|2|(?TP & SL)Trailing Long Stop %|
|v_input_14|2|Trailing Short Stop %|
|v_input_15|2|Long Profit Start %|
|v_input_16|2|Short Profit Start %|
|v_input_17|3|Max Long Stop Loss (%)|
|v_input_18|2.5|Max Short Stop Loss (%)|
|v_input_19|100|Long Take Profit (%)|
|v_input_20|100|Short Take Profit (%)|
|v_input_21|95|(?CAPITAL TO INVEST)Capital Percentage to Invest (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-05 00:00:00
end: 2023-11-09 23:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © onurenginogutcu

//@version=4
strategy("R19 STRATEGY", overlay=true, calc_on_every_tick=true , margin_long=100, margin_short=100 ,  process_orders_on_close=true )



sym = input(title="Symbol", type=input.symbol, defval="BINANCE:BTCUSDT" , group = "SYMBOL") 
timeFrame = input(title="Strategy Decision Time Frame", type = input.resolution ,  defval="60")

adxlen = input(14, title="ADX Smoothing" , group = "ADX")
dilen = input(14, title="ADX DI Length", group = "ADX")
adxemalenght = input(30, title="ADX EMA", group = "ADX")
adxconstant = input(19, title="ADX CONSTANT", group = "ADX")

fibvar = input (title = "Fibo Look Back Canles" , defval = 50 , minval = 0 , group = "FIBO MACD SMA")
smaLookback = input (title = "SMA Look Back Candles" , defval = 30 , minval = 0 , group = "FIBO MACD SMA")
MACDFast = input (title = "MACD Fast Lenght" , defval = 15 , minval = 0 , group = "FIBO MACD SMA")
MACDSlow = input (title = "MACD Slow Lenght" , defval = 30 , minval = 0 , group = "FIBO MACD SMA")
MACDSmooth = input (title = "MACD Signal Smoothing" , defval = 9 , minval = 0 , group = "FIBO MACD SMA")
MACDLookback = input (title = "MACD Look Back Candles" , defval = 100 , minval = 0 , group = "FIBO MACD SMA")

trailingStopLong = input (title = "Trailing Long Stop %" , defval = 2.0 , step = 0.1, group = "TP & SL") * 0.01
trailingStopShort = input (title = "Trailing Short Stop %" , defval = 2.0 , step = 0.1 , group = "TP & SL") * 0.01
LongTrailingProfitStart = input (title = "Long Profit Start %" , defval = 2.0 , step = 0.1 , group = "TP & SL") * 0.01
ShortTrailingProfitStart = input (title = "Short Profit Start %" , defval = 2.0 , step = 0.1, group = "TP & SL") * 0.01

lsl = input(title="Max Long Stop Loss (%)",
     minval=0.0, step=0.1, defval=3.0, group = "TP & SL") * 0.01
     
ssl = input(title="Max Short Stop Loss (%)",
     minval=0.0, step=0.1, defval=2.5, group = "TP & SL") * 0.01
     
longtp = input(title="Long Take Profit (%)",
     minval=0.0, step=0.1, defval=100, group = "TP & SL") * 0.01
     
shorttp = input(title="Short Take Profit (%)",
     minval=0.0, step=0.1, defval=100, group = "TP & SL") * 0.01
     
capperc = input(title="Capital Percentage to Invest (%)",
     minval=0.0, maxval=100, step=0.1, defval=95, group = "CAPITAL TO INVEST") * 0.01
     

symClose = security(sym, timeFrame, close)
symHigh = security(sym, timeFrame, high)
symLow = security(sym, timeFrame, low)

atr = atr (14) 

/////////adx code

dirmov(len) =>
	up = change(symHigh)
	down = -change(symLow)
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
emasig = ema (sig , adxemalenght )


////////adx code over



i = ema (symClose , MACDFast) - ema (symClose , MACDSlow) 
r = ema (i , MACDSmooth)

sapust = highest (i , MACDLookback) * 0.729 
sapalt = lowest (i , MACDLookback) * 0.729  


simRSI = rsi (symClose , 50 ) 




fibtop = lowest (symLow , fibvar) + ((highest (symHigh , fibvar) - lowest (symLow , fibvar)) * 0.50)
fibbottom = lowest (symLow , fibvar) + ((highest (symHigh , fibvar) - lowest (symLow , fibvar)) * 0.50)





cond1 = 0
cond2 = 0
cond3 = 0
cond4 = 0


longCondition = crossover(i, r) and i < sapalt and sig > adxconstant and symClose < sma (symClose , smaLookback) and simRSI < sma (simRSI , 50) and symClose < fibbottom 
shortCondition = crossunder(i, r) and i > sapust and sig > adxconstant and  symClose > sma (symClose , smaLookback) and simRSI > sma (simRSI , 50) and symClose > fibtop 


//////////////////////probability long/short
if (crossover(i, r) and i < sapalt)
    cond1 := 35
else if (crossunder(i, r) and i > sapust)
    cond1 := -35
else
    cond1 := 0
    
if (symClose < sma (symClose , smaLookback))
    cond2 := 30
else if (symClose > sma (symClose , smaLookback))
    cond2 := -30
else
    cond2 := 0
    
if (simRSI < sma (simRSI , 50))
    cond3 := 25
else if (simRSI > sma (simRSI , 50))
    cond3 := -25
else
    cond3 := 0
    
if (symClose < fibbottom)
    cond4 := 10
else if (symClose > fibbottom)
    cond4 := -10
else
    cond4 := 0
    
probab = cond1 + cond2 + cond3 + cond4
////////////////////////////////////////////////////////////////

///////////////////////////////////////////STRATEGY ENTRIES AND STOP LOSSES /////
var startTrail = 0
var trailingLongPrice = 0.0
var trailingShortPrice = 0.0

if (longCondition and strategy.position_size == 0)
    strategy.entry("Long", strategy.long , qty = capperc * strategy.equity / close )

if (shortCondition and strategy.position_size == 0)
    strategy.entry("Short" , strategy.short , qty = capperc * strategy.equity / close )
    
    
if (strategy.position_size == 0)    
    trailingShortPrice := 0.0
    trailingLongPrice := 0.0  
    startTrail := 0
/////////////////////////////////strategy exit

if (strategy.position_size > 0 and close >= strategy.position_avg_price * (1 + LongTrailingProfitStart))
    startTrail := 1

if (strategy.position_size < 0 and close <= strategy.position_avg_price * (1 - ShortTrailingProfitStart))
    startTrail := -1
    



trailingLongPrice := if strategy.position_size > 0 and startTrail == 1
    stopMeasure = close * (1 - trailingStopLong)
    max (stopMeasure , trailingLongPrice [1])
else if strategy.position_size > 0 and startTrail == 0
    strategy.position_avg_price * (1 - lsl)


trailingShortPrice := if strategy.position_size < 0 and startTrail == -1
    stopMeasure = close * (1 + trailingStopShort)
    min (stopMeasure , trailingShortPrice [1])
else if strategy.position_size < 0 and startTrail == 0
    strategy.position_avg_price * (1 + ssl)




if (strategy.position_size > 0)
    strategy.exit("Exit Long", "Long", stop = trailingLongPrice , limit=strategy.position_avg_price*(1 + longtp))
 

if (strategy.position_size < 0)
    strategy.exit("Exit Short", "Short", stop = trailingShortPrice , limit=strategy.position_avg_price*(1 - shorttp))


////////////////////////vertical colouring signals
bgcolor(color=longCondition ? color.new (color.green , 70) : na)
bgcolor(color=shortCondition ? color.new (color.red , 70) : na)

plot (trailingLongPrice , color = color.green) ///long price trailing stop
plot (trailingShortPrice , color = color.red) /// short price trailing stop
plot (startTrail , color = color.yellow)
plot (probab , color = color.white) ////probability

```

> Detail

https://www.fmz.com/strategy/431928

> Last Modified

2023-11-13 11:52:22

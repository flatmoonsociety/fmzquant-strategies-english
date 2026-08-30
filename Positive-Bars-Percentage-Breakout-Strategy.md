
> Name

Customized upward breakout strategyPositive-Bars-Percentage-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/127d7202a6b82baba28.png)
[trans]
## Overview
The custom upward breakthrough strategy is a quantitative trading strategy based on price judgment. This strategy determines whether the market is currently in a continued upward trend by calculating the proportion of positive K lines within a specified period. When the proportion of positive K lines is higher than the upper limit set by the user, the strategy determines that the market is currently in an upward trend, and you will go long at this time; when the proportion of positive K lines is lower than the lower limit set by the user, the strategy determines that the market is currently in a downward trend, and you will go short at this time.
## Strategy Principle
The core indicator of this strategy is the proportion of positive K lines. A positive K-line refers to a K-line that opens from a low point and closes higher than the opening price, indicating that the price has increased during the period. The strategy counts the ratio of the number of positive K-lines to all K-lines in the previous periods specified by the user. When the ratio is greater than the upper limit, it is judged that the current market is continuing to rise, and then go long; when the ratio is less than the lower limit, it is judged that the current market is continuing to fall, and then go short. The stop loss and take profit for long and short positions are set according to the stop loss method set by the user.
Example: The user sets the number of cycles to 20, the upper limit to 70, and the lower limit to 30. The strategy looks back at the last 20 K lines. If 16 of them are positive K lines, the proportion is 16/20=80%. At this time, it is higher than the upper limit set by the user, 70, and a long operation is performed. If among the recent 20 K lines, only 5 are positive K lines, the proportion is 5/20=25%. If the price is lower than the user-set lower limit of 30, short selling will be performed.
## Advantage Analysis
This strategy has the following advantages:
1. The strategic ideas are simple, intuitive and easy to understand;
2. Only one indicator is required, reducing the risk of over-optimization;
3. Users can customize parameters to adapt to different varieties;
4. Built-in stop loss and stop profit function, which can prevent huge losses;
5. You can place an order directly in the opposite direction, without waiting for the position to be closed before opening a position, and you can track the market faster.
## Risk Analysis
There are also some risks with this strategy:
1. Using only one indicator can easily produce false signals;
2. Indicator parameters are easy to be over-optimized, and the actual effect may vary greatly;
3. When the market fluctuates violently, the stop loss may be breached and result in losses;
4. The reverse position opening function may increase losses;
5. The effect is closely related to the variety and needs to be tested separately.
In order to reduce risks, you can optimize from the following aspects:
1. Add filtering conditions to avoid false signals;
2. Optimize the stop loss strategy and reduce single losses;
3. Evaluate and control the amount of single loss;
4. Test the effects on different varieties.
## Optimization direction
This strategy can be optimized from the following directions:
1. Add auxiliary judgment indicators such as volume and price rationality to avoid false signals
2. Optimize the stop loss method, you can consider trailing stop loss, oscillating stop loss, etc.
3. Add filter conditions for opening a position, such as breaking through the Bollinger Band before entering again
4. Test the adaptability of different forward K-line parameters to different varieties
5. Evaluate the maximum drawdown and control the size of a single loss
## Summarize
The overall idea of ​​the custom upward breakthrough strategy is clear and simple. It can judge the continuous rising or falling status by counting the proportion of positive K lines, and use simple indicators to capture the trend. This strategy is easy to understand, user-friendly, and suitable for beginners to practice quantitative trading. However, relying only on a single indicator and parameter setting will result in certain profit volatility, and it is necessary to continue to optimize the risk of the strategy so that it can make stable profits in more markets.
|| 

## Overview

The Positive Bars Percentage Breakout Strategy is a quantitative trading strategy based on price action judgments. It calculates the percentage of uptrend candles in a specified period to determine whether the market is currently in an uptrend state. When the percentage of uptrend candles is higher than the user-defined upper limit, the strategy judges that the market is currently in an uptrend and goes long. When the percentage is lower than the user-defined lower limit, the strategy judges that the market is currently in a downtrend and goes short.

## Strategy Logic  

The core indicator of this strategy is the percentage of uptrend candles. An uptrend candle opens below the previous low and closes above the open, indicating the price rose during that period. The strategy counts the number of uptrend candles in the user-defined lookback period and calculates the percentage of uptrend candles among all candles. When the percentage is higher than the upper limit, the strategy judges the market is in a persistent uptrend and goes long. When the percentage is lower than the lower limit, the strategy judges the market is in a downtrend and goes short. The stop loss and take profit orders are set according to the stop loss method defined by the user.

For example, if the user sets the lookback period to 20, upper limit to 70, lower limit to 30, the strategy traces back the latest 20 candles. If 16 of them are uptrend candles, the percentage would be 16/20=80%. Since 80% is higher than the 70% upper limit, the strategy will execute a long order. If among the latest 20 candles, only 5 are uptrend candles, then the percentage would be 5/20=25%. This is lower than the 30% lower limit, the strategy will execute a short order.

## Advantage Analysis 

The main advantages of this strategy are:

1. The strategy logic is simple and intuitive, easy to understand;  
2. It relies on only one indicator, reducing the risk of overfitting;
3. Users can customize parameters for different products; 
4. It has built-in stop loss/take profit functions to prevent huge losses;
5. Allow reverse trade without exiting positions first, faster tracking of trends.

## Risk Analysis   

The main risks of this strategy are:  

1. Relying solely on one indicator can generate false signals;  
2. Parameters are prone to overfitting, live performance may differ greatly;
3. Stop loss can be hit by volatile price swings, leading to losses;
4. Reverse trade may amplify losses;
5. Performance relies heavily on symbol, requiring separate tests.

The risks can be reduced by:

1. Adding filters to avoid false signals;  
2. Optimizing the stop loss logic to limit losses;
3. Evaluating and controlling maximum loss size;
4. Testing on different symbols separately.

## Optimization Directions

The main directions to optimize this strategy include:

1. Adding auxiliary indicators like volume to avoid false signals;
2. Optimizing stop loss methods, such as trailing stop loss; 
3. Adding entry filters like breakout of Bollinger Bands;
4. Testing optimal parameters of uptrend candles for different symbols;  
5. Evaluating maximum drawdown and controlling loss size.

## Conclusion   

The Positive Bars Percentage Breakout Strategy has a simple and straightforward logic to capture trends by statistically judging persistence of uptrends/downtrends. It is easy to understand and user-friendly, suitable for beginner quants. But its reliance on a single indicator and parameter optimization requires further improvements on risk control for stable profitability across different markets.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Strategy Direction|
|v_input_2|true|-----------------Strategy Inputs-------------------|
|v_input_3|13|Lookback|
|v_input_4|70|Upper Limit|
|v_input_5|30|Lower Limit|
|v_input_6|true|-----------------General Inputs-------------------|
|v_input_7|true|Use Stop Loss and Take Profit|
|v_input_8|0|Type Of Stop: ATR Stop|Swing Lo/Hi|Strategy Stop|
|v_input_9|10|Swing Point Lookback|
|v_input_10|2|Swing Point SL Perc Increment|
|v_input_11|14|ATR Length|
|v_input_12|10|ATR Multiple|
|v_input_13|1.6|Take Profit Risk Reward Ratio|
|v_input_14|true|Allow Direct Position Reverse|
|v_input_15|false|Reverse Trades|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-31 00:00:00
end: 2024-01-04 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/


// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © ZenAndTheArtOfTrading 
// © TweakerID

// Based on the calculations by ZenAndTheArtOfTrading, I added stop loss, take profit and reverse line codes.
// The Positive Bars % calculates the number of green (positive) bars, relative to a lookback period, defined 
// by the user. If the percentage is low, it means that there was a bigger number of red candles in the 
// lookback period. The strategy goes long when the percentage is high and short when it's low, although
// this logic can be reversed with positive results on different time frames.

//@version=4
strategy("Positive Bars % Strat", 
     overlay=true, 
     default_qty_type=strategy.percent_of_equity, 
     default_qty_value=100, 
     initial_capital=10000, 
     commission_value=0.04, 
     calc_on_every_tick=false, 
     slippage=0)

direction = input(0, title = "Strategy Direction", type=input.integer, minval=-1, maxval=1)
strategy.risk.allow_entry_in(direction == 0 ? strategy.direction.all : (direction < 0 ? strategy.direction.short : strategy.direction.long))

/////////////////////// STRATEGY INPUTS ////////////////////////////////////////
title1=input(true, "-----------------Strategy Inputs-------------------")  

lookback = input(title="Lookback", type=input.integer, defval=13)
upperLimit = input(title="Upper Limit", type=input.integer, defval=70)
lowerLimit = input(title="Lower Limit", type=input.integer, defval=30)

/////////////////////// BACKTESTER /////////////////////////////////////////////
title2=input(true, "-----------------General Inputs-------------------")  

// Backtester General Inputs
i_SL=input(true, title="Use Stop Loss and Take Profit")
i_SLType=input(defval="ATR Stop", title="Type Of Stop", options=["Strategy Stop", "Swing Lo/Hi", "ATR Stop"])
i_SPL=input(defval=10, title="Swing Point Lookback")
i_PercIncrement=input(defval=2, step=.1, title="Swing Point SL Perc Increment")*0.01
i_ATR = input(14, title="ATR Length")
i_ATRMult = input(10, step=.1, title="ATR Multiple")
i_TPRRR = input(1.6, step=.1, title="Take Profit Risk Reward Ratio")

// Bought and Sold Boolean Signal
bought = strategy.position_size > strategy.position_size[1] 
 or strategy.position_size < strategy.position_size[1]

// Price Action Stop and Take Profit
LL=(lowest(i_SPL))*(1-i_PercIncrement)
HH=(highest(i_SPL))*(1+i_PercIncrement)
LL_price = valuewhen(bought, LL, 0)
HH_price = valuewhen(bought, HH, 0)
entry_LL_price = strategy.position_size > 0 ? LL_price : na 
entry_HH_price = strategy.position_size < 0 ? HH_price : na 
tp=strategy.position_avg_price + (strategy.position_avg_price - entry_LL_price)*i_TPRRR
stp=strategy.position_avg_price - (entry_HH_price - strategy.position_avg_price)*i_TPRRR

// ATR Stop
ATR=atr(i_ATR)*i_ATRMult
ATRLong = ohlc4 - ATR
ATRShort = ohlc4 + ATR
ATRLongStop = valuewhen(bought, ATRLong, 0)
ATRShortStop = valuewhen(bought, ATRShort, 0)
LongSL_ATR_price = strategy.position_size > 0 ? ATRLongStop : na 
ShortSL_ATR_price = strategy.position_size < 0 ? ATRShortStop : na 
ATRtp=strategy.position_avg_price + (strategy.position_avg_price - LongSL_ATR_price)*i_TPRRR
ATRstp=strategy.position_avg_price - (ShortSL_ATR_price - strategy.position_avg_price)*i_TPRRR

// Strategy Stop
float LongStop = na
float ShortStop = na
float StratTP = na
float StratSTP = na

/////////////////////// STRATEGY LOGIC /////////////////////////////////////////

//Calculations
positiveBars = 0
for i = (lookback - 1) to 0
    if close[i] > open[i]
        positiveBars := positiveBars + 1
positiveBarsPercent = (positiveBars / lookback) * 100

BUY=positiveBarsPercent >= upperLimit
SELL=positiveBarsPercent <= lowerLimit

//Trading Inputs
DPR=input(true, "Allow Direct Position Reverse")
reverse=input(false, "Reverse Trades")

// Entries
if reverse
    if not DPR
        strategy.entry("long", strategy.long, when=SELL and strategy.position_size == 0)
        strategy.entry("short", strategy.short, when=BUY and strategy.position_size == 0)
    else     
        strategy.entry("long", strategy.long, when=SELL)
        strategy.entry("short", strategy.short, when=BUY)
else
    if not DPR 
        strategy.entry("long", strategy.long, when=BUY and strategy.position_size == 0)
        strategy.entry("short", strategy.short, when=SELL and strategy.position_size == 0)
    else
        strategy.entry("long", strategy.long, when=BUY)
        strategy.entry("short", strategy.short, when=SELL)


SL= i_SLType == "Swing Lo/Hi" ? entry_LL_price : i_SLType == "ATR Stop" ? LongSL_ATR_price : LongStop
SSL= i_SLType == "Swing Lo/Hi" ? entry_HH_price : i_SLType == "ATR Stop" ? ShortSL_ATR_price : ShortStop
TP= i_SLType == "Swing Lo/Hi" ? tp : i_SLType == "ATR Stop" ? ATRtp : StratTP
STP= i_SLType == "Swing Lo/Hi" ? stp : i_SLType == "ATR Stop" ? ATRstp : StratSTP

strategy.exit("TP & SL", "long", limit=TP, stop=SL, when=i_SL)
strategy.exit("TP & SL", "short", limit=STP, stop=SSL, when=i_SL)

/////////////////////// PLOTS //////////////////////////////////////////////////

plot(i_SL and strategy.position_size > 0 ? SL : na , title='SL', style=plot.style_cross, color=color.red)
plot(i_SL and strategy.position_size < 0 ? SSL : na , title='SSL', style=plot.style_cross, color=color.red)
plot(i_SL and strategy.position_size > 0 ? TP : na, title='TP', style=plot.style_cross, color=color.green)
plot(i_SL and strategy.position_size < 0 ? STP : na, title='STP', style=plot.style_cross, color=color.green)
// Draw price action setup arrows
plotshape(BUY ? 1 : na, style=shape.triangleup, location=location.belowbar, 
 color=color.green, title="Bullish Setup", size=size.auto)
plotshape(SELL ? 1 : na, style=shape.triangledown, location=location.abovebar, 
 color=color.red, title="Bearish Setup", size=size.auto)
```

> Detail

https://www.fmz.com/strategy/438012

> Last Modified

2024-01-08 10:32:25


> Name

SuperTrend-Basic-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
The Supertrend Basics Strategy is a reliable and profitable algorithmic trading strategy based on three powerful indicators: the Supertrend Indicator (ATR), the Relative Strength Index (RSI), and the Exponential Moving Average (EMA). This strategy aims to identify the direction and strength of the market trend, enter the market at the best entry point, and exit the market when the stop-loss or take-profit point is reached.
## Strategy Principle
This strategy uses the Super Trend indicator to determine whether the price is in an up or down trend. The Supertrend indicator is based on average true volatility and a factor that indicates an uptrend when the price is above the Supertrend and a downtrend when the price is below the Supertrend.
The Relative Strength Index is used to detect overheating and overbought or oversold conditions. When the RSI is above 50, the market is strong, and vice versa. RSI can filter out false breakouts.
Exponential moving averages are used to determine long-term trend direction. When the price is above the EMA, it is in an uptrend, and when it is below, it is in a downtrend. Can be used to confirm trading direction.
The trading signals for this strategy are as follows:
Long Entry: Go long when the price is above the super trend and the RSI is above 50 and the price is above the EMA
Long exit: price closes below super trend or stop loss or take profit
Short Entry: Go short when price is below the super trend and RSI is below 50 and price is below EMA
Short Exit: Price closes above super trend or stop loss or take profit
Stop Loss and Take Profit can be set as a percentage of the entry price.
## Advantage Analysis
This strategy has the following advantages:
1. Use a combination of three indicators to reliably determine the trend direction
2. The super trend indicator can clearly determine the upward trend and downward trend.
3. The RSI indicator can filter out false breakthroughs and avoid overbought and oversold
4. EMA can be used to confirm the direction of the general trend
5. The strategy signals are simple, clear and easy to operate.
6. ATR period, RSI parameters and EMA period can be customized for optimization
7. Stop loss and take profit can be set to control risks
8. You can only go long or only short to adapt to different market environments.
9. Can be used in any time period
## Risk Analysis
The main risks of this strategy are as follows:
1. When the general trend reverses, the super trend indicator will lag, which may lead to losses.
2. If the stop loss and stop profit set are too small, you may not be able to capture the big market trend.
3. EMA cannot determine the trend reversal point
4. Unable to judge the divergence phenomenon
5. There will be a certain degree of volatility risk and time trading risk
Corresponding solutions:
1. Combine with other indicators to determine trend reversal
2. Optimize stop loss and take profit parameters
3. Combine with other indicators to determine trend reversal
4. Combined with divergence indicators
5. Properly adjust position management
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize ATR cycle parameters to balance sensitivity and stability
2. Optimize RSI parameters and improve accuracy
3. Optimize the EMA cycle to adapt to different markets
4. Add other indicators to judge reversal, such as MACD, KD, etc.
5. Add divergence indicator to judge reversal
6. Combined with wave theory to judge reversal
7. Use algorithms such as machine learning to dynamically optimize parameters
8. Add advanced stop loss algorithms, such as trailing stop loss, trailing stop loss, etc.
9. Optimize position management and adapt to markets with different volatility
10. Test more complex combinations of entry and exit conditions
## Summarize
The super trend basic strategy integrates the three major indicators of super trend, RSI and EMA to form a simple and practical trend following strategy. It can clearly identify the trend direction, filter out false signals, and confirm the general trend. At the same time, there are clear entry and exit rules and stop loss and profit settings. This strategy is easy to operate, reliable and profitable, and is suitable for any time period. By optimizing indicator parameters, adding trend judgment tools, improving stop loss algorithms, etc., this strategy can be optimized into a more powerful trading system.
|| 

## Overview

The SuperTrend basic strategy is a reliable and profitable algorithmic trading strategy based on three powerful indicators: SuperTrend (ATR), RSI and EMA. It aims to identify the direction and strength of market trends, enter the market at optimal points, and exit when stop loss or take profit is reached.

## Strategy Logic

The strategy uses SuperTrend indicator to determine if price is in an uptrend or downtrend. SuperTrend is based on Average True Range and a factor, above SuperTrend is uptrend and below is downtrend.

RSI is used to detect overbought/oversold conditions. Above 50 is bullish and below 50 bearish. RSI filters out false signals.

EMA judges long term trend direction. Above EMA is uptrend, below is downtrend. It confirms trade direction.

The trading signals are:

Long entry: Price above SuperTrend and RSI above 50 and Price above EMA
Long exit: Price closes below SuperTrend or Stop loss or Take profit

Short entry: Price below SuperTrend and RSI below 50 and Price below EMA 
Short exit: Price closes above SuperTrend or Stop loss or Take profit

Stop loss and take profit can be set as percentage of entry price.

## Advantage Analysis 

The advantages of this strategy:

1. Combination of 3 indicators, reliable trend detection

2. SuperTrend clearly identifies uptrend and downtrend

3. RSI filters out false breakouts, avoids overbought/oversold

4. EMA confirms overall trend direction  

5. Simple and clear trading signals, easy to follow

6. Customizable ATR period, RSI parameters and EMA period for optimization

7. Stop loss and take profit to control risk

8. Long only or short only mode for different markets

9. Applicable to any timeframe

## Risk Analysis

The main risks:

1. Lagging of SuperTrend in trend reversal, may cause losses

2. Small stop loss/take profit fails to catch big moves

3. EMA cannot spot trend reversal points

4. No divergence detection 

5. Still has volatility risk and time risk

Solutions:

1. Add other indicators to detect reversal

2. Optimize stop loss/take profit

3. Add other indicators to spot reversal

4. Incorporate divergence indicators

5. Adjust position sizing  

## Optimization Directions

Ways to optimize the strategy:

1. Optimize ATR period for sensitivity and stability

2. Optimize RSI parameters for higher accuracy

3. Optimize EMA period for different markets

4. Add indicators like MACD, KD for reversal detection

5. Add divergence indicators 

6. Use Elliott Waves to spot reversals

7. Use machine learning to dynamically optimize parameters

8. Advanced stop loss algorithms like trailing stop loss

9. Optimize position sizing for different volatility

10. Test more complex entry and exit conditions

## Conclusion

The SuperTrend basic strategy integrates SuperTrend, RSI and EMA into a simple and practical trend following system. It identifies trend direction clearly, filters out false signals and confirms overall trend. Clear entry, exit rules and stop loss/take profit configuration. Easy to use, reliable profitability. Applicable to any timeframe. It can be further optimized by tuning parameters, adding reversal tools, enhancing stops to become a more powerful trading system.

[/trans]


> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_string_1|0|Type Of Strategy: Pullback|Simple|
|v_input_1|10|(?Supertrend Settings)ATR Length|
|v_input_float_1|3|Factor|
|v_input_bool_1|true|(?Ema Settings)Ema Condition On/Off|
|v_input_int_1|200|Ema Length|
|v_input_source_1_close|0|Ema Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_bool_2|true|(?Rsi Settings)Rsi Condition On/Off|
|v_input_2_close|0|RSI Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|14|RSI Length|
|v_input_4|50|RSI BUY Level|
|v_input_5|50|RSI SELL Level|
|v_input_6|timestamp(2005-01-01)|(?Backtest Period)Start calculations from|
|v_input_7|timestamp(2045-03-01)|End calculations|
|v_input_string_2|0|(?Trade Direction)Trade Direction: Both|Short|Long|
|v_input_float_2|true|(?Sl/Tp Settings)Stop Loss %|
|v_input_float_3|true|Take Profit %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-10 00:00:00
end: 2023-10-10 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © JS_TechTrading

//@version=5
// strategy("Supertrend", overlay=true,default_qty_type =strategy.percent_of_equity,default_qty_value = 1,process_orders_on_close = false)

// group string////
var string group_text000="Choose Strategy"
var string group_text0="Supertrend Settings"
var string group_text0000="Ema Settings"
var string group_text00="Rsi Settings"
var string group_text1="Backtest Period"
var string group_text2="Trade Direction"
// var string group_text3="Quantity Settings"
var string group_text4="Sl/Tp Settings"
////////////////////
option_ch=input.string('Pullback',title = "Type Of Strategy",options =['Pullback','Simple'])

//atr period input supertrend 
atrPeriod = input(10, "ATR Length",group = group_text0)
factor = input.float(3.0, "Factor", step = 0.01,group=group_text0)

[supertrend, direction] = ta.supertrend(factor, atrPeriod)

bodyMiddle = plot((open + close) / 2, display=display.none)
upTrend = plot(direction < 0 ? supertrend : na, "Up Trend", color = color.green, style=plot.style_linebr)
downTrend = plot(direction < 0? na : supertrend, "Down Trend", color = color.red, style=plot.style_linebr)

fill(bodyMiddle, upTrend, color.new(color.green, 90), fillgaps=false)
fill(bodyMiddle, downTrend, color.new(color.red, 90), fillgaps=false)

long=direction < 0 ? supertrend : na
short=direction < 0? na : supertrend

longpos=false
shortpos=false

longpos :=long?true :short?false:longpos[1]
shortpos:=short?true:long?false:shortpos[1]

fin_pullbuy= (ta.crossunder(low[1],long) and long and high>high[1])
fin_pullsell=(ta.crossover(high[1],short) and short and low<low[1]) 

//Ema 1
on_ma=input.bool(true,"Ema Condition On/Off",group=group_text0000)
ma_len= input.int(200, minval=1, title="Ema Length",group = group_text0000)
ma_src = input.source(close, title="Ema Source",group = group_text0000)
ma_out = ta.ema(ma_src, ma_len)

ma_buy=on_ma?close>ma_out?true:false:true
ma_sell=on_ma?close<ma_out?true:false:true

// rsi indicator and condition
// Get user input
en_rsi    = input.bool(true,"Rsi Condition On/Off",group = group_text00)
rsiSource = input(title='RSI Source', defval=close,group = group_text00)
rsiLength = input(title='RSI Length', defval=14,group = group_text00)
rsiOverbought = input(title='RSI BUY Level', defval=50,group = group_text00)
rsiOversold   = input(title='RSI SELL Level', defval=50,group = group_text00)

// Get RSI value
rsiValue = ta.rsi(rsiSource, rsiLength)

rsi_buy=en_rsi?rsiValue>=rsiOverbought ?true:false:true
rsi_sell=en_rsi?rsiValue<=rsiOversold?true:false:true

// final condition
buy_cond=option_ch=='Simple'?long and not(longpos[1]) and rsi_buy and ma_buy:option_ch=='Pullback'?fin_pullbuy and rsi_buy and ma_buy:na
sell_cond=option_ch=='Simple'?short and not(shortpos[1]) and rsi_sell and ma_sell:option_ch=='Pullback'?fin_pullsell and rsi_sell and ma_sell:na

//backtest engine
start = input(timestamp('2005-01-01'), title='Start calculations from',group=group_text1)
end=input(timestamp('2045-03-01'), title='End calculations',group=group_text1)
time_cond =true

// Make input option to configure trade direction

tradeDirection = input.string(title='Trade Direction', options=['Long', 'Short', 'Both'], defval='Both',group = group_text2)

// Translate input into trading conditions
longOK  = (tradeDirection == "Long") or (tradeDirection == "Both")
shortOK = (tradeDirection == "Short") or (tradeDirection == "Both")



// strategy start
if buy_cond and longOK and time_cond and strategy.position_size==0
    strategy.entry('long',direction = strategy.long)
if sell_cond and shortOK and time_cond and strategy.position_size==0
    strategy.entry('short',direction =strategy.short)

// fixed percentage based stop loss and take profit 

// User Options to Change Inputs (%)
stopPer = input.float(1.0,step=0.10, title='Stop Loss %',group =group_text4) / 100
takePer = input.float(1.0,step =0.10, title='Take Profit %',group =group_text4) / 100

// Determine where you've entered and in what direction
longStop  = strategy.position_avg_price * (1 - stopPer)
shortStop = strategy.position_avg_price * (1 + stopPer)
shortTake = strategy.position_avg_price * (1 - takePer)
longTake  = strategy.position_avg_price * (1 + takePer)


if strategy.position_size > 0
    strategy.exit(id='Close Long',stop=longStop, limit=longTake)
if strategy.position_size < 0
    strategy.exit(id='Close Short',stop=shortStop, limit=shortTake)

//PLOT FIXED SLTP LINE
plot(strategy.position_size > 0 ? longStop : na, style=plot.style_linebr, color=color.new(color.red, 0), linewidth=1, title='Long Fixed SL')
plot(strategy.position_size < 0 ? shortStop :na, style=plot.style_linebr, color=color.new(color.red, 0), linewidth=1, title='Short Fixed SL')
plot(strategy.position_size > 0 ? longTake : na, style=plot.style_linebr, color=color.new(color.green, 0), linewidth=1, title='Long Take Profit')
plot(strategy.position_size < 0 ? shortTake : na, style=plot.style_linebr, color=color.new(color.green, 0), linewidth=1, title='Short Take Profit')

//
```

> Detail

https://www.fmz.com/strategy/428973

> Last Modified

2023-10-11 15:14:54

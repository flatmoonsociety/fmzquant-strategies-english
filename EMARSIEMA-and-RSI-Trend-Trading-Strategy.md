
> Name

Trend trading strategy based on EMA and RSI EMA-and-RSI-Trend-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy combines two indicators, EMA and RSI, to identify trend direction and make entry and exit trades. Bullish when the price is above the EMA and the RSI is below the buy point; bearish when the price is below the EMA and the RSI is above the sell point. At the same time, combined with the closing price relationship of the last two K lines, the trend direction is determined and trend trading is realized.
## Strategy Principle
1. Calculate the 200-day EMA as a moving average indicator to determine the trend. EMA responds quickly to price changes and can effectively determine the trend direction.
2. Calculate the 14-day RSI to determine whether it is overbought or oversold. RSI below 50 is considered oversold, and above 50 is considered overbought. At the same time, combine the upward and downward trends of RSI to determine the buying and selling timing.
3. Compare the closing prices of the last two K lines to determine the trend direction. An increase in the last two closing prices is considered to be in an upward trend, and a decrease in the last two closing prices is considered to be in a downward trend.
4. When in an uptrend, the price is above the 200-day EMA, and the RSI is below 50 and rising, a buy signal is issued.
5. When in a downtrend, the price is below the 200-day EMA, and the RSI is above 50 and falling, a sell signal is issued.
6. ATR and the highest and lowest prices of the last 14 K lines are used to calculate stop loss and take profit points.
7. Use a trailing stop loss strategy to achieve risk control.
## Advantage Analysis
1. Combine dual indicators to determine the trend direction and improve accuracy. EMA determines the main trend, and the relationship between RSI and K-line determines local trends and buying and selling opportunities.
2. The RSI indicator effectively avoids false breakthroughs. Use the long and short state of RSI to avoid unnecessary transactions caused by the lag of the EMA indicator.
3. Trailing stop loss effectively controls losses caused by individual large amplitude fluctuations.
4. The optimized parameter combination makes the policy parameters more robust.
## Risk Analysis
1. In large-amplitude oscillating markets, EMA and RSI have a high probability of generating false signals, and such markets should be avoided.
2. If the stop loss point is too small, it will easily cause excessive stop loss; if the stop loss point is too large, it will be difficult to control the loss. ATR parameters should be adjusted appropriately.
3. There is a high probability of a correction after breaking through the EMA during the day. At this time, the RSI parameter should be appropriately relaxed to avoid missing the trend.
## Optimization direction
1. Appropriately adjust the ATR parameters and stop loss distance to find a better stop loss point.
2. Optimize the EMA and RSI indicator parameters and find a more suitable parameter combination.
3. Add other auxiliary indicators for filtering, such as MACD, Bollinger Bands, etc., to improve signal accuracy.
4. The difference in parameter settings of different varieties can be tested to further improve the stability of parameters.
5. You can try to turn off the strategy during a specific time period to avoid time periods that are prone to error signals.
## Summarize
This strategy is relatively stable overall, with stable returns, and the maximum drawdown and Sharpe rate are also very good. Through parameter optimization and stop loss point adjustment, the effect of the strategy can be further improved. At the same time, you also need to be wary of false signals that may occur under specific market conditions, and use auxiliary indicators or time filters to avoid these markets. This strategy is expected to become a stable strategy worthy of long-term holding through continuous optimization.
|| 

## Overview

This strategy combines EMA and RSI indicators to identify trend direction and make trading decisions. It goes long when price is above EMA and RSI is below the buy point, and goes short when price is below EMA and RSI is above the sell point. It also uses the relationship between the last two candle closes to determine trend direction for trend trading.

## Strategy Logic

1. Calculate 200-day EMA as the trend line indicator. EMA responds quickly to price changes and effectively determines trend direction.

2. Calculate 14-day RSI to judge overbought and oversold conditions. RSI below 50 is considered oversold, while above 50 overbought. Also use the upward or downward trend of RSI to determine entry and exit timing.

3. Compare the size relationship between the last two candle closes to determine trend direction. Incremental last two closes signal an uptrend, while decremental last two closes signal a downtrend.

4. When in an uptrend, price above 200-day EMA, and RSI below 50 and rising, a buy signal is generated.

5. When in a downtrend, price below 200-day EMA, and RSI above 50 and falling, a sell signal is generated.

6. ATR and highest/lowest prices of last 14 candles are used to calculate stop loss and take profit. 

7. Adopt a trailing stop strategy for risk management.

## Advantage Analysis 

1. The combination of two indicators improves accuracy in determining trend direction. EMA judges major trend and RSI&Candle relationship judges local trend and entry/exit timing.

2. RSI effectively avoids false breakouts. RSI overbought/oversold status avoids unnecessary trades caused by EMA's lagging.

3. Trailing stop effectively controls loss caused by occasional large amplitude fluctuations.

4. Optimized parameter combination enhances robustness.

## Risk Analysis

1. EMA and RSI are likely to generate incorrect signals in large amplitude sideways markets, which should be avoided.

2. A too tight stop loss causes frequent stops while a too wide stop loss fails to control loss. ATR parameter should be adjusted properly.

3. Probability of pullback after breakthrough is high. RSI parameter should be relaxed to avoid missing trends.

## Improvement Directions

1. Adjust ATR parameter and stop distance to find better stop loss points.

2. Optimize EMA and RSI parameters to find better parameter combinations. 

3. Add other indicators for filtration, like MACD, Bollinger Bands etc, to improve signal accuracy.

4. Test parameter differences among different products to further enhance robustness.

5. Try disabling strategy during specific time periods to avoid wrong signal-prone hours.

## Summary 

The overall strategy is quite stable with steady returns, maximum drawdown and Sharpe ratio. It can be further improved by parameter optimization and stop loss adjustment. Also need to watch out wrong signals during specific market conditions, and avoid them via auxiliary indicators or time filters. This strategy has the potential to become a long-term stable strategy through continuous optimization.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|200|EMA Length|
|v_input_2|50|RSI Buy Value|
|v_input_3|50|RSI Sell Value|
|v_input_bool_1|false|Show Data|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-01 00:00:00
end: 2023-08-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
// strategy("EMA RSI Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=1)


///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
// Author       : AJ Rupasinghege
// Date         : 06/11/2022
// Release      : v6.0
// Description  : If the last two closes are in ascending order, the rsi is below 50 and ascending, and the current candle is above 200 ema, then LONG. 
//                If the last two closes are in descending order, the rsi is above 50 and descending, and the current candle is below 200 ema, then SHORT. 
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////


//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////// INPUTS //////////////////////////////////////////////////////////////

ema_length = input(200, "EMA Length")
rsi_buy_value = input(50, "RSI Buy Value")
rsi_sell_value = input(50, "RSI Sell Value")
show_data = input.bool(0, "Show Data")


/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////// VARIABLES //////////////////////////////////////////////////////////

var stop_loss = 0.0
var last_trade_entry_price = 0.0
var low_value= 0.0
var atr = 0.0
var high_value = 0.0
var stop_loss_points = 0.0
var limit = 0.0
var bar_id_entry = 0


/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////// FUNCTIONS //////////////////////////////////////////////////////////

getTradeConditionsLong() =>
    //@function         Used to calculate stop_loss, stop_loss points, limit and label values for long trades
    //@param direction  (float) // strategy.poistion.size
    //@returns          stop_loss, stop_loss_points, limit
    //@Dependancies     low_value, atr, last_trade_entry_price,bar_id_entry
    _stop_loss = low_value - atr
    _stop_lossPoints = (last_trade_entry_price - _stop_loss) *100000
    _limit = last_trade_entry_price + (last_trade_entry_price - low_value + atr) 
    value = "OpenValue: " + str.tostring(last_trade_entry_price) + 
         "\n OpenBarIndex: " + str.tostring(bar_id_entry) + 
         "\n LowValue: " + str.tostring(low_value) + 
         "\n atr: " + str.tostring(atr) + "\n stop_loss: " + 
         str.tostring(_stop_loss) + "\n Limit: " +
         str.tostring(_limit)

    [_stop_loss,_stop_lossPoints,_limit, value]

getTradeConditionsShort() =>
    //@function         Used to calculate stop_loss, stop_loss points, limit and label values for short trades
    //@param direction  (float) // strategy.poistion.size
    //@returns          stop_loss, stop_loss_points, limit
    //@Dependancies     high_value, atr, last_trade_entry_price,bar_id_entry
    _stop_loss = high_value + atr
    _stop_lossPoints = (_stop_loss  -last_trade_entry_price) * 100000
    _limit = last_trade_entry_price - (high_value - last_trade_entry_price + atr)
    value = "OpenValue: " + str.tostring(last_trade_entry_price) + 
         "\n OpenBarIndex: " + str.tostring(bar_id_entry) + 
         "\n HighValue: " + str.tostring(high_value) + 
         "\n atr: " + str.tostring(atr) + "\n stop_loss: " + 
         str.tostring(_stop_loss)  + "\n Limit: " +
         str.tostring(_limit)
    [_stop_loss,_stop_lossPoints,_limit, value]




/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////// SIGNALS //////////////////////////////////////////////////////////

ema = ta.ema(close,ema_length)
rsi = ta.rsi(close,14)

ema_buy_signal = ema < low
ema_sell_signal = ema > high


rsi_buy_signal = rsi < rsi_buy_value and rsi[1] < rsi[0]
rsi_sell_signal = rsi > rsi_sell_value and rsi[1] > rsi[0]

trend_buy_signal = close[2] < close[1] and close[1] < close[0]
trend_sell_signal = close[2] > close[1] and close[1] > close[0]

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////// TRADES //////////////////////////////////////////////////////////
long = trend_buy_signal 
         and ema_buy_signal 
         and rsi_buy_signal
short = trend_sell_signal 
         and ema_sell_signal  
         and rsi_sell_signal

/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////// STRATEGY //////////////////////////////////////////////////////////



if long 
    strategy.entry("Long", strategy.long)

if short 
    strategy.entry("Short", strategy.short)
   

// Calculate Trade Entry Variables
last_trade_entry_price := strategy.opentrades.entry_price(strategy.opentrades - 1)
bar_id_entry := strategy.opentrades.entry_bar_index(strategy.opentrades - 1) 
atr := ta.atr(14) 
low_value := ta.lowest(14)
high_value := ta.highest(14)


// Exit Strategy for Long Positions 
if (strategy.position_size[1] != strategy.position_size and strategy.position_size>0)
    [_stop_loss,_stop_loss_points, _limit, value] = getTradeConditionsLong()
    stop_loss := _stop_loss
    stop_loss_points := _stop_loss_points
    limit := _limit
    

    if show_data
        label.new(bar_id_entry,stop_loss - 0.005,str.tostring(value),xloc = xloc.bar_index,yloc = yloc.price,style = label.style_none) 
    strategy.exit("Long Exit", "Long", trail_offset = stop_loss_points/2, trail_points = stop_loss_points/2 , stop = stop_loss , limit = limit   )


// Exit Strategy for Short Positions 
if (strategy.position_size[1] != strategy.position_size and strategy.position_size<0)
    [_stop_loss,_stop_loss_points, _limit, value] = getTradeConditionsShort()
    stop_loss := _stop_loss
    stop_loss_points := _stop_loss_points
    limit := _limit

    if show_data
        label.new(bar_id_entry,stop_loss + 0.005,str.tostring(value),xloc = xloc.bar_index,yloc = yloc.price,style = label.style_none) 
    strategy.exit("Short Exit", "Short", trail_offset = stop_loss_points/2, trail_points = stop_loss_points/2 , stop = stop_loss , limit = limit )


/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////// PLOTS //////////////////////////////////////////////////////////

plot(ema, "SMA", color = color.blue, linewidth = 2 )


p1 = plot(strategy.position_size>0? stop_loss:na, style = plot.style_linebr , color = color.rgb(82, 240, 42) )
p2 = plot(strategy.position_size<0? stop_loss:na, style = plot.style_linebr , color = color.rgb(223, 85, 85) )
p3 = plot(strategy.position_size!=0?limit : na, style = plot.style_linebr , color = color.rgb(94, 85, 223, 100) )


fill(p1, p3, color = color.new(color.green, 90))
fill(p2, p3, color = color.new(#e98787, 90))
```

> Detail

https://www.fmz.com/strategy/427366

> Last Modified

2023-09-20 14:21:16

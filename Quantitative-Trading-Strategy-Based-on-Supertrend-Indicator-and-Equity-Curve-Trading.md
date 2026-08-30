
> Name

Quantitative-Trading-Strategy-Based-on-Supertrend-Indicator-and-Equity-Curve-Trading
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/617bdb097e0a34c0a9400f66bcd1d10d3f66718f6dc71963f1f7030866ae92dc.png)
[trans]
## Overview
The core idea of ​​this strategy is to combine the super-trend indicator with equity curve trading. When the super-trend indicator sends a buy or sell signal, we do not directly execute the transaction, but determine whether the current equity curve is lower than its moving average. We will open a position only when the equity curve is above the moving average. When the equity curve is below the moving average, we will suspend trading on the current strategy. This can effectively prevent the expansion of losses.
## Strategy Principle
This strategy mainly consists of two parts:
1. Super trend indicator
2. Equity Curve Trading
The calculation formula of the super trend indicator is as follows:
Upper rail = source price - ATR multiplier * ATR
Lower track = source price + ATR multiplier * ATR
Among them, ATR represents the average true amplitude. The super trend indicator uses ATR to set the upper and lower rails. When the price breaks through the upper rail, it is a sell signal, and when the price breaks through the lower rail, it is a buy signal.
The idea of ​​net worth curve trading is that we perform a moving average on the net worth curve of the strategy. When the net worth curve is lower than the moving average, the trading of the current strategy is suspended, and the trading is started again after waiting for the net worth curve to rise above the moving average.
This strategy combines the two. After the super-trend indicator generates a trading signal, we do not trade directly, but determine whether the current equity curve is higher than the moving average. Only if both conditions are met at the same time, we will open the position. This can effectively avoid the risk of the super-trend indicator itself and prevent excessive losses.
## Advantage Analysis
The main advantages of this strategy are:
1. It can effectively prevent the risk of super-trend indicators. Supertrend indicators themselves cannot effectively avoid losses, and equity curve trading can make up for this shortcoming.
2. When the transaction is unfavorable, you can suspend the trading of the strategy to avoid excessive losses. It can be opened again when the market improves.
3. Positions can be managed automatically without manual intervention. It automatically pauses when the net value curve is lower than the moving average and starts automatically when it is higher than the moving average.
## Risk Analysis
This strategy also has certain risks:
1. Incorrect parameter setting may result in the inability to effectively exert the effect of equity curve trading. An appropriate moving average period needs to be selected.
2. When market trends change, positions may not be adjusted in time. This will result in certain losses.
3. Because you need to wait for the equity curve to rebound, you may miss a better entry opportunity.
Countermeasures:
1. Optimize parameters and select the best moving average period.
2. Combine with other indicators to judge the trend and adjust positions in a timely manner.
3. Appropriately shorten the trading suspension time to reduce the probability of missing an entry.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test different parameter combinations to find the best ATR period and ATR multiplier.
2. Try other types of moving averages, such as exponential moving average, Hull moving average, etc.
3. Add other indicators to judge the market trend and adjust positions in a timely manner when the trend changes.
4. Optimize the moving average period and find the best balance point. If the cycle is too long, opportunities will be missed; if the cycle is too short, opportunities will be frequently paused.
5. Optimize the conditions for suspending trading, such as setting a stop loss line and suspending trading only when the loss reaches a certain level.
## Summarize
This strategy cleverly combines supertrend indicators with equity curve trading. It not only retains the advantages of super-trend indicators in judging trends, but also effectively controls risks through equity curve trading. Test results show that in most cases, applying equity curve trading will reduce profitability. Therefore, this strategy is more suitable for defensive traders. Through parameter optimization and rule optimization, this strategy can become a very practical quantitative trading strategy.
|| 

## Overview  

The core idea of this strategy is to combine the Supertrend indicator with equity curve trading. When the Supertrend indicator generates a buy or sell signal, we do not directly execute the trade. Instead, we check if the current equity curve is below its moving average. We will open positions only when the equity curve is above the moving average. When the equity curve is below the moving average, we will pause trading for the current strategy. This can effectively prevent the expansion of losses.

## Strategy Logic  

This strategy mainly consists of two parts:  

1. Supertrend Indicator  
2. Equity Curve Trading  

The calculation formula for the Supertrend indicator is:  

Upper Band = Source Price - ATR Multiplier * ATR 
Lower Band = Source Price + ATR Multiplier * ATR  

Where ATR stands for Average True Range. The Supertrend indicator uses the ATR to set the upper and lower bands. A breakout above the upper band stands for a sell signal, while a breakout below the lower band stands for a buy signal.

The idea behind equity curve trading is that we take the moving average of the strategy's equity curve. When the equity curve falls below its moving average, we pause trading for the current strategy and wait for the equity curve to rebound back above the moving average before re-enabling trading.  

This strategy combines the two techniques, so that after the Supertrend indicator generates a trading signal, we do not directly enter trades. Instead, we check if the current equity curve is above its moving average. Only when both conditions are met will we open positions. This can effectively mitigate the risks inherent in the Supertrend indicator itself and prevent excessive losses.

## Advantages  

The main advantages of this strategy are:  

1. It can effectively prevent the risks of the Supertrend indicator. The Supertrend indicator itself cannot effectively curb losses. Equity curve trading makes up for this shortcoming.

2. When trading becomes unfavorable, it pauses trading to avoid excessive losses. We can resume trading after the market recovers.  

3. It can automatically manage positions without manual intervention. Trading is paused automatically when the equity curve falls below the moving average, and resumed when the equity curve rebounds back above it.

## Risks 

There are also some risks with this strategy:  

1. Incorrect parameter settings may render equity curve trading ineffective. Appropriate moving average periods need to be selected.  

2. It may fail to adjust positions promptly when market trend changes. This can lead to certain losses.  

3. It may miss good trading opportunities while waiting for the equity curve to rebound.

Counter measures:  

1. Optimize parameters and select the best moving average period.  

2. Incorporate other indicators to judge trend and adjust positions accordingly.   

3. Shorten the duration of suspended trading to lower the probability of missing opportunities.  

## Optimization Directions   

We can optimize the strategy from the following aspects:

1. Test different parameter combinations to find the optimal ATR period and multiplier.  

2. Try other types of moving averages, like Exponential Moving Average, Hull Moving Average etc.   

3. Add other indicators to determine market trend, and adjust positions when trend changes.

4. Optimize the moving average period to find the best balance. Too long periods may miss opportunities, while too short may pause too frequently.   

5. Optimize the conditions to pause trading, like setting a stop loss threshold before suspension.  

## Conclusion   

This strategy cleverly combines the Supertrend indicator with equity curve trading, leveraging the strengths of both techniques. The test results show that in most cases, applying equity curve trading actually decreases profitability. As such, this strategy is more suitable for defensive traders. With parameter and logic optimization, it can become a very practical quantitative trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_bool_1|true|Show Original Equity Curve and MA|
|v_input_bool_2|true|Show Filtered Equity Curve by MA|
|v_input_int_1|25|(?New Equity Curve Settings)EQ EMA len|
|v_input_1|10|(?SuperTrend Settings)ATR Period|
|v_input_2_hl2|0|Source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_float_1|3|ATR Multiplier|
|v_input_3|true|Change ATR Calculation Method ?|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-14 00:00:00
end: 2024-01-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('Supertrend & Equity curve with EMA', overlay=false, format=format.price, precision=2, initial_capital=100000)

eqlen = input.int(25, "EQ EMA len", group = "New Equity Curve Settings")
shEQandMA = input.bool(true, "Show Original Equity Curve and MA")
shEQfilt = input.bool(true, "Show Filtered Equity Curve by MA")

Periods = input(title='ATR Period', defval=10, group = "SuperTrend Settings")
src = input(hl2, title='Source', group = "SuperTrend Settings")
Multiplier = input.float(title='ATR Multiplier', step=0.1, defval=3.0, group = "SuperTrend Settings")
changeATR = input(title='Change ATR Calculation Method ?', defval=true, group = "SuperTrend Settings")

//SuperTrend Code
atr2 = ta.sma(ta.tr, Periods)
atr = changeATR ? ta.atr(Periods) : atr2
up = src - Multiplier * atr
up1 = nz(up[1], up)
up := close[1] > up1 ? math.max(up, up1) : up
dn = src + Multiplier * atr
dn1 = nz(dn[1], dn)
dn := close[1] < dn1 ? math.min(dn, dn1) : dn
trend = 1
trend := nz(trend[1], trend)
trend := trend == -1 and close > dn1 ? 1 : trend == 1 and close < up1 ? -1 : trend

// Strategy main code
buySignal = trend == 1 and trend[1] == -1
sellSignal = trend == -1 and trend[1] == 1
if buySignal
    strategy.entry('Long', strategy.long)
if sellSignal
    strategy.entry('Short', strategy.short)



//Equity Curve calcs
eq = strategy.netprofit
ch = ta.change(eq)
neq = ch != 0 ? eq : na
mova = ta.ema(neq,eqlen)

// New Equity Curve
var float neweq = 0
var int ttrades = 0
var int wintrades = 0
var int losetrades = 0

switch
    strategy.netprofit == strategy.netprofit[1]  => na
    strategy.netprofit < mova and strategy.netprofit[1] > mova  => neweq := neweq + ch
    strategy.netprofit < mova and strategy.netprofit[1] < mova => na
    strategy.netprofit > mova and strategy.netprofit[1] > mova => neweq := neweq + ch

newch = ta.change(neweq)
switch
    newch == 0 => na
    newch > 0 => 
        wintrades := wintrades +1
        ttrades := ttrades +1
    newch < 0 =>
        losetrades := losetrades +1
        ttrades := ttrades +1

//plot(eq, linewidth = 2)
//plot(mova, color=color.red)
//plot(neweq, color= color.green, linewidth = 3)


//Table 
var testTable = table.new(position = position.top_right, columns = 5, rows = 10, bgcolor = color.green, border_width = 1)
table.cell(table_id = testTable, column = 0, row = 0, text = "Strategy: ", bgcolor=color.white)     
table.cell(table_id = testTable, column = 1, row = 0, text = "Original: ", bgcolor=color.white)     
table.cell(table_id = testTable, column = 2, row = 0, text = "Equity Curve EMA: ", bgcolor=color.white)     

table.cell(table_id = testTable, column = 0, row = 1, text = "Total Trades: ", bgcolor=color.white)     
table.cell(table_id = testTable, column = 0, row = 2, text = "Win Trades: ", bgcolor=color.white)     
table.cell(table_id = testTable, column = 0, row = 3, text = "Lose Trades: ", bgcolor=color.white)     
table.cell(table_id = testTable, column = 0, row = 4, text = "Win Rate: ", bgcolor=color.white)     
table.cell(table_id = testTable, column = 0, row = 5, text = "Net Profit: ", bgcolor=color.white)     

//Equity Curve EMA stat
table.cell(table_id = testTable, column = 2, row = 1, text = str.tostring(ttrades), bgcolor=color.white)     
table.cell(table_id = testTable, column = 2, row = 2, text = str.tostring(wintrades), bgcolor=color.white)
table.cell(table_id = testTable, column = 2, row = 3, text = str.tostring(losetrades), bgcolor=color.white)
table.cell(table_id = testTable, column = 2, row = 4, text = str.tostring(math.round(100*wintrades/ttrades,2)), bgcolor=color.white)
table.cell(table_id = testTable, column = 2, row = 5, text = str.tostring(math.round(neweq)), bgcolor=color.white)

//Original Strategy stat
// table.cell(table_id = testTable, column = 1, row = 1, text = str.tostring(strategy.closedtrades), bgcolor=color.white)     
// table.cell(table_id = testTable, column = 1, row = 2, text = str.tostring(strategy.wintrades), bgcolor=color.white)
// table.cell(table_id = testTable, column = 1, row = 3, text = str.tostring(strategy.losstrades), bgcolor=color.white)
// table.cell(table_id = testTable, column = 1, row = 4, text = str.tostring(math.round(100*strategy.wintrades/strategy.closedtrades,2)), bgcolor=color.white)
// table.cell(table_id = testTable, column = 1, row = 5, text = str.tostring(math.round(strategy.netprofit)), bgcolor=color.white)




//New Equity curve
var newcurve = array.new_float(0)
var int ida = 0
var bool printEQ = false
if newch !=0 
    array.push(newcurve, neweq)
if bar_index > last_bar_index - array.size(newcurve) - 1 - 20  and array.size(newcurve) > 20 
    printEQ := true
else
    printEQ := false

plot(printEQ and ida < strategy.closedtrades and shEQfilt ? array.get(newcurve, ida) : na, color=color.green, linewidth = 2)

if printEQ
    ida := ida + 1
if ida >= array.size(newcurve) and printEQ
    ida := array.size(newcurve) -1



//Original Equity curve
var newcurve2 = array.new_float(0)
var int ida2 = 0
var bool printEQ2 = false
if ch !=0 
    array.push(newcurve2, eq)
if bar_index > last_bar_index - array.size(newcurve2) - 1 - 20  and array.size(newcurve2) > 20 
    printEQ2 := true
else
    printEQ2 := false

plot(printEQ2 and ida2 < strategy.closedtrades and shEQandMA  ? array.get(newcurve2, ida2) : na, color=color.blue, linewidth = 2)

if printEQ2
    ida2 := ida2 + 1
if ida2 >= array.size(newcurve2) and printEQ2
    ida2 := array.size(newcurve2) -1



//Moving Average Array
var marray = array.new_float(0)
if ch
    array.push(marray, mova)

plot(printEQ2 and  array.size(marray) > 40 and shEQandMA ? array.get(marray, ida2-1) : na, color=color.red, linewidth = 1)

hline(0,"0 line", color=color.black, linestyle = hline.style_dotted)


if (last_bar_index-1) and array.size(newcurve2) > 20 and array.size(newcurve) > 20
    l = label.new(bar_index+2, array.get(newcurve2, array.size(newcurve2)-1), "Original Equity Curve", color=color.rgb(33, 149, 243, 85), textcolor = color.black, style = label.style_label_left)
    label.delete(l[1])
    f = label.new(bar_index+2, array.get(newcurve, array.size(newcurve)-1), "Filtered Equity Curve", color=color.rgb(69, 238, 97, 85), textcolor = color.black, style = label.style_label_left)
    label.delete(f[1])
```

> Detail

https://www.fmz.com/strategy/438771

> Last Modified

2024-01-15 11:41:53

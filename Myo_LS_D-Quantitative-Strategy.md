
> Name

Tracking profit-taking strategy based on long and short dual tracks Myo_LS_D-Quantitative-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1349a0e28875de1ec72.png)

[trans]
# Myo_LS_D quantization strategy
## Overview
Myo_LS_D quantitative strategy is a trailing take-profit strategy based on long and short dual tracks. This strategy comprehensively uses multiple indicators such as moving averages, price breakthroughs, risk-reward ratios, etc. to construct trading signals. On the premise of accurate trend judgment, a higher winning rate and profitability rate are achieved.
## Strategy Principle
This strategy mainly consists of a trend judgment module, a long module, a short module, a tracking and profit-taking module, etc.
1. The trend judgment module uses the donchain channel to judge the overall trend direction. The premise for long entry is that it is in an upward trend, and for short entry, it needs to be in a downward trend.
2. The long module considers new highs, lows, long-term moving average positions and other factors. The short-selling module takes into account new highs, lows, short-term moving average positions, and other factors. This ensures that a position is opened on a breakout of key price points either upward or downward.
3. The tracking take profit module uses two SMA moving averages with different periods to track price changes in real time. When the price falls below the moving average, close the position and take profit. This real-time tracking can maximize profits from trends.
4. When setting stop loss, consider enlarging the stop loss and ensuring that the stop loss point is far away from the support level to avoid being shaken out.
## Advantage Analysis
The biggest advantage of this strategy is to separate long and short positions and track the profit-taking strategy. Specifically, it is mainly reflected in:
1. The separation of long and short can maximize profit opportunities in capturing unilateral trend markets.
2. Tracking take profit can achieve higher profitability through real-time adjustment. Compared with the traditional take-profit method, the income can be significantly improved.
3. Expanding the stop loss can reduce the probability of being shaken out and reduce the risk of loss.
## Risks and Solutions
The main risks of this strategy focus on the following points:
1. Errors in trend judgment may result in losses when opening a position against the trend. You can adjust the donchain parameters appropriately or add other indicators to optimize.
2. The trailing stop-profit is too aggressive, which may prevent sustained profits from being stopped early. Optimization can be achieved by appropriately expanding the distance between take-profit and moving averages.
3. If the stop loss range is too small, it may increase the probability of being shaken out. The stop loss range can be appropriately expanded to reduce risks.
## Optimization direction
This strategy can be continuously optimized from the following aspects:
1. Optimize the trend judgment module and improve the accuracy of judgment. You can consider combining more indicators such as MACD to achieve this.
2. Adjust the tracking and profit-taking method to further expand the profit margin. For example, you can move the take profit line proportionally, etc.
3. Expand the stop loss range or consider indenting the stop loss to further reduce the probability of being shaken out.
4. Different varieties have different parameters and can be trained to obtain the optimal parameter combination. Further enhance strategic returns.
## Summary
Myo_LS_D strategy is generally a relatively mature and stable long-short tracking and profit-taking strategy. It has obvious advantages and controllable risks. It is one of the quantitative solutions worth holding for a long time. In the future, through further optimization, its revenue performance can be continuously improved and become a more outstanding quantitative strategy.
||

## Overview
The Myo_LS_D quantitative strategy is a dual-track tracking stop-profit strategy based on long and short positions. The strategy combines multiple indicators such as moving averages, price breakthroughs, and risk-return ratios to build trading signals. It achieves a high win rate and profit rate on the premise of accurate trend judgment.

## Principle  
The strategy consists mainly of a trend judgment module, long position module, short position module, tracking stop profit module, etc.

1. The trend judgment module uses the Donchain channel to determine the overall trend direction. The prerequisite for going long is an upward trend, while going short requires a downward trend.  

2. The long position module takes into account factors such as new highs, lows, long moving average positions, etc. The short position module considers new highs, lows, short moving average positions and other factors. This ensures the opening of positions when breaking through critical price points upwards or downwards.

3. The tracking stop profit module uses two SMA moving averages of different cycles to track price changes in real time. When the price breaks through the moving average line, the position is closed for profit. This kind of real-time tracking can maximize profits from the trend.  

4. Stop loss setting considers enlarged stop loss to keep the stop loss point far away from the support level to avoid being knocked out.

## Advantage Analysis 
The biggest advantage of this strategy is the separate long and short position building and tracking stop profit strategy. Specifically, it is mainly embodied in:  

1. Separate long and short positions can maximize profit opportunities by capturing one-sided trend trading opportunities.  

2. Tracking stop profit can obtain higher profit margin through real-time adjustment. Compared with traditional stop profit methods, income can be significantly improved.

3. Enlarged stops can reduce the probability of being knocked out and reduce the risk of losses.


## Risk and Solutions
The main risks of this strategy are concentrated in the following points:   

1. Incorrect trend judgment may result in contrarian positions and losses. Optimization can be achieved by appropriately adjusting Donchain parameters or adding other indicators for judgment.

2. Tracking stop profit is too aggressive and may prematurely stop profit without being able to sustain gains. Optimization can be achieved by appropriately increasing the spacing between stop profit moving averages.  

3. The stop loss range is too small, which may increase the probability of being knocked out. Appropriately expanding the stop loss magnitude can mitigate risks.

## Optimization Directions
The main optimization directions for this strategy are:  

1. Optimize the trend judgment module to improve judgment accuracy. Consider combining more indicators such as MACD.  

2. Adjust the tracking stop profit method to further expand profit space. For example, moving stop profit lines in proportion.

3. Expanding the stop loss range or considering shrinkage stops can further reduce the probability of being knocked out.   

4. Different varieties have different parameters. Optimal parameter combinations can be obtained through training to further improve strategy returns.


## Summary   
In general, the Myo_LS_D strategy is a relatively mature and stable dual-track tracking stop-profit quantitative strategy. It has obvious advantages and controllable risks. It is one of the quantitative solutions worth holding for the long term. Future optimizations can enable continuous performance improvement to make it an even more superior quantitative strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|100|Stop loss length for long|
|v_input_int_2|100|Short stop loss length|
|v_input_int_3|0|Long trailing take profit SMA length 1: 10|5|20|40|60|80|
|v_input_int_4|0|Long trailing take profit SMA length 2: 20|10|5|40|60|80|
|v_input_int_5|0|Short trailing take profit SMA length 1: 5|10|20|40|60|80|
|v_input_int_6|0|Short trailing take profit SMA length 2: 10|5|20|40|60|80|
|v_input_int_7|0|Long trend line: 400|200|300|100|500|
|v_input_int_8|0|Short trend line: 300|200|100|400|500|
|v_input_int_9|20|Number of short-term average price K lines|
|v_input_int_10|60|Quantity of medium-term average price K lines|
|v_input_int_11|120|Number of long-term average price K lines|
|v_input_int_12|8|Trend baseline|
|v_input_int_13|26|Short Baseline|

> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-15 00:00:00
end: 2024-01-14 00:00:00
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © agresiynin

//@version=5
// ©Myo_Pionex
strategy(
 title                  =   "Ｍyo_simple strategy_LS_D",
 shorttitle             =   "Myo_LS_D",
 overlay                =   true )


// var
lowest_price = ta.lowest(low, 200)
highest_price = ta.highest(high, 200)
min_800 = ta.lowest(low, 800)
max_800 = ta.highest(high, 800)
tp_target_L = min_800 + (max_800 - min_800) * math.rphi
tp_target_S = max_800 - (max_800 - min_800) * math.rphi
sl_length_L = input.int(100, "做多的止損長度", minval = 50, maxval = 300, step = 50)
sl_length_S = input.int(100, "做空的止損長度", minval = 50, maxval = 300, step = 50)
sl_L = lowest_price * (1 - 0.005)
sl_S = highest_price * (1 + 0.005)
rrr_L = tp_target_L - sl_L / sl_L
rrr_S = ta.lowest(low, 800) + ta.highest(high, 800) - ta.lowest(low, 800) * math.rphi / ta.highest(high, 200) + 0.005 * ta.highest(high, 200) - ta.lowest(low, 200) - 0.005 * ta.lowest(low, 200)
smalen1 = input.int(10, "做多追蹤止盈SMA長度1", options = [5, 10, 20, 40, 60, 80])
smalen2 = input.int(20, "做多追蹤止盈SMA長度2", options = [5, 10, 20, 40, 60, 80])
smalen1_S = input.int(5, "做空追蹤止盈SMA長度1", options = [5, 10, 20, 40, 60, 80])
smalen2_S = input.int(10, "做空追蹤止盈SMA長度2", options = [5, 10, 20, 40, 60, 80])
TrendLength_L = input.int(400, "做多趨勢線", options = [100, 200, 300, 400, 500])
TrendLength_S = input.int(300, "做空趨勢線", options = [100, 200, 300, 400, 500])
SMA1 = ta.sma(close, smalen1)
SMA2 = ta.sma(close, smalen2)
SMA1_S = ta.sma(close, smalen1_S)
SMA2_S = ta.sma(close, smalen2_S)
shortlength = input.int(20, "短期均價K線數量")
midlength = input.int(60, "中期均價K線數量")
longlength = input.int(120, "長期均價K線數量")
ShortAvg = math.sum(close, shortlength)/shortlength
MidAvg = math.sum(close, midlength)/midlength
LongAvg = math.sum(close, longlength)/longlength

// Trend
basePeriods = input.int(8, minval=1, title="趨勢基準線")
basePeriods_Short = input.int(26, "做空基準線")
donchian(len) => math.avg(ta.lowest(len), ta.highest(len))
baseLine = donchian(basePeriods)
baseLine_Short = donchian(basePeriods_Short)
trend = request.security(syminfo.tickerid, "D", baseLine)
isUptrend = false
isDowntrend = false
baseLine_D = request.security(syminfo.tickerid, "D", baseLine)
plot(baseLine_D, color=#B71C1C, title="趨勢基準線")
if close[0] > baseLine_D
    isUptrend := true
if close[0] < baseLine_Short
    isDowntrend := true
// Long
// Condition
// entry
con_a = low > lowest_price ? 1 : 0
con_b = high > highest_price ? 1 : 0
con_c = close[0] > ta.sma(close, TrendLength_L) ? 1 : 0
con_d = isUptrend ? 1 : 0
con_e = rrr_L > 3 ? 1 : 0
con_a1 = close[0] > ShortAvg[shortlength] ? 1 : 0
con_b1 = close[0] > MidAvg[midlength] ? 1 : 0

// close
con_f = ta.crossunder(close, SMA1) and ta.crossunder(close, SMA2) ? 1 : 0
con_g = close < ta.lowest(low, sl_length_L)[1] * (1 - 0.005) ? 1 : 0

// exit
con_h = tp_target_L

// Main calculation
LongOpen = false
AddPosition_L = false

if con_a + con_b + con_c + con_e + con_a1 + con_b1 >= 4 and con_d >= 1
    LongOpen := true
// Short
// Condition
// entry
con_1 = high < highest_price ? 1 : 0
con_2 = low < lowest_price ? 1 : 0
con_3 = close[0] < ta.sma(close, TrendLength_S) ? 1 : 0
con_4 = isDowntrend ? 1 : 0
con_5 = rrr_S > 3 ? 1 : 0
con_11 = close[0] < ShortAvg[shortlength] ? 1 : 0
con_12 = close[0] < MidAvg[midlength] ? 1 : 0

// close
con_6 = ta.crossover(close, SMA1_S) and ta.crossover(close, SMA2_S) ? 1 : 0
con_7 = close > ta.highest(high, sl_length_S)[1] * (1 + 0.005) ? 1 : 0

// exit
con_8 = tp_target_S

// Main calculation
ShortOpen = false
AddPosition_S = false

if con_1 + con_2 + con_3 + con_4 + con_5 + con_11 + con_12 >= 5
    ShortOpen := true

//
// execute
//
strategy.initial_capital = 50000
if strategy.position_size == 0
    if LongOpen
        strategy.entry("Long Open" , strategy.long , comment= "Long Open " + str.tostring(close[0]), qty=strategy.initial_capital/close[0])

if strategy.position_size > 0
    if (con_f > 0 or con_g > 0 or ShortOpen) and close <= baseLine_D
        strategy.close_all(comment="Close Long " + str.tostring(close[0]))

if strategy.position_size == 0
    if ShortOpen
        strategy.entry("Short Open" , strategy.short , comment= "Short Open " + str.tostring(close[0]), qty=strategy.initial_capital/close[0])

if strategy.position_size < 0
    if (con_6 > 0 or con_7 > 0 or LongOpen) and close >= baseLine_D
        strategy.close_all(comment="Close Short " + str.tostring(close[0]))


plot(ta.sma(close, TrendLength_L), color=#e5c212, title="LTradeTrend")
plot(ta.sma(close, TrendLength_S), color=#1275e5, title="STradeTrend")
plot(SMA1, "SMA1", color = color.lime, linewidth = 2)
plot(SMA2, "SMA2", color = color.rgb(255, 0, 255), linewidth = 2)
```

> Detail

https://www.fmz.com/strategy/438820

> Last Modified

2024-01-15 14:56:03

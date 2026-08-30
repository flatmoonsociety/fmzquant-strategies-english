
> Name

Yesterdays-High-Breakout-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy operates based on the highest price of the previous trading day and is a trend following type strategy. It will open a long position when it breaks through the highest price of the previous trading day, and it will open a long position repeatedly even if there are multiple breakthroughs that day.
### Strategy Principles
1. Use the LucF function to avoid peeking at the latest K-line during backtesting.
2. Determine whether it is the opening of a new trading day. Record the highest price max_today and the lowest price min_today of the day.
3. Compare the current highest price high with max_today, and update max_today.
4. Compare the current lowest price low with min_today, and update min_today.
5. Draw the high and low prices of the previous trading day.
6. Set the opening point when it breaks through the highest price of the previous trading day. You can add a certain amount of GAP to the highest price to delay or advance entry.
7. Set the stop loss ratio sl and the take profit ratio tp.
8. Open a long position when the price breaks through the highest price of the previous trading day.
9. Set stop loss and take profit points.
10. You can choose whether to enable trailing stop loss, set the minimum requirements for activating trailing stop loss, and the distance of trailing stop loss.
11. You can choose whether to judge the EMA status when closing.
### Advantage Analysis
This is a relatively simple trend following strategy with the following advantages:
1. The strategy signal is simple, clear and easy to implement.
2. Using the trend confirmation signal formed by the breakthrough of the previous trading day's highest price can effectively filter out the noise that shocks the market.
3. The entry sensitivity can be adjusted through the GAP parameter.
4. The overall risk is controllable and the stop loss is clear.
5. You can choose whether to use trailing stop loss to lock in more profits.
6. You can combine it with EMA judgment to avoid being trapped in a dead cross.
### Risk Analysis
There are also some risks to be aware of with this strategy:
1. Failure to break through may cause losses, and a reasonable stop loss price needs to be set.
2. The effectiveness of breakthroughs depends on the market being in a trend state, and it is easy to be trapped in a volatile market.
3. If the trailing stop loss is not set properly, it may be too sensitive and the stop loss will be adjusted slightly by the price.
4. EMA judgment may be too sensitive or slow if the parameters are improperly selected.
5. There are many variables that need to be paid attention to and optimized, such as GAP, stop loss width, trailing stop loss settings, etc.
### Optimization direction
This strategy can be further optimized from the following aspects:
1. Adjust the stop loss from a fixed value to a dynamic stop loss of ATR or trend.
2. Add standard deviation filtering to judge the effectiveness of breakthroughs.
3. Add volatility-based conditions to avoid invalid breakthroughs in volatile markets.
4. Optimize EMA parameters to make the judgment more stable and accurate.
5. Optimize the parameters of trailing stop loss to make it more consistent with the range of market fluctuations.
6. Test the parameter robustness of different varieties.
7. Add a mechanism to dynamically adjust position size.
### Summarize
This strategy is relatively simple and practical overall and is a typical trend following strategy. The breakthrough of the highest price on the previous trading day is used as a signal to track the trend. Risk control mainly relies on stop loss. Through reasonable parameter optimization, the strategy can achieve better results in trend markets. However, you need to pay attention to controlling the stop loss strategy and filtering conditions to avoid being trapped in the volatile market. This strategy can be used as the basic framework of the trend following strategy for expansion and optimization.
|| 

## Overview

This strategy operates based on the previous trading day's high, working in a trend-following mode. It goes long when yesterday's high is broken out, even if there are multiple breakouts in a day.

## Strategy Logic

1. Use LucF function to avoid lookahead bias in backtesting. 

2. Identify if it's a new trading day open. Record the day high max_today and low min_today.

3. Compare current high with max_today, update max_today if surpassed.

4. Compare current low with min_today, update min_today if breached.

5. Plot previous trading day's high and low levels.

6. Set entry point on breakout of previous day's high, GAP can be added to advance or delay entry.

7. Set stop loss percentage sl and take profit percentage tp. 

8. Go long when price breaks previous trading day's high.

9. Set stop loss price and take profit price.

10. Optionally enable trailing stop loss, with activation level and offset distance.

11. Optionally close trade based on EMA crossover.

## Advantage Analysis

This simple trend following strategy has the following advantages:

1. Clear and straightforward signal generation. Easy to implement.

2. Breakout of previous day's high provides trend confirmation, reducing whipsaws. 

3. GAP parameter allows adjusting entry sensitivity.

4. Overall risk is controlled with clear stop loss. 

5. Trailing stop can be used to lock in more profits.

6. EMA crossover avoids being trapped in downtrends.

## Risk Analysis

There are some risks to note:

1. Failed breakout can cause losses. Reasonable stop loss needed.

2. Requires trending market. Whipsaws likely in ranging conditions.

3. Improper trailing stop can get stopped out prematurely. 

4. Poor EMA parameter choice can make it too sensitive or lagging.

5. Multiple variables need tuning like GAP, stop loss, trailing stop etc.

## Improvement Opportunities

Some ways to further optimize the strategy:

1. Use dynamic stop loss based on ATR or trend.

2. Add filter for valid breakout using standard deviation. 

3. Add volatility condition to avoid false breakout in choppy markets.

4. Optimize EMA parameter for more robust signal. 

5. Fine tune trailing stop parameters to match market volatility.

6. Test parameter robustness across different instruments. 

7. Add dynamic position sizing mechanism. 

## Conclusion

The strategy is simple and practical as a typical trend following system based on previous day's high breakout. Risk management depends on stop loss primarily. With proper parameter tuning, it can perform well in trending conditions. But proper stop loss and filters are needed to avoid whipsaws. The framework can be enhanced further as a basis for trend following strategies.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_bool_1|false|(?ROC Filter from CloseD)roc_enable|
|v_input_float_1|true|Treshold|
|v_input_float_2|true|(?Entry)Gap%|
|v_input_float_3|3|Stop-loss|
|v_input_float_4|9|Take-profit|
|v_input_float_5|2|(?Trailing Stop Settings)Trailing-stop|
|v_input_float_6|true|Offset Trailing|
|v_input_bool_2|true|Trailing-stop|
|v_input_bool_3|false|Close EMA|
|v_input_int_1|10|EMA length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-30 00:00:00
end: 2023-10-07 00:00:00
period: 15m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)
// © TheSocialCryptoClub

//@version=5

strategy("Yesterday's High", overlay=true, pyramiding = 1,
         initial_capital=10000, 
         default_qty_type=strategy.percent_of_equity, default_qty_value=10,
         slippage=1, backtest_fill_limits_assumption=1, use_bar_magnifier=true,
         commission_type=strategy.commission.percent, commission_value=0.075
         )

// -----------------------------------------------------------------------------
// ROC Filter
// -----------------------------------------------------------------------------

// f_security function by LucF for PineCoders available here: https://www.tradingview.com/script/cyPWY96u-How-to-avoid-repainting-when-using-security-PineCoders-FAQ/
f_security(_sym, _res, _src, _rep) => request.security(_sym, _res, _src[not _rep and barstate.isrealtime ? 1 : 0])[_rep or barstate.isrealtime ? 0 : 1]
high_daily = f_security(syminfo.tickerid, "D", high, false)

roc_enable = input.bool(false, "", group="ROC Filter from CloseD", inline="roc")
roc_threshold = input.float(1, "Treshold", step=0.5, group="ROC Filter from CloseD", inline="roc")

closed = f_security(syminfo.tickerid,"1D",close, false)
roc_filter= roc_enable ? (close-closed)/closed*100  > roc_threshold  : true


// -----------------------------------------------------------------------------
// Trigger Point 
// -----------------------------------------------------------------------------

open_session = ta.change(time('D'))
price_session = ta.valuewhen(open_session, open, 0)
tf_session = timeframe.multiplier <= 60

bgcolor(open_session and tf_session ?color.new(color.blue,80):na, title = "Session")

first_bar = 0
if open_session
    first_bar := bar_index

var max_today = 0.0
var min_today = 0.0
var high_daily1 = 0.0
var low_daily1 = 0.0
var today_open = 0.0

if first_bar
    high_daily1 := max_today
    low_daily1 := min_today
    today_open := open
    max_today := high
    min_today := low


if high >= max_today
    max_today := high

if low < min_today
    min_today := low


same_day  = today_open == today_open[1]

plot( timeframe.multiplier <= 240 and same_day ? high_daily1 : na, color= color.yellow , style=plot.style_linebr, linewidth=1, title='High line')
plot( timeframe.multiplier <= 240 and same_day ? low_daily1 : na, color= #E8000D , style=plot.style_linebr, linewidth=1, title='Low line')

// -----------------------------------------------------------------------------
// Strategy settings 
// -----------------------------------------------------------------------------

Gap = input.float(1,"Gap%", step=0.5, tooltip="Gap di entrata su entry_price -n anticipa entrata, con +n posticipa entrata", group = "Entry")
Gap2 = (high_daily1 * Gap)/100

sl  = input.float(3, "Stop-loss", step= 0.5,  group = "Entry")
tp  = input.float(9, "Take-profit", step= 0.5, group = "Entry")
stop_loss_price = strategy.position_avg_price * (1-sl/100)
take_price = strategy.position_avg_price * (1+tp/100)

sl_trl = input.float(2, "Trailing-stop", step = 0.5, tooltip = "Attiva trailing stop dopo che ha raggiunto...",group = "Trailing Stop Settings")//group = "Trailing Stop Settings")
Atrl= input.float(1, "Offset Trailing", step=0.5,tooltip = "Distanza dal prezzo", group = "Trailing Stop Settings")
stop_trl_price_cond = sl_trl * high/syminfo.mintick/100
stop_trl_price_offset_cond = Atrl * high/syminfo.mintick/100

stop_tick = sl * high/syminfo.mintick/100
profit_tick = tp * high/syminfo.mintick/100

mess_buy = "buy"
mess_sell = "sell"

// -----------------------------------------------------------------------------
// Entry - Exit - Close
// -----------------------------------------------------------------------------

if close < high_daily1 and roc_filter
    strategy.entry("Entry", strategy.long, stop = high_daily1 + (Gap2), alert_message = mess_buy)

ts_n  = input.bool(true, "Trailing-stop", tooltip = "Attiva o disattiva trailing-stop", group = "Trailing Stop Settings")
close_ema = input.bool(false, "Close EMA", tooltip = "Attiva o disattiva chiusura su EMA", group = "Trailing Stop Settings")
len1 = input.int(10, "EMA length", step=1, group = "Trailing Stop Settings")
ma1 = ta.ema(close, len1)

plot(ma1, title='EMA', color=color.new(color.yellow, 0))

if ts_n == true
    strategy.exit("Trailing-Stop","Entry",loss= stop_tick, stop= stop_loss_price, limit= take_price, trail_points = stop_trl_price_cond, trail_offset = stop_trl_price_offset_cond, comment_loss="Stop-Loss!!",comment_profit ="CASH!!", comment_trailing = "TRL-Stop!!", alert_message = mess_sell)
else
    strategy.exit("TP-SL", "Entry",loss= stop_tick, stop=stop_loss_price, limit= take_price, comment_loss= "Stop-loss!!!", comment_profit = "CASH!!", alert_message = mess_sell)

if close_ema == true and ta.crossunder(close,ma1)
    strategy.close("Entry",comment = "Close" , alert_message = mess_sell)


```

> Detail

https://www.fmz.com/strategy/428695

> Last Modified

2023-10-08 14:06:55

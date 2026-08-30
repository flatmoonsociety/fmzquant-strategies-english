
> Name

Bullish trend following strategy based on RSI indicator RSI-Based-Bullish-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/80de9bcba92c97002b4cfaad76ad7de9d607011d002366c563bd1efb8c3350dd.png)
[trans]

## Overview
This strategy is designed based on the Relative Strength Index (RSI) indicator, and is a long trend tracking trading strategy based on buying at the low point of RSI and stop loss and take profit at the high point. A buy signal is generated when the RSI indicator is below the overbought line, and a sell signal is generated when the RSI indicator is above the oversold line. Strategies optimize the performance of tracking trends and can effectively control trading risks.
## Strategy Principle
This strategy uses the RSI indicator to determine whether a stock's price is overvalued or undervalued. The RSI indicator combines with the overbought and oversold lines to form buy and sell signals. Specifically, if the RSI indicator crosses the oversold line of 20, a buy signal is generated; if the RSI indicator crosses the overbought line of 80, a sell signal is generated.
After entering a long position, the strategy sets an initial stop-loss level to control downside risk. At the same time, set two take-profit lines with different ratios, and take profits in batches to lock in profits. Specifically, first take profit on 50% of the position, and the take-profit price is 3% of the purchase price; then take profit on the remaining 50% of the position, and the take-profit price is 5% of the purchase price.
This strategy simply and effectively uses the RSI indicator to determine when to enter the market. The stop-profit and stop-loss settings are reasonable and can effectively control risks.
## Strategic Advantages
- Use RSI indicator to judge long and short positions and avoid blindly going long.
- RSI indicator parameters have been optimized and the indicator effect is better
- The double take-profit design is reasonable, which can realize profit-taking in batches and lock in more profits.
- Initial stop loss and continuous stop loss prevent huge losses
## Risk Analysis
- A long strategy is not effective in a bull market where profits cannot be sustained.
- There is a probability that the RSI indicator sends out wrong signals, and improper signal judgment may increase losses.
- The stop loss point is too deep, causing the risk of being unable to stop the loss.
- The lack of restrictions on the number and proportion of additional positions may cause losses to amplify
## Optimization direction
- Combine with other indicators to filter RSI signals to improve signal accuracy
- Add restrictions on the number and proportion of positions added
- Test the effects of different RSI parameters
- Optimize stop loss and profit points to reduce risks
## Summarize
This strategy uses the RSI indicator to judge the market, and the stop-profit and stop-loss settings are reasonable. It can effectively judge market trends and control transaction risks, and is suitable for use as a long tracking strategy. The stability of the strategy can be further improved through signal filtering, parameter testing, stop loss optimization, etc.
||


## Overview

This strategy is designed based on the Relative Strength Index (RSI) indicator for buying on RSI low points and taking profit and stop loss on RSI high points. It generates buy signals when RSI drops below the oversold line and sell signals when RSI rises above the overbought line. The strategy is optimized to track trends with effective risk control.

## Strategy Logic

The strategy uses the RSI indicator to determine if a stock is overvalued or undervalued. RSI combined with overbought and oversold lines forms buy and sell signals. Specifically, if RSI crosses above the 20 oversold line, a buy signal is generated; if RSI crosses below the 80 overbought line, a sell signal is generated.

After entering a long position, the strategy sets an initial stop loss to control the downside risk. At the same time, two take profit lines with different ratios are set to take profits in batches and lock in profits. Specifically, 50% of the position will take profit first at 3% above the entry price; then the remaining 50% position will take profit at 5% above the entry price.

The strategy effectively utilizes the RSI indicator to determine entry timing. The stop loss and take profit settings are reasonable to effectively control risks.

## Advantages

- Utilize RSI indicator to determine long/short positions and avoid trading blindly 
- Optimized RSI parameters for better indicator effect
- Reasonable dual take profit design allows taking profits in batches to lock in more profits  
- Initial stop loss and trailing stop loss prevent huge losses

## Risks

- Poor performance in a bull market that cannot sustain profits
- Probability of incorrect signals from RSI exists and can increase losses from improper signal judgement 
- Risk that stops cannot be triggered if stop loss points are set too deep
- Risk of magnified losses without limit on pyramiding times and ratio 

## Improvements

- Add other indicators to filter RSI signals and improve accuracy 
- Set limits on pyramiding times and ratios
- Test effects of different RSI parameters 
- Optimize stop loss and take profit points to lower risks

## Summary  

The strategy utilizes RSI to judge market condition and has reasonable stop loss and take profit configuration. It can effectively determine market trend and control trading risks, suitable as a bullish trend following strategy. Signal filtering, parameter testing, stop loss optimization etc. can further improve the stability of the strategy.


[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_string_1|0|Strategy Direction: long|short|all|
|v_input_1|21|length|
|v_input_2|20|overSold|
|v_input_3|80|overBought|
|v_input_4|true|Display info panels?|
|v_input_5|40|fibs label offset|
|v_input_string_2|0|fibs label size: size.normal|size.small|size.tiny|size.large|size.huge|
|v_input_6|false|trend|
|v_input_float_1|5| stop loss|
|v_input_int_1|50| qty_percent1|
|v_input_int_2|50| qty_percent2|
|v_input_float_2|3| Take profit1|
|v_input_float_3|5| Take profit2|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-17 00:00:00
end: 2023-12-24 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/

//@version=5

strategy(title='RSI Long Strategy', overlay=true, pyramiding=5, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, calc_on_order_fills=false, slippage=0, commission_type=strategy.commission.percent, commission_value=0.075)
strat_dir_input = input.string(title='Strategy Direction', defval='long', options=['long', 'short', 'all'])
strat_dir_value = strat_dir_input == 'long' ? strategy.direction.long : strat_dir_input == 'short' ? strategy.direction.short : strategy.direction.all
strategy.risk.allow_entry_in(strat_dir_value)
//INPUTS


length = input(21)
overSold = input(20)
overBought = input(80)
p = close

vrsi = ta.rsi(p, length)
price = close
var bool long = na
var bool short = na

long := ta.crossover(vrsi, overSold)
short := ta.crossunder(vrsi, overBought)

var float last_open_long = na
var float last_open_short = na

last_open_long := long ? close : nz(last_open_long[1])
last_open_short := short ? close : nz(last_open_short[1])
mpoint=(last_open_long+last_open_short)/2

entry_value = last_open_long
entry_value1 = last_open_short

// Rounding levels to min tick
nround(x) =>
    n = math.round(x / syminfo.mintick) * syminfo.mintick
    n
//
disp_panels = input(true, title='Display info panels?')
fibs_label_off = input(40, title='fibs label offset')
fibs_label_size = input.string(size.normal, options=[size.tiny, size.small, size.normal, size.large, size.huge], title='fibs label size')
r1_x = timenow + math.round(ta.change(time) * fibs_label_off)
r1_y = last_open_short
text1 = 'High : ' + str.tostring(nround(last_open_short))
s1_y = last_open_long
text3 = 'low : ' + str.tostring(nround(last_open_long))

R1_label = disp_panels ? label.new(x=r1_x, y=r1_y, text=text1, xloc=xloc.bar_time, yloc=yloc.price, color=color.orange, style=label.style_label_down, textcolor=color.black, size=fibs_label_size) : na
S1_label = disp_panels ? label.new(x=r1_x, y=s1_y, text=text3, xloc=xloc.bar_time, yloc=yloc.price, color=color.lime, style=label.style_label_up, textcolor=color.black, size=fibs_label_size) : na

label.delete(R1_label[1])
label.delete(S1_label[1])
//
plot(mpoint, title='avreage', color=color.new(color.red, 40), style=plot.style_linebr, linewidth=3, trackprice=true, offset=-9999)
plot(last_open_short, title='high', color=color.new(color.red, 40), style=plot.style_linebr, linewidth=3, trackprice=true, offset=-9999)
plot(last_open_long, title='low', color=color.new(color.blue, 40), style=plot.style_linebr, linewidth=3, trackprice=true, offset=-9999)
//
trend = input(false)
if barstate.islast and trend == true
    line z = line.new(bar_index[1], last_open_short[1], bar_index, last_open_short, extend=extend.both, color=color.red, style=line.style_dashed, width=1)
    line f = line.new(bar_index[1], mpoint[1], bar_index, mpoint, extend=extend.both, color=color.blue, style=line.style_dashed, width=1)
    line w = line.new(bar_index[1], last_open_long[1], bar_index, last_open_long, extend=extend.both, color=color.green, style=line.style_dashed, width=1)
    line.delete(z[1])
    line.delete(f[1])
    line.delete(w[1])
    
//bu = ta.crossover(close, mpoint)
//sz = ta.crossunder(close, mpoint)
//bu1 = ta.crossover(close, last_open_short)
sz1 = ta.crossunder(close, last_open_short)
bu2 = ta.crossover(close, last_open_long)
//sz2 = ta.crossunder(close, last_open_long)
//plotshape(sz, style=shape.triangledown, location=location.abovebar, color=color.new(color.orange, 0), size=size.tiny)
//plotshape(bu, style=shape.triangleup, location=location.belowbar, color=color.new(color.blue, 0), size=size.tiny)
//plotshape(sz1, style=shape.triangledown, location=location.abovebar, color=color.new(color.red, 0), size=size.tiny)
//plotshape(bu1, style=shape.triangleup, location=location.belowbar, color=color.new(color.green, 0), size=size.tiny)
//plotshape(sz2, style=shape.triangledown, location=location.abovebar, color=color.new(color.red, 0), size=size.tiny)
//plotshape(bu2, style=shape.triangleup, location=location.belowbar, color=color.new(color.green, 0), size=size.tiny)

l = bu2
s = sz1 
if l
    strategy.entry('buy', strategy.long)
if s
    strategy.entry('sell', strategy.short)
per(pcnt) =>
    strategy.position_size != 0 ? math.round(pcnt / 100 * strategy.position_avg_price / syminfo.mintick) : float(na)
stoploss = input.float(title=' stop loss', defval=5, minval=0.01)
los = per(stoploss)
q1 = input.int(title=' qty_percent1', defval=50, minval=1)
q2 = input.int(title=' qty_percent2', defval=50, minval=1)
tp1 = input.float(title=' Take profit1', defval=3, minval=0.01)
tp2 = input.float(title=' Take profit2', defval=5, minval=0.01)
//tp4 = input.float(title=' Take profit4', defval=5, minval=0.01)
strategy.exit('x1', qty_percent=q1, profit=per(tp1), loss=los)
strategy.exit('x2', qty_percent=q2, profit=per(tp2), loss=los)


```

> Detail

https://www.fmz.com/strategy/436524

> Last Modified

2023-12-25 14:32:19

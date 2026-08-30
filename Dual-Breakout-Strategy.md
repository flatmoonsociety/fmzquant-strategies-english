
> Name

Dual-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ac1bfb5c630b1a3269.png)

[trans]


### Overview
This strategy uses the Bollinger Bands indicator to find long and short breakthrough points, and combines it with the ADX indicator to filter out low-volatility adverse markets and achieve trend tracking.
### Strategy Principles
This strategy is mainly based on the Bollinger Bands indicator to determine the long and short direction. The middle line of Bollinger Bands is the moving average of N-day closing prices, and the bandwidth is calculated by the standard deviation. When the price breaks through the lower band, it is judged as a long signal; when the price breaks through the upper band, it is judged as a short signal.
In order to avoid erroneous transactions caused by invalid breakthroughs in non-trending markets, this strategy integrates the ADX indicator to filter low-volatility markets. Only when the ADX value is lower than the set threshold, a buy or sell signal will be issued. When the ADX value is higher than the threshold, all positions will be closed and wait for the market to turn trend.
The strategy also sets a pullback stop and an upward trailing take-profit. Specifically, after each position is opened, the lowest price on the previous N days will be recorded as the callback stop loss level in that direction, and the highest price will be used as the upward tracking stop loss level. This locks in profits while minimizing losses from reversals.
From the code logic point of view, the strategy first calculates the Bollinger Bands and ADX indicator parameters. Then determine whether the price breaks through the upper and lower Bollinger Bands and whether the ADX value is lower than the threshold. If so, a buy and sell signal will be generated. Afterwards, the stop-loss and stop-profit levels are updated and tracked in real time based on whether the position is held and the direction of the position.
### Advantage Analysis
- Use Bollinger Bands to determine clear long and short breakthrough points and seize trend opportunities.
- Comprehensive ADX indicator filtering to avoid following the trend when there is no clear trend
- Callback stop loss can effectively control single loss
- Trailing your take profit upward can lock in most of your profits
### Risk Analysis
- Bollinger Band breakthroughs do not take into account the relationship between volume and energy, and may result in false breakthroughs.
- Improper judgment of ADX filtering may also miss trend opportunities
- If the stop loss and take profit are too close, the exit may be reversed and stopped.
- Improper parameter settings can also affect strategy performance
You can consider combining other indicators to judge whether it can be supported to ensure a breakthrough in VALID; optimize the ADX filtering conditions and use the slope of the ADX curve to determine the turning point of the trend; appropriately relax the stop loss and profit range to prevent being stopped out if it is too close.
### Optimization direction
- Optimize Bollinger Band length parameters to find the best breakthrough effect
- Optimize ADX filtering conditions to balance trend judgment and misjudgment rate
- Add other indicators to judge the amount of support to avoid false breakthroughs
- Optimize the callback stop loss range to prevent being too sensitive and being stopped.
- Optimize the tracking take-profit range and appropriately widen the distance
### Summarize
The overall idea of ​​this strategy is clear and concise. It uses Bollinger Bands to determine clear long and short breakthrough signals, and uses the ADX indicator to filter the Choppy market without a clear trend, thereby locking in trend opportunities. At the same time, set callback stop loss and trailing take profit to control risks and lock in profits. This strategy is easy to understand and implement, deserves further testing and optimization, and can become a basic trend following strategy.
||


## Overview

This strategy uses Bollinger Bands to identify breakout points for long and short trades, combined with ADX indicator to filter low volatility unfavorable market conditions, in order to follow trends.

## Strategy Logic

The strategy is mainly based on Bollinger Bands indicator to determine long or short direction. The middle band of Bollinger Bands is N-day moving average of closing price, and the band width is calculated using standard deviation. A breakout below the lower band signals long trades, while a breakout above the upper band signals short trades.

To avoid invalid breakouts and erroneous trades in non-trending choppy markets, the strategy incorporates ADX indicator to filter low volatility market conditions. Trading signals are only generated when ADX value is below a threshold. When ADX goes above the threshold, all positions are closed to wait for trending conditions.

The strategy also sets trailing stop loss and take profit for open trades. Specifically, after opening a position, the lowest price and highest price of previous N days are recorded as the stop loss and take profit levels for that direction. This allows locking in profits while reducing losses from reversals.

From the code logic, the strategy first calculates Bollinger Bands and ADX parameters. Then it checks if price breaks Bands upper or lower band, and if ADX is below threshold, to generate trading signals. Afterwards the stop loss and take profit levels are dynamically updated and tracked based on current position direction.

## Advantage Analysis

- Bollinger Bands offer clear breakout signals to catch trend opportunities
- ADX filter avoids trading Choppy markets without clear trends 
- Stop loss effectively controls single trade loss
- Trailing take profit locks in most profits

## Risk Analysis

- Breakouts may be false without considering volume
- ADX filter may also miss trending opportunities 
- Stop loss and take profit too close may get stopped out
- Poor parameter tuning impacts strategy performance

Consider combining with other indicators to confirm breakout with volume; optimize ADX filter using slope to identify trend changes; widen stop loss and take profit range to avoid premature exit.

## Improvement Directions

- Optimize Bollinger Bands length for best breakout results
- Fine tune ADX filter to balance trend accuracy and false signals
- Add other indicators to confirm breakout validity  
- Optimize stop loss range to avoid excessive sensitivity
- Widen take profit range to lock in more profits

## Conclusion

The strategy has a clear and simple logic, using Bollinger Bands for obvious breakout signals, filtered by ADX for trending conditions, to capture trend opportunities. Stop loss and take profit are used to control risk and lock in profits. Easy to understand and implement, the strategy is worth further testing and optimization as a basic trend following system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Reverse Trades|
|v_input_2|true|ADX Close|
|v_input_3|false|Use Swing Lo/Hi Stop Loss & Take Profit|
|v_input_4|20|Swing Lo/Hi Lookback|
|v_input_5|false|SL Expander|
|v_input_6|false|TP Expander|
|v_input_7|14|ADX Smoothing|
|v_input_8|20|DI Length|
|v_input_9|30|adxlevel|
|v_input_10|false|-----------BB Inputs-----------|
|v_input_11|20|length|
|v_input_12|2|mult|
|v_input_13|9|MAlen|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-26 00:00:00
end: 2023-11-02 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © tweakerID

// This strategy uses Bollinger Bands to buy when the price 
// crosses over the lower band and sell when it crosses down
// the upper band. It only takes trades when the ADX is 
// below a certain level, and exits all trades when it's above it.

//@version=4
strategy("BB + ADX Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_value = 0.04, initial_capital=100)

//Inputs
i_reverse=input(false, title="Reverse Trades")
i_ADXClose=input(true, title="ADX Close")
i_SL=input(false, title="Use Swing Lo/Hi Stop Loss & Take Profit")
i_SwingLookback=input(20, title="Swing Lo/Hi Lookback")
i_SLExpander=input(defval=0, step=.5, title="SL Expander")
i_TPExpander=input(defval=0, step=.5, title="TP Expander")

//ADX Calculations
adxlen = input(14, title="ADX Smoothing")
dilen = input(20, title="DI Length")
dirmov(len) =>
	up = change(high)
	down = -change(low)
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
adxlevel=input(30, step=5)

//BB Calculations
BBCALC=input(false, title="-----------BB Inputs-----------")

length = input(20, minval=1)
mult = input(2.0, minval=0.001, maxval=50)
MAlen=input(defval=9)
source = close
basis = sma(source, length)
dev = mult * stdev(source, length)
upper = basis + dev
lower = basis - dev

//Entry Logic
BUY = crossover(source, lower) and sig < adxlevel
SELL = crossunder(source, upper) and sig < adxlevel

//SL & TP Calculations
SwingLow=lowest(i_SwingLookback)
SwingHigh=highest(i_SwingLookback)
bought=strategy.position_size != strategy.position_size[1]
LSL=valuewhen(bought, SwingLow, 0)-((valuewhen(bought, atr(14), 0))*i_SLExpander)
SSL=valuewhen(bought, SwingHigh, 0)+((valuewhen(bought, atr(14), 0))*i_SLExpander)
lTP=strategy.position_avg_price + (strategy.position_avg_price-(valuewhen(bought, SwingLow, 0))+((valuewhen(bought, atr(14), 0))*i_TPExpander))
sTP=strategy.position_avg_price - (valuewhen(bought, SwingHigh, 0)-strategy.position_avg_price)-((valuewhen(bought, atr(14), 0))*i_TPExpander)
islong=strategy.position_size > 0
isshort=strategy.position_size < 0
SL= islong ? LSL : isshort ? SSL : na
TP= islong ? lTP : isshort ? sTP : na

//Entries
strategy.entry("long", long=i_reverse?false:true, when=BUY)
strategy.entry("short", long=i_reverse?true:false, when=SELL)

//EXITS
if i_ADXClose
    strategy.close_all(when=sig > adxlevel)
if i_SL
    strategy.exit("longexit", "long", stop=SL, limit=TP)
    strategy.exit("shortexit", "short", stop=SL, limit=TP)

//Plots	
plot(i_SL ? SL : na, color=color.red, style=plot.style_cross, title="SL")
plot(i_SL ? TP : na, color=color.green, style=plot.style_cross, title="TP")
plot(upper)
plot(lower)



```

> Detail

https://www.fmz.com/strategy/431010

> Last Modified

2023-11-03 17:16:02

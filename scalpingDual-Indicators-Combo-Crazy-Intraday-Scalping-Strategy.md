
> Name

Dual-Indicators-Combo-Crazy-Intraday-Scalping-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/00bf5e3162909e757024f8ec72694d9c0515dc46bff2c931e734d6a0b1ed918f.png)

[trans]

## Overview
This strategy combines the buying and selling signals of the TMO and AMA indicators developed by LuxAlgo to capture the opportunity for the start of the trend during the shock consolidation. It will go long and short after meeting multiple conditions such as the TMO indicator buying and selling signal, the AMA indicator buying and selling extreme value, and the K-line physical volume gradually amplifying. The stop loss method is the highest and lowest price of the recent N K lines.
## Strategy Principle
The TMO indicator reflects price momentum. It is a type of oscillator that can send trading signals when prices diverge. The AMA indicator is a smoothed moving average indicator. It shows a range of price fluctuations. When the price is close to the upper and lower rails, it indicates overbought and oversold conditions.
The main logic behind this strategy is: the TMO indicator can reflect the divergence of the price trend and provide trading signals, the AMA indicator can show the area where the price may reverse, and at the same time, it can be combined with the amplification of the K-line physical volume to confirm the start of the trend. Therefore their combination can improve the success rate of transactions. Specifically, the strategy will open a long or short position under the following conditions:
1. The TMO indicator shows a long signal, that is, the price deviates upward AND the AMA indicator shows a long maximum value
2. The TMO indicator shows a short selling signal, that is, the price deviates downwards AND the AMA indicator shows a short selling minimum value
3. At the same time, the physical volume of the recent three K lines is required to become larger and larger.
This way it solves the problem of false signals caused by a single indicator. The stop loss method selects the highest price and the lowest price within the recent N K lines, which can better control risks.
## Strategic Advantages
This strategy has several advantages:
1. Indicator combination to improve signal accuracy. The TMO indicator and the AMA indicator verify each other, which can reduce false signals and thereby improve signal accuracy.
2. Combining multiple conditions to capture the beginning of the trend. The multiple conditions set by the strategy, such as TMO indicator signal, AMA indicator extreme value and K-line physical volume amplification, can effectively capture the timing of the start of the trend. This is the goal pursued by the Scalping strategy.
3. K-line stop loss method to control risks. Using the latest highest and lowest price of the K line as the stop loss method can better control the risk of each order. At the same time, there is no risk of lagging reversal caused by indicator recalculation.
4. Simple and effective transaction logic. This strategy uses only two indicators to implement a relatively complete Scalping strategy. It is not complicated and has simple and clear logic. And judging from the example results, the strategy has achieved good profits.
## Strategy Risk
This strategy mainly involves the following risks:
1. Frequent entry and exit risks. As a Scalping strategy, its position holding time is not long. If the transaction fees are high, it will have a certain impact on profits.
2. Risk of too aggressive K-line stop loss. Using the latest highest price and lowest price as the stop loss method may be too aggressive and cannot completely filter out market noise, which increases the probability of the stop loss being triggered.
3. Difficulties and risks in parameter optimization. Strategies involve multiple parameters, and it may be difficult to find the best combination of parameters.
## Optimization direction
This strategy can also be optimized from the following directions:
1. Adding more filtering indicators, such as market trading volume, can filter out some false signals and further improve signal quality.
2. Try to add filtering conditions to the stop loss method to avoid too aggressive stop loss. For example, wait for confirmation on several K lines before triggering the stop loss, and then stop the loss.
3. Carry out parameter optimization and find the best combination of indicator parameters. This may filter out more noise and improve the strategy's winning rate. Mainly optimize parameters such as TMO indicator length, AMA indicator length and multiples.
4. Try to conduct backtesting and real trading on different varieties and time periods to find the trading variety and period that best match the logic of the strategy.
## Summarize
This strategy combines the trading signals of the TMO indicator and the AMA indicator to find the opportunity for the trend to start in the volatile market for scaling. It has the advantages of high signal accuracy, catching trends early and controlling risks. After further optimization of parameters and rules, this strategy can become an intraday Scalping strategy with strong practical value.
||

## Overview

This strategy combines the buy and sell signals from LuxAlgo's TMO and AMA indicators to catch the beginning of a trend during range-bound consolidation. It goes long or short when the conditions of TMO signal, AMA extremities, and increasing candle body size are met. The stop loss is set at the latest swing high/low based on recent bars.  

## Strategy Logic

The TMO indicator reflects price momentum. It belongs to the oscillator indicator type and can generate trading signals when divergence occurs. The AMA indicator is a smoothed moving average. It shows a range of price fluctuations, indicating overbought/oversold conditions when price approaches the upper/lower band.

The main logic behind this strategy is: TMO can detect trend divergence to generate trading signals. AMA can identify price reversal zones. Together with the confirmation from increasing candle body size, they can improve the accuracy of capturing trend start. So the strategy will go long/short when:

1. TMO gives buy signal, i.e. bullish divergence AND AMA shows its max extremity  
2. TMO gives sell signal. i.e. bearish divergence AND AMA shows its min extremity
3. Also requires the most recent 3 candle's body to expand in size

This solves the false signal problem of single indicators. The stop loss based on recent bars' highest high/lowest low can control risk effectively.


## Advantages

The advantages of this strategy include:

1. Indicator combo improves signal accuracy. TMO and AMA validate each other to reduce false signals and improve accuracy.  

2. Multiple conditions capture trend start. The combo of TMO signal, AMA extremities and increasing candle size allows the strategy to effectively identify trend initiation, which scalping strategies pursue.

3. Candle-based stop loss manages risk. By using recent bars' highest/lowest price as stop loss, it controls the risk of each trade while avoiding the lagging risk from indicator recalculation.  

4. Concise and effective logic. With just two indicators, the strategy has implemented a complete scalping system with clear and simple logic. The backtest results also look profitable.


## Risks

The main risks of the strategy:

1. Frequent in-out trades risk. As a scalping strategy targeting short holding period, high trading cost can affect its profitability.

2. Aggressive stop loss risk. By using the recent extreme prices for stop loss, it may be vulnerable to market noise and increase the chance of stop loss trigger. 

3. Difficult parameter optimization risk. The strategy involves multiple parameters. Finding the optimal parameter combination can be challenging.


## Optimization

The strategy can be further optimized in the following areas:

1. Add more filter indicators like volume to remove false signals and further improve signal quality.  

2. Test modifications on stop loss rules to make it less aggressive, e.g. add confirmation bars before triggering stop loss.

3. Conduct parameter optimization to find the best parameter combination for the indicators, which may help filter out more noise and increase win rate. Mainly optimize TMO Length, AMA Length and Multiplier.  

4. Backtest and trade it live across different products and timeframes to find out the best fitting market condition for this strategy logic.


## Conclusion

This strategy combines the trading signals from TMO and AMA to scalp in range-bound markets by capturing early trend moves. It has the advantages of high signal accuracy, early trend capture and effective risk control. Further optimizations on parameters and strategy rules can make it a highly practical intraday scalping strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_float_1|2|Factor|
|v_input_1|true|As Smoothed Candles|
|v_input_2|true|Show Alternating Extremities|
|v_input_int_1|7|(?TMO Settings)TMO Length|
|v_input_source_1_close|0|TMO Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_source_2_close|0|(?AMA Settings)AMA Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_2|50|AMA Length|
|v_input_float_2|true|(?AMA Kernel Parameters)Lag|
|v_input_float_3|0.5|Overshoot|
|v_input_int_3|10|(?Stop Loss Settings)SL Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-23 00:00:00
end: 2023-11-30 00:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Kaspricci

//@version=5
strategy("TradeIQ - Crazy Scalping Trading Strategy [Kaspricci]", overlay=true, initial_capital = 1000, currency = currency.USD)

headlineTMO = "TMO Settings"

tmoLength   = input.int(7, "TMO Length", minval = 1, group = headlineTMO)
tmoSource   = input.source(close, "TMO Source", group = headlineTMO)

// calculate values
osc         = ta.mom(ta.sma(ta.sma(tmoSource, tmoLength), tmoLength), tmoLength)

// determine color of historgram
oscColor    = osc > osc[1] and osc > 0 ? #00c42b : osc < osc[1] and osc > 0 ? #4ee567 : osc < osc[1] and osc < 0 ? #ff441f : osc > osc[1] and osc < 0 ? #c03920 : na

// plot histogram
//plot(osc, "OSC", oscColor, linewidth = 3, style = plot.style_histogram)

// conditon to find highs and lows
up          = ta.highest(tmoSource, tmoLength)
dn          = ta.lowest(tmoSource, tmoLength)

// define conditions to be used for finding divergence
phosc = ta.crossunder(ta.change(osc), 0)
plosc = ta.crossover (ta.change(osc), 0)

// test for divergence
bear = osc > 0 and phosc and ta.valuewhen(phosc,osc,0) < ta.valuewhen(phosc,osc,1) and ta.valuewhen(phosc,up,0) > ta.valuewhen(phosc,up,1) ? 1 : 0
bull = osc < 0 and plosc and ta.valuewhen(plosc,osc,0) > ta.valuewhen(plosc,osc,1) and ta.valuewhen(plosc,dn,0) < ta.valuewhen(plosc,dn,1) ? 1 : 0

// -------------------------------------------------------------------------------------------------------------

headlineAMA = "AMA Settings"

amaSource   = input.source(defval = close, title = "AMA Source", group = headlineAMA)
amaLength   = input.int(defval = 50, title = "AMA Length", minval = 2, group = headlineAMA)


amaMulti    = input.float(defval = 2.0, title = "Factor", minval = 1)

amaShowCd   = input(defval = true , title = "As Smoothed Candles")
amaShowEx   = input(defval = true,   title = "Show Alternating Extremities")

amaAlpha    = input.float(1.0, "Lag",       minval=0, step=.1, tooltip='Control the lag of the moving average (higher = more lag)', group= 'AMA Kernel Parameters')
amaBeta     = input.float(0.5, "Overshoot", minval=0, step=.1, tooltip='Control the overshoot amplitude of the moving average (higher = overshoots with an higher amplitude)', group='AMA Kernel Parameters')

// -------------------------------------------------------------------------------------------------------------

headlineSL = "Stop Loss Settings"

slLength    = input.int(defval = 10, title = "SL Period", minval = 1, group = headlineSL, tooltip = "Number of bars for swing high / low")

// -------------------------------------------------------------------------------------------------------------

var b       = array.new_float(0)
var float x = na

if barstate.isfirst
    for i = 0 to amaLength - 1
        x := i / (amaLength - 1)
        w = math.sin(2 * 3.14159 * math.pow(x, amaAlpha)) * (1 - math.pow(x, amaBeta))
        array.push(b, w)

// local function to filter the source
filter(series float x) =>
    sum = 0.

    for i = 0 to amaLength - 1
        sum := sum + x[i] * array.get(b,i)
    
    sum / array.sum(b)

// apply filter function on source series

srcFiltered = filter(amaSource)

deviation   = ta.sma(math.abs(amaSource - srcFiltered), amaLength) * amaMulti

upper       = srcFiltered + deviation
lower       = srcFiltered - deviation

//----
crossHigh   = ta.cross(high, upper)
crossLow    = ta.cross(low, lower)

var os      = 0
os          := crossHigh ? 1 : crossLow ? 0 : os[1]

ext         = os * upper + (1 - os) * lower

//----
os_css = ta.rsi(srcFiltered, amaLength) / 100

extColor    = os == 1 ? #30FF85 : #ff1100

plot(srcFiltered, "MA", amaShowCd ? na : color.black, 2, editable = false)
plot(amaShowEx ? ext : na, "Extremities", ta.change(os) ? na : extColor, 2, editable=false)

// handle smoothed candles
var float h = na
var float l = na
var float c = na
var float body = na

if amaShowCd
    h := filter(high)
    l := filter(low)
    c := filter(amaSource)
    body := math.abs(math.avg(c[1], c[2]) - c)

ohlc_os = ta.rsi(c, amaLength) / 100

plotcandle(math.avg(c[1], c[2]), h, l, c, "Smooth Candles", #434651, bordercolor = na, editable = false, display = amaShowCd ? display.all : display.none)

// -------------------------------------------------------------------------------------------------------------

plotshape(bull ? ext : na, "Bullish Circle", shape.circle,    location.absolute, color = #00c42b, size=size.tiny)
plotshape(bear ? ext : na, "Bearish Circle", shape.circle,    location.absolute, color = #ff441f, size=size.tiny)
plotshape(bull ? ext : na, "Bullish Label",  shape.labeldown, location.absolute, color = #00c42b, text="Buy", textcolor=color.white, size=size.tiny)
plotshape(bear ? ext : na, "Bearish Label",  shape.labelup,   location.absolute, color = #ff441f, text="Sell", textcolor=color.white, size=size.tiny)

// -------------------------------------------------------------------------------------------------------------

candleSizeIncreasing = body[2] < body[1] and body[1] < body[0]

longEntryCond   = os == 1 and bull
shortEntryCond  = os == 0 and bear

longEntry       = strategy.opentrades == 0 and candleSizeIncreasing and not candleSizeIncreasing[1] and ta.barssince(longEntryCond)  < ta.barssince(os == 0) and ta.barssince(longEntryCond) < ta.barssince(bear)
shortEntry      = strategy.opentrades == 0 and candleSizeIncreasing and not candleSizeIncreasing[1] and ta.barssince(shortEntryCond) < ta.barssince(os == 1) and ta.barssince(shortEntryCond) < ta.barssince(bull)

longExit        = strategy.opentrades > 0 and strategy.position_size > 0 and (bear or os == 0)
shortExit       = strategy.opentrades > 0 and strategy.position_size < 0 and (bull or os == 1)

recentSwingHigh = ta.highest(high, slLength) // highest high of last candles
recentSwingLow  = ta.lowest(low,   slLength) // lowest low of recent candles

bgcolor(longEntry  ? color.rgb(76, 175, 79, 90) : na)
bgcolor(shortEntry ? color.rgb(255, 82, 82, 90) : na)

slLong          = (close - recentSwingLow) / syminfo.mintick  // stop loss in ticks
slShort         = (recentSwingHigh - close) / syminfo.mintick // stop loss in ticks

newOrderID         = str.tostring(strategy.closedtrades + strategy.opentrades + 1)
curOrderID         = str.tostring(strategy.closedtrades + strategy.opentrades)

alertMessageForEntry = "Trade {0} - New {1} Entry at price: {2} with stop loss at: {3}"

if (longEntry)
    alertMessage = str.format(alertMessageForEntry, newOrderID, "Long", close, recentSwingLow)
    
    strategy.entry(newOrderID, strategy.long, alert_message = alertMessage)
    strategy.exit("Stop Loss Long", newOrderID, loss = slLong, alert_message = "Stop Loss for Trade " + newOrderID)

if(longExit)
    strategy.close(curOrderID, alert_message = "Close Trade " + curOrderID)

if (shortEntry)
    alertMessage = str.format(alertMessageForEntry, newOrderID, "Short", close, recentSwingLow)

    strategy.entry(newOrderID, strategy.short, alert_message = alertMessage)
    strategy.exit("Stop Loss Short", newOrderID, loss = slShort, alert_message = "Stop Loss for Trade " + newOrderID)

if(shortExit)
    strategy.close(curOrderID, alert_message = "Close Trade " + curOrderID)
```

> Detail

https://www.fmz.com/strategy/433922

> Last Modified

2023-12-01 14:47:57


> Name

Trend-Tracking-Strategy-Based-on-Momentum-Breakout
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c485416b0d6677f217.png)

[trans]

## Overview
This strategy comprehensively uses a variety of technical indicators to identify the trend direction, tracks when the trend breaks through momentum, and pursues excess returns.
## Strategy Principle
1. Use the Donchian channel to determine the overall trend direction. When price breaks out of this channel, a trend shift is confirmed.
2. Hull moving average assists in determining the trend direction. This indicator is sensitive to price changes and can detect trend turning points in advance.
3. The half-orbit system sends buy and sell signals. The system is based on price channels and average true ranges to avoid false breakouts.
4. When the Donchian channel, Hull indicator and half-orbit system send signals at the same time, it is judged that the trend has a strong momentum breakthrough, and then enter the market.
5. Conditions for closing positions: When the above indicators send out reverse signals, it is determined that the trend has reversed and stop loss immediately.
## Advantage Analysis
-Multiple indicator combinations provide stronger judgment. Donchian channel determines fundamentals, Hull indicator and half-track determine details to grasp the precise turning point of the trend.
- Participate in momentum breakouts and pursue excess returns. Only enter the market when there is a strong breakthrough in the trend to avoid being caught in the shock.
- Strictly stop losses to ensure the safety of funds. Once the indicator sends a reverse signal, stop the loss immediately to avoid expanding the loss.
- Flexible parameter adjustment to adapt to various markets. Parameters such as channel length and fluctuation range can be adjusted to optimize for different cycles.
- Easy to understand and implement, even novices can master it. The combination of indicators and conditions is simple and clear, and easy to program.
## Risk Analysis
- Miss opportunities in the early stages of a trend. The entry time was late and the initial gains could not be captured.
- Retracement loss on failed breakout. Breakthrough failures and reversals may occur after entry, resulting in losses.
- The indicator sends an error signal. Due to improper parameter settings, errors in indicator judgment may occur.
- The number of transactions is limited. Only enter the market when there is a clear trend breakthrough, and the number of annual transactions is limited.
## Optimization direction
- Optimize parameter combination. Test different parameters to find the best combination.
- Add stop loss linear retracement conditions. Avoid stopping loss too early and missing trend opportunities.
- Add other indicator filters. Such as MACD, KDJ, etc. to assist judgment and reduce false signals.
- Optimize trading time periods. Parameters can be optimized in different time periods.
- Expand capital utilization efficiency. Improve the efficiency of capital use through leverage, fixed investment and other methods.
## Summarize
This strategy combines multiple indicators to determine the timing of a trend momentum breakthrough and achieves excess returns by tracking the established trend. Strict stop-loss mechanism controls risks, and flexible parameter adjustment adapts to different market environments. Although the transaction frequency is low, each transaction strives to achieve high returns. Through parameter optimization, introduction of auxiliary indicators, etc., this strategy can achieve continuous improvement.
|| 

# Overview

This strategy combines multiple technical indicators to identify trend direction and track the momentum when breakout happens, aiming for excess return. 

# Strategy Logic

1. Use Donchian Channel to determine the overall trend. A breakout of the channel confirms trend reversal.

2. Hull Moving Average assists in judging trend direction. It is sensitive to price change and can early detect trend reversal.

3. Halftrend system generates buy and sell signals based on price channel and ATR range. It avoids false breakout.

4. When Donchian, Hull and Halftrend signals align, a strong momentum breakout is confirmed and strategy enters. 

5. Exit when above indicators give reverse signal, indicating trend reversal.

# Advantage Analysis

- More robust signal with multiple indicators. Donchian for fundamentals, Hull and Halftrend for details. Catch trend turning points accurately.

- Pursuit of excess return by momentum breakout. Only enter on strong breakout, avoiding whipsaw in consolidation.

- Strict stop loss to ensure capital safety. Loss is capped once reverse signal shows.

- Flexible parameter tuning for different markets. Channel length, ATR range etc can be adjusted and optimized.

- Easy to understand and implement. Indicator combo is simple and clear, easy to code.

# Risk Analysis

- Miss early trend opportunity. Entry is relatively late, early rally is not captured.

- Loss from failed breakout and reversal. Drawdown may occur after entry.

- False signal from bad parameter. Indicators may fail due to bad tuning.

- Limited trade frequency. Only clear breakouts are traded, resulting in low annual trade numbers.

# Optimization Directions

- Optimize parameter combinations by testing. Find best parameters.

- Add trailing stop loss condition. Avoid premature stop loss. 

- Introduce more filters like MACD, KDJ. To filter bad signals.

- Optimize parameters for different sessions. Different sessions can be tuned separately. 

- Improve capital efficiency via leverage, DCA etc. Better capital utilization.

# Summary

This strategy combines multiple indicators to identify momentum breakout of established trend, and profit from trend tracking. Strict stop loss manages risk. Flexible parameters adapt to different market environments. Although trade frequency is low, each trade targets high profitability. The strategy can be improved continuously through parameter tuning, additional filters etc.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|30|dlen|
|v_input_1_hlc3|0|Source: hlc3|high|low|open|hl2|close|hlcc4|ohlc4|
|v_input_string_1|0|Hull Variation: Hma|Thma|Ehma|
|v_input_2|55|Length|
|v_input_3|true|Length multiplier |
|v_input_4|2|Amplitude|
|v_input_5|2|Channel Deviation|
|v_input_int_2|7|atr_length|
|v_input_int_3|50|atr_rsi_length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-29 00:00:00
end: 2023-11-05 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © kgynofomo

// @version=5
strategy(title="[Salavi] | Andy Super Pro Strategy",overlay = true)

//Doinchian Trend Ribbon
dlen = input.int(defval=30, minval=10)

dchannel(len) =>
    float hh = ta.highest(len)
    float ll = ta.lowest(len)

    int trend = 0
    trend := close > hh[1] ? 1 : close < ll[1] ? -1 : nz(trend[1])
    trend

dchannelalt(len, maintrend) =>
    float hh = ta.highest(len)
    float ll = ta.lowest(len)

    int trend = 0
    trend := close > hh[1] ? 1 : close < ll[1] ? -1 : nz(trend[1])
    maintrend == 1 ? trend == 1 ? #00FF00ff : #00FF009f : maintrend == -1 ? trend == -1 ? #FF0000ff : #FF00009f : na

maintrend = dchannel(dlen)
donchian_bull = maintrend==1
donchian_bear = maintrend==-1


//Hulls
src = input(hlc3, title='Source')
modeSwitch = input.string('Hma', title='Hull Variation', options=['Hma', 'Thma', 'Ehma'])
length = input(55, title='Length')
lengthMult = input(1.0, title='Length multiplier ')

useHtf = false
htf = '240'

switchColor = true
candleCol = false
visualSwitch = true
thicknesSwitch = 1
transpSwitch = 40

//FUNCTIONS
//HMA
HMA(_src, _length) =>
    ta.wma(2 * ta.wma(_src, _length / 2) - ta.wma(_src, _length), math.round(math.sqrt(_length)))
//EHMA    
EHMA(_src, _length) =>
    ta.ema(2 * ta.ema(_src, _length / 2) - ta.ema(_src, _length), math.round(math.sqrt(_length)))
//THMA    
THMA(_src, _length) =>
    ta.wma(ta.wma(_src, _length / 3) * 3 - ta.wma(_src, _length / 2) - ta.wma(_src, _length), _length)

//SWITCH
Mode(modeSwitch, src, len) =>
    modeSwitch == 'Hma' ? HMA(src, len) : modeSwitch == 'Ehma' ? EHMA(src, len) : modeSwitch == 'Thma' ? THMA(src, len / 2) : na

//OUT
_hull = Mode(modeSwitch, src, int(length * lengthMult))
HULL = useHtf ? request.security(syminfo.ticker, htf, _hull) : _hull
MHULL = HULL[0]
SHULL = HULL[2]

//COLOR
hullColor = switchColor ? HULL > HULL[2] ? #00ff00 : #ff0000 : #ff9800
hull_bull = HULL > HULL[2]
bull_start = hull_bull and hull_bull[1]==false
hull_bear = HULL < HULL[2]
bear_start = hull_bear and hull_bear[1]==false

barcolor(color=candleCol ? switchColor ? hullColor : na : na)

//halftrend
amplitude = input(title='Amplitude', defval=2)
channelDeviation = input(title='Channel Deviation', defval=2)
// showArrows = input(title='Show Arrows', defval=true)
// showChannels = input(title='Show Channels', defval=true)

var int trend = 0
var int nextTrend = 0
var float maxLowPrice = nz(low[1], low)
var float minHighPrice = nz(high[1], high)

var float up = 0.0
var float down = 0.0
float atrHigh = 0.0
float atrLow = 0.0
float arrowUp = na
float arrowDown = na

atr2 = ta.atr(100) / 2
dev = channelDeviation * atr2

highPrice = high[math.abs(ta.highestbars(amplitude))]
lowPrice = low[math.abs(ta.lowestbars(amplitude))]
highma = ta.sma(high, amplitude)
lowma = ta.sma(low, amplitude)

if nextTrend == 1
    maxLowPrice := math.max(lowPrice, maxLowPrice)

    if highma < maxLowPrice and close < nz(low[1], low)
        trend := 1
        nextTrend := 0
        minHighPrice := highPrice
        minHighPrice
else
    minHighPrice := math.min(highPrice, minHighPrice)

    if lowma > minHighPrice and close > nz(high[1], high)
        trend := 0
        nextTrend := 1
        maxLowPrice := lowPrice
        maxLowPrice

if trend == 0
    if not na(trend[1]) and trend[1] != 0
        up := na(down[1]) ? down : down[1]
        arrowUp := up - atr2
        arrowUp
    else
        up := na(up[1]) ? maxLowPrice : math.max(maxLowPrice, up[1])
        up
    atrHigh := up + dev
    atrLow := up - dev
    atrLow
else
    if not na(trend[1]) and trend[1] != 1
        down := na(up[1]) ? up : up[1]
        arrowDown := down + atr2
        arrowDown
    else
        down := na(down[1]) ? minHighPrice : math.min(minHighPrice, down[1])
        down
    atrHigh := down + dev
    atrLow := down - dev
    atrLow

ht = trend == 0 ? up : down

var color buyColor = color.blue
var color sellColor = color.red

htColor = trend == 0 ? buyColor : sellColor
// htPlot = plot(ht, title='HalfTrend', linewidth=2, color=htColor)

// atrHighPlot = plot(showChannels ? atrHigh : na, title='ATR High', style=plot.style_circles, color=color.new(sellColor, 0))
// atrLowPlot = plot(showChannels ? atrLow : na, title='ATR Low', style=plot.style_circles, color=color.new(buyColor, 0))

// fill(htPlot, atrHighPlot, title='ATR High Ribbon', color=color.new(sellColor, 90))
// fill(htPlot, atrLowPlot, title='ATR Low Ribbon', color=color.new(buyColor, 90))

HalfTrend_buySignal = not na(arrowUp) and trend == 0 and trend[1] == 1
HalfTrend_sellSignal = not na(arrowDown) and trend == 1 and trend[1] == 0

// plotshape(showArrows and buySignal ? atrLow : na, title='Arrow Up', style=shape.triangleup, location=location.absolute, size=size.tiny, color=color.new(buyColor, 0))
// plotshape(showArrows and sellSignal ? atrHigh : na, title='Arrow Down', style=shape.triangledown, location=location.absolute, size=size.tiny, color=color.new(sellColor, 0))




//ema
filter_ema = ta.ema(close,200)
ema_bull = close>filter_ema
ema_bear = close<filter_ema

atr_length = input.int(7)
atr = ta.atr(atr_length)
atr_rsi_length = input.int(50)
atr_rsi = ta.rsi(atr,atr_rsi_length)
atr_valid = atr_rsi>50

longCondition = bull_start and atr_valid
shortCondition = bear_start and atr_valid

Exit_long_condition = shortCondition
Exit_short_condition = longCondition

if longCondition
    strategy.entry("Andy Buy",strategy.long, limit=close,comment="Andy Buy Here")

if Exit_long_condition
    strategy.close("Andy Buy",comment="Andy Buy Out")
    // strategy.entry("Andy fandan Short",strategy.short, limit=close,comment="Andy 翻單 short Here")
    // strategy.close("Andy fandan Buy",comment="Andy short Out")


if shortCondition
    strategy.entry("Andy Short",strategy.short, limit=close,comment="Andy short Here")


// strategy.exit("STR","Long",stop=longstoploss)
if Exit_short_condition
    strategy.close("Andy Short",comment="Andy short Out")
    // strategy.entry("Andy fandan Buy",strategy.long, limit=close,comment="Andy 翻單 Buy Here")
    // strategy.close("Andy fandan Short",comment="Andy Buy Out")




inLongTrade = strategy.position_size > 0
inLongTradecolor = #58D68D
notInTrade = strategy.position_size == 0
inShortTrade = strategy.position_size < 0

// bgcolor(color = inLongTrade?color.rgb(76, 175, 79, 70):inShortTrade?color.rgb(255, 82, 82, 70):na)
plotshape(close!=0,location = location.bottom,color = inLongTrade?color.green:inShortTrade?color.red:na)


plotshape(longCondition, title='Buy', text='Andy Buy', style=shape.labelup, location=location.belowbar, color=color.new(color.green, 0), textcolor=color.new(color.white, 0), size=size.tiny)
plotshape(shortCondition, title='Sell', text='Andy Sell', style=shape.labeldown, location=location.abovebar, color=color.new(color.red, 0), textcolor=color.new(color.white, 0), size=size.tiny)

Fi1 = plot(MHULL, title='MHULL', color=hullColor, linewidth=thicknesSwitch, transp=50)
Fi2 = plot(SHULL, title='SHULL', color=hullColor, linewidth=thicknesSwitch, transp=50)

fill(Fi1, Fi2, title='Band Filler', color=hullColor, transp=transpSwitch)



```

> Detail

https://www.fmz.com/strategy/431212

> Last Modified

2023-11-06 09:56:20

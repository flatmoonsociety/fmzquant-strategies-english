
> Name

Trend-Following-EMA-and-RSI-Strategy Trend-Following-EMA-and-RSI-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy makes full use of the advantages of moving averages and relative strength indicators to realize the identification and tracking of trends. It only requires two indicators to determine the trend and select the time points of entries/exits. This strategy aims to capture medium- and long-term price trends and avoid being misled by short-term market noise.
## Strategy Principle
This strategy uses three EMA moving averages with different periods. EMA-A has the shortest period, EMA-B is the second, and EMA-C is the longest. When the short-period EMA-A crosses above the longer-period EMA-B, it means that the price is in an upward trend, and you can go long; conversely, when EMA-A crosses below the EMA-B, it means that the price has turned into a downward trend, and you can go short. In order to filter out false signals, it also introduces the longest period EMA-C, and only considers entry when the price breaks through EMA-C.
This strategy also incorporates the RSI indicator to locate the exit time point. When holding a long position, if the RSI goes above the 70 line, the position will be closed; when a short position is held, if the RSI goes below the 30 line, the position will be closed. This can lock in trend profits and prevent further losses.
## Advantage Analysis
- Take advantage of EMA to identify trend direction
- RSI indicator assists in determining entry and exit points
- Only 2 indicators are needed, the strategy is simple and easy to implement
- Configurable indicator parameters to freely adjust strategy style
- Can make profits at the beginning, middle and late stages of the trend
## Risk Analysis
- A rebound under a general trend may generate false signals
- It is easy to stop losses in volatile market conditions
- Improper setting of RSI parameters may result in premature stop loss
- You need to be careful when setting the EMA period. If it is too short, you will be sensitive to noise, and if it is too long, you will miss the trend.
These risks can be reduced by optimizing RSI parameters or adding additional filtering conditions. It can also be combined with technical analysis methods such as trends, support and resistance to improve strategic performance.
## Optimization direction
- Optimize RSI parameters and balance take profit and stop loss
- Test different EMA period combinations
- Confirmation of increased volume or other indicators
- The stop loss method can set the stop loss range according to ATR
- You can try to reduce your position in the middle of the trend
- Optimize entry opportunities, such as breaking the previous high/low point, or absorbing energy
- Consider adding a re-entry mechanism
## Summarize
This strategy integrates trend tracking and overbought and oversold indicators, and only needs two simple indicators to judge and capture the trend. Through parameter optimization and rule optimization, the effect can be greatly improved while keeping it simple. It is a very practical trend following strategy template suitable for medium and long-term investors.
||

## Overview

This strategy takes full advantage of moving averages and relative strength index to identify and follow trends. It only needs two indicators to determine the trend and find proper entry/exit timing. The strategy aims to capture medium-to-long term price trends while avoiding short-term market noise.

## Strategy Logic

The strategy uses three EMAs with different periods, with EMA-A having the shortest period, EMA-B medium, and EMA-C the longest. When the shorter EMA-A crosses above the longer EMA-B, it signals an upward trend, thus going long. Conversely, when EMA-A crosses below EMA-B, it signals a downward trend, thus going short. To filter false signals, it also uses the longest EMA-C - only considering entry after the price breaks EMA-C.

The strategy also uses RSI to locate exit points. When long, it closes the position if RSI crosses above 70. When short, it exits if RSI falls below 30. This locks in trend profits and prevents losses from expanding further.

## Advantage Analysis 

- Utilizes EMA's strength in trend identification
- RSI assists in entry and exit timing
- Simple strategy with only 2 indicators  
- Customizable parameters to adjust strategy style
- Profits from early, mid and late trend stages

## Risk Analysis

- Pullbacks in major trends may generate false signals
- Vulnerable to whipsaws in ranging markets
- Improper RSI parameters may cause premature exits 
- EMA periods need careful selection, too short may be noise sensitive, too long may miss trends

These risks can be reduced by optimizing RSI parameters, adding filters, and combining with trend analysis. 

## Optimization Directions

- Optimize RSI parameters for better profit taking and risk control
- Test different EMA period combinations
- Add volume or other confirmation indicators  
- Use ATR for stop loss sizing  
- Consider reducing position size mid-trend
- Optimize entry timing with breakouts, volume, etc
- Explore re-entry mechanisms

## Summary

This strategy combines trend following and oscillator indicators for trend identification and capturing. With simple parameter and logic optimization, it can be greatly improved while keeping simplicity. It is a very practical trend following template suitable for medium-to-long term investors.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_5|24|# bars|
|v_input_int_1|14|(?RSI)Length|
|v_input_source_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_2|10|(?Moving Averages)EMA A Length|
|v_input_int_3|20|EMA B Length|
|v_input_int_4|100|EMA C Length|
|v_input_bool_1|true|(?Strategy)Long entries|
|v_input_bool_2|false|Short entries|
|v_input_bool_3|true|Close after X # bars|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-26 00:00:00
end: 2023-09-25 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
//@author Alorse

//@version=5
// strategy(title='Tendency EMA + RSI [Alorse]', shorttitle='Tendece EMA + RSI [Alorse]', overlay=true, pyramiding=0, currency=currency.USD, default_qty_type=strategy.percent_of_equity, initial_capital=1000, default_qty_value=20, commission_type=strategy.commission.percent, commission_value=0.01)

// Bollinger Bands
len = input.int(14, minval=1, title='Length', group='RSI')
src = input.source(close, 'Source', group='RSI')
rsi = ta.rsi(src, len)

// Moving Averages
len_a = input.int(10, minval=1, title='EMA A Length', group='Moving Averages')
out_a = ta.ema(close, len_a)
plot(out_a, title='EMA A', color=color.purple)

len_b = input.int(20, minval=1, title='EMA B Length', group='Moving Averages')
out_b = ta.ema(close, len_b)
plot(out_b, title='EMA B', color=color.orange)

len_c = input.int(100, minval=1, title='EMA C Length', group='Moving Averages')
out_c = ta.ema(close, len_c)
plot(out_c, title='EMA B', color=color.green)

// Strategy Conditions
stratGroup = 'Strategy'
showLong = input.bool(true, title='Long entries', group=stratGroup)
showShort = input.bool(false, title='Short entries', group=stratGroup)
closeAfterXBars = input.bool(true, title='Close after X # bars', tooltip='If trade is in profit', group=stratGroup)
xBars = input.int(24, title='# bars')

entryLong = ta.crossover(out_a, out_b) and out_a > out_c and close > open
exitLong = rsi > 70

entryShort = ta.crossunder(out_a, out_b) and out_a < out_c and close < open
exitShort = rsi < 30


bought = strategy.opentrades[0] == 1 and strategy.position_size[0] > strategy.position_size[1]
entry_price = ta.valuewhen(bought, open, 0)
var int nPastBars = 0
if strategy.position_size > 0
    nPastBars := nPastBars + 1
    nPastBars
if strategy.position_size == 0
    nPastBars := 0
    nPastBars
if closeAfterXBars
    exitLong := nPastBars >= xBars and close > entry_price ? true : exitLong
    exitLong
    exitShort := nPastBars >= xBars and close < entry_price ? true : exitShort
    exitShort

// Long Entry
strategy.entry('Long', strategy.long, when=entryLong and showLong)
strategy.close('Long', when=exitLong)

// Short Entry
strategy.entry('Short', strategy.short, when=entryShort and showShort)
strategy.close('Short', when=exitShort)


```

> Detail

https://www.fmz.com/strategy/427881

> Last Modified

2023-09-26 15:39:48

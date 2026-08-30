
> Name

Hull-Filter-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/564b71a3d7405d48bef71c8ad78779d211bb58a18fab9221bad2ec18c14672ab.png)
[trans]

## Overview
This strategy uses two Hall moving averages, short-term and long-term, for the generation and filtering of trading signals. The short-term Hall moving average is used to generate signals, while the long-term Hall moving average is used to filter signals. Only when the short-term Hall moving average and the long-term Hall moving average change in the same direction will a trading signal be generated.
This strategy uses both the ATR indicator to set stop loss and take profit levels. Each time a position is opened, the stop loss and take profit levels of the current position will be dynamically set based on the value of ATR.
## Strategy Principle
The short-term Hall Moving Average is used to capture short-term trends and turning points in prices. When the direction of the short-term Hall Moving Average changes, it indicates that the short-term trend of prices has changed.
The long-term Hall Moving Average is used to determine the overall direction of prices. For example, when the direction of the long-term Hall Moving Average is upward, it indicates that prices are in an overall upward trend.
A trading signal will only be generated when the short-term Hall Moving Average turns and its turning direction is consistent with the overall trend of the long-term Hall Moving Average. In other words, this short-term signal is only traded when the short-term trend of the price changes and the overall trend changes in the same direction. This can effectively filter out false signals caused by short-term market noise.
After opening a position, the stop loss and take profit levels will be set based on the size of the ATR indicator. The ATR indicator can reflect the volatility and risk level of the market. The stop loss position will be placed below the price low point, while the take profit position will be placed above the price high point, and both will be linked to the ATR value. The range of stop loss and take profit will be adjusted according to the degree of market volatility.
## Advantage Analysis
This strategy combines short-term signals and long-term filtering, which can effectively identify mid-term price trends and capture turning points in a timely manner. Compared with a single moving average and other indicators, it can reduce the possibility of being deceived by market noise.
By dynamically adjusting the stop-loss and take-profit positions, you can set reasonable stop-loss and take-profit positions according to the degree of market fluctuations, ensuring profits while avoiding being too aggressive and reducing the risk of losses.
With the advantages of Hall moving average, price trends can be judged more flexibly and accurately, and it has stronger tracking performance than ordinary moving averages.
## Risk Analysis
This strategy relies on the intersection of two Hall moving averages, short-term and long-term, as a signal. If a false crossover occurs between the two moving averages, it may cause a wrong entry. At this time, you need to decide whether to filter the signal based on the long- and short-term market structure.
In a volatile market, the price may fluctuate back and forth within a smaller trading range, which will increase the signal error rate and increase the possibility of unnecessary transactions. At this time, you can avoid unnecessary transactions by expanding the trading signal filter conditions.
The stop-loss and take-profit settings depend on the ATR indicator. If the market fluctuations reflected by the ATR indicator are inaccurate, the stop-loss and take-profit positions will also be invalid. At this time, you can consider combining other volatility indicators to correct the ATR value.
## Optimization direction
You can consider combining other short-term indicators to assist signal judgment, such as overbought and oversold indicators such as RSI, to improve the filtering effect.
The filtering logic relationship between long and short-term Hall moving averages can be increased or optimized to make the filtering rules more stringent and avoid false signals.
The impact of different parameter settings on strategy stability and profitability can be studied. For example, different combinations of moving average parameters, ATR parameters, etc. can produce different trading performance.
## Summarize
This strategy comprehensively utilizes the short-term Hall moving average to capture signals, the long-term Hall moving average to filter signals, and the ATR indicator to set stop loss and profit, forming a relatively complete medium-term trend tracking strategy system. This strategy can effectively discover mid-term price turning points and avoid being disturbed by short-term market noise. It is an important stock selection tool for establishing a trend trading system. Through parameter optimization and the addition of auxiliary conditions, this strategy can further enhance the accuracy of signal judgment, thereby achieving better performance.
||

## Overview  

This strategy uses short-term and long-term Hull moving averages to generate and filter trading signals. The short-term Hull moving average is used to generate signals, while the long-term Hull moving average is used for filtering signals. Trades are only taken when the short-term Hull moving average changes direction and the long-term Hull moving average is moving in the same overall direction.

The strategy also uses the ATR indicator to dynamically set stop loss and take profit levels when entering trades.

## Strategy Logic

The short-term Hull moving average captures short-term price trends and turning points. When it changes direction, it signals a shift in the short-term price trend.  

The long-term Hull moving average determines the overall price trend. For example, when it is rising, prices are in an overall upward trend.

Trades are only taken when the short-term Hull moving average turns direction, and its new direction aligns with the direction of the long-term Hull moving average. This filters out signals that go against the overall trend and may just be short-term market noise.

After entering positions, stop loss and take profit levels are set based on the ATR indicator value. The ATR reflects market volatility and risk levels. The stop loss is placed below price lows while take profit targets price highs, with ranges tied to the current ATR reading.

## Advantage Analysis

Combining short-term signals and long-term filters effectively identifies mid-term trends and turning points, avoiding false signals from market noise.

Dynamic stop loss and take profit based on ATR sets reasonable ranges based on current volatility, balancing profit taking and loss prevention.

The Hull moving average has flexibility and accuracy advantages over standard moving averages, with better trend tracking. 

## Risk Analysis

The strategy relies on crosses between the Hull moving averages to generate signals. False crosses can result in bad trades, requiring analysis of overall market structure.  

In ranging, choppy markets with price oscillating in a trading range, signal errors and unnecessary trades may pile up. This can be avoided by filtering signals with wider conditions during such markets.

Stop loss and take profit reliance on ATR means inaccurate volatility reads will result in bad placement. Other volatility measures can augment ATR to correct this.

## Optimization  

Additional short-term indicators like RSI can improve signal accuracy through convergence.

The filter logic between the Hull moving averages can be enhanced to have more strict entry requirements, avoiding false signals.

Parameter tuning research can uncover stability and profitability improvements from changes to moving average lengths, ATR periods, etc.  

## Summary

This strategy combines short-term signal generation, long-term signal filtering, and ATR-based stop loss/take profit in a robust mid-term trend following framework. It capably identifies mid-term inflection points while filtering out short-term noise. With parametric optimizations and added filters, it can achieve even better performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|50|Period of signal HMA|
|v_input_3|200|Period of filter HMA|
|v_input_4|0|Strategy Direction: all|short|long|
|v_input_5|2|Stop Loss Factor|
|v_input_6|3|Take Profit Factor|
|v_input_7|14|ATR Period (SL/TP)|
|v_input_8|2010|Backtest Start Year|
|v_input_9|true|Backtest Start Month|
|v_input_10|true|Backtest Start Day|
|v_input_11|2030|Backtest Stop Year|
|v_input_12|12|Backtest Stop Month|
|v_input_13|31|Backtest Stop Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-04 00:00:00
end: 2024-01-03 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Hull Filtered Strategy", overlay=true, pyramiding=0, default_qty_type= strategy.percent_of_equity, default_qty_value = 10, calc_on_order_fills=false, slippage=0,commission_type=strategy.commission.percent,commission_value=0)

// Parameters for Hull Moving Averages
src = input(close, title="Source")
signal_period = input(50, title="Period of signal HMA")
filter_period = input(200, title="Period of filter HMA")

strat_dir_input = input(title="Strategy Direction", defval="all", options=["long", "short", "all"])

// Set allowed trading directions
strat_dir_value = strat_dir_input == "long" ? strategy.direction.long : strat_dir_input == "short" ? strategy.direction.short : strategy.direction.all
strategy.risk.allow_entry_in(strat_dir_value)

// stop loss and take profit
sl_factor = input(2,title="Stop Loss Factor")
tp_factor = input(3,title="Take Profit Factor")
atr_period = input(14, title="ATR Period (SL/TP)")

// Testing Start dates
testStartYear = input(2010, "Backtest Start Year")
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)

//Stop date if you want to use a specific range of dates
testStopYear = input(2030, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay,0,0)


// -----------------------------------------------------------------------------
// Global variables
// -----------------------------------------------------------------------------
var float tp = na
var float sl = na
var float position = na


// -----------------------------------------------------------------------------
// Functions
// -----------------------------------------------------------------------------
testWindow() =>
    time >= testPeriodStart and time <= testPeriodStop ? true : false


// -----------------------------------------------------------------------------
// The engine
// -----------------------------------------------------------------------------
hma_signal = hma(src, signal_period)
hma_filter = hma(src, filter_period)

// Used to determine exits and stop losses
atr_e = atr(atr_period)

// if hma_filter increases hma_trend is set to 1, if it decreases hma_trend is set to -1. If no trend is available, hma_trend is set to ß0
trend = hma_filter > hma_filter[1]  ?  1 : hma_filter < hma_filter[1] ? -1 : 0
signal = hma_signal > hma_signal[1] ? 1 : hma_signal  < hma_signal[1] ? -1 : 0


// -----------------------------------------------------------------------------
// signals
// -----------------------------------------------------------------------------
if signal[0] == 1 and signal[1] != 1 and trend == 1 and testWindow()
    sl := close - sl_factor*atr_e
    tp := close + tp_factor*atr_e
    strategy.entry("HMA_LNG", strategy.long)
    strategy.exit("LE", "HMA_LNG", profit=100*tp_factor*atr_e, loss=100*sl_factor*atr_e)
    
if signal[0] == -1 and signal[1] != -1 and trend == -1 and testWindow()
    sl := close + sl_factor*atr_e
    tp := close - tp_factor*atr_e
    strategy.entry("HMA_SHRT", strategy.short)
    strategy.exit("SE", "HMA_SHRT", profit=100*tp_factor*atr_e, loss=100*sl_factor*atr_e)


if strategy.position_size != 0
    sl := sl[1]
    tp := tp[1]

// -----------------------------------------------------------------------------
// PLOT
// -----------------------------------------------------------------------------
hma_s = plot(hma_signal, title="SIGNAL", color = signal == 1 ? color.green : color.red)
hma_l = plot(hma_filter, title="TREND", color = trend == 1 ? color.green : color.red)

plot(tp, title="TAKE PROFIT", color= strategy.position_size != 0 ? color.blue: na, linewidth=1)  
plot(sl, title="STOP LOSS", color= strategy.position_size != 0 ? color.red: na, linewidth = 1)

```

> Detail

https://www.fmz.com/strategy/437645

> Last Modified

2024-01-04 15:16:34

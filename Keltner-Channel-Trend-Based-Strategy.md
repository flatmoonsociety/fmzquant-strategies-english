
> Name

Keltner-Channel-Trend-Based-Strategy
> Author

ChaoZhang

> Strategy Description


![IMG](https://www.fmz.com/upload/asset/17870dae249cc312de0.png)
[trans]

## Overview
The strategy is based on three main indicators: trend indicator, Keltner Channel and DM indicator.
Trend indicators consist of SMA and EMA. When the EMA crosses the SMA, a trend is confirmed. The Keltner Channel is used to determine the opening and closing prices of Candle. The DM indicator is used to determine the long and short direction.
You can go long when the following entry conditions are met:
1. EMA crosses above SMA, confirming the upward trend
2. The opening price of the Candle is above the upper edge, and the closing price is inside the channel.
3. DM indicator is greater than the set baseline
The strategy sets two take-profit levels and one stop-loss level. Consider using a trailing stop to get more profits.
## Strategy Principle
### Trend Judgment
Determine the trend direction through the golden cross of EMA and SMA. The EMA parameter is 46 and the SMA parameter is 46. When the EMA crosses the SMA, it indicates that it has entered an uptrend.
### Keltner Channel
The Keltner Channel contains three lines: the middle line, the upper rail, and the lower rail. The middle line is the SMA of the closing price, with a length of 81. The upper and lower rails are a specified multiple of the true amplitude above and below the midline, respectively. Here it is set to 2.5 times the amplitude above and below the midline.
The Keltner Channel is mainly used to determine whether the price is within the channel and whether it is crossing the channel.
### DM indicator
The DM indicator contains three lines: ADX, +DI and -DI. +DI measures the strength of an uptrend, -DI measures the strength of a downtrend. ADX represents the average trend indicator and reflects the strength of the trend.
Here, set the ADX parameter to 10 and the DI parameter to 19. When the +DI line crosses the set baseline (default 27), it indicates a strong upward trend and is suitable for long positions.
## Advantage Analysis
This strategy combines trends, channels and strength indicators to effectively determine price trends and long and short directions. Has the following advantages:
1. The trend judgment is relatively accurate and can avoid counter-trend operations.
2. The Keltner Channel is clearly visible, forming support and pressure levels.
3. DM indicator can measure the power of long and short to ensure the correct direction of long and short.
4. The strategy conditions are strict and can effectively filter out false breakthroughs from highs and lows.
5. Setting stop-profit and stop-loss points will help you seize profit opportunities.
## Risk Analysis
This strategy also has certain risks:
1. The trend may turn, and the EMA may cross the SMA. You should exit in time.
2. In a strong market, the channel may fail and cannot be used as a strict support and pressure level.
3. The DM indicator may send out wrong signals and should be judged based on the price trend.
4. A false breakthrough may trigger entry, but it will soon fall back again, so a reasonable stop loss should be set.
5. Take-profit and stop-loss points need to be continuously optimized to adapt to market changes.
## Optimization direction
It can be further optimized from the following aspects:
1. Adjust parameters and test the effects of different trend judgment methods.
2. Optimize channel parameters to make them closer to the real fluctuation range.
3. Test different DM parameter combinations and select the best parameters.
4. Set different entry conditions, such as filtering based on trading volume.
5. Optimize the stop-profit and stop-loss strategy, such as trying trailing stop-loss to obtain more profits.
6. Test different varieties separately and select the best parameter combination.
## Summarize
This strategy comprehensively uses a variety of indicators to determine the trend direction, support and pressure levels, and long and short forces, which can effectively capture trends and control risks. However, you still need to pay attention to risks and optimize parameters to adapt to market changes. Overall, this strategy has strong practicality.
||


## Overview

This strategy is based on three main indicators: trend indicator, Keltner Channel and DM indicator.  

The trend indicator consists of SMA and EMA. Keltner Channel is used to determine the open and close price of candles. DM indicator is for judging the direction of long and short.

The entry signal is triggered when:

1. EMA crosses over SMA, confirming uptrend
2. Candle opens above the upper band and closes inside the channel  
3. DM indicator is above the benchmark

The strategy has two take profit levels and one stop loss level. Trailing stop can be used for optimizing profits.

## Strategy Principles 

### Trend Identification  

SMA and EMA crossovers are used to determine the trend direction. EMA (46) crossing over SMA (46) indicates an upward trend.

### Keltner Channel

The channel has three lines: middle, upper and lower. The middle line is SMA of close price with length of 81. The upper and lower bands are placed at a multiple of true range above and below the middle line. Here we use 2.5 times of true range.

Keltner Channel shows support and resistance levels. Price movements in relation to the channel are analyzed.

### DM Indicator

DM indicator contains ADX, +DI and -DI. +DI measures uptrend strength while -DI measures downtrend strength. ADX shows the trend strength.

Here ADX (10), DI (19) are used. When +DI crosses above the benchmark (default 27), it signals strong uptrend and good for long entry.

## Advantage Analysis

This strategy combines trend, channel and momentum indicators to effectively determine price actions and long/short direction. The advantages are:

1. Trend identification is relatively accurate to avoid counter trend trades.

2. Keltner Channel shows clear support and resistance levels. 

3. DM indicator measures long/short momentum to ensure direction.

4. Strict entry rules help filter false breakouts. 

5. Take profit and stop loss points allow capturing profits.

## Risk Analysis

There are also some risks to consider:

1. Trend may reverse when EMA crosses below SMA, so exit timely.

2. Channel can fail in strong trends, not strict support/resistance.

3. DM may generate false signals, check price action. 

4. False breakout may trigger entry but quickly fallback, use reasonable stop loss.

5. Take profit and stop loss need continuous optimization to adapt to changing market conditions.

## Optimization Directions

Some ways to further optimize the strategy:

1. Adjust parameters and test different trend identification methods.

2. Optimize channel parameters to better fit true range.

3. Test different DM parameters and find the optimal combination.

4. Add more entry filters like volume.

5. Try trailing stop loss for getting more profits. 

6. Test separately for different products to find best parameter sets.

## Conclusion

The strategy integrates multiple indicators for determining trend, support/resistance and momentum, which allows effectively catching trends and controlling risks. But risks need to be noticed and parameters require optimization as market changes. Overall, this is a strategy with strong practicality.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|46|Period|
|v_input_2|true|useTrueRange|
|v_input_3|81|length|
|v_input_4|2.5|mult|
|v_input_5|19|DI Length|
|v_input_6|27|DMI Benchmark|
|v_input_7|2019|Backtest Start Year|
|v_input_8|true|Backtest Start Month|
|v_input_9|true|Backtest Start Day|
|v_input_10|9999|Backtest Stop Year|
|v_input_11|12|Backtest Stop Month|
|v_input_12|31|Backtest Stop Day|
|v_input_13|4.5|Long Take Profit 1 %|
|v_input_14|15|Long Take Profit 1 Qty|
|v_input_15|20|Long Take Profit 2%|
|v_input_16|100|Long Take Profit 2 Qty|
|v_input_17|4|Long Stop Loss %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-27 00:00:00
end: 2023-11-02 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//Original Idea by: Wunderbit Trading

//@version=4
strategy("Keltner Channel ETH/USDT 1H", overlay=true, initial_capital=1000,pyramiding = 0, currency="USD", default_qty_type=strategy.percent_of_equity, default_qty_value=100,  commission_type=strategy.commission.percent,commission_value=0.07)


/// TREND
ribbon_period = input(46, "Period", step=1)

leadLine1 = ema(close, ribbon_period)
leadLine2 = sma(close, ribbon_period)

// p3 = plot(leadLine1, color= #53b987, title="EMA", transp = 50, linewidth = 1)
// p4 = plot(leadLine2, color= #eb4d5c, title="SMA", transp = 50, linewidth = 1)
// fill(p3, p4, transp = 60, color = leadLine1 > leadLine2 ? #53b987 : #eb4d5c)

//Upward Trend
UT=leadLine2 < leadLine1
DT=leadLine2>leadLine1

///////////////////////////////////////INDICATORS

// KELTNER //
source       = close
useTrueRange = input(true)
length       = input(81, step=1, minval=1)
mult         = input(2.5, step=0.1)

// Calculate Keltner Channel
ma      = sma(source, length)
range   = useTrueRange ? tr : high - low
rangema = sma(range, length)
upper = ma + rangema * mult
lower = ma - rangema * mult

plot(ma, title="Middle", color=color.orange)
p1=plot(upper, title="Upper", color=color.orange)
p2=plot(lower, title="Lower", color=color.orange)
fill(p1,p2)


// DMI INDICATOR //
adxlen = 10 // input(10, title="ADX Smoothing")
dilen = input(19, title="DI Length")
keyLevel = 23// input(23, title="key level for ADX")
dirmov(len) =>
	up = change(high)
	down = -change(low)
	truerange = rma(tr, len)
	plus = fixnan(100 * rma(up > down and up > 0 ? up : 0, len) / truerange)
	minus = fixnan(100 * rma(down > up and down > 0 ? down : 0, len) / truerange)
	[plus, minus]

adx(dilen, adxlen) =>
	[plus, minus] = dirmov(dilen)
	sum = plus + minus
	adx = 100 * rma(abs(plus - minus) / (sum == 0 ? 1 : sum), adxlen)
	[adx, plus, minus]

[sig, up, down] = adx(dilen, adxlen)

benchmark=input(title="DMI Benchmark", defval=27, minval=1,step=1)

// plot(sig, color=color.red, title="ADX")
// plot(up, style=plot.style_histogram, color=color.green, title="+DI")
// plot(down, style=plot.style_histogram, color=color.red, title="-DI")
// plot(keyLevel, color=color.white, title="Key Level")

///////////////////////////////////////////////////////////


////////////////////////////////////////////////////Component Code Start

testStartYear = input(2019, "Backtest Start Year")
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay,0,0)

testStopYear = input(9999, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay,0,0)

testPeriod() => true
///// Component Code Stop //////////////////////////////////////////

//////////////// STRATEGY EXECUTION //////////////////////////

//LONG SET UP
// Take Profit / Stop Loss
long_tp1_inp = input(4.5, title='Long Take Profit 1 %', step=0.1)/100
long_tp1_qty = input(15, title="Long Take Profit 1 Qty", step=1)

long_tp2_inp = input(20, title='Long Take Profit 2%', step=0.1)/100
long_tp2_qty = input(100, title="Long Take Profit 2 Qty", step=1)

long_take_level_1 = strategy.position_avg_price * (1 + long_tp1_inp)
long_take_level_2 = strategy.position_avg_price * (1 + long_tp2_inp)

long_sl_inp = input(4, title='Long Stop Loss %', step=0.1)/100
long_stop_level = strategy.position_avg_price * (1 - long_sl_inp)


// STRATEGY CONDITION
// LONG
entry_long = ((open > lower and open < upper) and close > upper) and up > down and up > benchmark //  and volume[0] > volume[1]
entry_price_long=valuewhen(entry_long,close,0)
SL_long = entry_price_long * (1 - long_sl_inp)
exit_long = (close < lower) or low < SL_long


// STRATEGY EXECUTION
if testPeriod()

    // LONG
    if UT
        strategy.entry(id="Long", long=true, when=entry_long, comment = "INSERT ENTER LONG COMMAND")
    strategy.exit("TP1","Long", qty_percent=long_tp1_qty, limit=long_take_level_1) // PLACE TAKE PROFIT IN WBT BOT SETTINGS 
    strategy.exit("TP2","Long", qty_percent=long_tp2_qty, limit=long_take_level_2) // PLACE TAKE PROFIT IN WBT BOT SETTINGS
    strategy.close(id="Long", when=exit_long, comment= "INSERT EXIT LONG COMMAND")


//PLOT FIXED SLTP LINE
// LONG POSITION
plot(strategy.position_size > 0 ? long_take_level_1 : na, style=plot.style_linebr, color=color.green, linewidth=1, title="1st Long Take Profit")
plot(strategy.position_size > 0 ? long_take_level_2 : na, style=plot.style_linebr, color=color.green, linewidth=1, title="2nd Long Take Profit")
plot(strategy.position_size > 0 ? long_stop_level : na, style=plot.style_linebr, color=color.red, linewidth=1, title="Long Stop Loss")
```

> Detail

https://www.fmz.com/strategy/431005

> Last Modified

2023-11-03 16:59:39

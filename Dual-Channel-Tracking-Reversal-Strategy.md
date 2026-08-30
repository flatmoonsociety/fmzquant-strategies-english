
> Name

Dual-Channel-Tracking-Reversal-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/fc6ef2d2cde331a266.png)
[trans]

## Overview
The Dual Track Reversal Strategy is a reversal trading strategy that combines Bollinger Bands, Keltner Channels and Momentum Indicators. This strategy uses the comprehensive judgment of Bollinger Bands and Keltner Channel to identify the timing when the price enters the compression area; at the same time, it combines the momentum indicator to judge the price reversal signal to form trading entry and exit signals.
## Strategy Principle
1. Calculate the middle track, upper track, and lower track in Bollinger Bands
- The middle rail adopts close SMA
    - The upper and lower rails are the standard deviation of the middle rail plus or minus an adjustable multiple
2. Calculate the middle rail, upper rail, and lower rail in the Keltner channel
- The middle rail adopts close SMA
    - The upper and lower rails are the middle rail plus or minus an adjustable multiple of ATR.
3. Determine whether the Bollinger Bands are inside the Keltner channel
- When the upper Bollinger Bands track is lower than the upper Keltner track and the lower Bollinger Bands track is higher than the lower Keltner track, it is considered to be in compression.
    - On the contrary, non-compressed
4. Calculate the linear regression slope val between close and the midpoint of Bollinger Band and Keltner Channel
- val > 0 means close is rising, val < 0 means close is falling
5. Calculate close’s rate of change ROC and its EMA
- Determine whether the change rate reaches an adjustable threshold
    - If it exceeds the threshold, it is considered to be in trend
6. On compression, go long when val > 0 and the rate of change reaches the threshold
- On the contrary, go short
7. Set stop loss and take profit conditions
## Strategic Advantages
1. Combined with the dual-rail system to determine the reversal time point to improve accuracy
2. Add linear regression and change rate judgment to avoid reversing false signals
3. Adjustable parameter settings are flexible and can be optimized for different varieties.
4. Adopting a stop-loss and stop-profit strategy can effectively control the risk of a single transaction.
5. Sufficient backtest data can verify the effectiveness of the strategy
## Strategic risks and solutions
1. Dual-rail compression does not necessarily produce effective inversion
- Optimized parameters and strict dual-track compression conditions
2. False breakthroughs generate false signals
- Add linear regression judgment to determine the trend direction
3. The stop loss setting is too loose and the single loss is too large
- Optimize stop loss points and strictly control single losses
4. Test cycle Datenichinhalt
- Add more backtest cycles to verify long-term effectiveness
## Strategy optimization direction
1. Optimize parameter settings to adapt to more varieties
2. Add machine learning to determine key points of support and resistance
3. Combine with changes in trading volume to improve the authenticity of breakthroughs
4. Add cross-time analysis to determine the continuity of trends
5. Optimize stop-loss and take-profit strategies to achieve dynamic tracking
## Summarize
The dual-track tracking reversal strategy is generally a reversal strategy that uses indicators such as Bollinger Bands and Keltner Channels. Through parameter optimization, this strategy can be adapted to different varieties and identify the authenticity of breakthroughs to a certain extent. However, reversal trading itself still has certain risks, and it is necessary to further combine machine learning and other technologies to improve the accuracy of judgment, so as to obtain more stable excess returns.
||


## Overview

The Dual Channel Tracking Reversal strategy is a reversal trading strategy that combines Bollinger Bands, Keltner Channels, and momentum indicators. It identifies price compression zones through the synthesis of Bollinger Bands and Keltner Channels, and utilizes momentum indicators to determine reversal signals for entry and exit.

## Strategy Logic

1. Calculate the middle, upper and lower bands for Bollinger Bands

    - Middle band uses SMA of close
    - Upper and lower bands are middle band ± adjustable standard deviation multiple 

2. Calculate the middle, upper and lower bands for Keltner Channels

    - Middle band uses SMA of close
    - Upper and lower bands are middle band ± adjustable ATR multiple

3. Determine if Bollinger Bands are inside Keltner Channels

    - Squeeze on when lower BB > lower KC and upper BB < upper KC 
    - Squeeze off otherwise

4. Calculate the linear regression slope val of close against BB and KC midpoints 

    - val > 0 indicates close is increasing, val < 0 means decreasing

5. Calculate the ROC and EMA of ROC for close

    - Determine if change rate exceeds adjustable threshold
    - Above threshold indicates existing trend

6. When in squeeze, long when val > 0 and ROC exceeds threshold

    - Vice versa for short

7. Set stop loss and take profit conditions

## Advantages

1. Improved accuracy by combining dual channel system for reversal

2. Avoid false signals using linear regression and change rate 

3. Flexible adjustable parameters for optimization across products

4. Effective risk control per trade with stop loss/take profit

5. Sufficient backtest data to validate strategy viability

## Risks and Solutions

1. Squeeze does not always lead to effective reversal

    - Optimize parameters and tighten squeeze criteria

2. False breakouts generate wrong signals

    - Add linear regression to determine trend direction

3. Stop loss too wide leading to excessive single loss

   - Optimize stop loss points and control per trade loss

4. Insufficient test periods

    - Expand testing into more periods to prove long-term viability

## Enhancement Opportunities

1. Parameter optimization for more products

2. Add machine learning for support/resistance identification

3. Incorporate volume change to improve breakout validity 

4. Perform multi-timeframe analysis for trend persistence

5. Optimize dynamic stop loss/take profit

## Conclusion

The Dual Channel Tracking Reversal strategy utilizes indicators like Bollinger Bands and Keltner Channels for reversal trading. With parameter optimization, it can be adapted across different products to identify breakout validity to some extent. But reversal trading still carries inherent risks, requiring further incorporation of machine learning etc. to improve accuracy for steady excess returns.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2012|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2019|Backtest Stop Year|
|v_input_5|12|Backtest Stop Month|
|v_input_6|31|Backtest Stop Day|
|v_input_7|20|BB Length|
|v_input_8|2|BB MultFactor|
|v_input_9|22|KC Length|
|v_input_10|1.5|KC MultFactor|
|v_input_11|true|Use TrueRange (KC)|
|v_input_12|30|roclength|
|v_input_13|7|pcntChange|
|v_input_14|100|Stop Loss %|
|v_input_15|5000|Take Profit %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-02 00:00:00
end: 2023-11-01 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
// Credit for the initial Squeeze Momentum code to LazyBear, rate of change code is from Kiasaki
strategy("Squeeze X BF ?", overlay=false, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.0)

/////////////// Time Frame ///////////////
testStartYear = input(2012, "Backtest Start Year") 
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay, 0, 0)

testStopYear = input(2019, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay, 0, 0)

testPeriod() => true

/////////////// Squeeeeze ///////////////
length = input(20, title="BB Length")
mult = input(2.0,title="BB MultFactor")
lengthKC=input(22, title="KC Length")
multKC = input(1.5, title="KC MultFactor")
 
useTrueRange = input(true, title="Use TrueRange (KC)")
 
// Calculate BB
source = close
basis = sma(source, length)
dev = mult * stdev(source, length)
upperBB = basis + dev
lowerBB = basis - dev

// Calculate KC
ma = sma(source, lengthKC)
range = useTrueRange ? tr : (high - low)
rangema = sma(range, lengthKC)
upperKC = ma + rangema * multKC
lowerKC = ma - rangema * multKC

sqzOn  = (lowerBB > lowerKC) and (upperBB < upperKC)
sqzOff = (lowerBB < lowerKC) and (upperBB > upperKC)
noSqz  = (sqzOn == false) and (sqzOff == false)

val = linreg(source - avg(avg(highest(high, lengthKC), lowest(low, lengthKC)),sma(close,lengthKC)), lengthKC,0)

///////////// Rate Of Change ///////////// 
roclength = input(30, minval=1), pcntChange = input(7, minval=1)
roc = 100 * (source - source[roclength]) / source[roclength]
emaroc = ema(roc, roclength / 2)
isMoving() => emaroc > (pcntChange / 2) or emaroc < (0 - (pcntChange / 2))

/////////////// Strategy ///////////////
long = val > 0 and isMoving()
short = val < 0 and isMoving()

last_long = 0.0
last_short = 0.0
last_long := long ? time : nz(last_long[1])
last_short := short ? time : nz(last_short[1])

long_signal = crossover(last_long, last_short)
short_signal = crossover(last_short, last_long)

last_open_long_signal = 0.0
last_open_short_signal = 0.0
last_open_long_signal := long_signal ? open : nz(last_open_long_signal[1])
last_open_short_signal := short_signal ? open : nz(last_open_short_signal[1])

last_long_signal = 0.0
last_short_signal = 0.0
last_long_signal := long_signal ? time : nz(last_long_signal[1])
last_short_signal := short_signal ? time : nz(last_short_signal[1])

in_long_signal = last_long_signal > last_short_signal
in_short_signal = last_short_signal > last_long_signal

last_high = 0.0
last_low = 0.0
last_high := not in_long_signal ? na : in_long_signal and (na(last_high[1]) or high > nz(last_high[1])) ? high : nz(last_high[1])
last_low := not in_short_signal ? na : in_short_signal and (na(last_low[1]) or low < nz(last_low[1])) ? low : nz(last_low[1])

sl_inp = input(100.0, title='Stop Loss %') / 100
tp_inp = input(5000.0, title='Take Profit %') / 100
 
take_level_l = strategy.position_avg_price * (1 + tp_inp)
take_level_s = strategy.position_avg_price * (1 - tp_inp)

since_longEntry = barssince(last_open_long_signal != last_open_long_signal[1]) 
since_shortEntry = barssince(last_open_short_signal != last_open_short_signal[1]) 

slLong = in_long_signal ? strategy.position_avg_price * (1 - sl_inp) : na
slShort = strategy.position_avg_price * (1 + sl_inp)
long_sl = in_long_signal ? slLong : na
short_sl = in_short_signal ? slShort : na

/////////////// Execution ///////////////
if testPeriod()
    strategy.entry("Long",  strategy.long, when=long)
    strategy.entry("Short", strategy.short, when=short)
    strategy.exit("Long Ex", "Long", stop=long_sl, limit=take_level_l, when=since_longEntry > 0)
    strategy.exit("Short Ex", "Short", stop=short_sl, limit=take_level_s, when=since_shortEntry > 0)
    
/////////////// Plotting ///////////////
bcolor = iff(val > 0, iff(val > nz(val[1]), color.lime, color.green), iff(val < nz(val[1]), color.red, color.maroon))
plot(val, color=bcolor, linewidth=4)
bgcolor(not isMoving() ? color.white : long ? color.lime : short ? color.red : na, transp=70)
bgcolor(long_signal ? color.lime : short_signal ? color.red : na, transp=50)
hline(0, color = color.white)
```

> Detail

https://www.fmz.com/strategy/430881

> Last Modified

2023-11-02 16:31:50

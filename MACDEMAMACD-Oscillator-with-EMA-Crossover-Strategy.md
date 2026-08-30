
> Name

MACD-Oscillator-with-EMA-Crossover-Strategy MACD-Oscillator-with-EMA-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy is a simple and efficient trading strategy that combines the oscillator indicator MACD with the moving average EMA. It is currently set to a 4-hour K-line and can be adjusted to other time periods as needed. It has performed well on the data of Bitcoin and Ethereum over the past three years, outperforming the pure holding strategy. Through optimization and modification, it can be adjusted to futures, stock index, foreign exchange, stock and other markets.
### Strategy Principles
The strategy mainly consists of the following components:
1. MACD indicator: determines changes in price momentum.
2. EMA moving average: determine the direction of price trend.
3. Time conditions: Limit the effective time period of the strategy.
4. Long and short selection: Choose the long or short direction.
The specific trading rules are as follows:
1. Go long/short: When the closing price is higher than the EMA, the MACD histogram is positive, and the current K-line is higher than the previous day, go long/short.
2. Go short/close long: When the closing price is lower than EMA, the MACD histogram is negative, and the current K line is lower than the previous day, go short/close long.
This strategy is concise and clear, integrating the two major trading ideas of trend and short-term, forming an efficient quantitative decision-making system.
### Advantage Analysis
Compared with a single indicator, this strategy mainly has the following advantages:
1. MACD determines short-term momentum, EMA determines trend direction, and the indicators are closely coordinated.
2. The rules are simple and clear, easy to understand and implement, and not difficult to implement.
3. Parameters can be flexibly adjusted, suitable for different varieties and time periods.
4. You can only choose one-way long or short, or two-way trading.
5. The effective time period of the strategy can be set to avoid unnecessary transactions.
6. Stable and superior performance, with continuous profits over the years.
7. Controllable fund management can avoid excessive losses in a single transaction.
8. Machine learning technology can be introduced for optimization and improvement.
### Risk Analysis
Although this strategy has many advantages, the following risks need to be paid attention to:
1. The parameter optimization range is wide and there is a risk of over-optimization.
2. If stop loss and stop profit are not set, there is a risk of loss expansion.
3. Without considering trading volume, false breakthroughs may occur.
4. There is a lag in identifying trend turning points and losses cannot be completely avoided.
5. The effect may be weakened due to changes in the market environment.
6. Based only on historical data, attention should be paid to the robustness of the model.
7. The higher the transaction frequency, the higher the transaction cost.
8. Pay attention to the return drawdown ratio to avoid the curve being too jagged.
### Optimization direction
Based on the above analysis, this strategy can be optimized from the following aspects:
1. Add trading volume indicators to avoid false breakthroughs.
2. Add stop loss and stop profit settings to control single profit and loss.
3. Evaluate the effect of parameters in different time periods.
4. Introduce machine learning technology to achieve dynamic optimization.
5. Multi-market verification to improve robustness.
6. Adjust position size and reduce transaction frequency.
7. Optimize fund management strategies.
8. Test CFDs and increase frequency.
9. Continuous backtesting to prevent overfitting.
### Summarize
Overall, this strategy forms a simple and efficient quantitative strategy with the cooperation of MACD and EMA indicators. However, any strategy needs to be continuously optimized and verified to maintain adaptability and robustness to changes in the market environment. Trading strategies need to constantly evolve and be updated.
||


### Overview

This is a simple yet efficient trading strategy combining the MACD oscillator and EMA crossover. Currently set up for 4h candles but adaptable to other timeframes. It has performed well on BTC and ETH over the past 3 years, beating buy and hold. With optimizations it can be adapted for futures, indexes, forex, stocks etc.

### Strategy Logic 

The key components are:

1. MACD: Judging price momentum changes.

2. EMA: Determining price trend direction. 

3. Time condition: Defining valid strategy period.

4. Long/short option: Choosing long or short direction.

The trading rules are:

1. Long/exit short: When close above EMA, MACD histogram positive, and current candle higher than previous candle.

2. Short/exit long: When close below EMA, MACD histogram negative, and current candle lower than previous candle.

The strategy combines trend following and momentum in a simple and efficient system.

### Advantages

Compared to single indicators, the main advantages are:

1. MACD judges short-term momentum, EMA determines trend direction. 

2. Simple and clear rules, easy to understand and implement.

3. Flexible parameter tuning for different products and timeframes.

4. Option for long/short only or bidirectional trading.

5. Can define valid strategy period to avoid unnecessary trades.

6. Stable outperformance over years.

7. Controllable risk per trade.

8. Potential to optimize further with machine learning.

### Risks

Despite the merits, risks to consider:

1. Broad parameter tuning risks overfitting. 

2. No stops in place, risks unlimited losses.

3. No volume filter, risk of false breakouts.

4. Lag in catching trend turns, cannot avoid all losses.

5. Performance degradation from changing market regimes.

6. Based only on historical data, model robustness is key.

7. High trade frequency increases transaction costs. 

8. Need to monitor reward/risk ratios and equity curves.

### Enhancements

The strategy can be enhanced by:

1. Adding volume filter to avoid false breakouts.

2. Implementing stops to control loss per trade.

3. Evaluating parameter efficacy across time periods.

4. Incorporating machine learning for dynamic optimizations.

5. Robustness testing across markets.

6. Adjusting position sizing to reduce frequency.

7. Optimizing risk management strategies.

8. Testing spread instruments to increase frequency.

9. Continual backtesting to prevent overfitting.

### Conclusion

In summary, the strategy forms a simple yet powerful system from the MACD and EMA combo. But continual optimizations and robustness testing are critical for any strategy to adapt to changing market conditions. Trading strategies need to keep evolving.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|false|Use Heikin Ashi Candles in Algo Calculations|
|v_input_2|true|From Day|
|v_input_3|true|From Month|
|v_input_4|2020|From Year|
|v_input_5|31|To Day|
|v_input_6|12|To Month|
|v_input_7|2021|To Year|
|v_input_8|9|Length|
|v_input_9_hl2|0|Source: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_10|12|Fast Length|
|v_input_11|26|Slow Length|
|v_input_12|9|Signal Smoothing|
|v_input_13|false|Simple MA (Oscillator)|
|v_input_14|false|Simple MA (Signal Line)|
|v_input_15|true|longEntry|
|v_input_16|false|shortEntry|


> Source (PineScript)

``` pinescript
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © SoftKill21

//@version=4
strategy("My Script", overlay=true)

//heiking ashi calculation
UseHAcandles    = input(false, title="Use Heikin Ashi Candles in Algo Calculations")
//
// === /INPUTS ===

// === BASE FUNCTIONS ===

haClose = UseHAcandles ? security(heikinashi(syminfo.tickerid), timeframe.period, close) : close
haOpen  = UseHAcandles ? security(heikinashi(syminfo.tickerid), timeframe.period, open) : open
haHigh  = UseHAcandles ? security(heikinashi(syminfo.tickerid), timeframe.period, high) : high
haLow   = UseHAcandles ? security(heikinashi(syminfo.tickerid), timeframe.period, low) : low

//timecondition
fromDay = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
fromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
fromYear = input(defval = 2020, title = "From Year", minval = 1970)
 //monday and session 
 
// To Date Inputs
toDay = input(defval = 31, title = "To Day", minval = 1, maxval = 31)
toMonth = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
toYear = input(defval = 2021, title = "To Year", minval = 1970)

startDate = timestamp(fromYear, fromMonth, fromDay, 00, 00)
finishDate = timestamp(toYear, toMonth, toDay, 00, 00)
time_cond = true

//ema data  -- moving average
len = input(9, minval=1, title="Length")
src = input(hl2, title="Source")
out = ema(src, len)
//plot(out, title="EMA", color=color.blue)

//histogram
fast_length = input(title="Fast Length", type=input.integer, defval=12)
slow_length = input(title="Slow Length", type=input.integer, defval=26)
signal_length = input(title="Signal Smoothing", type=input.integer, minval = 1, maxval = 50, defval = 9)
sma_source = input(title="Simple MA (Oscillator)", type=input.bool, defval=false)
sma_signal = input(title="Simple MA (Signal Line)", type=input.bool, defval=false)

// Calculating
fast_ma = sma_source ? sma(src, fast_length) : ema(src, fast_length)
slow_ma = sma_source ? sma(src, slow_length) : ema(src, slow_length)
macd = fast_ma - slow_ma
signal = sma_signal ? sma(macd, signal_length) : ema(macd, signal_length)
hist = macd - signal


//main variables to apply conditions are going to be out(moving avg) and hist(macd)

long = haClose > out and haClose > haClose[1] and out > out[1] and hist> 0 and hist[1] < 0 and time_cond
short = haClose < out and haClose < haClose[1] and out < out[1] and hist < 0 and hist[1] > 0 and time_cond

//limit to 1 entry
var longOpeneda = false
var shortOpeneda = false
var int timeOfBuya = na



longCondition= long and not longOpeneda 

if longCondition
    longOpeneda := true
    timeOfBuya := time


longExitSignala = short
exitLongCondition = longOpeneda[1] and longExitSignala

if exitLongCondition
    longOpeneda := false
    timeOfBuya := na


plotshape(longCondition, style=shape.labelup, location=location.belowbar, color=color.green, size=size.tiny, title="BUY", text="BUY", textcolor=color.white)
plotshape(exitLongCondition, style=shape.labeldown, location=location.abovebar, color=color.red, size=size.tiny, title="SELL", text="SELL", textcolor=color.white)

//automatization

longEntry= input(true)
shortEntry=input(false)

if(longEntry)
    strategy.entry("long",strategy.long,when=longCondition)
    strategy.close("long",when=exitLongCondition)

if(shortEntry)
    strategy.entry("short",strategy.short,when=exitLongCondition)
    strategy.close("short",when=longCondition)


```

> Detail

https://www.fmz.com/strategy/427672

> Last Modified

2023-09-23 15:24:12

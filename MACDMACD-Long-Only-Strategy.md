
> Name

Long-term strategy based on MACD MACD-Long-Only-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/8d62e983ebbddf0003.png)
[trans]

### Overview
This strategy is based on the MACD indicator and long-term closing lines to achieve long-term trading of currency pairs. Open a position when the MACD indicator line crosses the long line, and close a position when the MACD indicator line crosses the closing line. At the same time, a stop loss strategy is set.
### Strategy Principles
This strategy uses the fast and slow lines of the MACD indicator. The fast line parameter is the 12-day EMA, and the slow line parameter is the 26-day EMA. The difference between the two moving averages is the MACD histogram. In addition, the 9-day EMA is calculated as the signal line. When the MACD histogram goes above 0.04, go long, and when it goes below 0.015, go long. At the same time, a 5% stop loss was set.
Specifically, the strategy first calculates the fast, slow and signal lines of the MACD indicator. Then set the long line to -0.04 and the closing line to 0.015. If the current MACD histogram is greater than the long-term line, go long; if the current MACD histogram is less than the closing line, go long. In addition, set the stop loss line to 95% of the opening price.
### Advantage Analysis
This strategy has the following advantages:
1. Use MACD indicator to judge the market trend with high accuracy.
2. Use double filtering of long-term and closing lines at the same time to avoid false signals
3. Set up stop-loss strategies to effectively control risks
4. Simple and clear, clear logic, easy to understand and implement
5. Only the MACD indicator is needed, and the resource usage is low
### Risk Analysis
This strategy also has certain risks:
1. The MACD indicator has a certain lag and may miss short-term opportunities.
2. The stop loss setting may be too conservative and cannot continue to track the long-term trend.
3. Parameter settings need to be repeatedly tested and optimized, otherwise they may be overfitted.
4. Only applicable to other currency pairs, the effect is doubtful
It can be optimized and improved by appropriately adjusting parameters and combining other indicators.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Test different MACD parameter combinations to find better parameters
You can try fast lines, slow lines, and signal lines of different lengths to find a more suitable combination.
2. Replace other indicators to test
For example, RSI, KD and other indicators may bring completely different effects.
3. Optimize long-term and closing line parameters
You can find more suitable long and closing parameters by repeatedly backtesting data.
4. Adjust stop loss strategy
You can consider methods such as trailing stop to make the stop loss more dynamically tracked.
5. Test multiple currency pairs
Apply the strategy to other currency pairs and examine the effects
### Summarize
This strategy is overall a very simple and intuitive long-term trading strategy. Use the MACD indicator to determine market trends and set up double filtering conditions to reduce mistaken transactions. At the same time, stop loss is configured to control risks. This strategy has clear logic, low resource usage, is easy to understand and implement, and is worth recommending. Of course, through parameter optimization, indicator adjustment and other means, this strategy still has a lot of room for improvement, which can make the effect even better.
||

### Overview

This strategy is based on the MACD indicator and long and close lines to implement long-term trading of the  currency pair. It opens positions when the MACD indicator line crosses over the long line and closes positions when the MACD indicator line crosses below the close line. Stop loss strategy is also configured.

### Strategy Logic

The strategy uses fast and slow lines of the MACD indicator. The fast line has a parameter of 12-day EMA and the slow line has a parameter of 26-day EMA. The difference between the two lines is the MACD histogram. In addition, 9-day EMA is calculated as the signal line. It goes long when the MACD histogram crosses above 0.04 and closes long positions when crossing below 0.015. Also, 5% stop loss is set.  

Specifically, the strategy first calculates the fast line, slow line and signal line of the MACD indicator. Then the long line is set at -0.04, the close line is set at 0.015. If the current MACD histogram is greater than the long line, it goes long. If the current MACD histogram is less than the close line, it closes the long position. In addition, the stop loss line is set at 95% of the entry price.

### Advantage Analysis

The strategy has the following advantages:

1. Use MACD indicator to judge market trend with high accuracy
2. Double filter with long and close lines avoids wrong signals  
3. Stop loss strategy effectively controls risks
4. Simple and clear logic, easy to understand and implement
5. Only needs  and MACD indicator, less resource occupation

### Risk Analysis 

The strategy also has some risks:

1. MACD indicator has some lagging, may miss short-term opportunities  
2. Stop loss setting may be too conservative to keep tracking long term trends
3. Parameter tuning needs lots of backtesting, otherwise overfitting may occur
4. Only applicable to , effectiveness for other pairs is uncertain

Methods like adjusting parameters, combining other indicators can be used to optimize and improve.

### Optimization Directions

The strategy can be optimized in the following aspects:

1. Test different MACD parameter combinations to find better parameters

   Fast line, slow line, signal line with different lengths can be tried to find more suitable combinations

2. Try other indicators

   Indicators like RSI, KD may have very different results

3. Optimize long and close line parameters

   More suitable parameters can be found through repetitive backtesting

4. Adjust stop loss strategy 

   Consider trailing stops to make stop loss more dynamic

5. Test on different currency pairs

   Apply the strategy to other pairs and examine the effects

### Conclusion

In conclusion, this is an overall very simple and intuitive  long term trading strategy. It judges market conditions using MACD indicator and sets double filter criteria to reduce false trading. Risk control is also configured through stop loss. The logic is clear and resource occupation is low. It is easy to understand and implement, worth recommending. Of course, there is still much room for improvement through parameter tuning, indicator change and other means, to make the strategy even more outstanding.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|Fast moving average|
|v_input_2|26|Slow moving average|
|v_input_3|12|Fast Length|
|v_input_4|26|Slow Length|
|v_input_5_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_6|9|Signal Smoothing|
|v_input_7|false|Simple MA(Oscillator)|
|v_input_8|false|Simple MA(Signal Line)|
|v_input_9|-0.04|Enter Long|
|v_input_10|0.015|Close Long|
|v_input_11|0.05|Stop Loss %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-04 00:00:00
end: 2024-01-11 00:00:00
period: 30m
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(shorttitle = "GBPJPY MACD", title = "GBPJPY MACD")
fastMA = input(title="Fast moving average",  defval = 12, minval = 7)
slowMA = input(title="Slow moving average",  defval = 26, minval = 7)
lastColor = yellow
[currMacd,_,_] = macd(close[0], fastMA, slowMA, 9)
[prevMacd,_,_] = macd(close[1], fastMA, slowMA, 9)
plotColor = currMacd > 0 ? currMacd > prevMacd ? lime : green : currMacd < prevMacd ? maroon : red
plot(currMacd, style = histogram, color = plotColor, linewidth = 3)
plot(0, title = "Zero line", linewidth = 1, color = gray)

//MACD
// Getting inputs
fast_length = input(title="Fast Length",  defval=12)
slow_length = input(title="Slow Length",  defval=26)
src = input(title="Source",  defval=close)
signal_length = input(title="Signal Smoothing",  minval = 1, maxval = 50, defval =9)
sma_source = input(title="Simple MA(Oscillator)", type=bool, defval=false)
sma_signal = input(title="Simple MA(Signal Line)", type=bool, defval=false)

// Plot colors
col_grow_above = #26A69A
col_grow_below = #FFCDD2
col_fall_above = #B2DFDB
col_fall_below = #EF5350
col_macd = #0094ff
col_signal = #ff6a00

// Calculating
fast_ma = sma_source ? sma(src, fast_length) : ema(src, fast_length)
slow_ma = sma_source ? sma(src, slow_length) : ema(src, slow_length)
macd = fast_ma - slow_ma
signal = sma_signal ? sma(macd, signal_length) : ema(macd, signal_length)
hist = macd - signal

//plot(hist, title="Histogram", style=columns, color=(hist>=0 ? (hist[1] < hist ? col_grow_above : col_fall_above) : (hist[1] < hist ? col_grow_below : col_fall_below) ), transp=0 )
plot(macd, title="MACD", color=col_macd, transp=0)
plot(signal, title="Signal", color=col_signal, transp=0)
///END OF MACD

//Long and Close Long Lines
linebuy = input(title="Enter Long", type=float, defval=-0.04)
linesell = input(title="Close Long", type=float, defval=0.015)

//Plot Long and Close Long Lines
plot(linebuy,color=green),plot(linesell,color=red)


//Stop Loss Input
sl_inp = input(0.05, title='Stop Loss %', type=float)/100


//Order Conditions
longCond = crossover(currMacd, linebuy)
exitLong = crossover(currMacd, linesell)
stop_level = strategy.position_avg_price * (1 - sl_inp)


//Order Entries
strategy.entry("long", strategy.long,  when=longCond==true)
strategy.close("long", when=exitLong==true)
strategy.exit("Stop Loss", stop=stop_level)
```

> Detail

https://www.fmz.com/strategy/438452

> Last Modified

2024-01-12 11:02:06

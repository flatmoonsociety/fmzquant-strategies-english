
> Name

Trend following strategy MACD-Trend-Following-Strategy based on MACD indicator
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/96418c6ef2eed7422d.png)
[trans]


## Overview
This strategy implements trend following trading based on the MACD indicator. The strategy uses the MACD indicator to identify the trend direction and cooperates with dynamic stop loss to lock in profits.
## Strategy Principle
1. Calculate fast line, slow line and MACD indicators. The fast line uses a 12-period exponential moving average, and the slow line uses a 26-period exponential moving average. MACD is the difference between the fast and slow lines.
2. Set buy and sell lines. A buy signal is generated when MACD crosses above the buy line; a sell signal is generated when MACD crosses below the sell line.
3. After opening a position, set a dynamic stop loss and track the stop loss line. The initial value of the stop loss line is 95% of the opening price. As the price moves, the stop loss line moves to lock in profits.
4. Close the position when stop loss or reverse signal is triggered.
## Advantage Analysis
1. Use the MACD indicator to identify the trend direction and track the trend effectively.
2. The dynamic stop-loss mechanism can continuously lock in profits and avoid losses from expanding.
3. The strategy logic is simple and clear, easy to understand and implement, and is suitable for automatic execution of quantitative transactions.
## Risk Analysis
1. The MACD indicator lags behind and may miss short-term trend reversals.
2. If the stop loss is too loose, some profits may be missed, and if the stop loss is too strict, the loss may be stopped prematurely.
3. Parameter tuning problem, MACD parameters and buying and selling lines need to be continuously tested and optimized.
4. The effect is better in the trending market, but there is a risk of loss in the volatile market.
## Optimization direction
1. Optimize MACD parameters and find the best parameter combination.
2. Test different stop loss methods, such as point stop loss, ATR stop loss, etc.
3. Add filter conditions and use other indicators to avoid mistaken transactions. For example, Bollinger Bands, RSI, etc.
4. Combined with trend judgment indicators, identify trends and volatile market conditions, and dynamically adjust strategy parameters.
## Summarize
The overall idea of ​​this strategy is clear. It uses the MACD indicator to track the trend and uses dynamic stop loss to lock in profits, which can effectively track the trend market. However, the MACD indicator has a lag problem, and the stop loss setting also needs to be optimized. The next step will be to further test parameter settings, optimize the stop loss mechanism, and filter with other indicators to make the strategy more suitable for different market conditions and improve the stability of the strategy.
||


## Overview

This strategy implements trend following trading  on the MACD indicator. It identifies trend direction using MACD and with dynamic stop loss to lock in profits. 

## Strategy Logic

1. Calculate Fast MA, Slow MA and MACD indicator. Fast MA uses 12-period EMA, Slow MA uses 26-period EMA. MACD is the difference between Fast and Slow MA.

2. Set buy and sell lines. Generate buy signal when MACD crosses over buy line, generate sell signal when MACD crosses below sell line.

3. Set dynamic stop loss after opening position. The initial stop loss is set at 95% of entry price, and will trail upwards as price runs.

4. Close position when stop loss is triggered or reverse signal appears.

## Advantage Analysis 

1. Using MACD to identify trend direction can effectively track trends.

2. The dynamic stop loss can continuously lock in profits and avoid enlarged losses.

3. The strategy logic is simple and clear, easy to understand and automate for quant trading.

## Risk Analysis

1. MACD has lagging effect, may miss short term trend reversal.  

2. Stop loss set too loose may miss some profits, too tight may stop out early.

3. Parameter tuning issue. MACD parameters and buy/sell lines need constant testing and optimization.

4. Works better in trending market, may have losses in choppy market.

## Optimization Directions

1. Optimize MACD parameters to find best combination.

2. Test different stop loss methods, like fixed points, ATR-based etc.

3. Add filter conditions using other indicators to avoid false signals, e.g. Bollinger Bands, RSI etc. 

4. Combine with trend identification tools, dynamically adjust strategy parameters based on trend vs range-bound market.

## Summary

The strategy has clear logic of using MACD to track trends and dynamic stop loss to lock in profits. It can effectively track trending markets. But MACD has lagging issue, and stop loss points need to be optimized. Next step is to further test parameters, optimize stop loss mechanism, add filters with other indicators, to make it robust across different market conditions, improving stability.

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
|v_input_9|-0.0002|Enter Long|
|v_input_10|0.0001|Close Long|
|v_input_11|0.05|Stop Loss %|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-16 00:00:00
end: 2023-11-15 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy(shorttitle = "EURUSD MACD", title = "EURUSD MACD")
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
linebuy = input(title="Enter Long", type=float, defval=-0.0002)
linesell = input(title="Close Long", type=float, defval=0.0001)

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

https://www.fmz.com/strategy/432361

> Last Modified

2023-11-16 17:42:09

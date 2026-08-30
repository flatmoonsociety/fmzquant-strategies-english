
> Name

Multi-EMA-Moving-RSI-Strategy
> Author

ChaoZhang

> Strategy Description


[trans]

## Strategy Principle
This strategy uses multiple sets of moving averages and RSI indicators for combined trading. When the fast EMA crosses the slow EMA and the RSI shows oversold, go short; when the price crosses the moving average again, close the position.
Specific transaction logic:
1. Calculate 4 sets of exponential moving averages with different periods, such as 9-day, 26-day, 100-day and 55-day moving averages
2. When the 9-day EMA falls below the 26-day EMA, consider a short selling signal
3. At the same time, when the RSI indicator is lower than the threshold (such as 40), a short signal is activated to avoid an oversold rebound.
4. After entering the short position, close the short position when the price crosses the 55-day or 100-day EMA.
5. Different moving average period combinations can be set to optimize parameters
This strategy makes full use of multiple moving averages to determine trends, and assists the RSI indicator to filter out false signals and short positions at oversold points.
## Strategic Advantages
- Multi-moving average combination judgment to improve accuracy
- RSI indicator avoids the risk of oversold rebounds
- Strategy with shorter moving average, stop loss with longer moving average, and retracement control
## Strategy Risk
- Requires repeated testing to determine appropriate parameters
- RSI parameter settings need to be carefully evaluated
- Only short-selling strategy may miss long opportunities
## Summarize
This strategy comprehensively uses the advantages of multiple moving averages, supplemented by the RSI indicator to filter signals. Parameter optimization and stop loss setting are crucial to strategy effectiveness. But only short trading is also a limitation.
||

## Strategy Logic

This strategy combines multiple moving averages with the RSI for trades. It goes short when a faster EMA crosses below a slower EMA, confirmed with RSI oversold.

The logic is:

1. Calculate 4 EMAs of differing periods, e.g. 9, 26, 100 and 55 periods

2. A short signal triggers when 9-period EMA crosses below 26-period EMA

3. Activate short only if RSI below threshold (e.g. 40) to avoid oversold bounce

4. After short entry, exit when price crosses above 55 or 100 EMA 

5. Different EMA combinations can be set for parameter optimization

The strategy utilizes multiple EMAs for trend and adds RSI for signal confirmation, going short at oversold levels. 

## Advantages

- Multiple EMAs improve accuracy 

- RSI avoids oversold bounce risk

- Faster EMA for entry, slower for stop loss

## Risks

- Extensive testing needed to find optimal parameters

- Careful evaluation of RSI parameters 

- SHORT only, so long opportunities missed

## Summary

This strategy combines the power of multiple EMAs with RSI confirmation and filtering. Parameter optimization and stop loss are critical. But being SHORT-only is a key limitation.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|9|EMA_L|
|v_input_int_2|26|EMA_L2|
|v_input_int_3|100|EMA_S|
|v_input_int_4|55|EMA_S2|
|v_input_int_5|5|RSI|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-14 00:00:00
end: 2023-09-13 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © YukalMoon

//@version=5
strategy(title="EMA SCALPEUR", overlay=true, initial_capital = 1000)


//// input controls

EMA_L = input.int (title = "EMA_L", defval = 9, minval = 1, maxval = 100, step =1)
EMA_L2 = input.int (title = "EMA_L2", defval = 26, minval = 1, maxval = 100, step =1)
EMA_S = input.int (title = "EMA_S", defval = 100, minval = 1, maxval = 100, step =1)
EMA_S2 = input.int (title = "EMA_S2", defval = 55, minval = 1, maxval = 100, step =1)
RSI1 = input.int (title = "RSI", defval = 5, minval = 1, maxval = 20 , step = 1)

/// mise en place de ema

RSI = ta.rsi(close, RSI1)

shortest = ta.ema(close, 9)
short = ta.ema(close, 26)
longer = ta.ema(close, 100)
longest = ta.ema(close, 55)

plot(shortest, color = color.red)
plot(short, color = color.orange)
plot(longer, color = color.aqua)
plot(longest, color = color.yellow)

plot(close)

//// trading indicators

EMA1 = ta.ema (close,EMA_L)
EMA2 = ta.ema (close,EMA_L2)
EMA3 = ta.ema (close, EMA_S)
EMA4 = ta.ema (close, EMA_S2)


//buy = ta.crossover(EMA1, EMA2) and RSI > 60 and RSI <70
sell = ta.crossunder(EMA1, EMA2) and RSI > 40

//buyexit = ta.crossunder(EMA3, EMA4)
sellexit = ta.crossover(EMA3, EMA4)

/////strategy


strategy.entry ("short", strategy.short, when = sell, comment = "ENTER-SHORT")


///// market exit


strategy.close ("short",  when = sellexit, comment = "EXIT-SHORT")












```

> Detail

https://www.fmz.com/strategy/426802

> Last Modified

2023-09-14 16:28:04

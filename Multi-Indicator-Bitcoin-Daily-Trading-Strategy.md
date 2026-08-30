
> Name

Multi-Indicator-Bitcoin-Daily-Trading-Strategy based on multiple indicators
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/bb27b02cb055b9f86c.png)

[trans]

## Overview
This strategy is based on a combination of multiple indicators and looks for trading opportunities within Bitcoin's daily time frame. Mainly use indicators such as MACD, RSI, Stoch RSI, combined with the direction of the moving average, to determine the current trend direction to issue buy and sell signals.
## Strategy Principle
This strategy mainly uses the following indicators:
1. MACD `(快线-慢线)` and its signal lines. When MACD crosses the signal line above, it is a buy signal, and when it crosses below 0, it is a sell signal.
2. RSI relative strength index. When the RSI crosses the set threshold, it is a buy signal.
3. Stoch RSI. The Stoch RSI indicator reflects the overbought and oversold conditions of the RSI. When Stoch RSI is lower than the set threshold, it is a buy signal, and when it is higher than the set threshold, it is a sell signal.
4. Moving average direction. When the closing price crosses below the moving average, it is a sell signal.
Based on these indicators, the trading signals for this strategy are as follows:
**Buy Signal**: When `(Stoch RSI < 设定阈值) 且 (MACD上穿阈值 或 RSI上穿阈值)`
**Sell Signal**: When `(MACD下穿0) 且 (收盘价下穿均线 或 Stoch RSI > 设定阈值)`
By combining multiple indicators, you can more accurately determine the current trend direction and send trading signals at trend turning points.
## Strategic Advantages
1. Using multiple indicators in combination can improve the accuracy of judgment and avoid false signals caused by a single indicator.
2. The MACD indicator can determine the current trend direction and strength. The RSI indicator reflects overbought and oversold conditions. Stoch RSI determines the overbought and oversold conditions of RSI. The moving average determines the current trend direction. These indicators verify each other and improve the effect.
3. The buy and sell signals set the combination conditions of multiple indicators, which can filter out some false signals and avoid unnecessary transactions.
4. The start time of the backtest of this strategy is January 1, 2017, which includes the huge price increase of Bitcoin at the end of 2017, which can test the performance of the strategy in the market.
5. The strategy includes stop loss settings, which can control the loss of a single transaction.
## Strategy Risk
1. Although a combination of multiple indicators can improve accuracy, there may also be differences between indicators, leading to a certain risk of misjudgment.
2. The stop loss level of strategy optimization may need to be adjusted according to different market conditions. If the stop loss is too wide, the single loss will be increased, and if the stop loss is too narrow, the stop loss will be taken out.
3. Daily-level strategies cannot carry out detailed operations in a shorter time frame. It cannot respond when emergencies cause large short-term fluctuations.
4. The strategy only backtests part of the historical market conditions, and there may be a risk of over-fitting. Testing over a longer time frame and in more markets is needed to verify the effectiveness of the strategy.
## Optimization direction
1. Test more indicator combinations and find better multi-indicator combination strategies.
2. Optimize the indicator parameters and find more suitable parameter values.
3. Test different stop loss levels and find the best combination of stop loss and take profit ratios.
4. Conduct backtesting in longer historical markets to avoid overfitting.
5. Try to apply this strategy idea in a higher frequency time range and conduct more frequent transactions.
## Summarize
This strategy combines MACD, RSI, Stoch RSI and other indicators to determine the current trend direction of Bitcoin's daily level and send trading signals at the turning point of the trend. Also set a stop loss to control trading risks. The backtest results of this strategy are excellent, but it still needs to be verified over a longer period of time and in more markets to avoid the risk of overfitting. By further optimizing indicator parameters and stop loss and take profit settings, better results can be obtained. This strategy provides a preliminary idea for a multi-index combination strategy and is worthy of further exploration and improvement.
||

## Overview  

This strategy combines multiple indicators to identify trading opportunities within the daily time frame for Bitcoin. It mainly uses indicators like MACD, RSI, Stoch RSI, together with the direction of moving average to determine the current trend direction for generating buy and sell signals.

## Strategy Logic

The strategy utilizes the following key indicators:

1. MACD (Fast MA - Slow MA) and its signal line. MACD crossing above signal line gives buy signal, and crossing below 0 gives sell signal.

2. RSI (Relative Strength Index). RSI crossing above a threshold gives buy signal.

3. Stoch RSI. Stoch RSI shows overbought/oversold levels of RSI. Stoch RSI below threshold gives buy signal, while above threshold gives sell signal.

4. Moving average direction. Close price crossing below MA gives sell signal.

According to these indicators, the trading signals are:

**Buy Signal**: When `(Stoch RSI < Threshold) AND (MACD crossing above threshold OR RSI crossing above threshold)` 

**Sell Signal**: When `(MACD crossing below 0) AND (Close below MA OR Stoch RSI > Threshold)`

Using multiple indicators together can better determine the current trend direction and identify trend reversal points for entering trades.

## Advantages

1. Combining multiple indicators improves accuracy and avoids false signals from a single indicator.

2. MACD shows trend direction and strength. RSI reflects overbought/oversold levels. Stoch RSI determines overbought/oversold of RSI. MA shows trend direction. These indicators verify each other.

3. The buy/sell signals require a combination of multiple indicators, filtering out some false signals and avoiding unnecessary trades.

4. Backtest starts from 2017/1/1, covering the huge bull run of Bitcoin at 2017 year end. Tests strategy performance in a real bull market.

5. Stop loss is set to control loss in single trades.

## Risks

1. Although using multiple indicators improves accuracy, discrepancy between them can still lead to some wrong signals.

2. The optimized stop loss level may need adjustments for different market situations. Stop loss too wide increases loss in single trades, while too tight may get stopped out prematurely.

3. Daily timeframe prevents detailed operations in shorter time ranges. Unable to respond to sudden short-term big moves.

4. Strategy is only backtested on limited historical data. Overfit risk exists. Requires further testing across longer timeframe and more markets.

## Enhancement Opportunities 

1. Test more indicator combinations to find optimal multi-indicator strategies.

2. Optimize parameters of the indicators for better values.

3. Test different stop loss levels to find optimal risk/reward ratio.

4. Conduct backtests across longer historical data to avoid overfitting. 

5. Explore applying strategy logic in higher frequency timeframes for more frequent trading.

## Conclusion

This strategy combines MACD, RSI, Stoch RSI and other indicators to determine the bitcoin daily trend direction and identify trend reversals for trade entry. Stop loss is set to control trade risk. Backtest shows positive results but still requires further verification across longer timeframe and more markets to avoid overfit risks. Further optimizations on indicator parameters and stop loss/take profit levels can improve results. The strategy provides an initial idea of multi-indicator combination approach which is worth deeper exploration and enhancement.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2017|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2019|Backtest Stop Year|
|v_input_5|12|Backtest Stop Month|
|v_input_6|31|Backtest Stop Day|
|v_input_7|30|rsi_threshold|
|v_input_8|4|rsi_length|
|v_input_9|8|srsi_length|
|v_input_10|4|srsi_smooth|
|v_input_11|57|srsi_sell_threshold|
|v_input_12|14|length|
|v_input_13|-1|dma_signal_threshold|
|v_input_14|11|fastLength|
|v_input_15|18|slowlength|
|v_input_16|6|MACDLength|
|v_input_17|-2|MACD_signal_threshold|
|v_input_18|5|short_loss_tol|
|v_input_19|5|long_loss_tol|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-23 00:00:00
end: 2023-10-29 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
// Original code is from CredibleHulk and modified by bennef
strategy("BTC Daily Strategy BF", overlay=false, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100, commission_type=strategy.commission.percent, commission_value=0.075)

/////////////// Time Frame ///////////////
testStartYear = input(2017, "Backtest Start Year") 
testStartMonth = input(1, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear,testStartMonth,testStartDay, 0, 0)

testStopYear = input(2019, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(31, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear,testStopMonth,testStopDay, 0, 0)

testPeriod() => true

/////////////// Input Params /////////////// 
rsi_threshold = input(30)
rsi_length = input(4)
srsi_length = input(8)
srsi_smooth = input(4)
srsi_sell_threshold = input(57)
length = input(14)
dma_signal_threshold = input(-1)
fastLength = input(11)
slowlength = input(18)
MACDLength = input(6)
MACD_signal_threshold = input(-2)
short_loss_tol = input(5)
long_loss_tol = input(5)

stop_level_long = strategy.position_avg_price * (1 - long_loss_tol / 100.0)
stop_level_short = strategy.position_avg_price * (1 + short_loss_tol / 100.0)
    
///////////////  Signal generation ///////////////
// MACD 
MACD = ema(close, fastLength) - ema(close, slowlength)
aMACD = ema(MACD, MACDLength)
delta = MACD - aMACD

// RSI and Stochastic RSI 
rs = rsi(close, rsi_length)
k = sma(stoch(rs, rs, rs, srsi_length), srsi_smooth)

// SMA 
norm = sma(ohlc4, length)
threshold = close - norm   

/////////////// Strategy ///////////////
long = ((crossover(delta, MACD_signal_threshold) or crossover(rs, rsi_threshold)) and k < srsi_sell_threshold)
short = (crossunder(delta, 0) or (crossunder(threshold, dma_signal_threshold) and k > srsi_sell_threshold))

if testPeriod()
    strategy.entry("L", strategy.long, when = long)
    strategy.entry("S", strategy.short, when = short)
    strategy.exit("stop loss L", from_entry = "L", stop = stop_level_long)
    strategy.exit("stop loss S", from_entry = "S", stop = stop_level_short)

/////////////// Plotting ///////////////
// MACD
plot(delta, color = delta > MACD_signal_threshold ? color.lime : delta < 0 ? color.red : color.yellow)
MACD_signal_threshold_line = hline(MACD_signal_threshold, color = color.yellow, title = "MACD Signal Threshold")

// RSI
plot(rs, color = rs > rsi_threshold ? color.lime : color.fuchsia)
rsi_threshold_line = hline(rsi_threshold, color = color.fuchsia, title = "RSI Threshold")

// Stochastic RSI 
plot(k, color = k > srsi_sell_threshold ? color.lime : color.red)
srsi_sell_threshold_line = hline(srsi_sell_threshold, color = color.white, title = "Stoch RSI Threshold")

// SMA
plot(threshold / 100, color = threshold < dma_signal_threshold ? color.red : color.blue)
dma_signal_threshold_line = hline (dma_signal_threshold, color = color.blue, title = "DMA Signal Threshold")

bgcolor(long ? color.lime : short ? color.red : na, transp=50)
```

> Detail

https://www.fmz.com/strategy/430544

> Last Modified

2023-10-30 10:37:58

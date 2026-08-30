
> Name

Trend-Tracking-Moving-Average-RSI-Strategy Trend-Tracking-Moving-Average-RSI-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1d7f34bf091a108b7bc.png)
[trans]

## Overview
The Trend Following Moving Average RSI strategy is an automated stock trading strategy that utilizes both trend analysis and overbought and oversold indicators. This strategy uses a simple moving average to determine the direction of the market trend, and combines it with the Relative Strength Index (RSI) indicator to send trading signals to determine and track the trend.
## Strategy Principle
The strategy mainly consists of three parts:
1. Trend judgment: Calculate the 200-day simple moving average of the long-term trend, and calculate the 30-day and 50-day simple moving average of the short-term trend. When the short-term moving average crosses the long-term moving average, it is a bullish signal, and when it crosses below the long-term moving average, it is a bearish signal to determine the long-term and short-term trend of the market.
2. Judgment of overbought and oversold: Calculate the 14-day RSI indicator. RSI above 80 is the overbought zone, and below 20 is the oversold zone. A trading signal is issued when the RSI indicator falls from the overbought zone or rises from the oversold zone.
3. Entry and exit: When an overbought or oversold signal is detected, if the direction of the signal is consistent with the trend judgment, enter the market long/short. When a golden cross occurs between the short-term and long-term moving averages, it is judged that the trend has reversed, and the position is closed at this time.
Through this strategy, you can enter the market in time when the stock price reverses, and at the same time filter out some noise transactions based on trend judgment, and it is relatively excellent in retracement control.
## Advantage Analysis
This strategy has the following advantages:
1. Combine trend judgment and overbought and oversold indicators to filter out noise and identify market reversal points.
2. Consider the trend direction in both long and short time periods at the same time to make a more accurate judgment.  
3. Using the moving average as a stop loss method, the stop loss point can be set according to the degree of market volatility.
4. Strict entry conditions can effectively avoid false breakthroughs.
## Risks and Solutions
There are also some risks with this strategy:
1. If the market fluctuates for a long time, a large number of invalid transactions will be opened. The solution is to add more filtering conditions to avoid unnecessary transactions.
2. There is a certain risk of time lag. The solution is to appropriately shorten the period parameters of the moving average.
3. The effect of the signal sent by the RSI indicator will be affected by the stock and the market. The solution is to judge the effect based on more factors such as K-line shape.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Add more filtering conditions, such as trading volume, K-line shape, etc., to further improve the effectiveness of the signal.  
2. Optimize the parameter periods of the moving average and RSI to make them more consistent with the characteristics of different stocks.
3. Establish a dynamic moving average and automatically adjust parameters based on market volatility and risk appetite.
4. Use more advanced technologies such as machine learning to judge market trends and improve judgment accuracy.
## Summarize
The trend-following moving average RSI strategy is generally a very practical strategy idea. It combines trend analysis and overbought and oversold indicators to filter market noise to a certain extent and make trading signals more accurate and effective. By continuously optimizing means and parameters, this strategy can become a stable and profitable long-term trading system.
||

## Overview  

The Trend Tracking Moving Average RSI strategy is an automated stock trading strategy that utilizes both trend analysis and overbought-oversold indicators. The strategy employs simple moving averages to determine market trend direction and combines Relative Strength Index (RSI) indicators to generate trading signals, realizing trend judgment and tracking.

## Strategy Logic

The strategy consists of three main parts:

1. Trend judgment: Calculates the long-term trend with 200-day simple moving average, and the short-term trend with 30-day and 50-day simple moving averages. When the short-term moving average crosses over the long-term one, it is a bullish signal, and when it crosses below, it's a bearish signal, to determine long-term and short-term market trends.

2. Overbought-Oversold Analysis: Calculates the 14-day RSI indicator. RSI above 80 is the overbought zone and below 20 is the oversold zone. Trading signals are generated when the RSI indicator drops from the overbought zone or rises from the oversold zone.  

3. Entry and Exit: When overbought or oversold signals are identified, if the direction is consistent with the trend analysis, long/short positions will be opened. When short-term and long-term moving averages have golden crosses, it is judged that trends are reversing and existing positions will be closed.

With this strategy, it is possible to enter the market timely when prices reverse, while filtering out some noisy trades by incorporating trend analysis, with relatively excellent drawdown control.

## Advantage Analysis 

The strategy has the following advantages:

1. Combining trend analysis and overbought-oversold indicators to filter out noise and identify turns in the market.
2. Considering trends in both long-term and short-term timeframes for more accurate judgments.   
3. Using moving averages as stop loss methods so that stop loss points can be set based on market volatility.  
4. Strict entry conditions help avoid false breakouts effectively.

## Risks and Solutions

There are also some risks with this strategy:   

1. Frequent insignificant trades may occur if the market stays range-bound for a prolonged time. Additional filters can be added to avoid unnecessary trades.
2. There is some time lag risk. Shortening moving average cycle parameters can mitigate it.  
3. RSI signals can be influenced by stocks and markets. More factors like candlestick patterns should be combined to judge the effectiveness.

## Optimization Directions

The strategy can be further optimized in the following aspects:

1. Adding more filters like volume, candlestick patterns to further improve signal quality.   
2. Optimizing moving average and RSI cycle parameters to match different stock characteristics.  
3. Building dynamic moving averages to automatically adjust parameters based on market volatility and risk appetite.  
4. Using more advanced techniques like machine learning to determine market trends with higher accuracy.

## Summary   

In general, the Trend Tracking Moving Average RSI Strategy is a very practical strategy idea, filtering out market noise to some extent by combining trend analysis and overbought-oversold indicators, making trading signals more accurate and valid. As optimization tools and parameters continue to be enhanced, this strategy can become a steadily profitable long-term trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Length|
|v_input_2_ohlc4|0|Source: ohlc4|high|low|open|hl2|hlc3|hlcc4|close|
|v_input_3|3000|maxLoss|
|v_input_4|200|trendMA|
|v_input_5|30|shortMA|
|v_input_6|50|longMA|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-16 00:00:00
end: 2023-11-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © mattehalen

// INPUT per TIMEFRAME
// 5min     = Legnth = 9, Source = ohlc4,MaxLoss = 1000 TrendMA = 200, ShortMA = 4, LongMA = 10
// 30min    = Legnth = 7, Source = ohlc4,MaxLoss = 1000 TrendMA = 200, ShortMA = 10, LongMA = 20

strategy("Mathias & Christer Timeframe RSI", shorttitle="M&C_RSI",overlay=true, process_orders_on_close = true, default_qty_type =  strategy.percent_of_equity, default_qty_value = 100)
len = input(9, title="Length", type=input.integer)
src = input(ohlc4, title="Source", type=input.source)
//show4h = input(true, title="show 4h", type=input.bool)
maxLoss = input(3000)

rsiCurrent = rsi(src, len)
//rsi4h = security(syminfo.ticker, "240", rsi(src, len))
rsi4h   = rsi(src, len)

//--------------------------------------------------
//MA
trendMAInput = input(200, title="trendMA", type=input.integer)
shortMAInput = input(30, title="shortMA", type=input.integer)
longMAInput = input(50, title="longMA", type=input.integer)

trendMA = ema(close,trendMAInput)
shortMA = ema(close,shortMAInput)
longMA  = ema(close,longMAInput)
plot(trendMA, color=color.black, linewidth=5)
plot(shortMA, color=color.red, linewidth=2)
plot(longMA, color=color.green, linewidth=2)
bgcolor(crossunder(shortMA,longMA) ? color.black : na, transp=10)

//--------------------------------------------------
//RSI
BuySignalBarssince = barssince(rsi4h[1]<rsi4h[0] and rsi4h[1]<20)
BuySignal       = (rsi4h[1]<rsi4h[0] and rsi4h[1]<20 and BuySignalBarssince[1]>10)
BuySignalOut   = crossunder(longMA[1],shortMA[1])
bgcolor(BuySignal ? color.green : na, transp=70)
bgcolor(BuySignalOut ? color.green : na, transp=10)



SellSignalBarssince = barssince(rsi4h[1]>rsi4h[0] and rsi4h[1]>80)
SellSignal      = (rsi4h[1]>rsi4h[0] and rsi4h[1]>80 and SellSignalBarssince[1]>10)
SellSignalOut   = crossunder(shortMA[1],longMA[1])
bgcolor(SellSignal ? color.red : na, transp=70)
bgcolor(SellSignalOut ? color.red : na, transp=10)


if BuySignal
    strategy.close("short", comment = "Exit short")
    strategy.entry("long", true)
    strategy.exit("Max Loss", "long", loss = maxLoss)

if BuySignalOut
    strategy.close("long", comment = "Exit Long")
if SellSignal
    // Enter trade and issue exit order on max loss.
    strategy.close("long", comment = "Exit Long")
    strategy.entry("short", false)
    strategy.exit("Max Loss", "short", loss = maxLoss)
if SellSignalOut
    // Force trade exit.
    strategy.close("short", comment = "Exit short")
    
//--------------------------------------------------
//ATR
MyAtr = atr(10)
AtrFactor = 10
mySLBuy  = close[BuySignalBarssince]
mySLSell = close[SellSignalBarssince]

plotchar(BuySignal, "BuySignal", "⬆", location.belowbar, color.lime,size =size.huge )
plotchar(BuySignalOut, "BuySignalOut", "█", location.belowbar, color.lime,size =size.small)
plotchar(SellSignal, "SellSignal", "⬇", location.abovebar ,color.red,size =size.huge)
plotchar(SellSignalOut, "SellSignalOut", "█", location.abovebar, color.red,size =size.small)



```

> Detail

https://www.fmz.com/strategy/433026

> Last Modified

2023-11-23 17:13:06

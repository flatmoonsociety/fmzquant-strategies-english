
> Name

Bollinger-Bands and RSI Combination Trading Strategy Bollinger-Bands-and-RSI-Combination-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/133e922f3a57fcaaf22.png)
[trans]
### Overview
This is a strategy that utilizes Bollinger Bands and the Relative Strength Index (RSI) to trade in combination. Its core idea is to generate buy and sell signals when the RSI reaches the overbought or oversold zone, combined with the upper and lower bands of the Bollinger Bands.
### Policy name
BB-RSI combination trading strategy
### Strategy Principles
This strategy first calculates the regular Bollinger Bands, including the middle band, upper band, and lower band. The middle rail is a simple moving average of closing prices within a certain period, and the upper and lower rails are one standard deviation above and below the middle rail.
At the same time, the strategy calculates the RSI indicator. RSI determines whether the current market is overbought or oversold by comparing the average closing increase and the average closing decrease over a period of time.
When the RSI is less than the low (default 30), it means the market is oversold; when the RSI is greater than the high (default 70), it means the market is overbought.
What this strategy does is generate a buy signal if the price closes below the lower Bollinger Bands when the RSI reaches the oversold zone, and generate a sell signal if the price closes above the upper Bollinger Bands when the RSI reaches the overbought zone.
### Advantage Analysis
The biggest advantage of this combination strategy is its ability to detect turning points in the market. When the stock price is in an area with a large Bollinger Bands breadth, it means that the market is highly volatile. At this time, RSI can be used to determine whether the market is overbought and oversold, and the opportunity for reversal can be located.
Another advantage is the flexible parameter setting. Both the Bollinger Bands and RSI indicators have adjustable parameters that traders can optimize according to their needs.
### Risk Analysis
The biggest risk with this strategy is that it generates fewer signals. Especially when the market has long-term unilateral trends, overfitting is prone to occur. At this time, it is difficult for RSI to reach the overbought and oversold state and cannot generate trading signals.
Another risk is the difficulty of parameter setting. Both Bollinger Bands and RSI need to set parameters such as period, and improper selection may lead to poor strategy effects. This requires traders to have a full understanding of the market, otherwise this strategy should be used with caution.
### Optimization direction
In order to obtain more trading opportunities, the overbought and oversold lines of RSI can be adjusted appropriately. For example, you can raise the oversold line to 40 and lower the overbought line to 60, so that a signal can be easily formed.
Another direction is to introduce a trend judgment mechanism to avoid blind reversal in unilateral market conditions. For example, the direction of the long-period moving average can be calculated as a filter condition, and a signal is generated only when the direction of the moving average matches.
### Summarize
The BB-RSI combination strategy uses Bollinger Bands to determine support and resistance, RSI determines overbought and oversold, and generates signals at reversal points. It can effectively locate the turning point of the market and is a typical reversal trading strategy. Through parameter optimization and rule improvement, this strategy can become a powerful tool for quantitative trading.
||

### Overview

This is a combination trading strategy using Bollinger Bands and Relative Strength Index (RSI). Its core idea is to generate buy and sell signals when RSI reaches overbought or oversold areas, combined with Bollinger Bands upper and lower rails.

### Strategy Name 

BB-RSI Combination Trading Strategy

### Strategy Principle

The strategy first calculates regular Bollinger Bands, including middle rail, upper rail and lower rail. The middle rail is the simple moving average of closing prices over a certain period, and the upper and lower rails are above and below one standard deviation of the middle rail.

At the same time, the strategy calculates the RSI indicator. RSI judges whether the current market is overbought or oversold by comparing the average closing uptrend and the average closing downtrend over a period of time.

When RSI is less than the low point (default 30), it means the market is oversold. When RSI is greater than the high point (default 70), it means the market is overbought.  

What this strategy does is that when RSI reaches the oversold zone, if the closing price is lower than the Bollinger Bands lower rail, a buy signal is generated. When RSI reaches the overbought zone, if the closing price is higher than Bollinger Bands upper rail, a sell signal is generated.

### Advantage Analysis

The biggest advantage of this combination strategy is that it can discover turning points in the market. When the stock price is in a relatively large area of ​​Bollinger Bands width, it means the market fluctuation is large. At this time, by judging whether the market is overbought or oversold through RSI, the timing of reversal can be located.

Another advantage is flexible parameter settings. Both Bollinger Bands and RSI indicators have adjustable parameters that traders can optimize based on their needs.

### Risk Analysis

The biggest risk of this strategy is the small number of signals generated. Especially in the long-term one-way trend market, it is prone to over-fitting. At this time, it is difficult for RSI to reach overbought and oversold status, unable to generate trading signals.  

Another risk is the difficulty in parameter settings. Bollinger Bands and RSI both need to set cycle and other parameters. Improper selection may lead to poor strategy results. This requires the trader to have a thorough understanding of the market, otherwise they should use the strategy with caution.

### Optimization Directions

In order to obtain more trading opportunities, the overbought and oversold lines of RSI can be appropriately adjusted. For example, the oversold line can be raised to 40 and the overbought line lowered to 60, so that signals can be formed more easily.

Another direction is to introduce a trend judgment mechanism to avoid blind reversal in one-way trend markets. For example, the direction of long cycle moving averages can be calculated as a filter condition. Signals are generated only when the moving average direction matches.  

### Summary 

The BB-RSI combination strategy uses Bollinger Bands to determine support and resistance, and RSI to determine overbought and oversold status, generating signals at reversal points. It can effectively identify turning points in the market and is a typical reversal trading strategy. Through parameter optimization and rule refinement, this strategy can become a powerful tool for quantitative trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|Precio base: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|20|Longitud|
|v_input_3|2|Desviación estándar|
|v_input_4_close|0|RSI Fuente: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_5|14|RSI Longitud|
|v_input_6|70|RSI Sobrecompra|
|v_input_7|30|RSI Sobrevendido|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-28 00:00:00
end: 2024-02-03 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © samuelarbos


//@version=4
strategy("Estrategia de Bandas de Bollinger y RSI", overlay=true)

// Definimos los parámetros de las bandas de Bollinger
source = input(close, title="Precio base")
length = input(20, minval=1, title="Longitud")
mult = input(2.0, minval=0.001, maxval=50, title="Desviación estándar")

// Calculamos las bandas de Bollinger
basis = sma(source, length)
dev = mult * stdev(source, length)
upper = basis + dev
lower = basis - dev

// Definimos el RSI y sus parámetros
rsi_source = input(close, title="RSI Fuente")
rsi_length = input(14, minval=1, title="RSI Longitud")
rsi_overbought = input(70, minval=0, maxval=100, title="RSI Sobrecompra")
rsi_oversold = input(30, minval=0, maxval=100, title="RSI Sobrevendido")

// Calculamos el RSI
rsi = rsi(rsi_source, rsi_length)

// Definimos las señales de compra y venta
buy_signal = crossover(close, lower) and rsi < rsi_oversold
sell_signal = crossunder(close, upper) and rsi > rsi_overbought

// Compramos cuando se da la señal de compra
if (buy_signal)
    strategy.entry("Buy", strategy.long)
    
// Vendemos cuando se da la señal de venta
if (sell_signal)
    strategy.entry("Sell", strategy.short)
```

> Detail

https://www.fmz.com/strategy/440982

> Last Modified

2024-02-04 15:09:35

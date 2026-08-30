
> Name

BMSB-Breakout-Strategy-BMSB-Breakout Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/6b2f6a1f80b9731af0b16a1bf1356bd5f6d04ee25ed8fbf0738b146c283c76d3.png)

[trans]
#### Overview
BMSB Breakout Strategy is a moving average based breakout strategy. This strategy uses a 20-period simple moving average (SMA) and a 21-period exponential moving average (EMA) to determine the trend direction of the market. When the closing price crosses above the SMA, the strategy generates a buy signal; when the closing price crosses below the EMA, the strategy generates a sell signal. The main idea of ​​this strategy is to capture the formation and reversal of trends and trade in the direction of the trend.
#### Strategy Principle
The core of this strategy is to use two moving averages with different periods to determine market trends. The 20-period SMA is relatively slow and represents the mid- to long-term trend of the market; the 21-period EMA is relatively fast and represents the short-term trend of the market. When the closing price crosses above the EMA, it means that the market has turned into an upward trend in the medium and long term, and the strategy generates a buy signal at this time; when the closing price crosses below the EMA, it means that the market has turned into a downward trend in the short term, and at this time the strategy generates a sell signal. In this way, the strategy can intervene in the early stages of a trend and exit promptly when the trend reverses.
#### Advantage Analysis
1. Simple and easy to understand: The indicators used by this strategy are simple, the principles are clear, and easy to understand and implement.
2. Trend following: Through two moving averages of different periods, the strategy can effectively capture the trend direction of the market and intervene in time when the trend is formed.
3. Timely stop loss: When the trend reverses, the strategy can promptly close the position through the signal of crossing the EMA and control the loss.
4. Strong adaptability: This strategy can be applied to different markets and varieties and has good adaptability.
#### Risk Analysis
1. Oscillatory market: In the case of market turbulence, this strategy may generate more trading signals, leading to frequent transactions and higher transaction costs.
2. Lagging: Since the moving average is a lagging indicator, the buy and sell signals of the strategy may be delayed to a certain extent, missing the best trading opportunities.
3. Parameter optimization: The performance of the strategy will be affected by the selection of the moving average period, and different parameters may lead to different results.
#### Optimization direction
1. Parameter optimization: You can optimize the period parameters of SMA and EMA to find the best parameter combination and improve the performance of the strategy.
2. Trend filtering: When generating trading signals, other trend indicators or price action patterns can be introduced to further confirm the strength and persistence of the trend and improve the reliability of the signal.
3. Risk control: You can introduce stop-loss and stop-profit mechanisms to control the risk exposure of a single transaction; you can also use position management to dynamically adjust the position size according to market volatility to reduce the overall risk of the strategy.
4. Long and short timing: When buying and selling signals are generated, other timing indicators or market sentiment indicators can be combined to evaluate the strength of the long and short parties and choose a more advantageous direction for trading.
#### Summarize
BMSB Breakout Strategy is a simple and easy-to-use trend tracking strategy that uses two moving averages of different periods to determine the market trend, intervene in time when the trend is formed, and exit in time when the trend reverses. The advantage of this strategy is that it is simple and easy to understand and has strong adaptability. At the same time, it also has risks such as frequent trading in volatile markets and lagging signals. Through parameter optimization, trend filtering, risk control and long-short timing, the performance and stability of the strategy can be further improved.
|| 

#### Overview

The BMSB Breakout Strategy is a moving average-based breakout strategy. It uses a 20-period Simple Moving Average (SMA) and a 21-period Exponential Moving Average (EMA) to determine the trend direction of the market. When the closing price crosses above the SMA, the strategy generates a buy signal; when the closing price crosses below the EMA, the strategy generates a sell signal. The main idea of this strategy is to capture the formation and reversal of trends and trade in the direction of the trend.

#### Strategy Principle

The core of this strategy is to use two moving averages with different periods to determine the market trend. The 20-period SMA is relatively slow and represents the medium to long-term trend of the market; the 21-period EMA is relatively fast and represents the short-term trend of the market. When the closing price crosses above the SMA, it indicates that the market has turned into an upward trend from a medium to long-term perspective, and the strategy generates a buy signal; when the closing price crosses below the EMA, it indicates that the market has turned into a downward trend from a short-term perspective, and the strategy generates a sell signal. In this way, the strategy can enter the market at an early stage of trend formation and exit in a timely manner when the trend reverses.

#### Advantage Analysis

1. Simple and easy to understand: The indicators used in this strategy are simple, the principle is clear, and it is easy to understand and implement.

2. Trend tracking: By using two moving averages with different periods, the strategy can effectively capture the trend direction of the market and enter in a timely manner when the trend is formed.

3. Timely stop-loss: When the trend reverses, the strategy can close positions in a timely manner through the signal of crossing below the EMA, controlling losses.

4. Strong adaptability: This strategy can be applied to different markets and varieties, and has good adaptability.

#### Risk Analysis

1. Oscillating market: In the case of market oscillation, this strategy may generate more trading signals, leading to frequent trades and higher transaction costs.

2. Lag: Since moving averages are lagging indicators, the buy and sell signals of the strategy may have a certain delay and miss the best trading opportunities.

3. Parameter optimization: The performance of the strategy will be affected by the choice of moving average periods, and different parameters may lead to different results.

#### Optimization Direction

1. Parameter optimization: By optimizing the period parameters of SMA and EMA, the best parameter combination can be found to improve the performance of the strategy.

2. Trend filtering: When generating trading signals, other trend indicators or price behavior patterns can be introduced to further confirm the strength and persistence of the trend, improving the reliability of the signals.

3. Risk control: Stop-loss and take-profit mechanisms can be introduced to control the risk exposure of a single transaction; position management can also be used to dynamically adjust the position size according to market volatility, reducing the overall risk of the strategy.

4. Long-short timing: When generating buy and sell signals, other timing indicators or market sentiment indicators can be combined to assess the strength of both long and short sides, and choose the more advantageous direction for trading.

#### Summary

The BMSB Breakout Strategy is a simple and easy-to-use trend tracking strategy that uses two moving averages with different periods to determine the market trend, entering the market in a timely manner when the trend is formed, and exiting in a timely manner when the trend reverses. The advantages of this strategy are simplicity, ease of understanding, and strong adaptability. At the same time, it also has risks such as frequent trading in oscillating markets and lagging signals. Through parameter optimization, trend filtering, risk control, and long-short timing, the performance and stability of this strategy can be further improved.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-01 00:00:00
end: 2024-04-30 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("BMSB Breakout Strategy", overlay=true)

// Definición de la BMSB
smaLength = 20
emaLength = 21
source = close
sma = ta.sma(source, smaLength)
ema = ta.ema(source, emaLength)

outSma = request.security(syminfo.tickerid, timeframe.period, sma)
outEma = request.security(syminfo.tickerid, timeframe.period, ema)

smaPlot = plot(outSma, color=color.new(color.red, 0), title='20w SMA')
emaPlot = plot(outEma, color=color.new(color.green, 0), title='21w EMA')

fill(smaPlot, emaPlot, color=color.new(color.orange, 75), fillgaps=true)

// Señales de Compra y Venta
buySignal = ta.crossover(close, outSma)
sellSignal = ta.crossunder(close, outEma)

// Lógica de la Estrategia
if (buySignal)
    if (strategy.opentrades > 0)
        strategy.close_all()
    strategy.entry("Buy", strategy.long)

if (sellSignal)
    if (strategy.opentrades > 0)
        strategy.close_all()
    strategy.entry("Sell", strategy.short)

plotshape(series=buySignal, title="Compra", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(series=sellSignal, title="Venta", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)

```

> Detail

https://www.fmz.com/strategy/451528

> Last Modified

2024-05-15 16:40:40

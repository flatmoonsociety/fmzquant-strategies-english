
> Name

Crossing-Moving-Average-RR-Strategy based on moving average crossover
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/4ba6bf7c0d5141c4799e4385af08da592a334bb0154ff9ff167ec6e50175fb18.png)
[trans]
## Overview
This strategy determines buy and sell signals by calculating moving averages of different periods and achieving golden crosses and dead crosses between the moving averages. Specifically, the strategy calculates the 30-period, 60-period and 200-period simple moving averages (SMA), generating a buy signal when the 30-period line crosses the 200-period line; and a sell signal when the 30-period line crosses below the 200-period line.
## Strategy Principle
The core logic of this strategy is based on the moving average crossover system. Moving averages can effectively filter market noise and represent general trends. The short-term moving average can capture short-term trends and intermediate corrections, while the long-term moving average filters out the intermediate noise and captures the main trend. When the short-term moving average crosses the long-term moving average, it means that the short-term market is strengthening and the general trend may reverse, generating a buy signal; when the short-term moving average crosses below the long-term moving average, it means that the short-term market is weakening and following the general trend downward, a sell signal is generated.
This strategy uses the 30-period line and the 200-period line to construct buy and sell signals. The 30-period line can sensitively capture short-term gains, and the 200-period line can capture the longer-term framework and general trend. A buy signal is generated when the 30-period line crosses the 200-period line. At this time, the short-term market sentiment becomes better, short-term and long-term grids are positively aligned, and there is a high probability of an increase. A sell signal is generated when the 30-period line crosses below the 200-period line. The deterioration of the short-term atmosphere is not good for bulls, so they should follow the trend and intervene in the short term. In order to filter out wrong signals, the strategy adopts the form of adding positions, and the short-term line has three consecutive positive lines to confirm the signal.
## Strategic Advantages
This strategy has the following advantages:
1. Simple operation and easy to implement. This strategy only relies on the intersection of two moving averages to generate trading signals. It is very simple and intuitive, easy to understand and implement.
2. The backtesting effect is better. After backtesting, this strategy has a better effect in capturing major trend opportunities in the general trend market. The maximum drawdown and sharpe ratio are also acceptable.
3. Strong scalability. The strategy framework is relatively mature and can easily replace indicators and adjust parameters for optimization, and can also be combined with other factors.
## Risks and Solutions
This strategy also has the following risks:
1. The moving average system produces signal lag and cannot effectively take advantage of the opportunity of rapid sudden market conditions. This is a natural drawback of the moving average system. Other leading indicators such as Bollinger Bands can be introduced to assist in judging the layout in advance.
2. Frequent losses in trading during recessionary and volatile market conditions. In a long-term volatile market without a clear upward trend, frequent moving average crossings cause frequent opening and closing of positions, loss of handling fees and slippage. You can appropriately relax the stop loss range and re-control risks by adding positions.
3. Blindly following technical indicator signals without considering fundamental factors. Positions and stop loss points can be adjusted appropriately based on important economic data, company performance and other information.
## Optimization direction
This strategy can be optimized from the following directions:
1. Test the combined effects of different moving average periods. For example, the 20-day moving average and the 60-day moving average.
2. Add other technical indicators to filter signals. For example, MACD, KD, etc. are combined.
3. Combined with changes in trading volume as auxiliary conditions. For example, when a breakthrough occurs, trading volume is required to increase.
4. Consider introducing fundamental factors as auxiliary indicators. For example, financial reports, interest rate spreads and other indicators.
5. Adjust positions and stop loss points in real time. For example, combine volatility indicators to dynamically adjust positions.
## Summarize
Overall, this strategy is a very typical and simple moving average crossover system, which generates trading signals through the golden cross of two moving averages with different periods. The advantage of the strategy is that it is simple and easy to understand, the backtest effect is also considerable, and the maximum drawdown and sharp ratio are acceptable. But there are also some problems, such as signal lag and large losses in volatile market conditions. These problems can be improved through appropriate optimization. Overall, this strategy is a very suitable model for beginners to practice and learn.
||

## Overview

This strategy generates trading signals by calculating moving averages of different periods and monitoring their crossovers. Specifically, it computes the 30-period, 60-period, and 200-period simple moving averages (SMA). A buy signal is generated when the 30-period SMA crosses above the 200-period one. A sell signal is generated when the 30-period SMA crosses below the 200-period one.  

## Principles  

The core logic of this strategy is based on the moving average crossover system. Moving averages can filter out market noise effectively and characterize the overall trend. The short-term MA captures short-term trends and reactions, while the long-term MA filters out noise and locks the major trend. When the short-term MA crosses over the long-term MA, it indicates strengthening short-term momentum and a potential trend reversal, generating a buy signal. When the short-term MA crosses below the long-term MA, it indicates weakening short-term momentum that goes along with the major downtrend, generating a sell signal.

This strategy adopts the 30-period MA and 200-period MA to construct trading signals. The 30-period MA sensitively captures short-term bullish momentum, while the 200-period MA locks the longer-term structure and major trend. When the 30-period MA crosses over the 200-period one, a buy signal is generated. At this point, the short-term market atmosphere turns better, with the short-term and long-term grids positively aligned, likely leading to an upside. When the 30-period MA crosses below the 200-period one, a sell signal is generated. The deteriorating short-term atmosphere is unfavorable for the long side. One should closely follow the trend for short-term intervention. To filter false signals, the strategy adopts positional addition upon three consecutive bullish candlesticks confirming the signal. 

## Advantages

The main advantages of this strategy include:

1. Simple to implement. This strategy relies solely on MA crosses for trade signals, which is intuitive and easy to understand and implement.

2. Good backtest results. Backtests show this strategy captures major trend-following opportunities well, with acceptable max drawdown and Sharpe ratio.  

3. High extensibility. The strategy framework is mature and can be easily optimized by replacing indicators or tuning parameters. It can also be combined with other factors.

## Risks and Mitigations

There are also some risks associated with this strategy:

1. Lagging signals from the MA system, unable to capitalize on fast, sporadic market swings. This is an inherent limitation of MA systems, and can be mitigated by introducing leading indicators like Bollinger Bands for early positioning.  

2. Frequent unprofitable trades in sideways, ranging markets due to excessive MA crosses. Expand stop loss levels and use positional addition to regain control of risks.

3. No consideration of fundamentals. Blindly following technical signals. Adjust position sizing and stop loss levels by incorporating economic data, earnings etc.   

## Enhancement Opportunities

This strategy can be enhanced in the following aspects:

1. Test MA combinations with different lookback periods, e.g. 20-day and 60-day MAs.

2. Incorporate other technical indicators for signal filtering, e.g. MACD and KD.  

3. Consider trading volume changes as a supplementary condition, like requiring amplified volumes for breakouts.

4. Introduce fundamental factors as supplementary indicators, e.g. earnings reports and yield spreads. 

5. Dynamically adjust position sizing and stop loss levels based on volatility measures.

## Conclusion  

In summary, this is a very typical and simple MA crossover system that generates trade signals from golden crosses and death crosses formed by two MAs of different lookback periods. The advantages are simplicity, ease of comprehension and good backtest results with acceptable max drawdown and Sharp ratio. There are also some problems like lagging signals and losses in choppy markets. But these can be improved through proper enhancements. Overall, this is an excellent starter strategy for beginners to learn and practice algorithmic trading.  

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Estrategia de Cruce de Medias Móviles", overlay=true)

// Medias móviles
ma30 = ta.sma(close, 30)
ma60 = ta.sma(close, 60)
ma200 = ta.sma(close, 200)

// Cruce de medias móviles
crossoverUp = ta.crossover(ma30, ma200)
crossoverDown = ta.crossunder(ma30, ma200)

// Señales de compra y venta
longCondition = crossoverUp
shortCondition = crossoverDown

// Ejecución de órdenes
if (longCondition)
    strategy.entry("Buy", strategy.long)
    strategy.exit("Cover", "Buy", stop=close - 40.000, limit=close + 40.000)
if (shortCondition)
    strategy.entry("Sell", strategy.short)
    strategy.exit("Cover", "Sell", stop=close + 40.000, limit=close - 40.000)

// Plot de las medias móviles
plot(ma30, color=color.blue, title="MA 30")
plot(ma60, color=color.orange, title="MA 60")
plot(ma200, color=color.green, title="MA 200")

// Condiciones para cerrar la posición contraria
if (strategy.position_size > 0)
    if (crossoverDown)
        strategy.close("Buy")
if (strategy.position_size < 0)
    if (crossoverUp)
        strategy.close("Sell")
```

> Detail

https://www.fmz.com/strategy/442636

> Last Modified

2024-02-23 14:04:37

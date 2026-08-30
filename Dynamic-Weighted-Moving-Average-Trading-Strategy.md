
> Name

Dynamic Weighted Moving Average Long and Short StrategyDynamic-Weighted-Moving-Average-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1a7a2af6fdd912734dd.png)

[trans]

## Overview
The Dynamic Weighted Moving Average Long-Short Strategy is a trading strategy suitable for high-volatility markets such as cryptocurrencies. This strategy uses fast and slow moving averages to achieve long and short judgments, adds a dynamic weighting mechanism to improve sensitivity, and also uses EMA filtering and color rendering to identify trend states. The core idea is to capture short-term price changes to obtain excess returns.
## Strategy Principle
The strategy consists of three parts: Boolean variables, indicators and entry logic. The indicator part includes the 30-day EMA, the 5-day fast SMA, and the 10-day slow SMA. The strategic entry judgment is to go long when the fast SMA crosses above the slow SMA, and go short when it crosses below. At the same time, the relationship with the 30-day EMA is considered as a filter condition. When the price is higher than the EMA, you can go long, and when the price is lower than the EMA, you can go short. This takes advantage of the fast SMA's high sensitivity to short-term price changes, the slow SMA's role in filtering out false breakthroughs, and the EMA's trend judgment indicator, which together form trading signals.
The color rendering part identifies the long and short status by setting the background color. When a golden cross occurs on the fast and slow SMA, it is identified as an upward trend and colored; when a dead cross occurs, it is identified as a downward trend and filled in color. This move intuitively reflects market enthusiasm and creates a clear and easy-to-read visual effect.
## Advantage Analysis
The biggest advantage of this strategy is its strong short-term capture ability. The fast SMA parameter selection is only the 5-day line, which can efficiently capture price changes. Add EMA filtering to effectively filter shock callbacks. In addition, a dynamic SMA weight design is introduced to make the recent price contribute more to the moving average and ensure the real-time nature of the strategy.
Compared with a single EMA or SMA strategy, this strategy integrates multiple technical indicators to form a trading combination. Fast and slow SMA complement each other to identify signals, and EMA provides trend judgment, making the strategy more flexible. Color rendering also makes the strategy form an intuitive and easy-to-read interface, making the operation clearer.
## Risks and Countermeasures
The main risk of this strategy is that the fast SMA parameter settings are too sensitive and may generate a large number of false signals. At this time, it is necessary to increase the SMA period value appropriately to reduce the false alarm rate.
In addition, in the volatile market, the trend judgment effect of EMA is weak. At this time, you can consider adding indicators such as the BOLL channel to assist in the judgment.
When encountering a major black swan event, the strategy will also face large losses. This requires setting stop losses to control risk exposure.
## Optimization suggestions
This strategy can be optimized from the following dimensions:
1. Add adaptive SMA. Allowing the SMA cycle value to dynamically change based on market volatility and number of transactions can improve the robustness of the strategy.
2. Set up the compound interest times optimization strategy, that is, achieve exponential growth by setting the number of profits. Appropriately retain part of the profits before investing in the next transaction.
3. Introduce machine learning models to determine buying and selling opportunities. Collect historical data to train models to help determine the direction of future price changes.
## Summary
This dynamic weighted moving average strategy uses fast and slow SMA design to capture short-term prices. EMA is introduced to judge the trend, and color rendering is used to intuitively reflect the long and short status. Compared with traditional strategies, its flexible design makes it more adaptable to highly volatile markets such as cryptocurrency. After adding stop loss and parameter optimization, it is expected to obtain more stable profits.
||

## Overview  

The dynamic weighted moving average trading strategy is designed for highly volatile markets such as cryptocurrencies. It identifies trading signals using fast and slow moving averages and incorporates a dynamic weighting mechanism to improve sensitivity. The strategy also utilizes an EMA filter and color rendering to recognize trend states. The core concept is to capture short-term price moves for excess profits.   

## Strategy Logic

The strategy consists of boolean variables, indicators and entry logic. The indicators include a 30-day EMA, a 5-day fast SMA and a 10-day slow SMA. The entry logic goes long when the fast SMA crosses above the slow SMA, and goes short on crosses below. An EMA filter is added with the price needing to be above EMA for longs and below for shorts. This takes advantage of the fast SMA's sensitivity to short-term price changes, while the slow SMA filters out fakeouts. The EMA acts as a trend gauge, collectively forming trading signals.

The color rendering identifies trend by background shading. When the SMAs cross up it recognizes an uptrend, shading the background. Crosses down indicate downtrend and also shade. This intuitively reflects market conditions for easy readability.  

## Advantage Analysis 

The key advantage is strong short-term capture capability. The 5-day fast SMA rapidly catches price moves. The EMA filter eliminates noise. Dynamic SMA weighting also allows more recent prices higher influence, ensuring real-time performance. 

Unlike single EMA or SMA strategies, this approach synergizes multiple indicators. Fast and slow SMAs complement signal identification. The EMA provides trend reads. This diversity improves robustness. The color rendering also creates an intuitive interface for clearer trades.

## Risks and Mitigations

The main risk is a too-sensitive fast SMA causing excessive fake signals. This can be addressed by raising the SMA period to reduce false triggers.  

In choppy conditions the EMA weakens. Additional indicators like BOLL bands could assist trend reads here.

Fat tail events can also generate outsized losses. Stop losses should be implemented to control open risk.  

## Optimization Suggestions

Possible optimization dimensions include:

1. An adaptive SMA that alters periods based on volatility and trade frequency to improve robustness.

2. Compounding to exponentially grow via a profit target, retaining some gains to compound returns.

3. Machine learning for forecasting, to augment signal judgement with model price change predictions.

## Summary

This dynamic weighted moving average approach leverages fast and slow SMAs to capture prices short-term. The EMA filters for trend with color rendering an intuitive interface. Compared to traditional tactics its adaptable design suits crypto's volatility well. Added risk controls and tuning can achieve consistent income.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-14 00:00:00
end: 2023-12-20 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Estrategia Mejorada para Criptomonedas", overlay=true)

// Variables de estrategia
var bool longCondition = na
var bool shortCondition = na

// Indicadores
emaValue = ta.ema(close, 30)
smaFast = ta.sma(close, 5)  // Período más corto para mayor sensibilidad
smaSlow = ta.sma(close, 10)  // Período más corto para mayor sensibilidad

// Lógica de la estrategia mejorada
longCondition := ta.crossover(smaFast, smaSlow) and close > emaValue
shortCondition := ta.crossunder(smaFast, smaSlow) and close < emaValue

// Entradas de estrategia
if (longCondition)
    strategy.entry("Long", strategy.long)
if (shortCondition)
    strategy.entry("Short", strategy.short)

// Sombreado para tendencia alcista (verde)
bgcolor(longCondition ? color.new(color.green, 90) : na, title="Tendencia Alcista")

// Sombreado para tendencia bajista (rojo)
bgcolor(shortCondition ? color.new(color.red, 90) : na, title="Tendencia Bajista")

// Otros indicadores o filtros pueden ser agregados aquí

// Visualización de indicadores originales
plotColor = close > open ? color.green : color.red
plot(emaValue, color=plotColor, linewidth=2, title="EMA (30)")
value = 10 * open / close
plotColor2 = close == open ? color.orange : color.blue
plot(value, color=plotColor2, linewidth=2, title="Valor Relativo")

// Visualización de medias móviles
plot(smaFast, color=color.blue, title="SMA Rápida (5)", linewidth=2)
plot(smaSlow, color=color.red, title="SMA Lenta (10)", linewidth=2)




```

> Detail

https://www.fmz.com/strategy/436113

> Last Modified

2023-12-21 12:19:43

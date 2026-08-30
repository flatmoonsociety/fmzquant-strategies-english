
> Name

Momentum-Oscillation-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f1144a1d86d9d0beb5.png)

[trans]

## Overview
This strategy is based on the Bollinger Bands indicator and combined with the momentum indicator to achieve a combined trading strategy of Bollinger Bands regression and momentum breakthrough. Go long when the price breaks through the midline from below the Bollinger Bands, go short when the price breaks through the midline from above the Bollinger Bands, track the stop loss and take profit conditions, and close the position after reaching the target profit-loss ratio.
## Strategy Principle
This strategy uses the middle line SMA of Bollinger Bands as the moving average indicator, and the bandwidth is dynamically adjusted through the parameter mult*stdev. When the price breaks through the midline from below, it means that the price has gained upward movement, and you will go long; when the price breaks through the midline from above, it means that the price has gained downward movement, and you will go short. Set take-profit and stop-loss parameters after long and short positions to track profits and control risks.
Specifically, the calculation of Bollinger Bands is completed through two parameters: length and mult. The length determines the period of the midline, and mult determines the size of the bandwidth. enterLong and enterShort determine the timing of breakthrough, and exitLong and exitShort calculate the stop-loss and take-profit price based on the entry price and the target take-profit and stop-loss ratio.
## Strategic Advantages
This strategy combines moving average regression and momentum indicators, which can capture larger market prices at the beginning of the trend. Compared with simply tracking the moving average, momentum judgment based on the width of Bollinger Bands is added, which can filter out some false breakthroughs. Take profit and stop loss settings are calculated directly based on the entry price without manual intervention.
## Strategy Risk
- There is a lag when Bollinger Bands fit prices, and part of the market may be missed.
- Stop loss settings that are too loose will increase the risk of loss
- Short selling signals in a long market may not be well received
It can be optimized by adjusting the Bollinger midline cycle, bandwidth parameters and stop loss range to make the strategy more adaptable to different market conditions.
## Strategy optimization
- Add trading volume or volatility indicators to avoid low-volume false breakthroughs
- Param optimizes Bollinger cycle length, width coefficient, and stop loss width in batches
- Only go long or only go short during a specific market phase
- Add machine learning model to determine trend direction
## Summarize
This strategy integrates the advantages of Bollinger Band regression and momentum indicators. It can capture part of the market at the beginning of the trend. It can adapt to the market at different stages through parameter adjustment. It is a more general breakthrough system. Take profit and stop loss settings are calculated directly from the price to reduce manual intervention. There is also some room for improvement in this strategy, such as adding more auxiliary decision indicators, etc., which will be further improved in subsequent research and optimization.
||

## Overview  

This strategy is based on the Bollinger Bands indicator, combined with momentum indicators to implement a combination trading strategy of Bollinger Bands reversion and momentum breakout. It goes long when the price breaks through the middle line of the Bollinger Bands from below and goes short when the price breaks through the middle line from above. It also tracks stop loss and take profit based on entry price to close positions when target risk-reward ratio is met.

## Strategy Logic

The strategy uses Bollinger Bands middle line sma as the moving average indicator, and dynamically adjusts the band width through param mult*stdev. When price breaks through the middle line from below, it indicates upward momentum is gained and thus goes long. When price breaks down through the middle line from above, it shows downward momentum is gained and thus goes short. After entering long/short positions, stop loss and take profit parameters are set to track profits and control risks.   

Specifically, Bollinger Bands are calculated with two parameters - length and mult. Length determines the period of the middle line and mult decides the band width. enterLong and enterShort judge the breakout timing. exitLong and exitShort calculate stop loss and take profit prices based on entry price and target percentage.

## Advantages  

This strategy combines reversion to the mean and momentum, which enables it to capture major trends early on. Compared to simply tracking moving averages, the added momentum judgment based on Bollinger Bands width can filter out some false breakouts. Stop loss and take profit are set directly based on entry price without manual intervention.  

## Risks  

- Lagging in Bollinger Bands fitting prices, may miss some moves
- Stop loss set too wide may increase loss risks 
- Short signals in bull market may not turn out well

Parameters like periods, band width and stop loss range can be optimized to make the strategy adaptable to different market conditions.  

## Enhancement  

- Add trading volume or volatility to avoid low volume false breakouts
- Param grid search to optimize periods, width coefficient and stop loss percentage 
- Go only long or short based on market regime
- Add Machine Learning model to determine trend direction  

## Conclusion   

This strategy combines the strengths of Bollinger Bands reversion and momentum, which enables it to capture some trends early on. Through parameter tuning it can adapt to different market stages. The direct stop loss/take profit calculation reduces manual intervention. There is still room for improvement, e.g. incorporating more auxiliary indicators. These will be incrementally enhanced in further research and optimization.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Length|
|v_input_2|2|Multiplier|
|v_input_3|0.5|Target Percent|
|v_input_4|95|Stop Loss Percent|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-13 00:00:00
end: 2023-11-20 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("BURATINO", overlay=true)

// Входные параметры
length = input(20, minval=1, title="Length")
mult = input(2.0, minval=0.1, maxval=5, title="Multiplier")
target_percent = input(0.5, minval=0.1, title="Target Percent")
stop_loss_percent = input(95, minval=0.1, title="Stop Loss Percent")

// Расчет полос Боллинджера
basis = sma(close, length)
dev = mult * stdev(close, length)
upper = basis + dev
lower = basis - dev

// Переворот снизу вверх через среднюю линию Боллинджера для открытия лонга
enterLong = cross(close, basis) and close[1] < basis[1]

// Переворот сверху вниз через среднюю линию Боллинджера для открытия шорта
enterShort = cross(basis, close) and close[1] > basis[1]

// Закрытие лонга после роста цены на указанный процент или падения на указанный процент
exitLong = close >= strategy.position_avg_price * (1 + (target_percent / 100)) or close <= strategy.position_avg_price * (1 - (stop_loss_percent / 100))

// Закрытие шорта после падения цены на указанный процент или роста на указанный процент
exitShort = close <= strategy.position_avg_price * (1 - (target_percent / 100)) or close >= strategy.position_avg_price * (1 + (stop_loss_percent / 100))

// Управление позициями и ограничениями на открытие противоположных позиций
strategy.entry("Long", strategy.long, when = enterLong and strategy.position_size == 0)
strategy.entry("Short", strategy.short, when = enterShort and strategy.position_size == 0)

strategy.close("Long", when = exitLong)
strategy.close("Short", when = exitShort)

// Визуализация полос Боллинджера
plot(basis, color=color.blue, title="Basis")
plot(upper, color=color.red, title="Upper")
plot(lower, color=color.green, title="Lower")
```

> Detail

https://www.fmz.com/strategy/432804

> Last Modified

2023-11-21 16:57:20

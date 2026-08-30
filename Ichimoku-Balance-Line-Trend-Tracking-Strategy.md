
> Name

Trend tracking strategy based on Ichimoku-Balance-Line-Trend-Tracking-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy uses the Conversion Line, Base Line and the leading and trailing lines of the line cloud in the Ichimoku Kinko Hyo indicator to identify the trend direction of the price and implement trend following transactions. Go long when the price breaks through the cloud top, go short when it breaks through the cloud bottom, take profit when it reaches the preset profit ratio, and stop loss when it reaches the preset loss ratio.
## Strategy Principle
This strategy mainly uses the following Ichimoku indicator lines:
- Conversion Line (Tenkan-sen): Conversion line, which represents the short-term trend and is the average of the highest and lowest prices in 9 periods
- Base Line (Kijun-sen): The base line represents the mid-term trend and is the average of the highest and lowest prices in 26 periods.
- Leading Span A (Senkou Span A): Leading Span A is the average of the conversion line and the baseline
- Leading Span B (Senkou Span B): Leading Span B is the average of the highest and lowest prices in 52 periods
When the price crosses the front line cloud above, go long; when the price crosses the front line cloud below, go short. ConfigEntry and ExitReason open positions when they break through the cloud top and cloud bottom respectively, and close when they reach the profit and loss ratio.
## Advantage Analysis
- Use the Ichimoku indicator to identify the trend direction and avoid being misled by market fluctuations
- Use the method of breaking through the cloud top/cloud bottom to identify trend turning points and improve trading efficiency
- Set take-profit and stop-loss points to help seize profit opportunities and control risks
## Risk Analysis
- The Ichimoku indicator lags and may miss the best point for a trend turning point
- Parameter periods need to be set appropriately. Improper period settings such as conversion lines, baselines, etc. may lead to false signals.
- If the stop loss point is set too small, the loss may be stopped prematurely; if the stop loss point is set too large, the loss may be expanded.
## Optimization direction
- Consider combining other indicators to identify trends and improve accuracy
- Dynamically optimize parameter cycles to adapt to different cycles and market environments
- Set a trailing stop and let the stop loss point adjust according to price fluctuations to avoid premature stop loss
- Consider developing automatic take-profit and stop-loss strategies to intelligently adjust take-profit and stop-loss points based on market volatility
## Summarize
This strategy uses the Ichimoku cloud to identify trend directions and conduct trend following trades simply and effectively. Although there is a certain risk of lag and false signals, improvements can be achieved through parameter optimization, stop loss technology improvement, and combination with other indicators. This strategy is easy to understand and implement, suitable for beginners to learn, and can also be used as a reference for other strategies. Through continuous testing and optimization, the strategy parameters and rules can be made more perfect, and better performance can be obtained in the real market.
||


## Overview

This strategy uses the Conversion Line, Base Line and cloud boundaries from the Ichimoku Kinko Hyo indicator to identify the trend direction and implement trend tracking trades. It goes long when price breaks above the cloud top and goes short when price breaks below the cloud bottom. Profits are taken when a preset profit ratio is reached. Losses are cut when a preset loss ratio is reached.

## Strategy Logic

The strategy primarily utilizes the following Ichimoku indicator lines:

- Conversion Line (Tenkan-sen): Represents short-term trend, calculated as the average of the highest high and lowest low over the past 9 periods
- Base Line (Kijun-sen): Represents medium-term trend, calculated as the average of the highest high and lowest low over the past 26 periods  
- Leading Span A (Senkou Span A): The mean of the Conversion and Base Lines
- Leading Span B (Senkou Span B): The average of the highest high and lowest low over the past 52 periods

It goes long when price breaks above the cloud and goes short when price breaks below the cloud. Entry and Exit reasons are triggered when price breaks the cloud top and bottom respectively. Exits are triggered when profit or loss ratios are reached.

## Advantage Analysis

- Uses Ichimoku to identify trend direction, avoiding false signals from market noise
- Breaking cloud top/bottom identifies trend reversal points efficiently 
- Take profit and stop loss points help lock in profits and control risk

## Risk Analysis

- Ichimoku has lag and may miss best entry points 
- Poor parameter tuning of lines like Conversion Line could cause false signals
- Stop loss set too tight risks early exit; too loose risks large losses

## Optimization Directions

- Consider combining other indicators to improve accuracy
- Dynamically optimize parameters for different periods and markets
- Use trailing stop loss to adjust stops based on price action and avoid early exit
- Develop automated profit/loss strategy to intelligently adjust points based on volatility

## Summary

This strategy uses Ichimoku cloud to identify trends and implement simple trend tracking. Despite some lag and false signals, optimizations in parameters, stops, and using other indicators can improve it. Easy to understand and implement, it's good for beginners to learn from and reference when developing other strategies. Continuous testing and optimizations will improve parameters and rules for better live performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|Tenkan-sen (Linha de Conversão)|
|v_input_2|26|Kijun-sen (Linha Base)|
|v_input_3|52|Senkou Span B (Nível adiantado B)|
|v_input_4|26|Deslocamento|
|v_input_5|5|Goal (%)|
|v_input_6|0.5|Stop (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-04 00:00:00
end: 2023-10-08 00:00:00
period: 5m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Estratégia com Ichimoku" , pyramiding=0, calc_on_every_tick = true, initial_capital = 20000, commission_type = strategy.commission.cash_per_order, commission_value = 10.00)

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
/////////////////////////////////////////////////////////////////Ichimoku Clouds////////////////////////////////////////////////////////////////
/////////////////////////////////////////////////////////////////(VERSÃO 40.0)//////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

periodoLinhaDeConversao = input(defval=9, title="Tenkan-sen (Linha de Conversão)",  minval=1)
periodoLinhaBase = input(defval=26, title="Kijun-sen (Linha Base)",  minval=1)
periodoNivelAdiantadoB = input(defval=52, title="Senkou Span B (Nível adiantado B)",  minval=1)
deslocamento = input(defval=26, title="Deslocamento",  minval=1)

linhaDeConversao = (highest(high,periodoLinhaDeConversao)+lowest(low,periodoLinhaDeConversao))/2
linhaBase = (highest(high,periodoLinhaBase)+lowest(low,periodoLinhaBase))/2
nivelAdiantadoA = (linhaDeConversao + linhaBase)/2
nivelAdiantadoB = (highest(high,periodoNivelAdiantadoB)+lowest(low,periodoNivelAdiantadoB))/2

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
strategy.initial_capital = 50000
//Hardcoded quantity - strategy.entry(qty=)
capitalInicial = strategy.initial_capital
lotes = (strategy.initial_capital - (strategy.initial_capital % (open*100)))/open

//Percentage input goal - strategy.exit(profit=)
percentGoal = input (defval = 5.0, title = "Goal (%)", type = float, minval=0.0, step=0.1)
longGoal = (strategy.position_avg_price * (percentGoal/100)) * 100
shortGoal = (strategy.position_avg_price - (strategy.position_avg_price / (1+(percentGoal/100)))) * 100

//Percentage input stop - strategy.exit(loss=)
percentStop = input (defval = 0.5, title = "Stop (%)", type = float, minval=0.0, step=0.1)
longStop = (strategy.position_avg_price * (percentStop/100)) * 100
shortStop = (strategy.position_avg_price * (percentStop/100)) * 100

strategy.entry('entryLong', strategy.long, lotes, when = strategy.position_size == 0 and crossover(close,max(nivelAdiantadoA[deslocamento], nivelAdiantadoB[deslocamento])))
strategy.entry('entryShort', strategy.short, lotes, when = strategy.position_size == 0 and crossunder(close,min(nivelAdiantadoA[deslocamento], nivelAdiantadoB[deslocamento])))
strategy.exit('exitLong', 'entryLong', profit = longGoal, loss = longStop)
strategy.exit('exitShort', 'entryShort', profit = shortGoal, loss = shortStop)

plot(strategy.equity, title="Variação de capital", color=white)
//plot(strategy.position_size, color=red)
```

> Detail

https://www.fmz.com/strategy/429084

> Last Modified

2023-10-12 17:29:46

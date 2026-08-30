
> Name

Trend Following Strategy Based on Moving Average Crossover Moving-Average-Crossover-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/bd8e872263f9a8b707.png)
[trans]
## Overview
This strategy implements trend tracking by calculating moving averages of different periods and setting their intersections as buy and sell signals. The core logic is to use shorter-period moving averages to track turning points in longer-period trends.
## Strategy Principle
1. Calculate 200-period and 100-period moving averages
2. When the 100-period moving average crosses the 200-period moving average, go long
3. When the 100-period moving average crosses below the 200-period moving average, close the long position
4. When the 100-period moving average crosses below the 200-period moving average, go short
5. When the 100-period moving average crosses the 200-period moving average, close the short position
The logic behind the above trading signal settings is that short-period moving averages can respond to price changes faster and reflect the latest trends; long-period moving averages can better reflect the overall trend and filter out noise. When the short-period moving average crosses the long-period moving average, it indicates that the trend has turned, so a trading signal is set.
## Strategic advantage analysis
1. The strategic ideas are clear and simple, easy to understand and implement
2. Through the combination of long and short cycle lines, you can seize the turning point of the trend and the effect is better.
3. There is no need to predict the specific price direction, only tracking trend turning points, reducing the error rate.
4. Can adapt to different market environments by optimizing the moving average cycle
## Analysis of strategic risks and solutions
1. When the trend fluctuates greatly, multiple false signals may occur, leading to losses. The solution is to appropriately adjust the moving average period parameters.
2. When emergencies lead to rapid reversals, the simple moving average strategy cannot respond in time and is prone to losses. The solution is to add additional judgment indicators, such as increase indicators. 
3. The number of transactions may be too frequent, increasing transaction costs and slippage losses. The solution is to appropriately adjust the moving average cycle parameters and reduce the frequency of transactions.
## Strategy optimization direction
1. Optimize the moving average cycle parameter combination to adapt to more market conditions
2. Add filtering indicators to avoid false signals, such as trading volume, MACD, etc.
3. Add stop-loss and stop-profit strategies to control single profit and loss
4. Carry out parameter combination optimization and find the optimal parameters
## Summarize
This strategy uses a simple moving average crossover to capture changes in price trends and is a typical trend following strategy. The advantage is that it is simple to understand and operate, and can be adapted to a variety of market environments by adjusting parameters. The disadvantage is that it is not responsive to emergencies and easily generates false signals. Overall, this strategy has a clear idea and is one of the introductory strategies for quantitative trading. However, when applying it in real trading, you need to pay attention to risk control and carry out appropriate optimization.
|| 

## Overview

This strategy generates trading signals by calculating moving averages of different periods and using their crossover as buy and sell signals to follow the trend. The core logic is to use a shorter period moving average to track the turning points of a longer period trend.  

## Strategy Principle  

1. Calculate the 200-period and 100-period moving averages
2. When the 100-period MA crosses above the 200-period MA, go long
3. When the 100-period MA crosses below the 200-period MA, close long position
4. When the 100-period MA crosses below the 200-period MA, go short
5. When the 100-period MA crosses above the 200-period MA, close short position

The logic behind the trading signals is that the shorter period MA can respond to price changes faster and reflect the latest trend, while the longer period MA can better represent the overall trend and filter out noise. When the shorter MA crosses the longer MA, it indicates a trend reversal, so trading signals are triggered.  

## Advantage Analysis

1. The strategy idea is simple and clear, easy to understand and implement
2. Catching trend turning points through long and short period MA combination works well 
3. No need to predict specific price direction, just follow trend reversals, lower error rate
4. Can optimize MA periods to adapt to different market environments

## Risks and Solutions

1. Too many false signals when trend fluctuates greatly. Solution is to adjust MA periods properly.  
2. Fail to respond fast on sudden reversals. Solution is to add confirming indicators like volume.
3. Potentially too frequent trading, increasing costs. Solution is to adjust periods to lower frequency.  

## Optimization Directions  

1. Optimize MA period combinations to adapt more markets
2. Add filters like volume and MACD to avoid false signals 
3. Add stop loss and take profit to control single trade risk
4. Parameter combination optimization to find optimum

## Summary  

This strategy catches trend changes by simple MA crossovers. It belongs to typical trend following strategies. The pros are being simple, easy to use and adaptable by parameter tuning. The cons are slow reaction and false signals. Overall it has a clear logic and is a good starting point for algo trading. Proper risk management and optimization are needed for live trading.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-23 00:00:00
end: 2024-02-29 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("MA Crossover Strategy", overlay=true)

// Функция для получения скользящего среднего на заданном таймфрейме
getMA(source, length, timeframe) =>
    request.security(syminfo.tickerid, timeframe, ta.sma(source, length))

// Вычисляем 200-периодное и 100-периодное скользящее среднее для текущего таймфрейма
ma200 = getMA(close, 200, "240")
ma100 = getMA(close, 100, "240")

// Открываем позицию Long, если 100-периодное скользящее среднее пересекает 200-периодное сверху вниз
if (ta.crossover(ma100, ma200))
    strategy.entry("Long", strategy.long)

// Закрываем позицию Long, если 100-периодное скользящее среднее пересекает 200-периодное сверху вниз
if (ta.crossunder(ma100, ma200))
    strategy.close("Long")

// Открываем позицию Short, если 100-периодное скользящее среднее пересекает 200-периодное сверху вниз
if (ta.crossunder(ma100, ma200))
    strategy.entry("Short", strategy.short)

// Закрываем позицию Short, если 100-периодное скользящее среднее пересекает 200-периодное снизу вверх
if (ta.crossover(ma100, ma200))
    strategy.close("Short")

// Рисуем линии скользящих средних на графике
plot(ma200, color=color.blue, linewidth=2, title="200 MA")
plot(ma100, color=color.red, linewidth=2, title="100 MA")

```

> Detail

https://www.fmz.com/strategy/443230

> Last Modified

2024-03-01 10:59:03

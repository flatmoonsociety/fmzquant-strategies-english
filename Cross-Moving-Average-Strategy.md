
> Name

Cross-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/145e88392f14eb11f35.png)
[trans]

## Overview
This strategy determines the timing of entry and exit by calculating the golden cross of the fast moving average and the slow moving average. When the fast line crosses the slow line from below, go long; when the fast line crosses the slow line from above, go short.
## Strategy Principle
This strategy is mainly based on the golden cross and dead cross principle of the moving average. Calculate a fast moving average of length 3, and a slow moving average of length 266. When the fast line crosses the slow line from below, a buy signal is generated; when the fast line crosses the slow line from above, a sell signal is generated. After receiving the signal, an entry order is issued on the third K line.
The basis for this strategy to judge the trend is that when the price rises, the short-term moving average moves up more quickly; when the price falls, the short-term moving average moves down more quickly. Therefore, there will be a crossing between the short-term fast line and the long-term slow line.
## Advantage Analysis
The biggest advantage of this strategy is that it calculates moving averages of different length periods and uses the golden cross and dead cross relationships between them to determine the trend turning point. Compared with a single moving average and other indicators, it can capture price turning points more accurately.
First of all, the fast moving average can capture price changes more sensitively, while the slow moving average plays a role in filtering noise and can effectively identify the trend direction. Use two moving averages together to avoid generating false signals.
Secondly, this strategy adopts a lagging entry method, that is, entering the market on the third K line after the signal is generated. This can further avoid erroneous trades due to moving average fluctuations.
Furthermore, the parameter selection is reasonable and simple. Judgment can be completed by relying only on two moving averages, without the need to calculate complicated indicators, which reduces the possibility of over-optimization.
## Risk Analysis
Although this strategy has no obvious flaws or risks, you still need to pay attention to a few points when using it in real terms:
First of all, relying solely on the moving average as a trend judgment indicator may miss entry opportunities judged by other indicators. You can consider appropriately adding alternative indicators and making comprehensive judgments.
Secondly, in a strong trend, the price may run above or below the fast line for an extended period of time. At this time, there will be a situation where no signal is generated for a long time. The parameters need to be adjusted to make the express line closer to the price.
Thirdly, the indicator parameters are not 100% reliable, and the optimal parameters will be different under different varieties and cycles. It needs to be continuously tested and optimized based on actual feedback.
Finally, the trading lot size, stop loss point and take profit point also need to be accurately evaluated to avoid excessive losses or failure to take profits in time.
## Optimization direction
This strategy also has several main optimization directions:
First, you can consider adding the judgment logic of other auxiliary indicators when the golden cross is dead. For example, when the RSI indicator shows overbought and oversold, it further confirms the trading signal.
Second, parameter optimization is crucial. Factors such as cycles and trading types can be comprehensively considered, and parameters can be continuously tested and adjusted through historical backtesting and simulated real trading methods to make the strategy more adaptable to the market environment.
Third, optimize the entry method. In addition to the simple third K-line entry, you can also study the methods of lagging 'N' K-line entry, price difference entry, breakthrough new high and new low entry, etc. The specific situation can be fine-tuned according to the variety and cycle.
Finally, it is equally important to improve the stop-loss and take-profit methods. You can combine the volatility ATR indicator to adjust the stop-profit and stop-loss ranges in real time. In addition, methods such as trailing stop loss and batch take profit are also worth considering. These will significantly increase strategic profitability.
## Summarize
This strategy uses the classic principle of moving average golden crosses and dead crosses to determine the future direction of prices, generates trading signals through reasonable parameter settings, and uses delayed entry and stop-loss and take-profit methods to control risks. It is a simple and practical quantitative trading strategy. It has the potential for further improvement in many aspects such as optimizing indicator parameters, improving the indicator system, and adjusting entry and exit logic.
||


## Overview

This strategy judges entry and exit points by calculating the golden cross and death cross between fast and slow moving average lines. It goes long when the fast line crosses above the slow line, and goes short when the fast line crosses below the slow line.

## Principles

The strategy is mainly based on the golden cross and death cross principles of moving averages. It calculates a fast moving average line with a length of 3 and a slow moving average line with a length of 266. A buy signal is generated when the fast line crosses above the slow line, and a sell signal is generated when the fast line crosses below the slow line. It enters the market on the third candlestick after the signal is received.

The basis for this strategy to judge the trend is that when prices rise, the short-term moving average line moves up faster; when prices fall, the short-term moving average line moves down faster. Thus crossovers between the short-term fast line and the long-term slow line will occur.  

## Advantage Analysis 

The biggest advantage of this strategy is that it uses the golden cross and death cross relationship between moving averages of different cycle lengths to determine trend reversal points. Compared with a single moving average line and other indicators, it can more accurately capture price turns.

Firstly, the fast moving average line can more sensitively capture price changes, while the slow moving average line plays the role of filtering out noise and can effectively identify the trend direction. The two lines work together to avoid generating false signals.

Secondly, the strategy adopts a lagged entry method, i.e. entering the market on the third candlestick after the signal is generated. This can further avoid wrong trades caused by moving average oscillations.

Moreover, the parameter selection is reasonable and simple. It only relies on two moving average lines to complete the judgment, without calculating complex indicators, thus reducing the possibility of over-optimization.

## Risk Analysis  

Although the strategy has no obvious flaws and risks, several points still need to be noted when used for live trading:

Firstly, relying solely on the moving average as the trend judging indicator may miss trading opportunities identified by other indicators. It is advisable to appropriately include alternative indicators for combined judgment.

Secondly, in a strong trend, prices may run for a long time above or below the fast line. This will result in long periods without signal generation. Parameters need to be adjusted to make the fast line closer to prices. 

Also, indicator parameters are not 100% reliable. The optimal parameters may vary across different products and cycle periods. Continual testing and optimization based on live trading feedback are necessities.

Lastly, accurate assessment on trading size, stop loss and take profit levels is also important to avoid excessive losses or failure to take profits timely.

## Optimization Directions

There are several major optimization directions for this strategy:

Firstly, consider adding judgment logics from other auxiliary indicators together with golden crosses and death crosses. For example, further confirm trading signals when RSI indicator shows overbought or oversold conditions. 

Secondly, parameter optimization is crucial. Comprehensive considerations can be given to cycle, product variety and other factors. Keep testing and adjusting parameters through historical backtests and demo trading to make the strategy more adaptive to market conditions.

Thirdly, optimize entry methods. Apart from simple third candlestick entry, study lagging entry after ‘N’ candlesticks, price spread entry, breakout entry, etc. Details should be fine tuned according to different products and cycle periods.

Lastly, improving stop loss and take profit methods is equally important. Indicators like ATR can be used to dynamically adjust levels of stop loss and take profit. Moreover, trailing stop loss, partial profit taking and other techniques are also worth studying. These will greatly improve the strategy’s profitability.

## Conclusion

The strategy utilizes the classic principle of using moving average golden crosses and death crosses to determine future price direction. By reasonably setting parameters to generate trading signals and adopting lagging entry and stop loss/take profit methods to control risks, it is a simple, practical quantitative trading strategy. There remains much potential for further improvement in areas like indicator parameter optimization, indicator system enhancement, entry/exit logic adjustment, etc.

[/trans]



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
strategy("Cruzamento de Médias Móveis", overlay=true)

// Definir os parâmetros da estratégia
length_fast = 3
length_slow = 266
price = close
take_profit = 10000.0
stop_loss = 2000.0

// Calcular as médias móveis
fast_ma = vwma(price, length_fast)
slow_ma = sma(price, length_slow)

// Definir as condições de entrada
buy_signal = crossover(fast_ma, slow_ma)
sell_signal = crossunder(fast_ma, slow_ma)

// Enviar ordens de negociação com base nas condições de entrada
if (buy_signal[3]) // Verifica se o sinal de compra ocorreu 3 velas atrás
    strategy.entry("Buy", strategy.long)
    strategy.exit("Sell", "Buy", profit=take_profit, loss=stop_loss)

if (sell_signal[3]) // Verifica se o sinal de venda ocorreu 3 velas atrás
    strategy.entry("Sell", strategy.short)
    strategy.exit("Cover", "Sell", profit=take_profit, loss=stop_loss)

// Plotar as médias móveis no gráfico
plot(fast_ma, color=color.rgb(238, 0, 0))
plot(slow_ma, color=color.rgb(0, 132, 240))
```

> Detail

https://www.fmz.com/strategy/432773

> Last Modified

2023-11-21 13:33:20

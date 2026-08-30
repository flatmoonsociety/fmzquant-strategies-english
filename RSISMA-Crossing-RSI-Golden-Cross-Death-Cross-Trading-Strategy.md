
> Name

SMA-Crossing-RSI-Golden-Cross-Death-Cross-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/76bf221aa13311d822e7ffe253944b175182c94d18098cd8518535c7eeff521c.png)

[trans]


## Overview
This strategy combines the moving average and the relative strength indicator RSI, and forms trading signals through the direction of the moving average and the high and low positions of the RSI. It is a typical trend following strategy. It aims to identify undervalued and overvalued opportunities through the RSI indicator, combined with the moving average direction, to build positions at the beginning of the trend.
## Strategy Principle
This strategy is mainly based on two indicators:
1. Simple Moving Average SMA: Calculate the average closing price within a certain period and determine the direction of the price trend.
2. Relative Strength Index RSI: By comparing the average closing increase and the average closing decrease over a period of time, you can determine whether the current stock price is overvalued or undervalued. An RSI above 70 is an overbought zone, and an RSI below 30 is an oversold zone.
Strategy logic:
1. When the closing price is below the SMA and the RSI indicator breaks down from the oversold area, a buy signal is generated.
2. When the closing price is above the SMA and the RSI indicator breaks above the oversold area, a sell signal is generated.
This strategy combines the moving average to determine the direction of the general trend, and the RSI to determine the overbought and oversold areas, and builds positions at the beginning of the trend. RSI high and low positions can effectively identify short-term value levels, and can be used in combination with the moving average direction to generate lower-risk trading signals.
## Advantage Analysis
This strategy has the following advantages:
1. Combine trend and value judgment to reduce the probability of wrong transactions and make the signal more reliable.
2. After the RSI indicator parameters are optimized, it can effectively identify the overbought and oversold range.
3. After SMA parameters are optimized, the general trend direction can be accurately determined.
4. The trading strategy rules are simple and clear, easy to understand and implement, and suitable for novices to learn.
5. It can be applied to different varieties and cycles, and has a wide range of applications.
6. The strategy performance can be optimized by adjusting SMA and RSI parameters.
## Risk Analysis
This strategy also has the following risks:
1. The SMA moving average is generated lagging behind, and the best opportunity to start the trend may be missed. You can shorten the moving average period appropriately or use EMA.
2. The RSI overbought and oversold areas may be set improperly, resulting in inaccurate signals. Optimization of RSI parameters can be tested.
3. Divergence signals may indicate a trend reversal and require vigilance.
4. In the volatile market, false signals and stop losses may occur, so you may consider reducing your position.
5. Based only on SMA and RSI, other factors are not considered, and more indicator optimization can be introduced.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Test different SMA cycle parameters and select the cycle that produces a more accurate signal.
2. Test RSI overbought and oversold area parameter settings to determine the best parameters.
3. Add other indicator judgments, such as MACD, Bollinger Bands, etc., to improve signal accuracy.
4. Add a stop-loss strategy to control single losses.
5. Evaluate and increase position management strategies, such as fixed shares, etc., to control overall risks.
6. Evaluate the effects on different varieties and cycles and find the best applicable scenarios.
7. Add judgment logic for divergence signals to identify trend reversals.
## Summarize
Overall, this strategy is a typical trend following strategy. It combines trend judgment and overbought and oversold judgment to obtain lower-risk trading signals. Through parameter optimization and rule improvement, the stability and reliability of the strategy can be further enhanced. However, no strategy can be perfect, and investors need to evaluate it based on their own risk preferences and financial strength. In general, this strategy is suitable for investors with certain trading experience as an auxiliary tool for trend trading.

||

## Overview

This strategy combines moving average and relative strength index RSI to generate trading signals based on the direction of MA and the level of RSI. It belongs to a typical trend following strategy. It aims to identify undervalued and overvalued opportunities through RSI and combine with MA direction to establish positions at the beginning of trends.

## Strategy Logic

The strategy is mainly based on two indicators:

1. Simple Moving Average SMA: Calculates the average closing price over a certain period to determine the price trend. 

2. Relative Strength Index RSI: Compares the average gain and average loss over a period to determine if the current price is overbought or oversold. RSI above 70 is overbought zone and below 30 is oversold zone.

Strategy rules:

1. When close is below SMA and RSI crosses below overbought zone, a buy signal is generated.

2. When close is above SMA and RSI crosses above oversold zone, a sell signal is generated.

The strategy combines MA to determine the major trend and RSI to identify overbought and oversold levels, establishing positions at the beginning of trends. RSI high-low levels effectively identify short-term overvaluation and undervaluation. Combining with MA direction generates relatively low-risk trading signals.

## Advantage Analysis 

The strategy has the following advantages:

1. Combining trend and value analysis reduces incorrect trades and makes signals more reliable.

2. Optimized RSI parameters can effectively identify overbought and oversold levels.

3. Optimized SMA parameters accurately determine the major trend.

4. Simple and clear trading rules, easy to understand and implement, suitable for beginners.

5. Can be applied to different products and timeframes, wide applicability. 

6. Can optimize strategy performance by adjusting SMA and RSI parameters.

## Risk Analysis

The strategy also has the following risks:

1. SMA may lag and miss the best timing at the beginning of trends. Can consider shorter SMA period or use EMA.

2. RSI overbought and oversold levels may be improperly set, leading to inaccurate signals. Can test and optimize RSI parameters.

3. Divergence may signal trend reversal, need to be alert. 

4. Whipsaws may generate wrong signals and stop loss in ranging markets. Can consider lowering position size.

5. Based solely on SMA and RSI, other factors not considered. Can introduce more indicators.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Test different SMA periods to find the one that generates more accurate signals.

2. Test RSI overbought/oversold parameter settings to determine optimal values.

3. Add other indicators like MACD, Bollinger Bands to improve signal accuracy.

4. Add stop loss to control loss per trade. 

5. Evaluate position sizing strategies like fixed percentage to manage overall risk.

6. Assess performance across different products and timeframes to find optimal scenarios. 

7. Add logic for divergence to identify trend reversal.

## Conclusion

Overall this is a typical trend following strategy. Combining trend and overbought/oversold analysis provides relatively low risk trading signals. Further improvements through parameter optimization and rule refinement can enhance stability and reliability. However no strategy is perfect and needs evaluation based on risk preference and capital. Generally this strategy suits experienced investors as an auxiliary tool for trend trading.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-17 00:00:00
end: 2023-01-31 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Meu Robo com MA e RSI (Regras Específicas)", overlay=true)

// Configuração da Média Móvel
lengthMA = 200
sma200 = sma(close, lengthMA)

// Configuração do RSI
lengthRSI = 14
rsiValue = rsi(close, lengthRSI)
overBought = 70
overSold = 30

// Condições para compra
longCondition = close < sma200 and crossover(rsiValue, overSold)
if (longCondition)
    strategy.entry("Compra", strategy.long)

// Condições para venda
shortCondition = close > sma200 and crossunder(rsiValue, overBought)
if (shortCondition)
    strategy.close("Compra")

// Plot das Médias Móveis e sinais
plot(sma200, title="SMA 200", color=color.blue)
plotshape(series=longCondition, title="Sinal de Compra", location=location.belowbar, color=color.green, style=shape.labelup, text="Compra")
plotshape(series=shortCondition, title="Sinal de Venda", location=location.abovebar, color=color.red, style=shape.labeldown, text="Venda")

```

> Detail

https://www.fmz.com/strategy/430039

> Last Modified

2023-10-24 14:33:51

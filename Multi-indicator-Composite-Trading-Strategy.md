
> Name

Multi-indicator-Composite-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f7ada776cf2066f922.png)
 [trans]
## Overview
The multi-indicator fusion trading strategy is a composite trading strategy that integrates the analysis of four major indicators: moving average crossover, relative strength indicator, commodity path indicator and stochastic exponential smoothed moving average. This strategy achieves the function of more accurately judging market buying and selling points by judging trend indicator signals in different time periods.
## Strategy Principle
This strategy is mainly judged based on four indicators:
1. MACD: Calculate the difference between the fast moving average and the slow moving average to determine the price movement trend and momentum. When the fast line crosses the slow line, it is a buy signal.
2. RSI: Calculate the rise and fall of stock prices over a period of time. When the RSI is greater than 70, it is overbought, and when it is less than 30, it is oversold. This strategy uses 70 and 30 as the buying and selling standards.
3. CCI: Measures price momentum by calculating the percentage price deviates from its moving average. This strategy uses 100 and -100 as the buying and selling standards.
4. StochRSI: Combines stochastic index indicator and RSI indicator. The golden cross of K line and D line is a buy signal, and the death cross is a sell signal.
When the above four indicators meet the conditions at the same time, this strategy will generate actual buy and sell signals.
## Strategic Advantages
The biggest advantage of this multi-indicator fusion strategy is that it can combine multiple dimensions in the market to determine buying and selling points. Specifically, it mainly has the following advantages:
1. Able to filter out false signals and avoid chasing ups and downs at high levels. The possibility of indicators sending signals at the same time is very small, so that some false signals can be filtered out.
2. Be able to grasp the main trends of the market. Different indicators judge the market from different angles and can judge market trends more comprehensively.
3. There is a large space for optimization of strategy parameters. You can optimize the effect of the strategy by adjusting the parameters of each indicator.
4. The weight can be adjusted according to the market. In a bull market, the weight of trend indicators can be increased, and in a bear market, the weight of reversal indicators can be increased.
## Strategy Risk
This strategy mainly involves the following types of risks:
1. Risk of indicators sending wrong signals. This strategy generates false trades when multiple indicators send false signals at the same time.
2. The risk of violent fluctuations in stock prices. When the market experiences abnormal fluctuations, multiple indicators may send out wrong signals at the same time.
3. Risk of delayed buy signal. When multiple indicators are comprehensively judged, there will be a certain delay in issuing a buy signal.
4. Difficulties and risks in parameter optimization. Multi-index combination optimization parameters are relatively complex, and improper optimization may have counterproductive effects.
The main countermeasures are to adjust indicator parameters, set stop losses, and reduce the amount of funds invested in a single transaction to control risks.
## Optimization direction
This strategy can be further optimized from the following dimensions:
1. Test more combinations of indicators to find the best indicator portfolio. Can test KD, BOLL and other indicators.
2. Optimize the parameters of each indicator to achieve the best overall strategy effect. Optimization can be automated using methods such as machine learning.
3. Set different parameter combinations for different stocks and industries.
4. Add a stop-loss mechanism to the strategy. Automatic stop loss when the price breaks through the support level.
5. Update the stock pool and select outstanding stocks in the subdivided industries. Adjusting the stock pool can improve overall returns.
## Summarize
This strategy integrates the four classic indicators MACD, RSI, CCI and StochRSI, and can effectively identify market buying and selling points by judging signals in multiple time dimensions and setting strict buying and selling standards. This strategy can effectively increase the probability of profit and reduce the probability of stop loss. The strategy effect can be further improved by optimizing parameters, updating the stock pool, and adding stop losses. It is one of the most effective quantitative trading strategies.
||

## Overview  

The multi-indicator composite trading strategy integrates four major indicators: moving average convergence divergence (MACD), relative strength index (RSI), commodity channel index (CCI) and stochastic relative strength index (StochRSI). It is a composite trading strategy that analyzes signals across these four indicators. By judging indicator signals across different timeframes, this strategy can more accurately identify market entry and exit points.

## Strategy Logic

This strategy mainly makes judgments based on four indicators:

1. MACD: Calculates the difference between fast and slow moving averages to judge price momentum and trends. A buy signal is generated when the fast line crosses above the slow line.  

2. RSI: Calculates the magnitude of price changes over a period of time. An RSI above 70 indicates overbought conditions and below 30 oversold. This strategy uses 70 and 30 as thresholds.

3. CCI: Measures price momentum by calculating the percentage deviation of price from its moving average. This strategy uses 100 and -100 as thresholds.  

4. StochRSI: Combines Stochastics and RSI. A golden cross between the StochRSI %K and %D lines signals a buy, while a death cross signals a sell.

Only when all four indicators meet the criteria simultaneously will an actual buy or sell signal be generated.  

## Advantages

The key advantages of this multi-indicator strategy are:

1. Filters false signals by requiring agreement of all indicators, avoiding chasing tops or panic selling bottoms. 

2. Captures primary trends across different dimensions by combining different indicator perspectives.

3. Large parameter optimization space to tune each indicator for overall optimal performance.

4. Weights can be adjusted based on bull or bear markets to focus on trend or mean reversion strategies.

## Risks

The main risks are:

1. Indicators may generate concurrent false signals, triggering incorrect trades.

2. Prices can move violently enough for concurrent false signals across indicators.  

3. Delayed buy signals as indicators align.

4. Difficult to optimize many parameters, possibly overfit.

Mitigations include parameter tuning, stop losses, and position sizing control.

## Enhancement Opportunities

Enhancement opportunities:

1. Test combinations with more indicators like KD, Bollinger Bands to find optimal portfolio.

2. Optimize parameters for highest overall performance, maybe via machine learning.

3. Customize parameters for different stocks and sectors.  

4. Add stop loss mechanisms in strategy code, like selling when price breaches support.

5. Select stocks with strong performance within sectors to improve portfolio returns.

## Conclusion
This strategy integrates signals across four major indicators – MACD, RSI, CCI, and StochRSI. By setting strict entry and exit criteria based on multi-timeframe analysis, it can effectively identify market turning points. Refinements like parameter optimization, updating stock universe, and adding stops can further improve performance. Overall an effective quantitative trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|12|Fast Length|
|v_input_2|26|Slow Length|
|v_input_3|9|Signal Length|
|v_input_4|14|RSI Length|
|v_input_5|70|RSI Overbought Level|
|v_input_6|8|CCI Length|
|v_input_7|100|CCI Overbought Level|
|v_input_8|14|Stoch Length|
|v_input_9|3|Stoch K|
|v_input_10|3|Stoch D|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-01 00:00:00
end: 2023-12-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("MACD RSI CCI StochRSI Strategy", shorttitle="MRCSS", overlay=true)

// MACD göstergesi
fastLength = input(12, title="Fast Length")
slowLength = input(26, title="Slow Length")
signalLength = input(9, title="Signal Length")
[macdLine, signalLine, _] = macd(close, fastLength, slowLength, signalLength)

// RSI göstergesi
rsiLength = input(14, title="RSI Length")
rsiLevel = input(70, title="RSI Overbought Level")
rsiValue = rsi(close, rsiLength)

// CCI göstergesi
cciLength = input(8, title="CCI Length")
cciLevel = input(100, title="CCI Overbought Level")
cciValue = cci(close, cciLength)

// Stochastic Oscillator göstergesi
stochLength = input(14, title="Stoch Length")
stochK = input(3, title="Stoch K")
stochD = input(3, title="Stoch D")
stochValue = stoch(close, high, low, stochLength)
stochDValue = sma(stochValue, stochD)

// Alış ve Satış Sinyalleri
buySignal = crossover(macdLine, signalLine) and rsiValue < rsiLevel and cciValue < cciLevel and stochValue > stochDValue
sellSignal = crossunder(macdLine, signalLine) and rsiValue > (100 - rsiLevel) and cciValue > (100 - cciLevel) and stochValue < stochDValue

// Ticaret stratejisi uygula
strategy.entry("Buy", strategy.long, when = buySignal)
strategy.close("Buy", when = sellSignal)
strategy.entry("Sell", strategy.short, when = sellSignal)
strategy.close("Sell", when = buySignal)

// Göstergeleri çiz
hline(rsiLevel, "RSI Overbought", color=color.red)
hline(100 - rsiLevel, "RSI Oversold", color=color.green)
hline(cciLevel, "CCI Overbought", color=color.red)
hline(100 - cciLevel, "CCI Oversold", color=color.green)

// Grafik üzerinde sinyal okları çiz
plotshape(series=buySignal, title="Buy Signal", color=color.green, style=shape.triangleup, location=location.belowbar, size=size.small)
plotshape(series=sellSignal, title="Sell Signal", color=color.red, style=shape.triangledown, location=location.abovebar, size=size.small)

```

> Detail

https://www.fmz.com/strategy/440297

> Last Modified

2024-01-29 10:06:25

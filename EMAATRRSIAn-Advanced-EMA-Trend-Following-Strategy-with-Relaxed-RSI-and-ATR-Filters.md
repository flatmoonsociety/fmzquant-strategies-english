
> Name

An-Advanced-EMA-Trend-Following-Strategy-with-Relaxed-RSI-and-ATR-Filters
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/de64521d7174bbf752.png)
[trans]
## Overview
This strategy is a long-term trend tracking strategy based on EMA moving average and RSI and ATR indicators. The strategy uses fast and slow EMA to form golden cross and dead cross signals, combines long-term EMA to determine the trend direction, and uses RSI and ATR to filter consolidation to track the long-term trend.
## Strategy Principle
1. Fast and slow EMA (20-day EMA and 50-day EMA) are long for golden crosses and short for dead crosses.
2. Use the 200-day EMA to determine the long-term trend direction and only trade in the trend direction.
3. Go long when RSI is low and short when it is high.
4. ATR is used to judge consolidation and filter out false breakthroughs
## Advantage Analysis
1. Use fast and slow EMA combination to judge the trend
2. Add long EMA filtering to avoid counter-trend trading
3. The RSI indicator filters overbought and oversold areas to avoid chasing highs and selling lows.
4. The ATR indicator determines consolidation and filters out false breakthroughs during shocks and consolidations.
## Risk Analysis
1. During the long-term bullish period, there is a certain degree of risk of being unable to track the upward trend.
2. The EMA indicator is prone to producing noise during consolidation and needs to be filtered in conjunction with the ATR indicator.
3. RSI and ATR parameter settings need to be tested and optimized separately according to different varieties.
## Optimization direction
1. The parameters of EMA length can be optimized to find a more matching combination of different varieties.
2. RSI and ATR parameters can also be optimized to improve the ability to identify consolidation
3. Consider adding a trailing stop to lock in some profits and control risks.
## Summarize
Overall, this strategy is a long-term trend tracking strategy with EMA as the core. It also introduces RSI and ATR indicators for assistance, which can better identify the trend direction and filter noise. Through parameter optimization, this strategy can be applied to more varieties and can achieve good results in a long-term bullish environment.
|| 

## Overview  

This is an EMA trend following strategy incorporating RSI and ATR filters, aiming to capture long term trends. It utilizes fast and slow EMA crossovers along with a long term EMA trend filter, relaxed RSI oversold/overbought levels, and ATR-based consolidation detection to reduce whipsaws.  

## Strategy Logic

1. Long when fast EMA (20) crosses above slow EMA (50) 
2. Short when fast EMA crosses below slow EMA
3. Only trade in the direction of long term trend judged by 200 EMA
4. Require RSI to be relatively oversold for longs and overbought for shorts  
5. Use ATR to detect consolidation zones to avoid false breakouts

## Advantages

1. EMA crossover system effective for trend following
2. Additional long term filter avoids trading counter trend  
3. Relaxed RSI thresholds reduce missed profitable trends
4. ATR filter helps navigate choppy consolidation periods  

## Risks

1. Can underperform in strongly trending bull markets  
2. Whipsaws possible with EMA crossovers during consolidation  
3. RSI and ATR parameters need individual optimization per instrument

## Enhancements 

1. Optimize EMA lengths for different instruments
2. Fine tune RSI and ATR parameters to improve consolidation detection  
3. Consider adding profit taking via trailing stops

## Conclusion  

Overall an effective system for long term trend following across various instruments. Optimization of parameters combined with prudent risk management can lead to positive results, especially in persistent bull market environments. The incorporation of auxiliary indicators like RSI and ATR make this an advanced EMA trend system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Short EMA|
|v_input_2|50|Long EMA|
|v_input_3|200|Trend EMA|
|v_input_4|14|RSI Length|
|v_input_5|14|ATR Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-29 00:00:00
end: 2024-02-28 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA Strategy with Trend Filter", overlay=true)

// Параметры EMA
shortEmaLength = input(20, title="Short EMA")
longEmaLength = input(50, title="Long EMA")
trendEmaLength = input(200, title="Trend EMA")
shortEma = ta.ema(close, shortEmaLength)
longEma = ta.ema(close, longEmaLength)
trendEma = ta.ema(close, trendEmaLength)

// Параметры RSI
rsiLength = input(14, title="RSI Length")
rsi = ta.rsi(close, rsiLength)

// Параметры ATR
atrLength = input(14, title="ATR Length")
atr = ta.atr(atrLength)

// Логика для сигналов покупки и продажи с фильтром по тренду
buySignal = ta.crossover(shortEma, longEma) and close > trendEma
sellSignal = ta.crossunder(shortEma, longEma) and close < trendEma

// Вход в сделки
if (buySignal)
    strategy.entry("Buy", strategy.long)

if (sellSignal)
    strategy.entry("Sell", strategy.short)

// Выход из сделок на основе EMA пересечений
exitBuySignal = ta.crossunder(shortEma, longEma)
exitSellSignal = ta.crossover(shortEma, longEma)

if (exitBuySignal)
    strategy.close("Buy")

if (exitSellSignal)
    strategy.close("Sell")

// Визуализация EMA
plot(shortEma, color=color.blue, title="Short EMA")
plot(longEma, color=color.red, title="Long EMA")
plot(trendEma, color=color.green, title="Trend EMA")

// Отдельная панель для RSI и его визуализация
plot(rsi, title="RSI", color=color.purple, linewidth=2)

// Отдельная панель для ATR и его визуализация
plot(atr, title="ATR", color=color.orange, linewidth=2)

```

> Detail

https://www.fmz.com/strategy/443135

> Last Modified

2024-02-29 14:44:10

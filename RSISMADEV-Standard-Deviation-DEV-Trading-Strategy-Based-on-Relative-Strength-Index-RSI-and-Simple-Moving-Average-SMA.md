
> Name

Standard-Deviation-DEV-Trading-Strategy-Based-on-Relative-Strength-Index-RSI-and-Simple-Moving-Average-SMA
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1001c0360d7a17534bc.png)

[trans]
#### Overview
This Pine Script strategy is based on the relative strength index RSI and the price's standard deviation of volatility DEV. It determines the entry point by comparing the price with the upper and lower tracks. It also uses RSI as an auxiliary filtering indicator. When the price touches the upper and lower tracks and the RSI reaches the overbought and oversold range, an opening signal is generated. When the price reversely breaks through the exit track or the RSI reversely reaches the overbought and oversold range, the position is closed. This strategy can dynamically adjust according to market fluctuations, stop losses in time when volatility is high, and hold positions to make profits when volatility is low. It is a quantitative trading strategy that can adapt to different market conditions.
#### Strategy Principle
1. Calculate the moving average SMA and standard deviation DEV of the price over the past length periods. 
2. Use SMA as the central axis, SMA+thresholdEntry*DEV as the upper track, and SMA-thresholdEntry*DEV as the lower track to construct a volatility channel.
3. At the same time, calculate the RSI indicator of the closing price of the past rsiLength periods.
4. When the price breaks through the lower track upwards and the RSI is less than the oversold threshold rsiOversold, a long position signal is generated.
5. When the price breaks through the upper track downwards and the RSI is greater than the overbought threshold rsiOverbought, a short position signal is generated.
6. Use SMA as the central axis, SMA+thresholdExit*DEV as the upper rail, and SMA-thresholdExit*DEV as the lower rail to construct another narrow exit channel.
7. When holding a long position, if the price breaks downward and exits the lower track or the RSI is greater than the overbought threshold, close the long position.
8. When holding a short position, if the price breaks upward and exits the upper track or the RSI is less than the oversold threshold, close the short position.
#### Advantage Analysis
1. Using price action and momentum indicators at the same time to assist judgment can effectively filter out false signals.
2. Dynamically adjust the channel width through volatility so that the strategy can adapt to different market conditions.
3. Set up two sets of channels to stop losses at the early stage of price reversal, control retracement, and still make profits after the trend is formed.
4. The code logic and parameter settings are clear and easy to understand and optimize.
#### Risk Analysis
1. When the market continues to run in a unilateral trend, this strategy may stop losses prematurely and miss trend profits.
2. Parameter settings have a great impact on strategy performance, and parameter optimization is required for different varieties and cycles.
3. The strategy has more advantages in volatile markets and average performance in trending markets. If the long-term trend suddenly reverses, this strategy may cause a large retracement.
4. If the volatility of the underlying asset changes drastically, the fixed parameter settings may become invalid.
#### Optimization direction
1. You can try to introduce trend judgment indicators, such as long-term and short-term moving average crossovers, ADX, etc., to distinguish trends and oscillating markets, and use different parameter settings.
2. Consider using a more adaptable volatility indicator, such as ATR, to dynamically adjust the width of the volatility channel.
3. Make a trend judgment on the price trend before opening a position, check whether it is in a clear trend, and avoid trading against the trend.
4. Different parameter combinations can be optimized through genetic algorithm, grid search and other methods to find the best parameter settings.
5. Consider using different parameter settings for long and short positions to control risk exposure.
#### Summary
This strategy combines the volatility channel and the relative strength index to judge the opening and closing of positions with reference to the RSI indicator while the price fluctuates. It can better grasp the phased trend, stop losses and take profits in a timely manner. However, the performance of the strategy is sensitive to parameter settings, and it needs to be optimized for different market environments and underlying assets. At the same time, other indicators should be considered to assist in judging market trends, so that the advantages of the strategy can be fully utilized. In general, this strategy has clear ideas and rigorous logic, and is a good quantitative trading strategy.
|| 

#### Overview
This Pine Script strategy is based on the Relative Strength Index (RSI) and the standard deviation (DEV) of price volatility. It determines entry points by comparing the price with upper and lower bands, while using RSI as an auxiliary filtering indicator. It generates long entry signals when the price breaks above the lower band and RSI is below the oversold threshold, and short entry signals when the price breaks below the upper band and RSI is above the overbought threshold. The strategy closes long positions when the price breaks below the exit lower band or RSI exceeds the overbought threshold, and closes short positions when the price breaks above the exit upper band or RSI falls below the oversold threshold. This strategy can dynamically adjust according to market volatility conditions, cutting losses in time during high volatility and holding positions for profit during low volatility. It is a quantitative trading strategy that can adapt to different market states.

#### Strategy Principle
1. Calculate the Simple Moving Average (SMA) and Standard Deviation (DEV) of the price over the past "length" periods.
2. Construct a volatility channel with SMA as the centerline, SMA+thresholdEntry*DEV as the upper band, and SMA-thresholdEntry*DEV as the lower band.
3. Simultaneously calculate the RSI indicator of the closing price over the past "rsiLength" periods.
4. When the price breaks above the lower band and RSI is below the oversold threshold "rsiOversold", generate a long entry signal.
5. When the price breaks below the upper band and RSI is above the overbought threshold "rsiOverbought", generate a short entry signal.
6. Construct another narrower exit channel with SMA as the centerline, SMA+thresholdExit*DEV as the upper band, and SMA-thresholdExit*DEV as the lower band.
7. When holding a long position, if the price breaks below the exit lower band or RSI exceeds the overbought threshold, close the long position.
8. When holding a short position, if the price breaks above the exit upper band or RSI falls below the oversold threshold, close the short position.

#### Advantage Analysis
1. By using both price behavior and momentum indicators for auxiliary judgment, it can effectively filter out false signals.
2. By dynamically adjusting the channel width based on volatility, the strategy can adapt to different market states.
3. By setting two sets of channels, it can cut losses in the early stage of price reversal and control drawdowns, while still being able to hold positions for profit after a trend is formed.
4. The code logic and parameter settings are clear and easy to understand and optimize.

#### Risk Analysis 
1. When the market continues to run in a unilateral trend, the strategy may cut losses too early and miss out on trend profits.
2. Parameter settings have a significant impact on the strategy's performance, and parameter optimization needs to be performed separately for different varieties and time frames.
3. The strategy performs better in oscillating markets and average in trending markets. If a long-term trend suddenly reverses, the strategy may experience a larger drawdown.
4. If the volatility of the underlying asset changes drastically, the fixed parameter settings may become invalid.

#### Optimization Direction
1. Try introducing trend judgment indicators, such as long-short term moving average crossovers, ADX, etc., to distinguish between trending and oscillating markets and use different parameter settings.
2. Consider using more adaptive volatility indicators, such as ATR, to dynamically adjust the width of the volatility channel.
3. Before opening a position, perform trend judgment on the price movement to detect whether it is in a clear trend to avoid counter-trend trading.
4. Use genetic algorithms, grid search, and other methods to optimize different parameter combinations and find the best parameter settings.
5. Consider using different parameter settings for long and short positions to control risk exposure.

#### Summary
This strategy combines volatility channels and the Relative Strength Index to make entry and exit decisions based on price fluctuations while referencing the RSI indicator. It can better capture short-term trends and cut losses and take profits in a timely manner. However, the strategy's performance is relatively sensitive to parameter settings and needs to be optimized for different market environments and underlying assets. At the same time, consider introducing other indicators to assist in judging market trends in order to fully leverage the advantages of this strategy. Overall, this strategy has a clear idea, rigorous logic, and is a good quantitative trading strategy.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-05-20 00:00:00
end: 2024-05-27 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © tmalvao

//@version=5
strategy("Estratégia de Desvio Padrão com RSI", overlay=true, margin_long=100, margin_short=100)

// Parâmetros
length = input.int(20, title="Período do Desvio Padrão")
thresholdEntry = input.float(1.5, title="Limite de Entrada")
thresholdExit = input.float(0.5, title="Limite de Saída")
rsiLength = input.int(14, title="Período do RSI")
rsiOverbought = input.int(70, title="RSI Overbought")
rsiOversold = input.int(30, title="RSI Oversold")

// Cálculo do Desvio Padrão
price = close
stdDev = ta.stdev(price, length)

// Média Móvel Simples
sma = ta.sma(price, length)

// Limites baseados no Desvio Padrão
upperLimit = sma + thresholdEntry * stdDev
lowerLimit = sma - thresholdEntry * stdDev
exitUpperLimit = sma + thresholdExit * stdDev
exitLowerLimit = sma - thresholdExit * stdDev

// Cálculo do RSI
rsi = ta.rsi(price, rsiLength)

// Condições de Entrada com RSI
longCondition = ta.crossover(price, lowerLimit) and rsi < rsiOversold
shortCondition = ta.crossunder(price, upperLimit) and rsi > rsiOverbought

// Condições de Saída com RSI
exitLongCondition = ta.crossunder(price, exitLowerLimit) or rsi > rsiOverbought
exitShortCondition = ta.crossover(price, exitUpperLimit) or rsi < rsiOversold

// Plotar Linhas
plot(upperLimit, color=color.red, title="Limite Superior")
plot(lowerLimit, color=color.green, title="Limite Inferior")
plot(exitUpperLimit, color=color.orange, title="Limite de Saída Superior")
plot(exitLowerLimit, color=color.blue, title="Limite de Saída Inferior")
plot(sma, color=color.gray, title="SMA")
hline(rsiOverbought, "RSI Overbought", color=color.red)
hline(rsiOversold, "RSI Oversold", color=color.green)
plot(rsi, title="RSI", color=color.purple)

// Estratégia de Trade
if (longCondition)
    strategy.entry("Long", strategy.long)

if (shortCondition)
    strategy.entry("Short", strategy.short)

if (exitLongCondition)
    strategy.close("Long")

if (exitShortCondition)
    strategy.close("Short")



```

> Detail

https://www.fmz.com/strategy/452691

> Last Modified

2024-05-28 10:57:06


> Name

EMA trend filter strategy EMA-Trend-Filter-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/1db812c331c10c323195e3f947b2390d409f0b355dfa03a15ad6f63410ff1839.png)
[trans]
#### Overview
This strategy uses three exponential moving averages (EMA) with different periods to determine market trends and buy and sell signals. The intersection of fast EMA, slow EMA and trend-filtered EMA, as well as the price position relative to the trend-filtered EMA, together form the core logic of this strategy. At the same time, this strategy also introduces the Fukuiz trend indicator as an auxiliary judgment, which will trigger closing operations in some cases.
#### Strategy Principle
1. Calculate three EMAs with different periods: fast EMA (default 9 periods), slow EMA (default 21 periods) and trend filtered EMA (default 200 periods).
2. Calculate the price standard deviation of 20 periods to measure market volatility.
3. Introduce the Fukuiz trend indicator (default 14-period EMA), and determine the color (green for rising, red for falling) based on its relationship with the previous period.
4. When the fast EMA crosses the slow EMA, the fast EMA is higher than the slow EMA, and the price is higher than the trend filter EMA, a buy signal is generated.
5. When the fast EMA crosses below the slow EMA, and the fast EMA is lower than the slow EMA, and the price is lower than the trend filter EMA, a sell signal is generated.
6. When holding a long position, if the Fukuiz trend indicator turns red, close the long position.
7. When holding a short position, if the Fukuiz trend indicator turns green, close the short position.
#### Advantage Analysis
1. Through the EMA combination of multiple periods, the market trend can be better captured.
2. The introduction of Fukuiz trend indicator provides additional basis for trend judgment and plays a role as a stop loss in some cases.
3. The parameters are adjustable and adaptable, and can be optimized according to different markets and cycles.
#### Risk Analysis
1. EMA is essentially a lagging indicator, and when the market turns rapidly, signal delays may occur.
2. The trend filter EMA has a long period, which may cause the strategy to miss some short-term trends.
3. The closing logic of the Fukuiz trend indicator may cause the strategy to stop loss prematurely, thus missing the subsequent trend.
#### Optimization direction
1. Optimize the period parameters of each EMA and find the parameter combination that is most suitable for the current market.
2. Introduce other auxiliary indicators, such as RSI, MACD, etc., to provide more basis for entry and exit.
3. Optimize the stop loss logic of the Fukuiz trend indicator, such as adding a certain buffer zone to avoid premature stop loss.
4. Consider adding position management and risk control modules to improve the stability and risk resistance of the strategy.
#### Summary
This strategy builds a relatively complete trend judgment and trading framework through the combination of multiple period EMAs and the assistance of the Fukuiz trend indicator. The strategy logic is clear, the parameters are adjustable, and the adaptability is strong. But there are also some potential risks, such as signal lag, trend judgment bias, etc. In the future, the strategy can be further improved from aspects such as parameter optimization, indicator combination, and risk management.
||

#### Overview
This strategy uses three exponential moving averages (EMAs) with different periods to determine market trends and generate buy/sell signals. The crossovers between the fast EMA, slow EMA, and trend filter EMA, along with the price position relative to the trend filter EMA, form the core logic of this strategy. Additionally, the Fukuiz trend indicator is introduced as an auxiliary judgment, which triggers position closing under certain conditions.

#### Strategy Principle
1. Calculate three EMAs with different periods: fast EMA (default 9 periods), slow EMA (default 21 periods), and trend filter EMA (default 200 periods).
2. Calculate the 20-period standard deviation of price to measure market volatility.
3. Introduce the Fukuiz trend indicator (default 14-period EMA) and determine its color based on its relationship with the previous period (green for upward, red for downward).
4. Generate a buy signal when the fast EMA crosses above the slow EMA, the fast EMA is higher than the slow EMA, and the price is above the trend filter EMA.
5. Generate a sell signal when the fast EMA crosses below the slow EMA, the fast EMA is lower than the slow EMA, and the price is below the trend filter EMA.
6. When holding a long position, if the Fukuiz trend indicator turns red, close the long position.
7. When holding a short position, if the Fukuiz trend indicator turns green, close the short position.

#### Advantage Analysis
1. The combination of multiple-period EMAs can effectively capture market trends.
2. The introduction of the Fukuiz trend indicator provides an additional basis for trend judgment and acts as a stop-loss in certain situations.
3. The parameters are adjustable, making the strategy highly adaptable and optimizable for different markets and timeframes.

#### Risk Analysis
1. EMAs are inherently lagging indicators, which may result in delayed signals during rapid market reversals.
2. The long period of the trend filter EMA may cause the strategy to miss some short-term trends.
3. The position closing logic based on the Fukuiz trend indicator may lead to premature stop-losses, missing out on subsequent trends.

#### Optimization Direction
1. Optimize the period parameters of each EMA to find the most suitable combination for the current market.
2. Introduce other auxiliary indicators, such as RSI and MACD, to provide more entry and exit bases.
3. Optimize the stop-loss logic of the Fukuiz trend indicator, such as adding a buffer zone to avoid premature stop-losses.
4. Consider incorporating position management and risk control modules to improve the strategy's stability and risk resistance.

#### Summary
This strategy constructs a relatively complete trend judgment and trading framework by combining multiple-period EMAs and the Fukuiz trend indicator. The strategy logic is clear, the parameters are adjustable, and the adaptability is strong. However, it also has some potential risks, such as signal lag and trend judgment deviation. In the future, the strategy can be further refined in terms of parameter optimization, indicator combination, and risk management.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-06-08 00:00:00
end: 2024-06-13 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EvilRed Trading Indicator Trend Filter", overlay=true)

// Parameters Definition
fastLength = input(9, title="Fast EMA Length")
slowLength = input(21, title="Slow EMA Length")
trendFilterLength = input(200, title="Trend Filter EMA Length")

// Moving Averages Calculation
fastEMA = ta.ema(close, fastLength)
slowEMA = ta.ema(close, slowLength)
trendEMA = ta.ema(close, trendFilterLength)

// Volatility Calculation
volatility = ta.stdev(close, 20)

// Add Fukuiz Trend Indicator
fukuizTrend = ta.ema(close, 14)
fukuizColor = fukuizTrend > fukuizTrend[1] ? color.green : color.red
plot(fukuizTrend, color=fukuizColor, title="Fukuiz Trend")

// Plotting Moving Averages
plot(fastEMA, color=color.blue, title="Fast EMA")
plot(slowEMA, color=color.red, title="Slow EMA")
plot(trendEMA, color=color.orange, title="Trend Filter")

// Plotting Buy and Sell Signals
buySignal = ta.crossover(fastEMA, slowEMA) and fastEMA > slowEMA and close > trendEMA
sellSignal = ta.crossunder(fastEMA, slowEMA) and fastEMA < slowEMA and close < trendEMA

// Entry and Exit Conditions
if (strategy.position_size > 0 and fukuizColor == color.red)
    strategy.close("Long", comment="Fukuiz Trend is Red")

if (strategy.position_size < 0 and fukuizColor == color.green)
    strategy.close("Short", comment="Fukuiz Trend is Green")

if (buySignal)
    strategy.entry("Long", strategy.long)
    
if (sellSignal)
    strategy.entry("Short", strategy.short)




plotshape(buySignal, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.small, title="Buy Signal")
plotshape(sellSignal, style=shape.triangledown, location=location.abovebar, color=color.red, size=size.small, title="Sell Signal")

```

> Detail

https://www.fmz.com/strategy/454151

> Last Modified

2024-06-14 15:51:05

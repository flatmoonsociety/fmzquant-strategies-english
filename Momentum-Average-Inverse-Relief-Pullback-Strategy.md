
> Name

Momentum-Average-Inverse-Relief-Pullback-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/df7cc5ab67264e2e3b.png)
[trans]
## Overview
The Momentum Average Inverse Relief Pullback Strategy is a simple strategy that performs reversal operations near the moving average. This strategy uses the 50-period exponential moving average as the main trend judgment indicator and combines it with the morphological engulfing rule to find reversal opportunities. After breaking through the moving average, wait for the formation of the second or third reverse K line. If it meets the reversal pattern, open a reverse position when the next K line closes and set a one-minute stop loss timer.
## Principle
This strategy is mainly based on two assumptions:
1. The 50-period EMA can effectively determine the market trend direction. When the price crosses upward, it is considered a long market; when it crosses downward, it is considered a short market.
2. After the trend breaks through the EMA, a short-term adjustment rebound often occurs. Using the morphological characteristics of the reversal K-line engulfment, you can capture the timing of the end of the rebound and perform reverse operations.
Specifically, the strategy first calculates the 50-period EMA, and then determines whether the price breaks through the EMA. If it breaks through the long position, wait for 2-3 downward negative K lines. If the next K line is engulfed by the bulls, go long when the K line closes; if it breaks through the short position, wait for 2-3 upward positive K lines. If the next K line is engulfed by the short side, go short when the K line closes. After going long or short, set a 1-minute timer and close the position after timeout.
## Advantage Analysis
This strategy has the following advantages:
1. The operation logic is simple and clear, easy to understand and implement, and is suitable for beginners.
2. Make full use of the trend judgment of moving averages and the characteristics of K-line patterns to make trading signals more effective.
3. Set a stop loss time to control the loss of a single transaction.
4. The procedural rules are clear, avoiding the influence of subjective judgment and making the strategy more reliable.
## Risk Analysis
This strategy also has certain risks:
1. The 50-day EMA cannot completely accurately determine the trend, and misjudgments may occur.
2. There is also a certain probability of misjudgment in K-line form judgment.
3. Improper stop loss time setting may increase losses or reduce profits.
4. There may be problems such as slippage and order stringing in machine trading, which will affect profits.
Countermeasures:
1. Optimize the period parameters of the moving average and find a more suitable value.
2. Combine with other indicators to make combined judgments to improve the reliability of the signal.
3. Test and optimize stop loss time parameters to find the optimal parameters.
4. Set slippage control in the strategy to avoid serious slippage losses.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the moving average period parameters and find the best parameters.
2. Replace other types of moving averages, such as weighted moving averages, etc.
3. Add filters such as volume and amplitude to avoid false signals during consolidation.
4. Combine Stochastics, MACD and other indicators to create a combination strategy to improve signal quality.
5. Set the best stop loss time according to the characteristics of different varieties and trading periods.
6. Add a profit-taking strategy and take the initiative to stop profits after the profit reaches a certain standard.
## Summarize
The momentum average reciprocal relief pullback strategy is a simple and practical short-term trading strategy. It mainly uses the moving average to determine the trend, and uses K-line engulfment to discover reversal opportunities, thereby conducting short-term operations. This strategy has the advantages of clear operation and simple implementation, but there is also some room for parameter optimization. With some testing and adjustments, this strategy can be a good starting point for beginners in quantitative trading.
||

## Overview

The Momentum Average Inverse Relief Pullback Strategy is a simple strategy to trade reversal around moving average lines. It uses 50-period Exponential Moving Average (EMA) as the main trend indicator, combined with candlestick engulfing patterns to identify reversal opportunities. After a penetration through the EMA, it waits for 2-3 candles in the opposite direction to form. If the next candle shows an engulfing reversal pattern, a reverse position will be taken at the candle close, with a 1-minute stop loss timer.  

## Principles  

The key assumptions of this strategy are:  

1. The 50-period EMA is effective in determining market trend. A close above it signals bull trend while a close below it signals bear trend.   

2. After a trend penetration through the EMA, there are often short-term pullbacks. By identifying the end of pullbacks using reversal candlestick patterns, profitable reverse trades can be executed.

Specifically, the strategy first calculates the 50-period EMA, then checks if price breaks through it. If a bull breakout happens, it waits for 2-3 red candles downwards. If the next candle shows a bullish engulfing pattern, long position will be taken on close. Similarly for bear breakouts. After taking positions, a 1-minute stop loss timer is started. Positions will be closed on timer expiration. 

## Advantages

The main advantages of this strategy:

1. The logic is simple and clear, easy to understand and implement, suitable for beginners.  

2. It utilizes both the trending effectiveness of moving averages and the predictive power of candlestick patterns, making the signals more reliable.  

3. The stop loss timer controls single trade risk.  

4. The systematic rules avoid subjective judgements and improve consistency.

## Risks 

Some main risks are:  

1. The 50-period EMA cannot fully capture trends accurately all the time. There can be misjudgements of trend.

2. Candlestick patterns also have probabilistic nature which leads to false signals.

3. Ineffective stop loss timer settings may lead to larger losses or profit giving up. 

4. Slippage, partial fills etc. impacts strategy performance.

Some mitigations:  

1. Optimize EMA period parameter to find the best fit.

2. Incorporate other indicators for strengthening signals.   

3. Test and find optimal risk parameters.  

4. Implement stop loss mechanisms against slippage in live trading.

## Enhancement Opportunities

Some ways to enhance the strategy:

1. Optimize EMA parameter to find best periods.  

2. Test other EMA variants e.g. weighted moving average.   

3. Add filters on volume or volatility to remove false signals during sideways periods.   

4. Create combination strategies with other indicators e.g. Stochastics, MACD to improve signal quality.

5. Fine tune the stop loss timer duration based on product specification and trading sessions.  

6. Consider adding profit taking mechanisms to lock gains after reaching profit targets.  

## Conclusion

The Momentum Average Inverse Relief Pullback Strategy is a simple and practical short term trading strategy. It uses EMA crossovers to determine trends and candlestick patterns to identify reversals for executing tactical trades. Despite some parameter optimization space, its clarity in logic makes it a good starting point strategy for novice quants. With proper testing and refinements, it can evolve into a robust tactical system.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|EMA Period|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-11 00:00:00
end: 2024-02-17 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("LinoR EMA Pullback Strategy", shorttitle="EPS", overlay=true)

// Define EMA period
emaPeriod = input(50, title="EMA Period")

// Calculate 50 EMA
ema50 = ta.ema(close, emaPeriod)

// Calculate engulfing conditions
engulfingBullish = close[1] < open[1] and close > open and close > close[1] and open < open[1]
engulfingBearish = close[1] > open[1] and open > close and open > open[1] and close < close[1]

// Define a 1-minute timer
var timer = 0
if bar_index > 0
    timer := timer[1] + 1

// Long condition
longCondition = ta.crossover(close, ema50) and engulfingBullish
if longCondition
    strategy.entry("Buy", strategy.long)

// Short condition
shortCondition = ta.crossunder(close, ema50) and engulfingBearish
if shortCondition
    strategy.entry("Sell", strategy.short)

// Exit after 1 minute
if timer >= 1
    strategy.close("Exit")

plotshape(series=longCondition, title="Long Signal", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(series=shortCondition, title="Short Signal", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)

```

> Detail

https://www.fmz.com/strategy/441965

> Last Modified

2024-02-18 10:21:04


> Name

Bollinger-Bands-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

## Overview
This strategy is based on the Bollinger Bands indicator, going long when the price breaks through the lower Bollinger Bands, and closing the position when the price touches the upper Bollinger Bands. This strategy uses the inclusive principle of Bollinger Bands to track abnormal price breakthroughs and achieve the purpose of buying low and selling high.
## Strategy Principle
1. Calculate the midline SMA of Bollinger Bands and take the simple moving average of recent closing prices.
2. Calculate the standard deviation StdDev, which reflects the price fluctuation range.
3. Add the midline SMA to the upper standard deviation to get the Bollinger Band upper track.
4. Subtract the lower deviation of the standard deviation from the midline SMA to obtain the lower Bollinger Band track.
5. When the closing price breaks through the lower rail from bottom to top, enter the market long.
6. When the price touches the upper track, it is considered that the price is abnormal and the position is closed.
## Advantage Analysis
The biggest advantage of this strategy is that it uses the statistical characteristics of the Bollinger Bands indicator to effectively track abnormal market fluctuations and achieve trend capture. Compared with the conventional moving average strategy, the Bollinger Bands strategy has more advantages:
1. The upper and lower rails of Bollinger Bands can automatically adapt to market fluctuations.
2. Breakthroughs are more reliable as entry signals.
3. Return to the central axis is reasonable as a take-profit signal.
4. There is a large space for parameter optimization and can be adjusted for different markets.
5. It can capture medium and long-term trends and can also be used for short-term.
## Risk Analysis
The potential risks of this strategy mainly include:
1. Bollinger Bands are not effective in sideways markets, so you must avoid entering by mistake.
2. The breakthrough signal may be a false breakthrough and must be judged with caution.
3. The take-profit position is too ideal and can be optimized to actual market conditions.
4. Improper parameter setting may lead to too frequent or conservative trading.
5. The backtest period needs to be long enough to avoid curve fitting.
Corresponding risk management measures:
1. Filter signals based on trading volume indicators.
2. Optimize parameters and test data effects in different markets.
3. Add trailing stop loss and rotating stop profit positions.
4. Evaluate signal divergence and avoid chasing highs and selling lows.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Try Bollinger Band parameters of different sizes to find the best combination.
2. Add moving average, MACD and other indicators to filter breakthrough signals.
3. Apply machine learning algorithms to optimize Bollinger Band parameters.
4. While entering the market on a breakthrough, evaluate its strength and adjust your position.
5. Backtest longer period data to test the stability of the strategy.
6. Add a stop-loss mechanism to control risk.
## Summarize
The Bollinger Bands strategy is generally a reliable trend following strategy. It can effectively capture abnormal price fluctuations. But we must also pay attention to its deviation from the actual market and constantly optimize the parameters. If it is used for real trading, risk management must be strictly carried out to control single losses.
|| 

## Overview

This strategy is based on the Bollinger Bands indicator. It goes long when the price breaks above the lower band and closes the position when the price touches the upper band. The strategy utilizes the containment principle of Bollinger Bands to track abnormal price breakouts for buying low and selling high.

## Strategy Principle 

1. Calculate the middle band SMA as the simple moving average of recent closing prices.

2. Calculate the standard deviation StdDev to reflect the price fluctuation range.

3. Add the upper offset of standard deviation to the middle band SMA to get the upper band.

4. Subtract the lower offset of standard deviation from the middle band SMA to get the lower band.

5. Go long when the closing price breaks above the lower band from bottom up. 

6. Close the position when the price touches the upper band, as the price is considered abnormal.

## Advantage Analysis

The biggest advantage of this strategy is utilizing the statistical properties of Bollinger Bands to effectively track abnormal market fluctuations and capture trends. Compared to regular moving average strategies, Bollinger Bands strategies have more advantages:

1. Bollinger Bands upper and lower bands can automatically adapt to market volatility.

2. Breakout signals are more reliable for entry.

3. Reversion to mean is reasonable for taking profit.

4. Huge parameter tuning space for adjusting to different markets.

5. Can capture mid-to-long term trends and also be used for short term.

## Risk Analysis

The potential risks of this strategy are mainly:

1. Poor performance of Bollinger Bands in range-bound markets, avoid wrong entries.

2. Breakout signals may be false breakouts, need prudent judgements. 

3. Profit taking position is too idealized, can be optimized to actual price action.

4. Improper parameter settings may lead to over-trading or over-conservatism. 

5. Backtest period needs to be long enough to avoid curve fitting.

Corresponding risk management measures:

1. Add trading volume indicators to filter signals.

2. Optimize parameters and test data from different markets.

3. Add trailing stop loss, stagger take profit levels. 

4. Assess signal divergences, avoid chasing highs and selling lows.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Try different combinations of Bollinger Bands parameters to find the optimal.

2. Add MA, MACD etc to filter breakout signals.

3. Apply machine learning algorithms to optimize Bollinger parameters. 

4. Assess the strength of breakouts and adjust position sizing.

5. Backtest longer periods to test stability. 

6. Add stop loss mechanisms to control risk.

## Summary 

In summary, the Bollinger Bands strategy is an overall reliable trend following strategy. It can effectively capture abnormal price fluctuations. But we should also note its deviation from actual price and constantly optimize the parameters. If used for live trading, strict risk management is a must to control loss per trade.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|2010|Backtest Start Year|
|v_input_2|true|Backtest Start Month|
|v_input_3|true|Backtest Start Day|
|v_input_4|2030|Backtest Stop Year|
|v_input_5|12|Backtest Stop Month|
|v_input_6|30|Backtest Stop Day|
|v_input_7|true|Color Background?|
|v_input_8|20|SMA Length|
|v_input_9|20|StdDev Length|
|v_input_10|2|Upper Band Offset|
|v_input_11|2|Lower Band Offset|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-11 00:00:00
end: 2023-09-12 04:00:00
period: 10m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4

strategy(title="BB training No Repainting (OTS Mode)", overlay=true)


// Strategy Rules:
// 1. Enter trade when price crosses above the lower band
// 2. Exit trade when price touches the upper band
// 

// Chart Properties
testStartYear = input(2010, "Backtest Start Year")
testStartMonth = input(01, "Backtest Start Month")
testStartDay = input(1, "Backtest Start Day")
testPeriodStart = timestamp(testStartYear, testStartMonth, testStartDay, 0, 0)

testStopYear = input(2030, "Backtest Stop Year")
testStopMonth = input(12, "Backtest Stop Month")
testStopDay = input(30, "Backtest Stop Day")
testPeriodStop = timestamp(testStopYear, testStopMonth, testStopDay, 0, 0)

// A switch to control background coloring of the test period
testPeriodBackground = input(title="Color Background?", type=input.bool, defval=true)
testPeriodBackgroundColor = testPeriodBackground and time >= testPeriodStart and time <= testPeriodStop ? #6c6f6c : na
bgcolor(testPeriodBackgroundColor, transp=97)

// User provided values
smaLength = input(title="SMA Length", type=input.integer, defval=20) // Middle band period length (moving average)
stdLength = input(title="StdDev Length", type=input.integer, defval=20) // Range to apply bands to
ubOffset = input(title="Upper Band Offset", type=input.float, defval=2.0, step=0.5) // Number of standard deviations above MA
lbOffset = input(title="Lower Band Offset", type=input.float, defval=2.0, step=0.5) // Number of standard deviation below MA

testPeriod() =>
    time >= testPeriodStart and time <= testPeriodStop ? true : false

smaValue = sma(close, smaLength) // Middle band
stdDev = stdev(close, stdLength)
upperBand = smaValue + stdDev * ubOffset // Top band
lowerBand = smaValue - stdDev * lbOffset // Bottom band

// Plot bands to chart
plot(series=smaValue, title="SMA", color=color.green)
plot(series=upperBand, title="UB", color=color.blue, linewidth=2)
plot(series=lowerBand, title="LB", color=color.blue, linewidth=2)

longCondition = (crossover(close, lowerBand))
closeLongCondition = (close >= upperBand)

if (longCondition and testPeriod())
    strategy.entry(id="CALL", long=true)

strategy.close(id="CALL", when=closeLongCondition)

```

> Detail

https://www.fmz.com/strategy/427264

> Last Modified

2023-09-19 16:06:56

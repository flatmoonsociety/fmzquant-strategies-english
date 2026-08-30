
> Name

Long and short trend judgment strategy EMA-Parabolic-Trend-Following-Strategy based on parabolic indicators and moving averages
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/18e88a6e7a7c99b19de.png)
[trans]

## Overview
The EPTS strategy is a trend following strategy based on the Parabolic SAR and two moving averages (EMA) with different periods. This strategy uses the parabolic indicator to determine the trend direction of the current market, and combines the relative positions of the fast and slow moving averages to generate a position opening signal. The main idea of ​​the strategy is "trend following", that is, going long in an upward trend and short in a downward trend, in order to obtain stable returns.
## Strategy Principle
1. Parabolic SAR is used to determine the direction of the current market trend. When the parabola is above the K-line, the market is in a downward trend; when the parabola is below the K-line, the market is in an upward trend.
2. Two exponential moving averages (EMA) with different periods are used to confirm trends and generate position opening signals. This strategy uses the 5-day EMA and the 20-day EMA. When the 5-day EMA is above the 20-day EMA, the market is considered to be in an upward trend; otherwise, the market is considered to be in a downward trend.
3. Opening conditions: When both the parabola and EMA show an upward trend, a long signal is generated; when both the parabola and EMA show a downward trend, a short signal is generated.
4. Position closing conditions: When the parabola breaks through the K line, close the current position and wait for the next opening signal.
5. Stop loss: When opening a position, set the stop loss price to the position of the current parabola. As the parabola moves, the stop loss position is dynamically adjusted to achieve moving stop loss.
Through the combined use of parabolic indicators and EMA, the EPTS strategy can better capture the market trend, close positions promptly when the trend reverses, and control risks. At the same time, the setting of dynamic stop loss further reduces the retracement risk of the strategy.
## Advantage Analysis
1. Trend following: The EPTS strategy is based on the idea of ​​trend following, which can effectively capture the main trends of the market and obtain stable returns.
2. Dynamic stop loss: The strategy uses a parabola as a dynamic stop loss position, and continuously adjusts the stop loss position as the trend develops, effectively controlling risks.
3. Double confirmation: Through the double confirmation of parabola and EMA, the reliability of position opening signals is improved and false signals are reduced.
4. Simple and easy to use: The strategy logic is clear, the parameters are simple to set, and easy to understand and implement.
## Risk Analysis
1. Shock market: In a shock market, the trend is not obvious and more false signals may be generated, leading to frequent transactions and large retracements.
2. Trend reversal: When the market trend suddenly reverses, the strategy may delay closing positions and suffer certain losses.
3. Parameter settings: The performance of the strategy is affected by parameter settings. Different parameters may lead to different results.
## Optimization direction
1. Introduce more indicators: Based on the existing parabola and EMA, introduce other trend indicators, such as MACD, ADX, etc., to improve the accuracy of trend judgment.
2. Optimize entry conditions: Optimize position opening conditions, such as considering the distance between price and EMA, trading volume and other factors, to improve the quality of position opening signals.
3. Dynamic parameter optimization: According to changes in market conditions, dynamically adjust strategy parameters, such as the step length of the parabola, the period of the EMA, etc., to adapt to different market environments.
4. Add position management: Dynamically adjust the position size according to the strength of the market trend and account risk to control risks while increasing returns.
## Summarize
The EPTS strategy is a trend following strategy based on parabolic indicators and moving averages. It captures the main market trends and closes positions in a timely manner to control risks and obtain stable returns. This strategy has clear logic, is easy to implement, and is suitable for market environments with obvious trends. However, in a volatile market, the strategy may face greater risk of retracement, and it is necessary to combine other indicators and optimization methods to improve the adaptability and robustness of the strategy. In addition, reasonable parameter settings and position management are also keys to the successful operation of the strategy. In general, the EPTS strategy provides a simple and effective idea for trend tracking, but it still needs to be optimized and improved based on actual market conditions in order to obtain better strategy performance.
|| 

## Overview

The EPTS strategy is a trend-following strategy based on the Parabolic SAR indicator and two exponential moving averages (EMAs) with different periods. The strategy uses the Parabolic SAR indicator to determine the current market trend direction and generates entry signals by considering the relative positions of the fast and slow EMAs. The main idea behind the strategy is "trend following," which means going long in an uptrend and short in a downtrend to achieve stable returns.

## Strategy Principles

1. The Parabolic SAR indicator is used to determine the direction of the current market trend. When the parabolic is above the candlesticks, the market is in a downtrend; when the parabolic is below the candlesticks, the market is in an uptrend.

2. Two exponential moving averages (EMAs) with different periods are used to confirm the trend and generate entry signals. This strategy uses a 5-day EMA and a 20-day EMA. When the 5-day EMA is above the 20-day EMA, the market is considered to be in an uptrend; otherwise, it is considered to be in a downtrend.

3. Entry conditions: When both the Parabolic SAR and EMAs indicate an uptrend, a long signal is generated; when both the Parabolic SAR and EMAs indicate a downtrend, a short signal is generated.

4. Exit conditions: When the Parabolic SAR crosses the candlesticks, the current position is closed, and the strategy waits for the next entry signal.

5. Stop-loss: When entering a position, the stop-loss price is set at the current position of the Parabolic SAR. As the Parabolic SAR moves, the stop-loss position is dynamically adjusted, implementing a trailing stop-loss.

By combining the Parabolic SAR indicator and EMAs, the EPTS strategy can effectively capture market trends and close positions in a timely manner when the trend reverses, controlling risk. Additionally, the dynamic stop-loss setting further reduces the strategy's drawdown risk.

## Advantages

1. Trend following: The EPTS strategy is based on the idea of trend following, which can effectively capture the main trends in the market and achieve stable returns.

2. Dynamic stop-loss: The strategy uses the Parabolic SAR as a dynamic stop-loss, adjusting the stop-loss position as the trend develops, effectively controlling risk.

3. Dual confirmation: By using dual confirmation from the Parabolic SAR and EMAs, the reliability of entry signals is improved, reducing false signals.

4. Simple and easy to use: The strategy logic is clear, and parameter settings are simple, making it easy to understand and implement.

## Risk Analysis

1. Choppy markets: In choppy markets where trends are not obvious, the strategy may generate more false signals, leading to frequent trades and larger drawdowns.

2. Trend reversals: When market trends suddenly reverse, the strategy may delay closing positions, incurring some losses.

3. Parameter settings: The performance of the strategy is influenced by parameter settings, and different parameters may lead to different results.

## Optimization Directions

1. Introduce more indicators: In addition to the existing Parabolic SAR and EMAs, introduce other trend-related indicators such as MACD and ADX to improve the accuracy of trend identification.

2. Optimize entry conditions: Optimize the entry conditions by considering factors such as the distance between the price and EMAs, trading volume, etc., to improve the quality of entry signals.

3. Dynamic parameter optimization: Dynamically adjust strategy parameters based on changes in market conditions, such as the step size of the Parabolic SAR and the periods of the EMAs, to adapt to different market environments.

4. Incorporate position sizing: Dynamically adjust position sizes based on the strength of market trends and account risk to control risk while improving returns.

## Summary

The EPTS strategy is a trend-following strategy based on the Parabolic SAR indicator and moving averages. By capturing the main market trends and closing positions in a timely manner to control risk, it aims to achieve stable returns. The strategy logic is clear and easy to implement, suitable for market environments with clear trends. However, in choppy markets, the strategy may face significant drawdown risks and needs to be combined with other indicators and optimization methods to improve its adaptability and robustness. In addition, reasonable parameter settings and position sizing are also key to the successful operation of the strategy. Overall, the EPTS strategy provides a simple and effective approach to trend following, but still requires optimization and improvement based on actual market conditions to achieve better strategy performance.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|0.02|start|
|v_input_2|0.02|increment|
|v_input_3|0.2|maximum|
|v_input_4|20|EMA 20 Length|
|v_input_5|5|EMA 5 Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-01 00:00:00
end: 2024-02-29 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("febin2024", overlay=true)

// Parabolic SAR Parameters
start = input(0.02)
increment = input(0.02)
maximum = input(0.2)

// EMA Parameters
ema20_length = input(20, title="EMA 20 Length")
ema5_length = input(5, title="EMA 5 Length")

// Calculate EMAs
ema20 = ta.ema(close, ema20_length)
ema5 = ta.ema(close, ema5_length)

// Parabolic SAR Logic
var bool uptrend = na
var float EP = na
var float SAR = na
var float AF = start
var float nextBarSAR = na

if bar_index > 0
    firstTrendBar = false
    SAR := nextBarSAR
    if bar_index == 1
        float prevSAR = na
        float prevEP = na
        lowPrev = low[1]
        highPrev = high[1]
        closeCur = close
        closePrev = close[1]
        if closeCur > closePrev
            uptrend := true
            EP := high
            prevSAR := lowPrev
            prevEP := high
        else
            uptrend := false
            EP := low
            prevSAR := highPrev
            prevEP := low
        firstTrendBar := true
        SAR := prevSAR + start * (prevEP - prevSAR)
    if uptrend
        if SAR > low
            firstTrendBar := true
            uptrend := false
            SAR := math.max(EP, high)
            EP := low
            AF := start
    else
        if SAR < high
            firstTrendBar := true
            uptrend := true
            SAR := math.min(EP, low)
            EP := high
            AF := start
    if not firstTrendBar
        if uptrend
            if high > EP
                EP := high
                AF := math.min(AF + increment, maximum)
        else
            if low < EP
                EP := low
                AF := math.min(AF + increment, maximum)
    if uptrend
        SAR := math.min(SAR, low[1])
        if bar_index > 1
            SAR := math.min(SAR, low[2])
    else
        SAR := math.max(SAR, high[1])
        if bar_index > 1
            SAR := math.max(SAR, high[2])
    nextBarSAR := SAR + AF * (EP - SAR)
    if barstate.isconfirmed
        if uptrend
            strategy.entry("ParSE", strategy.short, stop=nextBarSAR, comment="ParSE")
            strategy.cancel("ParLE")
        else
            strategy.entry("ParLE", strategy.long, stop=nextBarSAR, comment="ParLE")
            strategy.cancel("ParSE")

// Plot Parabolic SAR
plot(SAR, style=plot.style_cross, linewidth=3, color=color.orange)
plot(nextBarSAR, style=plot.style_cross, linewidth=3, color=color.aqua)

// Plot EMAs
plot(ema20, color=color.blue, linewidth=2, title="EMA 20")
plot(ema5, color=color.red, linewidth=2, title="EMA 5")

// Equity Plot
plot(strategy.equity, title="Equity", color=color.green, linewidth=2)

```

> Detail

https://www.fmz.com/strategy/446334

> Last Modified

2024-03-27 17:59:11


> Name

Dual-Indicator-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/b17f082103cb48450a.png)

[trans]

### Overview
The Dual Indicator Strategy is a quantitative trading strategy that combines the Simple Moving Average (SMA) and the Moving Average Convergence and Dispersion Index (MACD). This strategy uses a variety of technical indicators to confirm trading signals, aiming to improve the accuracy of trading decisions.
### Strategy Principles
The dual indicator strategy is mainly based on two technical indicators: SMA and MACD. The strategy uses 7, 15 and 60 K-line SMAs, as well as the MACD with standard 12/26/9 parameter settings.
When the 7-bar SMA is higher than the 15-bar SMA and the 60-bar SMA, and the 15-bar SMA is also higher than the 60-bar SMA, it is regarded as a bullish signal given by the SMA indicator, with a probability of 0.5.
At the same time, when the MACD line of the MACD indicator crosses the signal line, it is also regarded as a bullish signal given by the MACD indicator, with a probability of 0.5.
When the sum of the bullish signal probabilities of the two indicators reaches 1, a buy position is opened.
On the contrary, when the 7-bar SMA is lower than the 15-bar and 60-bar SMA, and the 15-bar SMA is also lower than the 60-bar SMA, it is regarded as a bearish signal given by the SMA indicator, with a probability of 0.5.
At the same time, when the MACD line of the MACD indicator crosses the signal line, it is also regarded as a bearish signal given by the MACD indicator, with a probability of 0.5.
When the sum of the bearish signal probabilities of the two indicators reaches 1, a sell position is opened.
In addition, the strategy uses two different take-profit points: when the price rises or falls by 9%, 50% of the position will be closed; when the price rises or falls by 21%, all remaining positions will be closed.
If a signal is generated in the opposite direction to the current position, the previous position will be closed first and then the position will be opened according to the new signal.
### Advantage Analysis
The biggest advantage of the dual indicator strategy is that it can take advantage of the advantages of both SMA and MACD indicators. SMA can effectively track changes in price trends and filter out market noise; while MACD can detect short-term trend reversal opportunities. Combining the two can improve the reliability of trading signals.
In addition, multiple groups of SMAs with different parameter settings can help identify mid- and long-term trends; and the take-profit strategy can lock in part of the profits and control risks.
### Risk Analysis
There are also some potential risks to be aware of with the dual indicator strategy. By relying solely on technical indicators, there may be situations where the indicators send out wrong signals. In addition, improper setting of take profit may also lead to premature exit and miss the big rise or fall.
The strategy can be optimized by adjusting the SMA cycle parameters or adding other filter indicators to ensure more reliable trading signals. At the same time, the take-profit level also needs to be dynamically adjusted according to the degree of market volatility to ensure that the trend market can continue to be captured.
### Optimization direction
The dual indicator strategy still has some room for optimization:
1. Test and add other technical indicators, such as RSI, Bollinger Bands, etc., to form multiple indicator filters;
2. Try machine learning algorithms and use multiple variables to establish a trading signal judgment model;
3. Optimize strategies according to different varieties and cycle parameters;
4. Add stop-loss strategies and strictly control single losses;
5. Optimize the profit-taking strategy and continue to make profits in the trend.
Through systematic backtesting and optimization, the stability and profitability of the strategy can be continuously improved.
### Summarize
The dual indicator strategy comprehensively uses the advantages of SMA and MACD to effectively control trading risks while improving signal accuracy. This strategy has good optimization space and scalability, and is a reliable and adaptable quantitative trading strategy. Through continuous data-driven and strategy optimization, the strategy can gradually develop into a powerful quantitative trading system.
||

### Overview

The Dual Indicator Strategy is a quantitative trading strategy that combines Simple Moving Average (SMA) and Moving Average Convergence Divergence (MACD) indicators. By utilizing multiple technical indicators, the strategy aims to increase the accuracy of trading signals.

### Strategy Logic

The core of the Dual Indicator Strategy relies on two indicators: SMA and MACD. The strategy adopts 7-, 15- and 60-period SMAs, as well as the standard 12/26/9 MACD parameter setting. 

When the 7-period SMA is above the 15- and 60-period SMAs, and the 15-period SMA is above the 60-period SMA, it is considered a bullish signal from the SMA indicator, with a probability of 0.5.

At the same time, when the MACD line crosses above the signal line, it is considered a bullish signal from the MACD indicator, also with a probability of 0.5.

When the bullish signal probabilities from the two indicators add up to 1, a long position will be opened.

Conversely, when the 7-period SMA falls below the 15- and 60-period SMA, and the 15-period SMA is below the 60-period SMA, it is considered a bearish signal from the SMA indicator, with a probability of 0.5. 

Meanwhile, when the MACD line crosses below the signal line, it is considered a bearish signal from the MACD indicator, with a probability of 0.5.

When the bearish signal probabilities from the two indicators add up to 1, a short position will be opened.

In addition, the strategy adopts two different take profit points: close out 50% of the position when price rises or falls by 9%, and close out the remaining position when price rises or falls by 21%.

If a signal opposite to the current position occurs, the current position will be closed first before opening a new position based on the new signal.

### Advantage Analysis 

The biggest advantage of the Dual Indicator Strategy is that it utilizes the strengths of both SMA and MACD indicators. SMA can effectively track price trend changes and filter out market noise, while MACD can identify short-term trend reversal opportunities. Combining the two can improve the reliability of trading signals.

In addition, adopting SMAs with different parameter settings helps discern long- to medium-term trends, while the take profit strategy locks in partial profits and controls risks.

### Risk Analysis

Some potential risks of the Dual Indicator Strategy need to be noted. As it relies solely on technical indicators, incorrect signals may occur. Also, improper take profit settings could lead to premature exit, missing major trends.

The strategy can be optimized by adjusting the SMA period parameters or incorporating additional filtering indicators to ensure more reliable signals. Take profit levels also need to be dynamically adjusted based on market volatility to sustain capturing trending moves.

### Optimization Directions 

Some aspects of the Dual Indicator Strategy can be further optimized:

1. Test adding other technical indicators like RSI, Bollinger Bands for multi-indicator filtering.

2. Try machine learning algorithms to build signal judgment models using multiple variables.

3. Perform parameter tuning based on different products and timeframes. 

4. Incorporate stop loss to strictly control single trade loss.

5. Optimize take profit strategy to ride sustained trends.

Through systematic backtesting and optimization, the strategy's stability and profitability can be continuously enhanced.

### Conclusion

The Dual Indicator Strategy combines the strengths of SMA and MACD to improve signal accuracy while effectively controlling risks. With strong optimization potential and versatility, it is a robust and adaptive quantitative trading strategy. With continuous data-driven improvements, the strategy can evolve into a powerful trading system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|7|7 Candle SMA Length|
|v_input_int_2|15|15 Candle SMA Length|
|v_input_int_3|60|60 Candle SMA Length|
|v_input_int_4|12|Fast Length|
|v_input_int_5|26|Slow Length|
|v_input_int_6|9|Signal Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-02 00:00:00
end: 2023-11-01 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("SMA & MACD Dual Direction Strategy", shorttitle="SMDDS", overlay=true, initial_capital=1000)

// SMA settings
sma7_length = input.int(7, title="7 Candle SMA Length")
sma15_length = input.int(15, title="15 Candle SMA Length")
sma60_length = input.int(60, title="60 Candle SMA Length")

// MACD settings
fast_length = input.int(12, title="Fast Length")
slow_length = input.int(26, title="Slow Length")
signal_length = input.int(9, title="Signal Length")

// Leverage
leverage = 10

// Calculate the SMAs
sma7 = ta.sma(close, sma7_length)
sma15 = ta.sma(close, sma15_length)
sma60 = ta.sma(close, sma60_length)

// Calculate the MACD line and Signal line
[macdLine, signalLine, _] = ta.macd(close, fast_length, slow_length, signal_length)

// SMA-based Probabilities
smaBullishProb = (sma7 > sma15 and sma7 > sma60 and sma15 > sma60) ? 0.5 : 0.0
smaBearishProb = (sma7 < sma15 and sma7 < sma60 and sma15 < sma60) ? 0.5 : 0.0

// MACD-based Probabilities
macdBullishProb = ta.crossover(macdLine, signalLine) ? 0.5 : 0.0
macdBearishProb = ta.crossunder(macdLine, signalLine) ? 0.5 : 0.0

// Combined Probabilities
combinedBullishProb = smaBullishProb + macdBullishProb
combinedBearishProb = smaBearishProb + macdBearishProb

// Trade logic using `if` conditions
if combinedBullishProb == 1.0
    strategy.close("Short")
    strategy.entry("Long", strategy.long, qty=leverage)

if combinedBearishProb == 1.0
    strategy.close("Long")
    strategy.entry("Short", strategy.short, qty=leverage)

// Exit conditions based on profit points
longTargetProfit1 = close * 1.09
longTargetProfit2 = close * 1.21

shortTargetProfit1 = close * 0.91
shortTargetProfit2 = close * 0.79

strategy.exit("Long TP1", from_entry="Long", limit=longTargetProfit1, qty_percent=0.5)
strategy.exit("Long TP2", from_entry="Long", limit=longTargetProfit2)

strategy.exit("Short TP1", from_entry="Short", limit=shortTargetProfit1, qty_percent=0.5)
strategy.exit("Short TP2", from_entry="Short", limit=shortTargetProfit2)

// Visualization (optional)
plot(sma7, color=color.green, title="7 Candle SMA")
plot(sma15, color=color.blue, title="15 Candle SMA")
plot(sma60, color=color.red, title="60 Candle SMA")
hline(0, "Zero Line", color=color.gray)
plot(macdLine - signalLine, color=color.blue, title="MACD Histogram")

```

> Detail

https://www.fmz.com/strategy/430864

> Last Modified

2023-11-02 15:30:54

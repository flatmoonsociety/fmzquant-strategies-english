
> Name

Fractal-and-Pattern-Based-Quantitative-Trading-Strategy based on patterns and candle lines
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/ae111deac11eeafa5adc28bc7c42b649ff83141247b2b74e1c40c64ecc5f8186.png)
[trans]
### Overview
This article will introduce a quantitative trading strategy that combines morphological analysis and candlestick patterns. This strategy achieves low-risk, high-yield automated trading by detecting important turning points in price graphs and candle patterns that represent strong reversals.
### Strategy Principles
This strategy is based on a detailed analysis of price trends, combined with morphological analysis and candle line analysis, and sets clear entry logic and stop loss logic, which can effectively track the trend.
Specifically, the entry conditions are: the price crosses the highest price of the first two K lines and appears to break through the previous high point pattern or one of the bull engulfing patterns or hammer patterns. This combination of conditions effectively confirms bullish opportunities. At the same time, the stop loss condition is: the price falls below the lowest price of the previous two K lines. Such stop-loss logic ensures timely and efficient stop-loss.
In terms of judging patterns, this strategy uses a combination of parting lines to identify important turning points and three typical candle patterns to judge trend reversals. Among them, the judgment of important turning point classification uses a relatively extensive classification theory, and the judgment of long, short engulfing and hammer patterns uses a relatively mature algorithm.
In terms of specific implementation, this strategy is written using pine script. The implementation logic of its detection and classification is that when the highest price of the current K line is equal to the highest price of the previous three K lines, it is the top classification type. The judgment principle of bottom parting is similar. The detection of engulfing patterns is based on the strict judgment of the relationship between the opening price and closing price.
### Strategic Advantages
The main advantages of this strategy are:
1. Combine typing and candle patterns to make accurate and reliable judgments;
2. The entry and stop loss logic is clear, simple and easy to implement;
3. Use mature theories and indicators to avoid over-fitting problems;
4. Pine script writing, suitable for mainstream platforms such as TradingView.
### Strategy Risk
This strategy still has certain risks that need to be noted:
1. There is still a certain degree of subjectivity in classification and morphological judgment;
2. Continuous false signals may be generated in the short term;
3. The stop loss range needs to be adjusted during high-frequency trading.
The above risks can be controlled by optimizing stop loss strategies, introducing trend filtering, and using quantitative tools to verify strategy parameters.
### Strategy optimization
Directions in which this strategy can be further optimized include:
1. Adjust the parameters of the candle pattern to ensure the accuracy of judgment;
2. Increase the judgment of trends and avoid false signals caused by short-term fluctuations;
3. Introduce machine learning and other methods to achieve automatic optimization of parameters.
Through the above optimization, the stability and profitability of the strategy can be further enhanced.
### Summarize
This article details a quantitative trading strategy based on parting lines and candlestick patterns. This strategy is accurate in judgment, easy to implement, and can effectively capture price trends and realize automated trading. After continuous optimization and verification, its performance will be further improved, worthy of in-depth study and application by investors or traders.
||

### Overview  

This article introduces a quantitative trading strategy that combines fractal analysis and candlestick patterns. By detecting key reversal points and bullish/bearish reversal candlestick patterns, this strategy enables low-risk high-return automated trading.  

### Strategy Principle  

This strategy is based on detailed price action analysis, using a combination of fractal analysis and candlestick pattern recognition to define clear entry and stop loss logic for capturing the trend.  

Specifically, its entry condition is: price breaks above the high of the previous 2 bars, and a fractal breakout or bullish engulfing or hammer pattern occurs. This combination solidly confirms long signals. The stop loss logic which defines exit at price breaking below the low of the previous 2 bars ensures quick and effective stops.  

For pattern detection, this strategy uses the commonly used fractal theory to identify key reversal points, as well as algorithms to detect the 3 classic candlestick reversal patterns.  

The coding is done in Pine script. Fractal high/low is identified when price makes 3-bar new high/low, and strict rules on open/close prices are used for engulfing patterns.  

### Advantages  

Main advantages of this strategy:

1. Accurate signal combining fractals and patterns  
2. Clear entry and stop loss logic  
3. Mature theories prevent overfitting  
4. Pine script allows backtesting 

### Risks

There are still risks to note:   

1. Subjectivity in fractal and pattern detection  
2. Whipsaws potentially generating consecutive losing trades 
3. Stop loss sizing requires adjustment for high frequency trading   

Methods like optimized stops, trend filtering and walk forward analysis can help control the above risks.  

### Enhancements

Areas for further enhancements:

1. Fine tune candlestick pattern parameter for robustness  
2. Add trend bias filter to avoid whipsaws
3. Introduce machine learning for automatic parameter optimization

These improvements will further strengthen the strategy’s stability and profitability.  

### Conclusion  

This article thoroughly covers a price action trading strategy combining fractals and candlestick patterns. With accurate signaling, easy implementation and effective trend following, this strategy can greatly benefit systematic traders and discretionary traders alike. Continual improvements and verification will further elevate its performance for practical trading.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-02-12 00:00:00
end: 2024-02-18 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Fractal & Pattern Entry/Exit Strategy", overlay=true)

// Fractal calculation
fractalHigh = high == highest(3)
fractalLow = low == lowest(3)

// Pattern detection
bullishEngulfing = open < close[1] and close > open[1] and close > open + (open[1] - close[1]) * 2 and low < min(open, close) and high > max(open, close) and open[1] > close[1]
bearishEngulfing = open > close[1] and close < open[1] and open > close + (close[1] - open[1]) * 2 and high > max(open, close) and low < min(open, close) and open[1] < close[1]
hammer = open < close and close > (high + low + open * 2) / 4 and close - open > (high - low) * 0.6 and high - close < (high - low) * 0.1 and open - low < (high - low) * 0.1
hangingMan = open > close and open < (high + low + close * 2) / 4 and open - close > (high - low) * 0.6 and high - open < (high - low) * 0.1 and close - low < (high - low) * 0.1

// Entry condition
longCondition = crossover(close, highest(2)[1]) and (fractalHigh or bullishEngulfing or hammer)
shortCondition = crossunder(close, lowest(2)[1]) and (fractalLow or bearishEngulfing or hangingMan)

// Exit condition
exitLongCondition = crossunder(close, lowest(2)[1])
exitShortCondition = crossover(close, highest(2)[1])

// Entry and exit orders
if (longCondition)
    strategy.entry("Long", strategy.long)
if (shortCondition)
    strategy.entry("Short", strategy.short)
if (exitLongCondition)
    strategy.close("Long")
if (exitShortCondition)
    strategy.close("Short")

// Plot fractals
plotshape(fractalHigh, title="Fractal High", style=shape.triangledown, location=location.abovebar, color=color.green, size=size.small)
plotshape(fractalLow, title="Fractal Low", style=shape.triangleup, location=location.belowbar, color=color.red, size=size.small)

// Plot patterns
plotshape(bullishEngulfing, title="Bullish Engulfing", style=shape.arrowup, location=location.belowbar, color=color.green, size=size.small)
plotshape(bearishEngulfing, title="Bearish Engulfing", style=shape.arrowdown, location=location.abovebar, color=color.red, size=size.small)
plotshape(hammer, title="Hammer", style=shape.arrowup, location=location.belowbar, color=color.green, size=size.small)
plotshape(hangingMan, title="Hanging Man", style=shape.arrowdown, location=location.abovebar, color=color.red, size=size.small)

```

> Detail

https://www.fmz.com/strategy/442113

> Last Modified

2024-02-19 14:32:45

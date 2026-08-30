
> Name

Interactive-Model-Based-Candlestick-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13a27951c699bbd50eb.png)
[trans]

### Overview
This strategy is based on the K-line shape and interaction mode to determine buy and sell signals. Mainly use breakthrough support and resistance for trading, and combine certain K-line patterns to assist decision-making.
### Strategy Principles
This strategy mainly judges the following K-line forms:
1. Small positive line: the closing price is higher than the opening price, and the physical part is shorter
2. Inverted Hammer: The opening price is close to the highest price and the closing price is close to the lowest price
3. Doji: The previous K line forms a cross with the current K line
While judging the K-line shape, this strategy also sets support and resistance levels. The specific logic is:
1. When a small positive line appears and the closing price is higher than the resistance level, a buy signal is generated
2. When an inverted hammer appears and the closing price is below the support level, a sell signal is generated
Through such combined judgment, some false signals can be filtered out, making trading decisions more reliable.
### Advantage Analysis
This strategy has the following advantages:
1. Combine graphic forms and numerical indicators to make trading signals more reliable
2. The setting of support and resistance levels avoids unnecessary repeated transactions.
3. The K-line form judgment is relatively simple and easy to understand and implement.
4. Customizable parameters to adapt to different market environments
In general, this strategy is relatively simple and practical, suitable for testing trading ideas, and can also be used to assist manual trading.
### Risk Analysis
This strategy also has some risks:
1. The judgment of K-line shape is not completely reliable and misjudgment may occur.
2. Improper setting of support and resistance levels will also affect the effectiveness of the strategy.
3. Unable to handle abnormal market conditions, such as large fluctuations caused by major malignant events
4. Insufficient backtest data may overestimate the effect of the strategy
The main countermeasures are to strictly check parameter settings, adjust support and resistance levels, and cooperate with stop losses to control risks. At the same time, backtesting must be conducted on a large amount of historical data to evaluate the actual effect of the strategy.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Add other types of K-line form judgments to enrich trading signals
2. Optimize the calculation method of support and resistance levels to make it more in line with market trends.
3. Add index indicators such as distance from the moving average and changes in trading volume to assist decision-making
4. Add machine learning algorithms and use big data to independently determine graphic features
Through these optimizations, strategy parameters can be made more automated, trading decisions more intelligent, and adapted to more complex market environments.
### Summarize
Overall, this strategy is relatively simple and practical, and is particularly suitable for individual traders to test their ideas and assist in decision-making. Combining the K-line shape and support and resistance judgment to generate trading signals, it can effectively filter out misjudgments. With certain optimization, this strategy can become a relatively reliable quantitative trading system.
||

### Overview

This strategy generates buy and sell signals based on candlestick patterns and interactive models. It mainly utilizes breakouts of support and resistance levels along with certain candlestick formations to assist in decision making.

### Strategy Logic

The strategy primarily identifies the following candlestick patterns:

1. Bullish Marubozu: Close higher than open with short real body
2. Inverted Hammer: Open near high and close near low
3. Doji Star: Previous candle crosses current doji candle

In conjunction with pattern recognition, support and resistance levels are set. The specific logic is:

1. When a Bullish Marubozu appears above resistance level, a buy signal is generated
2. When an Inverted Hammer appears below support level, a sell signal is triggered

This combination filtering helps avoid false signals and makes the trading decisions more reliable.

### Advantage Analysis 

The advantages of this strategy are:

1. Combines chart patterns and indicators for more robust signals
2. Support/Resistance levels avoid unnecessary whipsaws 
3. Candlestick patterns are simple to understand and implement
4. Customizable parameters suit different market environments

Overall, the strategy is relatively simple and practical for testing ideas and assisting manual trading.

### Risk Analysis

There are also some risks:

1. Candlestick patterns can be misleading resulting in bad signals
2. Poor support/resistance levels negatively impact performance
3. Unable to handle black swan events and huge volatility
4. Insufficient backtest data leading to overestimated results

Mitigations mainly involve strict parameter checking, support/resistance tuning, and incorporating stop losses to control risk. Additionally, extensive historical data backtesting is required to properly evaluate the actual strategy performance. 

### Enhancement Opportunities

Some ways the strategy can be enhanced:

1. Incorporate more candlestick pattern detections for more trade signals
2. Optimize support/resistance calculation methods to better fit market trends
3. Add secondary indicators like moving average distance, volume changes to supplement decisions 
4. Introduce machine learning to autonomously determine chart pattern features

These improvements can help automate strategy tuning and make trade decisions more intelligent to handle increasingly complex markets.


### Conclusion

Overall this is a simple, practical strategy well-suited for individual traders to test ideas and assist with decisions. Trading signals are generated by combining candlestick patterns and support/resistance analysis to effectively filter out false signals. With some enhancements, this strategy can become a relatively reliable quantitative system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|100|Support Level|
|v_input_2|200|Resistance Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-13 00:00:00
end: 2023-12-20 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Candlestick Pattern Strategy", overlay=true)

// Input for support and resistance levels
supportLevel = input(100, title="Support Level")
resistanceLevel = input(200, title="Resistance Level")

// Detecting Candlestick Patterns
isDoji = close == open
isPressure = close < open and open - close > close - open
isInvertedHammer = close > open and low == (close < open ? close : open) and close - open < 0.1 * (high - low)
isHammer = close > open and close - open > 0.6 * (high - low)

// Buy and Sell Conditions
buyCondition = isHammer and close > resistanceLevel
sellCondition = isInvertedHammer and close < supportLevel

// Strategy Logic
strategy.entry("Buy", strategy.long, when = buyCondition)
strategy.close("Buy", when = sellCondition)

// Plot Buy and Sell signals on the chart
plotshape(series=buyCondition, title="Buy Signal", color=color.green, style=shape.triangleup, location=location.belowbar)
plotshape(series=sellCondition, title="Sell Signal", color=color.red, style=shape.triangledown, location=location.abovebar)

// Plot Support and Resistance levels
plot(supportLevel, color=color.green, title="Support Level")
plot(resistanceLevel, color=color.red, title="Resistance Level")
```

> Detail

https://www.fmz.com/strategy/436093

> Last Modified

2023-12-21 10:55:06

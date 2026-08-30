
> Name

Quantitative-Trend-Capture-Strategy-Based-on-Candlestick-Wick-Length-Analysis
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/17a6960087c9000e0e9.png)

[trans]
#### Overview
This strategy is a quantitative trading system based on candlestick technical analysis. It mainly identifies potential trading opportunities by analyzing the total length of the upper and lower shadow lines of the candlesticks. The core of the strategy is to compare the total length of the shadow line calculated in real time with the offset-adjusted moving average. When the shadow line length breaks through the moving average, a long signal is generated. This strategy integrates a variety of moving average types, including simple moving average (SMA), exponential moving average (EMA), weighted moving average (WMA) and volume weighted moving average (VWMA), providing traders with flexible parameter selection space.
#### Strategy Principle
The core logic of the strategy includes the following key steps:
1. Calculate the length of the upper and lower shadow lines of each candle line: the upper shadow line is the difference between the highest price and the larger value of the closing price and the opening price, and the lower shadow line is the difference between the smaller value of the closing price and the opening price and the lowest price.
2. Calculate the total length of the shadow line: add the length of the upper and lower shadow lines to get the total length
3. Calculate the moving average of the shadow line length according to the moving average type (SMA/EMA/WMA/VWMA) selected by the user.
4. Add user-defined offset based on the moving average
5. When the total length of the real-time shadow line breaks through the shifted moving average, a long signal is triggered.
6. The position will be automatically closed after the holding time reaches the preset period.
#### Strategic Advantages
1. Reasonable selection of technical indicators: Shadow line length can effectively reflect market volatility and price movement intensity, and is an important indicator for judging trend turning.
2. Flexible parameter setting: Provides a variety of moving average choices and customized parameters to adapt to different market environments
3. Improved risk control: adopt a fixed holding period to avoid risks caused by excessive holdings
4. Outstanding visualization effects: use histograms to display shadow line lengths, line graphs to display moving averages, and intuitive display of trading signals.
5. Clear calculation logic: the code structure is concise, easy to understand and maintain
#### Strategy Risk
1. Market environment dependence: In a low volatility environment, the shadow length signal may not be obvious enough, affecting the strategy effect.
2. Parameter sensitivity: The selection of parameters such as moving average period and offset has a great impact on strategy performance.
3. Risk of false breakthrough: There may be a short-term breakthrough in shadow length but a rapid fall back, resulting in false signals
4. Limitations of fixed holding periods: Failure to dynamically adjust the holding period according to market conditions may result in missing out on greater gains.
5. One-way trading: only supports long transactions, and cannot make profits in falling markets.
#### Strategy optimization direction
1. Introducing volatility filtering: Combined with ATR or historical volatility indicators, start trading in a suitable volatility environment
2. Add trend filter conditions: combine long-term moving averages or trend indicators to trade in the main trend direction
3. Optimize position management: introduce a dynamic stop-profit and stop-loss mechanism, and adjust the position time based on market volatility
4. Add short selling function: add short selling transactions under appropriate conditions to increase the source of strategic income
5. Enhance signal filtering: consider multi-dimensional indicators such as trading volume and market sentiment to improve signal quality
#### Summary
This strategy builds a trading system with clear logic and strong practicality by analyzing the classic technical indicator of candle line shadow length and combining it with modern quantitative trading methods. The core advantage of the strategy lies in its parameter flexibility and completeness of risk control, but it also has limitations such as strong dependence on the market environment and parameter sensitivity. By introducing multi-dimensional indicators and optimizing position management, the strategy still has room for improvement. Overall, this is a quantitative trading strategy with a solid foundation and reasonable logic, suitable for further development and optimization.
|| 

#### Overview
This strategy is a quantitative trading system based on candlestick technical analysis, primarily identifying potential trading opportunities by analyzing the total length of candlestick upper and lower wicks. The core mechanism compares real-time calculated total wick length with an offset-adjusted moving average, generating long signals when the wick length breaks through the moving average. The strategy integrates multiple types of moving averages, including Simple Moving Average (SMA), Exponential Moving Average (EMA), Weighted Moving Average (WMA), and Volume Weighted Moving Average (VWMA), providing traders with flexible parameter selection options.

#### Strategy Principles
The core logic includes the following key steps:
1. Calculate upper and lower wick lengths for each candlestick: upper wick is the difference between high and the greater of close/open, lower wick is the difference between the lesser of close/open and low
2. Calculate total wick length by adding upper and lower wick lengths
3. Compute moving average of wick lengths based on user-selected type (SMA/EMA/WMA/VWMA)
4. Add user-defined offset to the moving average
5. Generate long signal when real-time total wick length breaks through the offset-adjusted moving average
6. Automatically close positions after preset holding period

#### Strategy Advantages
1. Rational technical indicator selection: wick length effectively reflects market volatility and price movement strength, crucial for trend reversal identification
2. Flexible parameter settings: multiple moving average options and customizable parameters adapt to different market conditions
3. Comprehensive risk control: fixed holding period prevents overexposure risks
4. Outstanding visualization: histogram displays wick length, line chart shows moving average, intuitively presenting trading signals
5. Clear calculation logic: concise code structure, easy to understand and maintain

#### Strategy Risks
1. Market environment dependency: signals may be less effective in low volatility environments
2. Parameter sensitivity: moving average period, offset value significantly impact strategy performance
3. False breakout risk: potential short-term wick length breakouts with quick reversals leading to false signals
4. Fixed holding period limitations: inability to dynamically adjust holding time based on market conditions
5. Unidirectional trading: only supports long positions, cannot profit in downtrends

#### Strategy Optimization Directions
1. Incorporate volatility filtering: combine ATR or historical volatility indicators to trade in suitable volatility environments
2. Add trend filtering conditions: integrate long-term moving averages or trend indicators to trade with main trend
3. Optimize position management: introduce dynamic stop-loss/profit mechanisms, adjust holding periods based on market volatility
4. Add short trading functionality: include short positions under appropriate conditions to diversify revenue sources
5. Enhance signal filtering: consider volume, market sentiment, and other multi-dimensional indicators to improve signal quality

#### Summary
This strategy combines classic technical indicators of candlestick wick analysis with modern quantitative trading methods, creating a trading system with clear logic and strong practicality. The core advantages lie in parameter flexibility and comprehensive risk control, though limitations include strong market environment dependency and parameter sensitivity. Significant improvement potential exists through multi-dimensional indicator integration and position management optimization. Overall, it represents a fundamentally sound and logically coherent quantitative trading strategy suitable for further development and optimization.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2025-01-04 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("Daytrading ES Wick Length Strategy", overlay=true)

// Input parameters
ma_length = input.int(20, title="Moving Average Length", minval=1)
ma_type = input.string("VWMA", title="Type of Moving Average", options=["SMA", "EMA", "WMA", "VWMA"])
ma_offset = input.float(10, title="MA Offset (Points)", step=1)
hold_periods = input.int(18, title="Holding Period (Bars)", minval=1)

// Calculating upper and lower wick lengths
upper_wick_length = high - math.max(close, open)
lower_wick_length = math.min(close, open) - low

// Total wick length (upper + lower)
total_wick_length = upper_wick_length + lower_wick_length

// Calculate the moving average based on the selected method
ma = switch ma_type
    "SMA" => ta.sma(total_wick_length, ma_length)
    "EMA" => ta.ema(total_wick_length, ma_length)
    "WMA" => ta.wma(total_wick_length, ma_length)
    "VWMA" => ta.vwma(total_wick_length, ma_length)

// Add the offset to the moving average
ma_with_offset = ma + ma_offset

// Entry condition: wick length exceeds MA with offset
long_entry_condition = total_wick_length > ma_with_offset

// Long entry
if (long_entry_condition)
    strategy.entry("Long", strategy.long)

// Automatic exit after holding period
if strategy.position_size > 0 and bar_index - strategy.opentrades.entry_bar_index(strategy.opentrades - 1) >= hold_periods
    strategy.close("Long")

// Plot the total wick length as a histogram
plot(total_wick_length, color=color.blue, style=plot.style_histogram, linewidth=2, title="Total Wick Length")

// Plot the moving average with offset
plot(ma_with_offset, color=color.yellow, linewidth=2, title="MA of Wick Length (Offset)")
```

> Detail

https://www.fmz.com/strategy/477603

> Last Modified

2025-01-06 16:33:16

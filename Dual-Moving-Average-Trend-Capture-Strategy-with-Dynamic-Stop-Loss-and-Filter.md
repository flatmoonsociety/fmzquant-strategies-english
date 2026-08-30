
> Name

Dual-Moving-Average-Trend-Capture-Strategy-with-Dynamic-Stop-Loss-and-Filter
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14f2fb9bb64188f2cf8.png)

[trans]
#### Overview
This is a trend following strategy based on a dual moving average system that combines dynamic stop loss and moving average filters. This strategy uses two moving averages with different periods to capture market trends, while limiting the trading direction by filtering the moving averages and providing flexible stop loss setting options. This approach aims to capture mid- to long-term trends while protecting capital through dynamic risk management.
#### Strategy Principle
The core principles of this strategy include the following aspects:
1. Dual moving average system: Use two moving averages, one as the main signal line (shorter period) and the other as a filter (longer period).
2. Trend confirmation: Only when the price and the main moving average are on the same side of the filtered moving average, a position will be considered. This helps ensure that the trading direction is consistent with the overall trend.
3. Entry signal: When the price breaks through the main moving average and meets the filtering conditions, the entry signal is triggered.
4. Dynamic Stop Loss: Two stop loss options are provided - dynamic stop loss based on percentage or fixed stop loss based on the previous candle's high and low points.
5. Fixed take profit: Use a fixed take profit level based on a percentage of the entry price.
6. Visualization: Draw moving averages, entry prices, stop loss and take profit levels on the chart to analyze trades visually.
#### Strategic Advantages
1. Trend following: By using the dual moving average system, this strategy can effectively capture mid- to long-term trends and increase profit opportunities.
2. Risk management: Dynamic stop-loss options allow the strategy to automatically adjust risk exposure according to market volatility and improve fund protection capabilities.
3. Flexibility: The strategy allows users to choose different types of moving averages (SMA, EMA, WMA) and customize various parameters to adapt to different trading styles and market environments.
4. Filtering mechanism: Using long-period moving averages as filters helps reduce false breakthroughs and counter-trend trading, and improves the stability of the strategy.
5. Visualization effect: By plotting key price levels and moving averages on the chart, traders can intuitively understand the strategy logic and current market conditions.
6. Automated execution: Strategies can be automatically executed on the trading platform, reducing human intervention and emotional impact.
#### Strategy Risk
1. Lagging: The moving average is essentially a lagging indicator, which may result in late entry or exit when the trend reverses.
2. Shock market performance: In sideways or shock markets, strategies may produce frequent false signals, leading to continuous losses.
3. Parameter sensitivity: Strategy performance is highly dependent on the selected parameters. Improper parameter settings may lead to over-trading or missing important opportunities.
4. Fixed take profit limits: Using a fixed percentage take profit can end profitable trades prematurely in a strong trend.
5. Changes in market conditions: The performance of strategies may differ significantly in different market environments and requires regular evaluation and adjustment.
6. Slippage and transaction costs: In actual trading, slippage and transaction costs may significantly affect the profitability of the strategy, especially in the case of high-frequency trading.
#### Strategy optimization direction
1. Dynamic parameter adjustment: realize adaptive moving average period and stop loss percentage to adapt to different market volatility and trend intensity.
2. Multi-time frame analysis: Integrate trend information of longer time periods to improve the accuracy of entry decisions and reduce false signals.
3. Volatility filtering: Introduce volatility indicators (such as ATR), suspend trading during periods of low volatility, and reduce losses in volatile markets.
4. Confirmation of trend strength: Combine with other technical indicators (such as ADX) to evaluate the strength of the trend, and only open positions in strong trends.
5. Dynamic take-profit: Implement a dynamic take-profit mechanism based on market volatility or trend strength to maximize profit potential.
6. Fund management optimization: Dynamically adjust position size according to account size and market volatility to optimize the risk-return ratio.
7. Machine learning integration: Use machine learning algorithms to optimize parameter selection and entry timing to improve the adaptability and performance of the strategy.
8. Sentiment analysis: Integrate market sentiment indicators, adjust strategic behavior during periods of extreme sentiment, and avoid overcrowded trading.
#### Summarize
The Dual Moving Average Trend Capture Strategy combined with dynamic stops and filters is a comprehensive trend following system designed to capture mid- to long-term market trends. By combining the main signal moving average and the filtered moving average, this strategy is able to effectively identify trend directions and generate trading signals. Dynamic stop-loss options provide flexible risk management, while visualization capabilities enhance strategy interpretability.
Although this strategy has strong potential, there are inherent risks such as lag and sensitivity to changes in market conditions. In order to improve the robustness and adaptability of the strategy, further optimization is recommended, such as implementing dynamic parameter adjustment, integrating multi-time frame analysis and introducing additional filtering mechanisms.
Overall, this strategy provides traders with a solid foundation that can be customized and improved based on individual needs and market characteristics. Through continuous monitoring, backtesting and optimization, this strategy has the potential to become a reliable trading tool suitable for a variety of market environments.
|| 

#### Overview

This is a trend-following strategy based on a dual moving average system, incorporating dynamic stop-loss and a moving average filter. The strategy uses two moving averages of different periods to capture market trends, while using a filter moving average to restrict trading direction and providing flexible stop-loss options. This approach aims to capture medium to long-term trends while protecting capital through dynamic risk management.

#### Strategy Principles

The core principles of this strategy include:

1. Dual Moving Average System: Uses two moving averages, one as the main signal line (shorter period) and another as a filter (longer period).

2. Trend Confirmation: Only considers opening positions when both price and the main moving average are on the same side of the filter moving average. This helps ensure that the trading direction aligns with the overall trend.

3. Entry Signals: Triggers entry signals when the price breaks through the main moving average and meets the filter conditions.

4. Dynamic Stop-Loss: Offers two stop-loss options - a percentage-based dynamic stop-loss or a fixed stop-loss based on the previous candle's high/low.

5. Fixed Take-Profit: Uses a fixed take-profit level based on a percentage of the entry price.

6. Visualization: Plots moving averages, entry prices, stop-loss, and take-profit levels on the chart for intuitive analysis of trades.

#### Strategy Advantages

1. Trend Following: By using a dual moving average system, the strategy can effectively capture medium to long-term trends, increasing profit opportunities.

2. Risk Management: The dynamic stop-loss option allows the strategy to automatically adjust risk exposure based on market volatility, enhancing capital protection.

3. Flexibility: The strategy allows users to choose different types of moving averages (SMA, EMA, WMA) and customize various parameters, adapting to different trading styles and market environments.

4. Filtering Mechanism: Using a longer-period moving average as a filter helps reduce false breakouts and counter-trend trades, improving strategy stability.

5. Visual Effects: By plotting key price levels and moving averages on the chart, traders can intuitively understand strategy logic and current market conditions.

6. Automated Execution: The strategy can be executed automatically on trading platforms, reducing human intervention and emotional influence.

#### Strategy Risks

1. Lag: Moving averages are inherently lagging indicators, which may lead to late entries or exits during trend reversals.

2. Performance in Ranging Markets: In sideways or choppy markets, the strategy may generate frequent false signals, leading to consecutive losses.

3. Parameter Sensitivity: Strategy performance is highly dependent on chosen parameters; improper parameter settings may result in overtrading or missing important opportunities.

4. Fixed Take-Profit Limitations: Using a fixed percentage take-profit may prematurely end profitable trades during strong trends.

5. Changing Market Conditions: Strategy performance may vary significantly under different market environments, requiring regular evaluation and adjustment.

6. Slippage and Trading Costs: In actual trading, slippage and trading costs can significantly impact strategy profitability, especially in high-frequency trading scenarios.

#### Strategy Optimization Directions

1. Dynamic Parameter Adjustment: Implement adaptive moving average periods and stop-loss percentages to suit different market volatilities and trend strengths.

2. Multi-Timeframe Analysis: Integrate trend information from longer timeframes to improve entry decision accuracy and reduce false signals.

3. Volatility Filtering: Introduce volatility indicators (such as ATR) to pause trading during low volatility periods, reducing losses in choppy markets.

4. Trend Strength Confirmation: Combine other technical indicators (like ADX) to assess trend strength and only open positions in strong trends.

5. Dynamic Take-Profit: Implement a dynamic take-profit mechanism based on market volatility or trend strength to maximize profit potential.

6. Position Sizing Optimization: Dynamically adjust position size based on account size and market volatility to optimize risk-reward ratio.

7. Machine Learning Integration: Utilize machine learning algorithms to optimize parameter selection and entry timing, improving strategy adaptability and performance.

8. Sentiment Analysis: Incorporate market sentiment indicators to adjust strategy behavior during extreme sentiment periods, avoiding overcrowded trades.

#### Conclusion

The Dual Moving Average Trend Capture Strategy with Dynamic Stop-Loss and Filter is a comprehensive trend-following system designed to capture medium to long-term market trends. By combining a main signal moving average with a filter moving average, the strategy can effectively identify trend direction and generate trading signals. The dynamic stop-loss option provides flexible risk management, while the visualization features enhance strategy interpretability.

While the strategy shows strong potential, it still has inherent risks such as lag and sensitivity to changing market conditions. To improve the strategy's robustness and adaptability, further optimizations are recommended, such as implementing dynamic parameter adjustments, integrating multi-timeframe analysis, and introducing additional filtering mechanisms.

Overall, this strategy provides traders with a solid foundation that can be customized and improved based on individual needs and market characteristics. Through continuous monitoring, backtesting, and optimization, the strategy has the potential to become a reliable trading tool suitable for various market environments.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-06-30 00:00:00
end: 2024-07-30 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Moving Average Breakout with Filter and Dynamic Stop Loss", overlay=true)

// Параметры
maLength = input.int(14, "MA Length")
maType = input.string("SMA", "MA Type", options=["SMA", "EMA", "WMA"])
takeProfitPercent = input.float(1.0, "Take Profit (%)", step=0.1)
filterMaLength = input.int(50, "Filter MA Length")
filterMaType = input.string("SMA", "Filter MA Type", options=["SMA", "EMA", "WMA"])
useDynamicStopLoss = input.bool(false, "Use Dynamic Stop Loss")
dynamicStopLossPercent = input.float(1.0, "Dynamic Stop Loss (%)", step=0.1)

// Выбор типа основной скользящей средней
float ma = na
switch maType
    "SMA" => ma := ta.sma(close, maLength)
    "EMA" => ma := ta.ema(close, maLength)
    "WMA" => ma := ta.wma(close, maLength)

// Выбор типа скользящей средней фильтра
float filterMa = na
switch filterMaType
    "SMA" => filterMa := ta.sma(close, filterMaLength)
    "EMA" => filterMa := ta.ema(close, filterMaLength)
    "WMA" => filterMa := ta.wma(close, filterMaLength)

// Построение скользящих средних
plot(ma, color=color.blue, linewidth=2, title="Moving Average")
plot(filterMa, color=color.orange, linewidth=2, title="Filter Moving Average")

// Логика открытия позиций
longCondition = ta.crossover(close, ma) and close > filterMa
shortCondition = ta.crossunder(close, ma) and close < filterMa

var bool inPosition = false
var float entryPrice = na
var float takeProfitLevel = na
var float stopLossLevel = na

if (longCondition and not inPosition and strategy.position_size == 0)
    entryPrice := close
    takeProfitLevel := close * (1 + takeProfitPercent / 100)
    if (useDynamicStopLoss)
        stopLossLevel := close * (1 - dynamicStopLossPercent / 100)
    else
        stopLossLevel := low[1]
    strategy.entry("Long", strategy.long)
    strategy.exit("Take Profit/Stop Loss", from_entry="Long", limit=takeProfitLevel, stop=stopLossLevel)
    // line.new(bar_index, entryPrice, bar_index + 1, entryPrice, color=color.blue, width=2)
    // line.new(bar_index, takeProfitLevel, bar_index + 1, takeProfitLevel, color=color.green, width=2, style=line.style_dashed)
    // line.new(bar_index, stopLossLevel, bar_index + 1, stopLossLevel, color=color.red, width=2, style=line.style_dashed)
    inPosition := true

if (shortCondition and not inPosition and strategy.position_size == 0)
    entryPrice := close
    takeProfitLevel := close * (1 - takeProfitPercent / 100)
    if (useDynamicStopLoss)
        stopLossLevel := close * (1 + dynamicStopLossPercent / 100)
    else
        stopLossLevel := high[1]
    strategy.entry("Short", strategy.short)
    strategy.exit("Take Profit/Stop Loss", from_entry="Short", limit=takeProfitLevel, stop=stopLossLevel)
    // line.new(bar_index, entryPrice, bar_index + 1, entryPrice, color=color.blue, width=2)
    // line.new(bar_index, takeProfitLevel, bar_index + 1, takeProfitLevel, color=color.green, width=2, style=line.style_dashed)
    // line.new(bar_index, stopLossLevel, bar_index + 1, stopLossLevel, color=color.red, width=2, style=line.style_dashed)
    inPosition := true

// Проверка закрытия позиции по тейк-профиту или стоп-лоссу
if (strategy.position_size == 0)
    inPosition := false

// Отображение текущих линий стоп-лосса и тейк-профита
// if (strategy.position_size > 0)
    // line.new(bar_index[1], takeProfitLevel, bar_index, takeProfitLevel, color=color.green, width=2, style=line.style_dashed)
    // line.new(bar_index[1], stopLossLevel, bar_index, stopLossLevel, color=color.red, width=2, style=line.style_dashed)
    // line.new(bar_index[1], entryPrice, bar_index, entryPrice, color=color.blue, width=2)

// if (strategy.position_size < 0)
    // line.new(bar_index[1], takeProfitLevel, bar_index, takeProfitLevel, color=color.green, width=2, style=line.style_dashed)
    // line.new(bar_index[1], stopLossLevel, bar_index, stopLossLevel, color=color.red, width=2, style=line.style_dashed)
    // line.new(bar_index[1], entryPrice, bar_index, entryPrice, color=color.blue, width=2)

```

> Detail

https://www.fmz.com/strategy/458249

> Last Modified

2024-07-31 11:46:38

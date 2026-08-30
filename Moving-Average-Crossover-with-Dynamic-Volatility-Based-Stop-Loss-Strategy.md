
> Name

Moving-Average-Crossover-with-Dynamic-Volatility-Based-Stop-Loss-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d808067861f1eb72f04c.png)
![IMG](https://www.fmz.com/upload/asset/2d85b2134d351dd0ca484.png)


[trans]

#### Overview
This quantitative trading strategy is a comprehensive system that combines moving average crossovers, Relative Strength Index (RSI) filtering, and a dynamic stop-loss mechanism based on the Average True Range (ATR). This strategy is mainly used to capture medium and long-term trends, while using the RSI indicator to avoid entering the market in excessively overbought or oversold conditions, and using the ATR indicator to set dynamic stop loss levels to adapt to changes in market volatility. The strategy performs particularly well on the 15-minute time frame, striking a good balance between capturing intraday trends and avoiding excessive noise on lower time frames.
#### Strategy Principle
The core logic of the strategy is based on the following key components:
1. **Moving Average Crossover Signal**: The strategy uses two simple moving averages (SMA), which are the 50-period short-term moving average and the 200-period long-term moving average. When the short-term moving average is lower than the long-term moving average and the RSI value is greater than 30, the system will trigger a long signal. This design is intended to identify potential trend turning points.
2. **RSI filtering mechanism**: The strategy uses the 14-period RSI indicator for entry filtering. Specifically, long positions are only allowed when the RSI value is above 30, which helps avoid blind entry into deeply oversold areas. Although the framework of short conditions is retained in the code, the current version mainly focuses on the long strategy.
3. **ATR dynamic stop loss**: The strategy uses the 14-period ATR indicator to calculate the dynamic stop loss level. The stop loss level is set to the entry price minus (ATR value × multiple), where the ATR multiple defaults to 1.0. This dynamic stop-loss mechanism can adaptively adjust according to the actual market volatility, providing a looser stop-loss space during periods of high volatility and maintaining tighter risk control during periods of low volatility.
4. **Risk-reward ratio**: The strategy implements a take-profit setting based on the risk-reward ratio (RRR), and the default value is 1.5. The take profit level is calculated as the entry price plus ((entry price - stop loss price) × risk reward ratio) to ensure that the potential profit of each transaction is appropriately proportioned to the risk taken.
#### Strategic Advantages
1. **Trend tracking combined with filtering**: The strategy not only uses moving average crossovers to capture trend changes, but also filters through the RSI indicator, reducing false signals and improving the quality of entry.
2. **Dynamic Risk Management**: The stop-loss mechanism based on ATR is a highlight of this strategy. It can dynamically adjust the stop-loss distance according to market volatility, avoiding the problem of fixed stop-loss being triggered prematurely in a high-volatility environment, while maintaining appropriate risk control during low-volatility periods.
3. **Risk-reward ratio optimization**: Through a preset risk-reward ratio, the strategy ensures that the potential return of each trade is proportional to the risk, which helps long-term capital growth, even when the winning rate is not high.
4. **Transaction visualization**: The strategy includes real-time drawing of stop loss and take profit levels, as well as the marking function of completed transactions, which greatly improves the visibility of strategy operation and facilitates backtest analysis and strategy optimization.
5. **Fund Management Integration**: The strategy defaults to using a percentage of the total account value for position management. This method is more flexible than fixed lots and can automatically adjust the transaction size as the account size changes.
#### Strategy Risk
1. **Trend Reversal Risk**: Although the strategy uses moving averages to identify trends, it may result in larger losses when the market suddenly reverses. The solution is to consider introducing more sensitive short-term indicators as auxiliary confirmation, or adjusting the RSI threshold to increase sensitivity to reversals.
2. **Parameter sensitivity**: The key parameters of the strategy, such as SMA period, RSI threshold, ATR multiple, etc., have a significant impact on performance. Different market environments may require different parameter settings, so sufficient historical backtesting is required to find the optimal parameter combination.
3. **Unilateral market limitations**: The current version mainly focuses on long strategies, which may perform poorly in markets that continue to fall. The solution is to activate the short-selling conditions in the code to achieve two-way trading capabilities.
4. **Risk of excessively wide stop loss**: During periods of extreme high volatility, the ATR value may increase significantly, resulting in an excessively wide stop loss distance and an increase in potential losses. You can consider setting a cap on the ATR multiple, or a hybrid solution that combines a fixed amount stop loss with a dynamic ATR stop loss.
5. **Uncertainty in trading frequency**: Since the strategy relies on the crossover of medium and long-term moving averages, trading signals may be sparse and affect the efficiency of capital utilization. The solution is to consider adding short-term trading signals as a supplement, or using shorter-term indicators to add to positions after the main trend is established.
#### Strategy optimization direction
1. **Multi-time frame analysis integration**: The current strategy only runs on a single time frame. You can consider integrating multi-time frame analysis, such as using a higher time frame to confirm the main trend direction, and then looking for entry points in a lower time frame to improve entry accuracy.
2. **Improvement of short-selling logic**: Activate and optimize the short-selling logic in the strategy so that it can be equally effective in falling markets. This may require adjusting the RSI threshold for shorting (such as shorting when the RSI is greater than 70), and setting different parameters for different market directions.
3. **Introduction of trading volume indicators**: Consider integrating trading volume indicators into the entry logic, and only execute trading signals when the trading volume is confirmed, which will help reduce losses caused by false breakthroughs.
4. **Optimize take-profit strategy**: The current strategy uses a fixed risk-reward ratio to set take-profit. You can consider implementing partial profit locking or trailing take-profit to obtain more profits when the trend continues to develop.
5. **Add trading period filter**: For markets with obvious period characteristics, time filters can be added to avoid trading during periods of low liquidity or high uncertainty.
6. **Parameter adaptive mechanism**: Implement a parameter adaptive adjustment mechanism based on historical volatility or other market characteristics, so that the strategy can automatically optimize parameters according to changes in the market environment.
#### Summarize
This quantitative strategy based on moving average crossover, RSI filtering and ATR dynamic stop loss provides a balanced trading framework, especially suitable for medium and long-term trend trading. Its core advantage lies in the seamless combination of technical indicator analysis and dynamic risk management, which can not only capture trend changes but also adjust risk exposure according to market volatility.
Although the strategy has limitations of parameter sensitivity and one-way trading, these problems can be effectively improved through the recommended optimization directions, such as multi-time frame analysis, improving short-selling logic, and introducing volume confirmation. In particular, combining dynamic parameter adjustment mechanisms with more complex take-profit strategies is expected to further enhance the robustness and profitability of the strategy.
For traders who seek to trade mid- to long-term trends while paying attention to risk control, this strategy provides a solid starting point and has the potential to become an efficient trading system through personalized adjustments and continuous optimization.
|| 

#### Overview

This quantitative trading strategy is a comprehensive system that combines moving average crossovers, Relative Strength Index (RSI) filtering, and dynamic stop-loss mechanisms based on Average True Range (ATR). The strategy is primarily designed to capture medium to long-term trends while avoiding entry in extremely overbought or oversold market conditions through RSI indicators, and employing ATR-based dynamic stop-loss to adapt to changing market volatility. The strategy performs particularly well on the 15-minute timeframe, achieving a good balance between capturing intraday trends and avoiding excessive noise often seen in lower timeframes.

#### Strategy Principles

The core logic of the strategy is based on several key components:

1. **Moving Average Crossover Signals**: The strategy utilizes two Simple Moving Averages (SMA), a 50-period short-term SMA and a 200-period long-term SMA. A long entry signal is triggered when the short-term SMA is below the long-term SMA and the RSI value is greater than 30. This design aims to identify potential trend reversal points.

2. **RSI Filtering Mechanism**: The strategy employs a 14-period RSI indicator for entry filtering. Specifically, long entries are only permitted when the RSI value is above 30, which helps avoid blind entries in deeply oversold areas. While the framework for short conditions is preserved in the code, the current version primarily focuses on long strategies.

3. **ATR Dynamic Stop-Loss**: The strategy uses a 14-period ATR indicator to calculate dynamic stop-loss levels. The stop-loss is set at the entry price minus (ATR value × multiplier), where the ATR multiplier defaults to 1.0. This dynamic stop-loss mechanism adapts to actual market volatility, providing wider stop-loss space during high volatility periods and maintaining tighter risk control during low volatility periods.

4. **Risk-Reward Ratio**: The strategy implements take-profit settings based on a Risk-Reward Ratio (RRR), with a default value of 1.5. The take-profit level is calculated as the entry price plus ((entry price - stop-loss price) × risk-reward ratio), ensuring that the potential gain for each trade maintains an appropriate proportion to the risk taken.

#### Strategy Advantages

1. **Combination of Trend Following and Filtering**: The strategy not only uses moving average crossovers to capture trend changes but also filters through the RSI indicator, reducing false signals and improving entry quality.

2. **Dynamic Risk Management**: The ATR-based stop-loss mechanism is a highlight of this strategy, as it dynamically adjusts stop-loss distances based on market volatility, avoiding the problem of fixed stops triggering too early in high volatility environments while maintaining appropriate risk control during low volatility periods.

3. **Risk-Reward Ratio Optimization**: Through a preset risk-reward ratio, the strategy ensures that the potential return for each trade is proportional to the risk, which aids long-term capital growth even when the win rate may not be high.

4. **Trade Visualization**: The strategy includes real-time plotting of stop-loss and take-profit levels, as well as marking of completed trades, which greatly enhances the visualization of strategy execution, facilitating backtesting analysis and strategy optimization.

5. **Integrated Capital Management**: By default, the strategy uses a percentage of the account's total value for position sizing, which is more flexible than fixed lot sizing and can automatically adjust trading size as the account grows or shrinks.

#### Strategy Risks

1. **Trend Reversal Risk**: Although the strategy uses moving averages to identify trends, sudden market reversals can lead to significant losses. The solution is to consider introducing more sensitive short-term indicators as auxiliary confirmation or adjusting RSI thresholds to increase sensitivity to reversals.

2. **Parameter Sensitivity**: Key parameters such as SMA periods, RSI thresholds, and ATR multipliers have a significant impact on performance. Different market environments may require different parameter settings, so thorough historical backtesting is needed to find the optimal parameter combinations.

3. **Unidirectional Market Limitations**: The current version primarily focuses on long strategies and may not perform well in continuously declining markets. The solution is to activate the short conditions in the code to implement bidirectional trading capabilities.

4. **Wide Stop-Loss Risk**: During extremely high volatility periods, ATR values may increase significantly, leading to excessively wide stop-loss distances and increased potential losses. Consider setting upper limits for ATR multipliers or implementing a hybrid approach combining fixed monetary stop-losses with ATR dynamic stop-losses.

5. **Trading Frequency Uncertainty**: As the strategy relies on medium to long-term moving average crossovers, it may result in sparse trading signals, affecting capital utilization efficiency. The solution is to consider adding short-term trading signals as supplements or using shorter-term indicators for position additions after the main trend is established.

#### Strategy Optimization Directions

1. **Multiple Timeframe Analysis Integration**: The current strategy operates on a single timeframe. Consider integrating multiple timeframe analysis, such as using higher timeframes to confirm the main trend direction and then looking for entry points on lower timeframes to improve entry precision.

2. **Refinement of Short Logic**: Activate and optimize the short logic in the strategy to make it equally effective in declining markets. This may require adjusting RSI thresholds for shorts (such as shorting when RSI is above 70) and setting different parameters for different market directions.

3. **Introduction of Volume Indicators**: Consider integrating volume indicators into the entry logic, executing trading signals only when confirmed by volume, which helps reduce losses from false breakouts.

4. **Optimization of Take-Profit Strategy**: The current strategy uses a fixed risk-reward ratio for take-profit setting. Consider implementing partial profit locking or trailing stops to capture more profit when trends continue to develop.

5. **Adding Trading Session Filters**: For markets with obvious session characteristics, add time filters to avoid trading during low liquidity or high uncertainty sessions.

6. **Parameter Adaptive Mechanism**: Implement parameter adaptive adjustment mechanisms based on historical volatility or other market characteristics, allowing the strategy to automatically optimize parameters according to changing market environments.

#### Summary

This quantitative strategy based on moving average crossovers, RSI filtering, and ATR dynamic stop-loss provides a balanced trading framework particularly suited for medium to long-term trend trading. Its core advantage lies in the seamless integration of technical indicator analysis with dynamic risk management, capable of both capturing trend changes and adjusting risk exposure based on market volatility.

Although the strategy has limitations in parameter sensitivity and unidirectional trading, these issues can be effectively addressed through the suggested optimization directions, such as multiple timeframe analysis, refined short logic, volume confirmation, etc. In particular, combining dynamic parameter adjustment mechanisms with more sophisticated take-profit strategies promises to further enhance the robustness and profitability of the strategy.

For traders seeking medium to long-term trend trading while emphasizing risk control, this strategy provides a solid starting point that, through personalized adjustments and continuous optimization, has the potential to become an efficient trading system.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-02 00:00:00
end: 2025-04-01 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BNB_USDT"}]
*/

//@version=6
strategy(title=" VS-NTC> NASDQ100 Long MA+RSI+ATR", shorttitle="VS-NTC> Long NASDQ100 MA+RSI+ATR", overlay=true, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// ————— Inputs —————
smaLenShort  = input.int(50,  title="Short SMA Length")
smaLenLong   = input.int(200, title="Long SMA Length")
rsiLen       = input.int(14,  title="RSI Length")
atrPeriod    = input.int(14,  title="ATR Period")
atrMult      = input.float(1.0, title="Stop-Loss ATR Multiplier", step=0.1)
rrRatio      = input.float(1.5, title="Risk-to-Reward Ratio",    step=0.1)

// ————— Indicator Calculations —————
smaShort = ta.sma(close, smaLenShort)
smaLong  = ta.sma(close, smaLenLong)
rsiVal   = ta.rsi(close, rsiLen)
atrVal   = ta.atr(atrPeriod)

// ————— Entry Conditions —————
// Long Condition: 50SMA > 200SMA and RSI < 70
longCondition = (smaShort < smaLong) and (rsiVal > 30)
// Short Condition: 50SMA < 200SMA and RSI > 30 (example: avoid oversold)
// Or use RSI > 70 to short if the market is overbought.
shortCondition = false
// shortCondition = (smaShort > smaLong) and (rsiVal < 35)

// ————— Entry Logic —————
if longCondition
    strategy.entry(id="Long", direction=strategy.long)

if shortCondition
    strategy.entry(id="Short", direction=strategy.short)

// ————— Stop-Loss & Take-Profit Calculation —————
var float stopPrice       = na
var float takeProfitPrice = na

// If we have a position open, we determine SL & TP differently for Long or Short.
if strategy.position_size > 0
    // We are in a Long trade
    stopPrice       := strategy.position_avg_price - (atrVal * atrMult)
    takeProfitPrice := strategy.position_avg_price + ((strategy.position_avg_price - stopPrice) * rrRatio)

    strategy.exit("Exit SL/TP", stop=stopPrice, limit=takeProfitPrice)
else if strategy.position_size < 0
    // We are in a Short trade
    stopPrice       := strategy.position_avg_price + (atrVal * atrMult)
    // For short, the distance from entry to stop is (stopPrice - entry)
    // So the take-profit is entry - that same distance times RR
    takeProfitPrice := strategy.position_avg_price - ((stopPrice - strategy.position_avg_price) * rrRatio)

    strategy.exit("Exit SL/TP", stop=stopPrice, limit=takeProfitPrice)
else
    // No open position → reset plots to na
    stopPrice       := na
    takeProfitPrice := na

// ————— Plot the Planned Stop-Loss & Take-Profit —————
plot(stopPrice,       title="Stop Loss",   color=color.red,   linewidth=2)
plot(takeProfitPrice, title="Take Profit", color=color.green, linewidth=2)


// ————— Label Each Closed Trade (Wins & Losses) —————
var int lastClosedTradeCount = 0
currentClosedCount = strategy.closedtrades

// If there's at least one new closed trade, label it
if currentClosedCount > lastClosedTradeCount
    newTradeIndex = currentClosedCount - 1

    tradeProfit  = strategy.closedtrades.profit(newTradeIndex)
    exitBarIndex = strategy.closedtrades.exit_bar_index(newTradeIndex)
    exitPrice    = strategy.closedtrades.exit_price(newTradeIndex)

    // Win label if profit > 0
    if tradeProfit > 0
        labelText  = "Win: " + str.tostring(tradeProfit)
        labelStyle = label.style_label_up
        labelColor = color.new(color.green, 0)
        label.new(exitBarIndex, exitPrice, text=labelText, style=labelStyle, color=labelColor, size=size.tiny)

    // Loss label if profit < 0
    if tradeProfit < 0
        labelText  = "Loss: " + str.tostring(tradeProfit)
        labelStyle = label.style_label_down
        labelColor = color.new(color.red, 0)
        label.new(exitBarIndex, exitPrice, text=labelText, style=labelStyle, color=labelColor, size=size.tiny)

    lastClosedTradeCount := currentClosedCount
```

> Detail

https://www.fmz.com/strategy/489152

> Last Modified

2025-04-02 11:08:39

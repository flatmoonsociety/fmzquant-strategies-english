
> Name

EMA-Crossover-Strategy-with-Target-Stop-loss-Ratio-and-Fixed-Position-Size based on target stop loss ratio and fixed position
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/956d881252bbdeb9a4253f38c7c576e62cdd942f3fc8295f1a943849944289d0.png)

[trans]
### Overview
This strategy is a trading strategy based on fast and slow exponential moving average (EMA) crossovers. When the fast EMA crosses the slow EMA from bottom to top, the strategy will perform a long trade; when the fast EMA crosses the slow EMA from top to bottom, the strategy will perform a short trade. This strategy uses a target stop-loss ratio to calculate stop-loss and take-profit prices, and trades using a fixed position size.
### Strategy Principles
The main principle of this strategy is to use two EMAs with different periods to capture changes in price trends. When a fast EMA crosses over a slow EMA, it usually means that the price trend has changed. Specifically, when the fast EMA crosses the slow EMA from bottom to top, it indicates that the price may start an upward trend, and the strategy will conduct long transactions at this time; when the fast EMA crosses the slow EMA from top to bottom, it indicates that the price may start a downward trend, at which time the strategy will conduct short transactions.
This strategy also introduces the concept of target stop-loss ratio, which is used to calculate the stop-loss and take-profit prices for each trade. The stop loss price is obtained by multiplying the average opening price by (1 - target stop loss ratio), while the take profit price is obtained by multiplying the average opening price by (1 + target stop loss ratio). This approach dynamically adjusts stop loss and take profit levels based on risk appetite.
In addition, this strategy uses a fixed position size approach to trading, meaning the amount of funds for each trade is fixed and does not adjust based on account balance or other factors. This helps control risk and maintain strategic consistency.
### Strategic Advantages
1. Simple and effective: This strategy is based on the classic EMA crossover principle, which is easy to understand and implement, and can effectively capture changes in price trends.
2. Dynamic stop-loss and take-profit: By introducing a target stop-loss ratio, the strategy can dynamically adjust the stop-loss and take-profit levels according to risk preference, improving the flexibility and adaptability of the strategy.
3. Risk control: Trading with a fixed position size helps control the risk exposure of each transaction and reduces the overall risk of the account.
4. Wide applicability: This strategy can be applied to various financial markets and trading varieties, such as stocks, futures, foreign exchange, etc., and has wide applicability.
### Strategy Risk
1. Parameter sensitivity: The performance of this strategy depends on the parameter selection of EMA, such as the periods of fast EMA and slow EMA. Different parameter combinations may lead to large differences in strategy performance, so parameters need to be carefully optimized and tested.
2. Under-optimization risk: If the strategy parameters are over-optimized, it may cause the strategy to perform poorly on out-of-sample data, which is an over-fitting problem. Therefore, the strategy needs to be fully backtested and forward tested to ensure its robustness.
3. Market risk: The performance of this strategy is affected by market trends and fluctuations. In a volatile market or when the trend is unclear, the strategy may produce more false signals, leading to frequent transactions and capital losses.
4. Black swan events: This strategy may have poor adaptability to extreme market events (such as financial crises, geopolitical conflicts, etc.), and these events may lead to large retracements of the strategy.
### Strategy optimization direction
1. Dynamic parameter optimization: Consider dynamically adjusting the cycle parameters of EMA based on market status or price fluctuation characteristics to adapt to different market environments. This can be achieved by introducing market state judgment indicators or volatility indicators.
2. Signal filtering: Based on the EMA cross signal, other technical indicators or market information are introduced to filter the signal to improve the reliability and accuracy of the signal. For example, it can be combined with volume, momentum indicators or market sentiment indicators, etc.
3. Position management optimization: Consider dynamically adjusting the size of trading positions based on market risk conditions or personal risk preferences instead of using fixed positions. This can be achieved by introducing risk control models or money management rules.
4. Long and short hedging: You can consider holding long and short positions at the same time and construct a market-neutral portfolio to reduce market risks and improve strategic stability.
### Summary
This strategy is a trend following strategy based on the EMA crossover principle. By introducing a target stop loss ratio and a fixed position size mechanism, it captures the price trend while controlling risks. The advantages of the strategy are simplicity and effectiveness, dynamic stop-loss and take-profit and wide applicability, but it also faces challenges such as parameter sensitivity, sub-optimization risk and market risk. In the future, the strategy can be improved and perfected from aspects such as dynamic parameter optimization, signal filtering, position management optimization, and long-short hedging to enhance its robustness and profitability.
|| 

### Overview
This strategy is a trading strategy based on the crossover of fast and slow exponential moving averages (EMAs). When the fast EMA crosses above the slow EMA, the strategy enters a long trade, and when the fast EMA crosses below the slow EMA, the strategy enters a short trade. The strategy uses a target/stop-loss ratio to calculate the stop-loss and take-profit prices and uses a fixed position size for each trade.

### Strategy Principles
The main principle of this strategy is to use two EMAs with different periods to capture changes in price trends. When the fast EMA crosses the slow EMA, it usually indicates a change in the price trend. Specifically, when the fast EMA crosses above the slow EMA from below, it suggests that the price may start an upward trend, and the strategy will enter a long trade. When the fast EMA crosses below the slow EMA from above, it suggests that the price may start a downward trend, and the strategy will enter a short trade.

The strategy also introduces the concept of a target/stop-loss ratio to calculate the stop-loss and take-profit prices for each trade. The stop-loss price is obtained by multiplying the average entry price by (1 - target/stop-loss ratio), while the take-profit price is obtained by multiplying the average entry price by (1 + target/stop-loss ratio). This approach allows for dynamic adjustment of stop-loss and take-profit levels based on risk preferences.

Furthermore, the strategy employs a fixed position size for each trade, meaning that the amount of funds for each trade is fixed and does not adjust based on account balance or other factors. This helps to control risk and maintain consistency in the strategy.

### Strategy Advantages
1. Simple and effective: The strategy is based on the classic principle of EMA crossover, which is easy to understand and implement while effectively capturing changes in price trends.

2. Dynamic stop-loss and take-profit: By introducing the target/stop-loss ratio, the strategy can dynamically adjust stop-loss and take-profit levels based on risk preferences, enhancing the flexibility and adaptability of the strategy.

3. Risk control: By using a fixed position size for each trade, the strategy helps to control the risk exposure of each trade and reduce the overall risk of the account.

4. Wide applicability: The strategy can be applied to various financial markets and trading instruments, such as stocks, futures, and forex, making it widely applicable.

### Strategy Risks
1. Parameter sensitivity: The performance of the strategy depends on the selection of EMA parameters, such as the periods of the fast and slow EMAs. Different parameter combinations may lead to significant differences in strategy performance, so careful optimization and testing of parameters are required.

2. Overoptimization risk: If the strategy parameters are excessively optimized, it may lead to poor performance on out-of-sample data, i.e., overfitting. Therefore, comprehensive backtesting and forward-testing are necessary to ensure the robustness of the strategy.

3. Market risk: The performance of the strategy is influenced by market trends and volatility. During choppy or trendless markets, the strategy may generate more false signals, leading to frequent trades and capital losses.

4. Black swan events: The strategy may have poor adaptability to extreme market events (such as financial crises or geopolitical conflicts), which can cause significant drawdowns.

### Strategy Optimization Directions
1. Dynamic parameter optimization: Consider dynamically adjusting the EMA period parameters based on market conditions or price volatility characteristics to adapt to different market environments. This can be achieved by introducing market state judgment indicators or volatility indicators.

2. Signal filtering: In addition to EMA crossover signals, introduce other technical indicators or market information to filter signals and improve signal reliability and accuracy. For example, volume, momentum indicators, or market sentiment indicators can be incorporated.

3. Position management optimization: Consider dynamically adjusting the trade position size based on market risk conditions or personal risk preferences, rather than using a fixed position size. This can be achieved by introducing risk control models or money management rules.

4. Long-short hedging: Consider simultaneously holding long and short positions to construct a market-neutral portfolio, reducing market risk and improving strategy stability.

### Summary
This strategy is a trend-following strategy based on the principle of EMA crossover, which captures price trends while controlling risk by introducing a target/stop-loss ratio and a fixed position size mechanism. The strategy's advantages lie in its simplicity, effectiveness, dynamic stop-loss and take-profit, and wide applicability. However, it also faces challenges such as parameter sensitivity, overoptimization risk, and market risk. In the future, improvements can be made to the strategy in terms of dynamic parameter optimization, signal filtering, position management optimization, and long-short hedging to enhance its robustness and profitability.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Fast EMA Length|
|v_input_2|50|Slow EMA Length|
|v_input_3|red|EMA Color|
|v_input_4|2|Target/Stop-loss Ratio|
|v_input_5|true|Fixed Position Size (Rs.)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-03-22 00:00:00
end: 2024-03-27 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © KarthicSRSivagnanam

//@version=5
strategy("EMA Crossover Strategy with Target/Stop-loss Ratio and Fixed Position Size", shorttitle="EMA Cross", overlay=true)

// Define input variables
fast_length = input(20, title="Fast EMA Length")
slow_length = input(50, title="Slow EMA Length")
ema_color = input(color.red, title="EMA Color")
target_ratio = input(2, title="Target/Stop-loss Ratio")
position_size = input(1, title="Fixed Position Size (Rs.)")

// Calculate EMAs
ema_fast = ta.ema(close, fast_length)
ema_slow = ta.ema(close, slow_length)

// Plot EMAs
plot(ema_fast, color=ema_color, title="Fast EMA")
plot(ema_slow, color=color.blue, title="Slow EMA")

// Long entry condition: Fast EMA crosses above Slow EMA
longCondition = ta.crossover(ema_fast, ema_slow)

// Short entry condition: Fast EMA crosses below Slow EMA
shortCondition = ta.crossunder(ema_fast, ema_slow)

// Calculate stop-loss and target levels
stopLoss = strategy.position_avg_price * (1 - target_ratio / 100)
takeProfit = strategy.position_avg_price * (1 + target_ratio / 100)

// Plot stop-loss and target levels
plot(stopLoss, color=color.red, title="Stop Loss")
plot(takeProfit, color=color.green, title="Take Profit")

// Entry conditions with fixed position size
if (longCondition)
    strategy.entry("Long", strategy.long, qty = position_size)
    
if (shortCondition)
    strategy.entry("Short", strategy.short, qty = position_size)

// Plot entry signals
plotshape(series=longCondition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(series=shortCondition, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)



```

> Detail

https://www.fmz.com/strategy/446460

> Last Modified

2024-03-28 18:04:32

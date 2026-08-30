
> Name

Long Short Strategy for Moving Average SMA Crossover-SMA-Crossover-Compounding-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/924b32acd5181bd5b65078bc0fc77476982c4848e6e354898d8a577941cf909c.png)
[trans]
#### Overview
This strategy is a long/short strategy based on a simple moving average (SMA) crossover. It uses two SMAs with different periods to generate trading signals. When the fast SMA crosses the slow SMA from below, a long signal is generated; when the fast SMA crosses the slow SMA from above, a short signal is generated. This strategy uses the concept of compound interest to dynamically adjust position size based on current account balance and accumulated profits. This allows the account balance to grow over time, thereby increasing the profitability of the strategy.
#### Strategy Principle
The core principle of this strategy is to use SMA crossovers to generate trading signals. The SMA is a trend-following indicator that determines the overall direction of prices by averaging closing prices over a past period. By using two SMAs with different periods, the strategy can capture changes in market trends. When the fast SMA crosses above the slow SMA, it indicates that an upward trend may be forming, so the strategy enters the long position; conversely, when the fast SMA crosses below the slow SMA, it indicates that a downtrend may be forming, so the strategy enters the short position.
The strategy uses the concept of compound interest to manage position sizing. It calculates the position size based on the current account balance and accumulated profits. This means that as the account balance grows, the strategy will increase the position size accordingly to maximize profit potential. By dynamically adjusting position sizes, strategies can take full advantage of account growth.
#### Strategic Advantages
1. Simple and easy to understand: This strategy is based on SMA crossover and is a simple and easy to understand trend following strategy. It does not require complex market timing or subjective judgment, making the strategy easy to implement and manage.
2. Trend following: By using SMA crossover, this strategy can effectively capture market trends. It allows for long trades in uptrends and short trades during downtrends, maximizing profit potential.
3. Dynamic position management: The strategy uses the concept of compound interest to manage position size. By dynamically adjusting position sizes based on account balance and accumulated profits, strategies can take full advantage of account growth and increase profitability.
4. Highly adaptable: This strategy can be applied to various markets and asset classes, such as stocks, foreign exchange, commodities, etc. Its simplicity and adaptability make it a versatile trading strategy.
#### Strategy Risk
1. Market risk: This strategy relies on the persistence of market trends. In the event of market volatility or trend reversal, the strategy may suffer losses. Factors such as emergencies and the release of economic data may cause sudden changes in market trends and adversely affect strategies.
2. Parametric risk: The performance of the strategy depends on the SMA cycle selection. Different cycle combinations may produce different results. Poorly chosen parameters can result in poor strategy performance or missed trading opportunities.
3. Overtrading: During periods of market volatility, frequent SMA crossovers may lead to overtrading, increasing transaction costs and slippage, thereby affecting the overall performance of the strategy.
4. Compound interest risk: Although compound interest can improve the profitability of a strategy, it also amplifies the risk of loss. In the event of continuous losses, the account balance may shrink rapidly, limiting the strategy's ability to recover.
#### Strategy optimization direction
1. Parameter optimization: Optimize the SMA cycle and find the best parameter combination to improve the performance of the strategy. Historical data can be used for backtesting, and optimization algorithms such as grid search or genetic algorithms can be used to find optimal parameters.
2. Risk management: Introduce risk management measures, such as stop loss and take profit, to limit the loss of a single transaction and protect profits. Stop loss and take profit levels can be dynamically adjusted based on market volatility to adapt to different market conditions.
3. Trend filtering: In addition to SMA crossover, other trend confirmation indicators, such as MACD or ADX, are introduced to filter out false signals and improve signal quality. Only trade when multiple indicators confirm the trend at the same time to increase the reliability of the strategy.
4. Position management optimization: Optimize the position management rules of the compound interest strategy, such as introducing risk control measures to limit the risk exposure of a single transaction. Consider using the Kelly formula or a fixed risk percentage to determine position size for each trade to balance risk and reward.
#### Summary
This strategy is a trend following strategy based on SMA crossover and uses the concept of compound interest to manage position size. Its advantages are simplicity and ease of understanding, strong trend tracking capabilities, dynamic position management and strong adaptability. However, it also faces challenges such as market risk, parameter risk, excessive trading and compound interest risk. In order to improve the strategy, parameter optimization, introduction of risk management measures, trend filtering and optimization of position management rules can be considered. Through continuous optimization and improvement, the strategy is expected to achieve stable performance under various market conditions.
|| 

#### Overview
This strategy is a long/short strategy based on the crossover of Simple Moving Averages (SMAs). It uses two SMAs with different periods to generate trading signals. When the fast SMA crosses above the slow SMA from below, it generates a long signal; when the fast SMA crosses below the slow SMA from above, it generates a short signal. The strategy incorporates the concept of compounding, dynamically adjusting position size based on the current account balance and cumulative profit. This allows the account balance to grow over time, enhancing the strategy's profitability.

#### Strategy Principle
The core principle of this strategy is to utilize SMA crossovers to generate trading signals. SMA is a trend-following indicator that determines the overall direction of the price by averaging the closing prices over a specified period. By using two SMAs with different periods, the strategy can capture changes in market trends. When the fast SMA crosses above the slow SMA, it indicates that an uptrend may be forming, prompting the strategy to enter a long position. Conversely, when the fast SMA crosses below the slow SMA, it suggests that a downtrend may be developing, leading the strategy to enter a short position.

The strategy employs the concept of compounding to manage position sizing. It calculates the position size based on the current account balance and cumulative profit. This means that as the account balance grows, the strategy proportionally increases the position size, maximizing the profit potential. By dynamically adjusting the position size, the strategy can fully capitalize on the advantages of account growth.

#### Strategy Advantages
1. Simplicity: The strategy is based on SMA crossovers, making it a simple and straightforward trend-following strategy. It does not require complex market timing or subjective judgments, making it easy to implement and manage.

2. Trend-following: By utilizing SMA crossovers, the strategy effectively captures market trends. It can engage in long trades during uptrends and short trades during downtrends, maximizing profit potential.

3. Dynamic Position Sizing: The strategy employs the concept of compounding to manage position sizes. By dynamically adjusting the position size based on the account balance and cumulative profit, the strategy can fully leverage the benefits of account growth, enhancing profitability.

4. Adaptability: The strategy can be applied to various markets and asset classes, such as stocks, forex, commodities, etc. Its simplicity and adaptability make it a versatile trading strategy.

#### Strategy Risks
1. Market Risk: The strategy relies on the persistence of market trends. It may suffer losses during market volatility or trend reversals. Unexpected events, economic data releases, and other factors can cause sudden changes in market direction, adversely affecting the strategy.

2. Parameter Risk: The strategy's performance depends on the choice of SMA periods. Different period combinations may yield different results. Improper parameter selection can lead to suboptimal strategy performance or missed trading opportunities.

3. Overtrading: During volatile market conditions, frequent SMA crossovers may result in overtrading, increasing transaction costs and slippage, which can impact the overall performance of the strategy.

4. Compounding Risk: While compounding can enhance the strategy's profitability, it also amplifies the risk of losses. In the event of consecutive losses, the account balance can rapidly diminish, limiting the strategy's recovery potential.

#### Strategy Optimization Directions
1. Parameter Optimization: Optimize the periods of the SMAs to find the optimal parameter combination that improves the strategy's performance. Utilize historical data for backtesting and employ optimization algorithms such as grid search or genetic algorithms to identify the best parameters.

2. Risk Management: Introduce risk management measures, such as stop-loss and take-profit, to limit losses per trade and protect profits. Dynamically adjust stop-loss and take-profit levels based on market volatility to adapt to different market conditions.

3. Trend Confirmation: In addition to SMA crossovers, incorporate other trend confirmation indicators, such as MACD or ADX, to filter out false signals and improve signal quality. Only execute trades when multiple indicators simultaneously confirm the trend, enhancing the reliability of the strategy.

4. Position Sizing Optimization: Optimize the compounding strategy's position sizing rules by introducing risk control measures to limit risk exposure per trade. Consider using the Kelly Criterion or fixed risk percentage to determine the position size for each trade, balancing risk and reward.

#### Conclusion
This strategy is a trend-following strategy based on SMA crossovers, incorporating the concept of compounding to manage position sizes. Its strengths lie in its simplicity, trend-following ability, dynamic position sizing, and adaptability. However, it also faces challenges such as market risk, parameter risk, overtrading, and compounding risk. To improve the strategy, consider parameter optimization, introducing risk management measures, trend confirmation, and optimizing position sizing rules. With continuous optimization and refinement, the strategy has the potential to achieve consistent performance across various market conditions.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|9|Fast SMA Length|
|v_input_int_2|21|Slow SMA Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-01 00:00:00
end: 2024-03-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Umesh SMA Crossover Strategy", overlay=true)

// Input parameters
fast_length = input.int(9, title="Fast SMA Length")
slow_length = input.int(21, title="Slow SMA Length")

// Calculate SMAs
fast_sma = ta.sma(close, fast_length)
slow_sma = ta.sma(close, slow_length)

// Plot SMAs
plot(fast_sma, color=color.blue, title="Fast SMA")
plot(slow_sma, color=color.red, title="Slow SMA")

// Strategy logic
longCondition = ta.crossover(fast_sma, slow_sma)
shortCondition = ta.crossunder(fast_sma, slow_sma)

// Initialize cumulative profit with netprofit
var float cumulative_profit = na
if (na(cumulative_profit))
    cumulative_profit := strategy.netprofit

// // Initialize starting balance
// var float starting_balance = na
// if (na(starting_balance))
//     starting_balance := strategy.equity

// Initialize starting balance
var float starting_balance = na
if (na(starting_balance))
    starting_balance := 100000.0 // Initial balance

// Calculate profit or gains
if (strategy.opentrades != 0)
    cumulative_profit := strategy.netprofit + (strategy.equity - starting_balance)

// Calculate position size based on current balance and cumulative profit
//position_size = 100000 
position_size = starting_balance + cumulative_profit

// Entry conditions
if (longCondition)
    strategy.entry("Long", strategy.long, qty = position_size / close)
if (shortCondition)
    strategy.entry("Short", strategy.short, qty = position_size / close)

// // Entry conditions
// if (longCondition)
//     strategy.entry("Long", strategy.long, qty = 100000 / close)
// if (shortCondition)
//     strategy.entry("Short", strategy.short, qty = 100000 / close)


// Plot strategy.equity 
plot(strategy.equity, color=color.green, title="Cumulative Profit")

// Print cumulative profit value on chart
label.new(x = bar_index, y = strategy.equity, text = str.tostring(strategy.equity), style=label.style_label_down, color=color.new(color.green, 0), size=size.small)
// Plot cumulative profit
plot(cumulative_profit, color=color.green, title="Cumulative Profit")

// Print cumulative profit value on chart
label.new(x = bar_index, y = cumulative_profit, text = str.tostring(cumulative_profit), style=label.style_label_down, color=color.new(color.green, 0), size=size.small)

// Plot cumulative profit
plot(position_size, color=color.green, title="Cumulative Profit")

// Print cumulative profit value on chart
label.new(x = bar_index, y = position_size, text = str.tostring(position_size), style=label.style_label_down, color=color.new(color.green, 0), size=size.small)

```

> Detail

https://www.fmz.com/strategy/446758

> Last Modified

2024-04-01 11:11:02

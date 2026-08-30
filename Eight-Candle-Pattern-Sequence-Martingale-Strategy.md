
> Name

Eight-Candle-Pattern-Sequence-Martinale-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d967b6e8a8f812c9cffb.png)
![IMG](https://www.fmz.com/upload/asset/2d914cc413d66b3912592.png)


[trans]

#### Overview
The eight-order candle pattern sequence martingale strategy is a quantitative trading strategy that combines specific candle sequence recognition with the martingale money management system. This strategy identifies potential market reversal points by analyzing the color pattern of 8 consecutive candles, while applying the Martingale betting system to manage trade size with a view to making up for previous losses by increasing positions after consecutive losses. The strategy mainly looks for two specific 8-candle sequences as entry signals, which are used for long and short positions respectively, while controlling risks through the fund management mechanism.
#### Strategy Principle
The core logic of the strategy is based on the identification of specific candle color sequences:
1. **Bull entry conditions**: When a specific 8-candle sequence "Down-Down-Down-Down-Up-Down-Up-Down" appears, the strategy triggers a long signal.
2. **Short entry conditions**: When a specific 8-candle sequence "Down-Down-Down-Up-Down-Up-Down-Up" appears, the strategy triggers a short signal.
3. **Martingal Fund Management**:
   - The initial position is determined by the "Admission Fund" parameter set by the user
   - After each transaction loses money, the position of the next transaction will be increased according to the "multiplier" parameter (default is 2 times)
   - If the transaction is profitable, the position is reset to the initial setting value
   - Set a maximum fund limit to ensure that a single transaction does not exceed available funds
Strategies use candle color sequences to capture specific patterns of movement in the market, believing that these specific sequences may signal a reversal in the market's direction in the short term. At the same time, the Martingale system attempts to cover previous consecutive losses with fewer profitable trades by increasing positions after losses.
#### Strategic Advantages
1. **Clarity of pattern recognition**: The strategy uses a clear 8-candle color sequence as entry conditions, which reduces the interference of subjective judgment and makes trading signals more objective and repeatable.
2. **Adaptability of fund management**: The Martingale system allows strategies to automatically adjust position sizes after encountering losses. This mechanism can help recover previous losses during market shocks or short-term adverse trends.
3. **Visual trading signals**: The strategy provides clear visual signal marks (BUY/SELL labels) and statistical tables, allowing traders to intuitively understand the execution and historical performance of the strategy.
4. **Risk Control Mechanism**: By setting a maximum capital limit, the strategy can prevent the problem of capital exhaustion caused by excessive position expansion in the event of continuous losses.
5. **Parameter Flexibility**: The strategy allows users to adjust the initial entry capital, Martingale multiplier and maximum capital limit, allowing traders to customize the strategy according to their own risk appetite and capital status.
#### Strategy Risk
1. **Inherent Risks of the Martingale System**:
   - Consecutive losses can lead to an exponential increase in capital requirements
   - Even if a maximum capital limit is set, long-term continuous losses may still result in large account losses
   - In a strong trending market, reverse operations may result in continuous losses triggering multiple martingale positions.
2. **Limitations of fixed pattern recognition**:
   - The effectiveness of a specific color sequence of 8 candles can vary significantly in different market environments and time periods
   - Does not consider richer price information such as the size of the candle's body, the length of the shadow line, etc.
   - In highly volatile markets, this simple color pattern can generate too many false signals
3. **Stop loss mechanism is missing**:
   - There is no clear stop loss mechanism in the code, which may lead to continued expansion of losses
   - The strategy relies on the Martingale system to deal with losses rather than exiting promptly.
4. **Fund Management Risk**:
   - In the case of continuous losses, even with the maximum capital limit, it may still result in a large proportion of account losses
   - The strategy does not consider the overall capital withdrawal limit and lacks control over the overall account risk
#### Strategy optimization direction
1. **Add price structure analysis**:
   - In addition to simple candle color, factors such as candle size, shadow length, trading volume, etc. can be considered
   - Combine support, resistance, trend lines and other technical indicators to filter out low-quality signals
   - Trend judgment indicators (such as moving averages) can be added to avoid counter-trend operations in strong trends
2. **Improve the fund management system**:
   - Introducing an anti-martingale system to reduce rather than increase positions after losses
   - Dynamically adjust position size based on market volatility instead of increasing by a fixed multiple
   - Set total account risk limits, such as suspending trading when the total loss reaches a certain percentage
3. **Add stop loss and profit mechanism**:
   - Implement a stop-loss mechanism with a fixed ratio or ATR multiple to limit the loss of a single transaction
   - Add a trailing stop function to lock in some profits
   - Set profit-taking conditions based on price structure or time
4. **Optimize entry conditions**:
   - Backtest optimization of specific 8 candle sequences to find more effective pattern combinations
   - Consider adding time filters to avoid trading during specific inefficient market periods
   - Confirm the validity of the signal in conjunction with volume
5. **Add adaptive mechanism**:
   - Dynamically adjust parameters based on recent strategy performance
   - Add market environment judgment and apply different trading rules under different market conditions
   - Achieve multi-time cycle confirmation and improve signal quality
#### Summary
The Eight-Order Candle Pattern Sequence Martingale strategy combines specific candle sequence recognition with the Martingale money management system to capture potential market reversal opportunities by looking for specific 8-candle color patterns. The main advantages of this strategy are the clear entry conditions and adaptive money management mechanism, but it also faces the risks inherent in the Martingale system and the limitations of simple pattern recognition.
In order to improve the robustness and profitability of the strategy, it is recommended to focus on optimizing the fund management system and reduce reliance on traditional Martingale; add more comprehensive price structure analysis to improve signal quality; add an effective stop-loss mechanism to control single transaction risks; and increase the market adaptability of the strategy so that it can maintain relatively stable performance in different market environments.
Ultimately, any strategy based on the Martingale system needs to be used with caution, and traders should fully understand its potential risks and ensure the safety and effectiveness of the strategy in actual trading through strict risk control and adequate backtesting. ||
#### Overview
The Eight-Candle Pattern Sequence Martingale Strategy is a quantitative trading approach that combines specific candle sequence recognition with a Martingale money management system. The strategy identifies potential market reversal points by analyzing the color pattern of eight consecutive candles, while applying the Martingale betting system to manage trade sizes, aiming to recover previous losses by increasing position sizes after consecutive losses. The strategy primarily looks for two specific eight-candle sequences as entry signals for long and short positions, while simultaneously controlling risk through its money management mechanism.

#### Strategy Principles
The core logic of the strategy is based on identifying specific candle color sequences:

1. **Long Entry Condition**: When the specific 8-candle sequence "down-down-down-down-up-down-up-down" appears, the strategy triggers a buy signal.
2. **Short Entry Condition**: When the specific 8-candle sequence "down-down-down-up-down-up-down-up" appears, the strategy triggers a sell signal.
3. **Martingale Money Management**:
   - Initial position size is determined by the user-defined "Initial Entry" parameter
   - After each losing trade, the next trade's position size increases according to the "Multiplier" parameter (default is 2x)
   - If a trade is profitable, the position size resets to the initial value
   - Maximum capital limit is set to ensure that a single trade doesn't exceed available funds

The strategy uses candle color sequences to capture specific oscillation patterns in the market, believing that these particular sequences may indicate short-term directional reversals. Meanwhile, the Martingale system attempts to cover previous consecutive losses by increasing position sizes, trying to recover with fewer profitable trades.

#### Strategy Advantages
1. **Clear Pattern Recognition**: The strategy uses well-defined 8-candle color sequences as entry conditions, reducing subjective judgment interference and making trading signals more objective and reproducible.

2. **Adaptive Money Management**: The Martingale system allows the strategy to automatically adjust position sizes after losses, which can help recover previous losses during market oscillations or short-term counter-trend movements.

3. **Visualized Trading Signals**: The strategy provides clear visual signal markers (BUY/SELL labels) and statistical tables, allowing traders to intuitively understand the strategy's execution and historical performance.

4. **Risk Control Mechanism**: By setting a maximum capital limit, the strategy can prevent excessive position expansion that could deplete funds during consecutive losses.

5. **Parameter Flexibility**: The strategy allows users to adjust the initial entry capital, Martingale multiplier, and maximum capital limit, enabling traders to customize the strategy according to their risk preferences and capital situation.

#### Strategy Risks
1. **Inherent Risks of the Martingale System**:
   - Consecutive losses can lead to exponential growth in capital requirements
   - Even with a maximum capital limit, long-term consecutive losses may still result in significant account drawdowns
   - In strong trending markets, counter-trend operations may trigger multiple Martingale position increases due to consecutive losses

2. **Limitations of Fixed Pattern Recognition**:
   - The effectiveness of specific 8-candle color sequences may vary significantly across different market environments and timeframes
   - The strategy doesn't consider more comprehensive price information such as candle body size or shadow length
   - In highly volatile markets, this simple color pattern may generate too many false signals

3. **Lack of Stop-Loss Mechanism**:
   - There is no clear stop-loss mechanism in the code, which may lead to continuously expanding losses
   - The strategy relies on the Martingale system to address losses rather than timely stop-loss exits

4. **Money Management Risks**:
   - Even with maximum capital limits, consecutive losses may still cause a large proportion of account drawdowns
   - The strategy doesn't consider overall capital drawdown limits, lacking control over total account risk

#### Strategy Optimization Directions
1. **Add Price Structure Analysis**:
   - Consider factors such as candle size, shadow length, and volume in addition to simple candle colors
   - Incorporate technical indicators like support/resistance levels and trend lines to filter low-quality signals
   - Add trend determination indicators (such as moving averages) to avoid counter-trend operations in strong trending markets

2. **Improve Money Management System**:
   - Introduce an anti-Martingale system, reducing rather than increasing position sizes after losses
   - Dynamically adjust position sizes based on market volatility instead of fixed multiplier increases
   - Set total account risk limits, for example, pausing trading when total losses reach a certain percentage

3. **Add Stop-Loss and Profit-Taking Mechanisms**:
   - Implement fixed percentage or ATR multiple stop-loss mechanisms to limit single trade losses
   - Add trailing stop-loss functionality to lock in partial profits
   - Set profit-taking conditions based on price structure or time

4. **Optimize Entry Conditions**:
   - Backtest and optimize the specific 8-candle sequences to find more effective pattern combinations
   - Consider adding time filters to avoid trading during specific inefficient market sessions
   - Incorporate volume confirmation to validate signal effectiveness

5. **Increase Adaptive Mechanisms**:
   - Dynamically adjust parameters based on recent strategy performance
   - Add market environment assessment to apply different trading rules in different market states
   - Implement multiple timeframe confirmation to improve signal quality

#### Summary
The Eight-Candle Pattern Sequence Martingale Strategy combines specific candle sequence recognition with a Martingale money management system, seeking potential market reversal opportunities by identifying specific 8-candle color patterns. The strategy's main advantages are clear entry conditions and adaptive money management, but it also faces inherent risks of the Martingale system and limitations of simple pattern recognition.

To improve the strategy's robustness and profitability, it is recommended to focus on optimizing the money management system, reducing dependence on traditional Martingale; adding more comprehensive price structure analysis to improve signal quality; implementing effective stop-loss mechanisms to control individual trade risk; and increasing the strategy's market adaptability to maintain relatively stable performance across different market environments.

Ultimately, any strategy based on the Martingale system should be used with caution. Traders should fully understand its potential risks and ensure the strategy's safety and effectiveness in actual trading through strict risk control and thorough backtesting.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-04-08 00:00:00
end: 2025-04-07 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=6
strategy("SUPRA MTS1", overlay=true)

// Martingale Parameters
initial_bet = input.float(1, title="Initial Bet")         // Initial bet amount
multiplier = input.float(2, title="Martingale Multiplier") // Multiplier in case of loss
max_capital = input.float(100, title="Maximum Capital")    // Loss limit

// Define if the candle is bullish (green) or bearish (red)
is_green = close > open
is_red = close < open

// Create buffers to store the last 8 candles
sequence_green_red =  is_red[7] and is_red[6] and is_red[5] and is_red[4] and is_green[3] and is_red[2] and is_green[1] and is_red
sequence_red_green = is_red[7] and is_red[6] and is_red[5] and is_green[4] and is_red[3] and is_green[2] and is_red[1] and is_green

// Martingale control variables
var float bet = initial_bet
var float current_capital = max_capital

// Counters for buy and sell signals
var int total_buys = 0
var int total_sells = 0

// If the last trade was a loss, double the bet (within capital limit)
new_bet = bet * multiplier
if strategy.opentrades > 0 and strategy.position_size == 0
    bet := new_bet < current_capital ? new_bet : current_capital // Ensure bet doesn't exceed capital

// If won, reset to initial bet
if strategy.opentrades == 0
    bet := initial_bet

// Entry conditions
if sequence_green_red
    strategy.entry("Buy", strategy.long, bet)
    total_buys := total_buys + 1

if sequence_red_green
    strategy.entry("Sell", strategy.short, bet)
    total_sells := total_sells + 1

// Plot signals on the chart
plotshape(sequence_green_red, location=location.belowbar, color=color.green, style=shape.labelup, title="Buy", text="BUY")
plotshape(sequence_red_green, location=location.abovebar, color=color.red, style=shape.labeldown, title="Sell", text="SELL")

// Create alert table
var table tbl = table.new(position=position.top_right, columns=2, rows=3, border_width=1)
if bar_index == 0
    table.cell(tbl, 0, 0, "Type", text_color=color.white, bgcolor=color.blue)
    table.cell(tbl, 1, 0, "Total", text_color=color.white, bgcolor=color.blue)
    table.cell(tbl, 0, 1, "Buys", text_color=color.white, bgcolor=color.green)
    table.cell(tbl, 1, 1, str.tostring(total_buys), text_color=color.white, bgcolor=color.green)
    table.cell(tbl, 0, 2, "Sells", text_color=color.white, bgcolor=color.red)
    table.cell(tbl, 1, 2, str.tostring(total_sells), text_color=color.white, bgcolor=color.red)

// Update table on every candle
if bar_index > 0
    table.cell(tbl, 1, 1, str.tostring(total_buys), text_color=color.white, bgcolor=color.green)
    table.cell(tbl, 1, 2, str.tostring(total_sells), text_color=color.white, bgcolor=color.red)

```

> Detail

https://www.fmz.com/strategy/489742

> Last Modified

2025-04-08 10:53:33

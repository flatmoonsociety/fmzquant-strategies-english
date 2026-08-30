
> Name

Multi-Level-RSI-Cross-Under-Regression-Pyramiding-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/796a1bbb87240fe478e9d01f43fec0fcbd62f2ba57bb43fe4203362409c895fb.png)
![IMG](assets/images/62133987eacf13d4a47bbc2395803e3342c205a349892815b3774d35bcd6f0b9.png)



[trans]
#### Overview
This strategy is an automated trading system based on the Relative Strength Index (RSI), which primarily captures potential rebound opportunities by identifying oversold conditions in the market. The strategy adopts a progressive position building method, gradually establishing multiple positions when RSI crosses at a low level, and controls risks by setting profit targets. The system is designed with a flexible fund management mechanism. Each transaction uses 6.6% of the total account amount for operation, allowing up to 15 pyramid positions.
#### Strategy Principles
The core logic of the strategy is based on the following key elements:
1. Entry signal: A buy signal is triggered when the 14-period RSI indicator falls below the oversold level of 28.5
2. Position management: A single position uses 6.6% of the account equity, and a maximum of 15 incremental positions are allowed.
3. Profit taking: when the price reaches an increase of 900% of the average opening price, close 50% of the position
4. Visual display: Mark buy and sell signals, RSI curve, entry price and target price on the chart
The strategy determines the market trend by observing the performance of the RSI indicator in the oversold area, and gradually builds a position when an oversold signal appears to reduce the cost of building a position.
#### Strategic Advantages
1. Systematic position building: automatically identify trading opportunities through preset RSI parameters to avoid subjective bias caused by human judgment.
2. Risk diversification: Adopt a progressive position building method to establish multiple positions at different prices to effectively diversify risks.
3. Flexible adaptation: strategy parameters can be adjusted according to different market environments and personal risk preferences
4. Profit protection: Set a clear profit target, automatically reduce the position when the target is reached, and lock in part of the profit
5. Fund efficiency: Improve the efficiency of fund use through reasonable position control and position addition mechanisms
#### Strategy Risk
1. Trend risk: In a strong downward trend, position opening signals may be triggered frequently, resulting in capital losses.
2. Parameter sensitivity: Improper settings of RSI parameters, position opening ratio, etc. may affect strategy performance.
3. Market Liquidity: In an illiquid market, it may be difficult to complete a transaction at the target price
4. Fund management: Excessive addition of positions may lead to excessive risk exposure
Solution:
- Added trend filter to suspend position opening in clear downtrend
- Optimize parameter settings through backtesting
- Set maximum drawdown limit
- Dynamically adjust the threshold for adding positions
#### Strategy optimization direction
1. Dynamic parameters: automatically adjust RSI parameters and position opening conditions according to market volatility
2. Stop-loss mechanism: Add a trailing stop-loss function to better control risks
3. Market filtering: Add trading volume, trend and other filtering conditions to improve signal quality
4. Exit optimization: Design a more flexible profit-taking mechanism, such as segmented position reduction
5. Risk control: Increase maximum drawdown limit and risk exposure control
#### Summary
This strategy uses the RSI indicator to identify oversold opportunities, and combines pyramid positioning and fixed-proportion profit taking to build a complete trading system. The advantage of the strategy lies in systematic operation and risk diversification, but it is necessary to pay attention to the impact of market trends and parameter settings on strategy performance. By adding optimization measures such as dynamic parameter adjustment, stop-loss mechanism and market filtering, the stability and profitability of the strategy can be further improved. ||
#### Overview
This strategy is an automated trading system based on the Relative Strength Index (RSI), primarily designed to capture potential rebounds by identifying oversold market conditions. The strategy employs a progressive position-building approach, gradually establishing multiple positions when RSI crosses at low levels, with risk control through profit targets. The system features a flexible capital management mechanism, using 6.6% of total account equity per trade, allowing up to 15 pyramiding entries.

#### Strategy Principles
The core logic of the strategy is based on the following key elements:
1. Entry Signal: Buy signals are triggered when 14-period RSI crosses below the oversold level of 28.5
2. Position Management: Single position size is 6.6% of account equity, allowing up to 15 progressive entries
3. Profit Taking: Closes 50% of the position when price reaches 900% gain from entry price
4. Visualization: Displays buy/sell signals, RSI curve, entry price, and target price on charts
The strategy observes RSI behavior in oversold territory to determine market trends, gradually building positions upon oversold signals to reduce average entry costs.

#### Strategy Advantages
1. Systematic Entry: Automatically identifies trading opportunities through preset RSI parameters, avoiding subjective bias
2. Risk Diversification: Uses progressive position building at different price levels, effectively spreading risk
3. Flexibility: Strategy parameters can be adjusted according to different market environments and risk preferences
4. Profit Protection: Sets clear profit targets with automatic position reduction to lock in partial gains
5. Capital Efficiency: Optimizes capital utilization through proper position control and pyramiding mechanism

#### Strategy Risks
1. Trend Risk: Frequent entry signals may trigger during strong downtrends, leading to losses
2. Parameter Sensitivity: Improper settings of RSI parameters and position sizing can affect strategy performance
3. Market Liquidity: Difficulty executing trades at target prices in illiquid markets
4. Capital Management: Excessive pyramiding may lead to overexposure
Solutions:
- Add trend filters to pause entries during clear downtrends
- Optimize parameters through backtesting
- Set maximum drawdown limits
- Dynamically adjust pyramiding thresholds

#### Strategy Optimization
1. Dynamic Parameters: Automatically adjust RSI parameters and entry conditions based on market volatility
2. Stop-Loss Mechanism: Add trailing stop-loss functionality for better risk control
3. Market Filters: Incorporate volume and trend filters to improve signal quality
4. Exit Optimization: Design more flexible profit-taking mechanisms, such as staged position reduction
5. Risk Control: Add maximum drawdown limits and exposure control

#### Summary
The strategy identifies oversold opportunities through RSI indicator, combining pyramiding entries with fixed-ratio profit-taking to create a complete trading system. Its strengths lie in systematic operation and risk diversification, but attention must be paid to market trends and parameter settings affecting strategy performance. The strategy's stability and profitability can be further enhanced through dynamic parameter adjustment, stop-loss mechanisms, and market filters.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-09-15 00:00:00
end: 2024-12-10 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("RSI Cross Under Strategy", overlay=true, initial_capital=1500, default_qty_type=strategy.percent_of_equity, default_qty_value=6.6)

// Input parameters
rsiLength = input(14, "RSI Length")
rsiOversold = input(28.5, "RSI Oversold Level")
profitTarget = input(900, "Profit Target (%)")
maxPyramiding = input(15, "Max Pyramiding")

// Calculate RSI
rsi = ta.rsi(close, rsiLength)

// Detect RSI crossunder
rsiCrossunder = ta.crossunder(rsi, rsiOversold)

// Calculate the profit target price
entryPrice = strategy.position_avg_price
targetPrice = entryPrice * (1 + profitTarget / 100)

// Buy condition
if (rsiCrossunder and strategy.position_size <= maxPyramiding * strategy.equity * 0.066)
    strategy.entry("Buy", strategy.long)

// Take profit condition
if (strategy.position_size > 0 and high >= targetPrice)
    strategy.close("Buy", qty_percent = 50)

// Plot buy signals
plotshape(rsiCrossunder, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)

// Plot sell signals (when position is partially closed)
plotshape(strategy.position_size > 0 and high >= targetPrice, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)

// Plot RSI
plot(rsi, "RSI", color=color.blue, linewidth=2)
hline(rsiOversold, "RSI Oversold", color=color.red, linestyle=hline.style_dashed)

// Plot entry and target prices
plot(strategy.position_size > 0 ? entryPrice : na, "Entry Price", color=color.green, linewidth=2, style=plot.style_linebr)
plot(strategy.position_size > 0 ? targetPrice : na, "Target Price", color=color.red, linewidth=2, style=plot.style_linebr)

// Display strategy information
var table infoTable = table.new(position.top_right, 3, 6, border_width=1)
table.cell(infoTable, 0, 0, "Strategy Info", bgcolor=color.blue, text_color=color.white)
table.cell(infoTable, 0, 1, "RSI Length: " + str.tostring(rsiLength))
table.cell(infoTable, 0, 2, "RSI Oversold: " + str.tostring(rsiOversold))
table.cell(infoTable, 0, 3, "Profit Target: " + str.tostring(profitTarget) + "%")
table.cell(infoTable, 0, 4, "Order Size: 6.6% of total")
table.cell(infoTable, 0, 5, "Max Pyramiding: " + str.tostring(maxPyramiding) + " times")

```

> Detail

https://www.fmz.com/strategy/482916

> Last Modified

2025-02-27 17:21:37

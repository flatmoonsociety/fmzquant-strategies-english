
> Name

Long-Grid-Strategy-Based-on-Drawdown-and-Target-Profit
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ce6cab9b294d00c93a.png)

[trans]
#### Overview
This strategy is a grid trading strategy that increases positions based on the price drop and closes positions when a fixed profit target is reached. The core logic of the strategy is to buy when the market falls to a preset range, close the position as a whole when the price rebounds to reach the target profit, and obtain profits by repeating this process. This strategy is particularly suitable for capturing short-term rebound opportunities in volatile markets.
#### Strategy Principle
The strategy uses a composite mechanism of grid trading and directional take-profit:
1. Initial position opening: After the set start time, the system will open a position for the first time at the current price when triggered for the first time.
2. Position addition mechanism: When the price falls by more than the preset decline (default 5%) relative to the initial position opening price, additional purchases will be made.
3. Position closing mechanism: When the price rises above the preset profit target (default 5%) relative to the initial opening price, the system will close all positions.
4. Statistical tracking: The system will count the number of transactions and accumulated profits in real time, and display them dynamically on the chart.
#### Strategic Advantages
1. High degree of automation: The strategy is completely systematic, requires no manual intervention, and can run continuously 24 hours a day.
2. Risk diversification: By building a position in batches, the risk of a single position can be effectively reduced.
3. Clear profit taking: Set a fixed profit target, and once the target is reached, you will immediately be safe.
4. Strong adaptability: Through parameter adjustment, it can adapt to different market environments and trading varieties.
5. Strong execution: The strategy has clear logic and is not affected by subjective emotions.
#### Strategy Risk
1. Trend risk: In a continued downward trend, positions may be continuously added, resulting in increased losses.
2. Fund management risk: If reasonable position control is not set up, excessive funds may be occupied due to excessive positioning.
3. Risk of slippage: When the market fluctuates violently, serious slippage may occur, affecting the performance of the strategy.
4. Parameter sensitivity: The strategy effect is relatively sensitive to parameter settings, and parameters need to be adjusted in time under different market environments.
#### Strategy optimization direction
1. Dynamic stop loss: It is recommended to add a dynamic stop loss mechanism based on ATR or volatility to prevent sharp declines.
2. Position management: Dynamic position management based on account equity can be introduced to ensure more reasonable use of funds.
3. Market screening: Add trend judgment indicators and suspend strategy operation in markets with obvious trends.
4. Profit target optimization: Dynamic profit targets can be designed and adaptively adjusted according to market fluctuations.
5. Position addition optimization: You can design a progressive position increase quantity to avoid excessive position building in the early stage.
#### Summary
This is a grid trading strategy with a simple but practical structure. It builds positions in batches based on the preset decline range and closes the positions uniformly when the target profit is reached. The core advantage of the strategy lies in the certainty of its execution and the diversification of risks, but when using it, attention needs to be paid to the selection of the market environment and the optimization of parameters. By adding dynamic stops and improving position management, the strategy still has a lot of room for optimization. When using it in real trading, it is recommended to conduct sufficient backtesting first and make parameter adjustments based on the actual market conditions. ||
#### Overview
This strategy is a grid trading system that adds positions based on price drops and closes positions when reaching a fixed profit target. The core logic is to buy when the market drops to a preset percentage, close all positions when the price rebounds to the target profit, and generate returns by repeatedly executing this process. This strategy is particularly suitable for capturing short-term rebounds in oscillating markets.

#### Strategy Principle
The strategy employs a combined mechanism of grid trading and directional take-profit:
1. Initial Position: After the set start time, the system takes the first position at the current price when triggered.
2. Position Adding Mechanism: Additional buying is triggered when the price drops beyond the preset percentage (default 5%) relative to the initial entry price.
3. Position Closing Mechanism: When the price rises above the preset profit target (default 5%) relative to the initial entry price, the system closes all positions.
4. Statistical Tracking: The system tracks trade counts and cumulative profits in real-time, displaying them dynamically on the chart.

#### Strategy Advantages
1. High Automation: The strategy is fully systematic, requiring no manual intervention and can operate 24/7.
2. Risk Diversification: The batch position building approach effectively reduces single-entry risks.
3. Clear Profit Targets: Fixed profit targets ensure immediate profit-taking when reached.
4. High Adaptability: Parameter adjustments allow adaptation to different market environments and trading instruments.
5. Strong Execution: Clear strategy logic eliminates subjective emotional influences.

#### Strategy Risks
1. Trend Risk: In continuously declining markets, repeated position adding may increase losses.
2. Capital Management Risk: Without proper position control, excessive position adding may lead to high capital utilization.
3. Slippage Risk: Severe slippage during volatile market conditions may affect strategy performance.
4. Parameter Sensitivity: Strategy effectiveness is sensitive to parameter settings, requiring timely adjustments in different market environments.

#### Strategy Optimization Directions
1. Dynamic Stop Loss: Recommend adding ATR or volatility-based dynamic stop-loss mechanisms to prevent significant drawdowns.
2. Position Management: Introduce equity-based dynamic position management for more rational capital utilization.
3. Market Selection: Add trend identification indicators to pause strategy operation in trending markets.
4. Profit Target Optimization: Design dynamic profit targets that self-adjust based on market volatility.
5. Position Adding Optimization: Design progressive position sizing to avoid excessive early positions.

#### Summary
This is a structurally simple but practical grid trading strategy that builds positions in batches at preset price drops and uniformly closes positions when reaching profit targets. The strategy's core advantages lie in its execution certainty and risk diversification, but market environment selection and parameter optimization are crucial during implementation. There is significant optimization potential through adding dynamic stop-losses and improving position management. For live trading, thorough backtesting and parameter adjustment based on actual market conditions are recommended.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2025-01-04 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Buy Down 5%, Sell at 5% Profit", overlay=true, default_qty_type=strategy.fixed, default_qty_value=1)

// Inputs
initial_date = input(timestamp("2024-01-01 00:00:00"), title="Initial Purchase Date")
profit_target = input.float(5.0, title="Profit Target (%)", minval=0.1)   // Target profit percentage
rebuy_drop = input.float(5.0, title="Rebuy Drop (%)", minval=0.1)        // Drop percentage to rebuy

// Variables
var float initial_price = na             // Initial purchase price
var int entries = 0                      // Count of entries
var float total_profit = 0               // Cumulative profit
var bool active_trade = false            // Whether an active trade exists

// Entry Condition: Buy on or after the initial date
if not active_trade
    initial_price := close
    strategy.entry("Buy", strategy.long)
    entries += 1
    active_trade := true

// Rebuy Condition: Buy if price drops 5% or more from the initial price
rebuy_price = initial_price * (1 - rebuy_drop / 100)
if active_trade and close <= rebuy_price
    strategy.entry("Rebuy", strategy.long)
    entries += 1

// Exit Condition: Sell if the price gives a 5% profit on the initial investment
target_price = initial_price * (1 + profit_target / 100)
if active_trade and close >= target_price
    strategy.close_all(comment="Profit Target Hit")
    active_trade := false
    total_profit += profit_target

// Display information on the chart
plotshape(series=close >= target_price, title="Target Hit", style=shape.labelup, location=location.absolute, color=color.green, text="Sell")
plotshape(series=close <= rebuy_price, title="Rebuy", style=shape.labeldown, location=location.absolute, color=color.red, text="Rebuy")

// Draw statistics on the chart
var label stats_label = na
if (na(stats_label))
    stats_label := label.new(x=bar_index, y=close, text="", style=label.style_none, size=size.small)

label.set_xy(stats_label, bar_index, close)
label.set_text(stats_label, "Entries: " + str.tostring(entries) + "\nTotal Profit: " + str.tostring(total_profit, "#.##") + "%")

```

> Detail

https://www.fmz.com/strategy/477600

> Last Modified

2025-01-06 16:29:17

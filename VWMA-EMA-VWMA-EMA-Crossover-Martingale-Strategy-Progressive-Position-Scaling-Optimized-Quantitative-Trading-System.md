
> Name

VWMA-EMA-Crossover-Martinale-Strategy-Progressive-Position-Scaling-Optimized-Quantitative-Trading-System
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8eab2455cae2d7f4d82.png)
![IMG](https://www.fmz.com/upload/asset/2d889949ae9afa1f4873f.png)





[trans]#### Overview
The VWMA-EMA moving average crossover Martingale strategy is a quantitative trading system based on technical analysis that combines the crossover signals of the Volume Weighted Moving Average (VWMA) and the Exponential Moving Average (EMA), and introduces the Martingale fund management method based on the Fibonacci sequence. This strategy mainly uses the long arrangement form of VWMA (shorter period) and EMA (longer period) and the breakthrough relationship between price and VWMA to determine the market trend direction. At the same time, it uses the Martingale method to gradually increase positions when the price pulls back to reduce the average cost, and finally achieves profits with a fixed percentage profit target.
#### Strategy Principle
The core principles of this strategy are divided into three main parts: signal generation, position management, and profit-taking exit.
1. Signal generation part:
   - The strategy calculates two moving averages: VWMA (default period 100) and EMA (default period 200)
   - Entry conditions consist of two key factors:
     a) VWMA is above EMA (long arrangement)
     b) Price breaks VWMA upward (momentum confirmation)
   - This combination ensures that entries are entered only when the overall trend is up, using price breakouts as triggers
2. Position management part (Martingal system):
   - Use the set capital ratio for initial entry (default 10%)
   - When the price falls to a certain level, additional buy operations will be triggered
   - Adopt Fibonacci decline percentage design: 1%, 2%, 3%, 6%, 12%, 24%
   - The position size for each additional purchase increases according to the set multiple (default 2 times)
   - The system limits the maximum number of Martingale operations (default 7 times) to control risks
   - Recalculate the average holding cost after each purchase
3. Profit exit part:
   - When the price rises to a specific percentage of the average holding cost (default 1%), all positions will be closed for profit
   - Reset all state variables after closing a position to prepare for the next round of trading
#### Strategic Advantages
Through in-depth analysis of the code implementation, this strategy has the following significant advantages:
1. Dual mechanism for trend confirmation: Through the relative position of VWMA and EMA and the combination conditions of price breakthrough VWMA, it can effectively filter out false breakthroughs and improve the quality of entry.
2. Intelligent risk management: Adopt Fibonacci sequential decline percentage design, and gradually increase the threshold for additional purchases as the correction amplitude increases, which is in line with the characteristics of market fluctuations and avoids premature additions.
3. High capital utilization efficiency: only use part of the funds initially (default 10%), and retain most of the funds for possible subsequent additional operations to avoid premature exhaustion of funds.
4. Low psychological burden: The strategy is completely automated, and traders do not need to face the psychological pressure during retracements and avoid human emotional interference.
5. Flexible parameter system: Provides multiple adjustable parameters (moving average cycle, profit target, Martingale multiple, etc.), which can be optimized according to different market environments and trading varieties.
6. Visual monitoring: The built-in status table displays key information (current positions, average cost, profit and loss status, next trigger price, etc.) in real time, making it easier for traders to monitor strategy execution.
7. Clear transaction marks: Mark all operating points (initial entry, additional buying, profit taking) on ​​the chart to facilitate backtest analysis and strategy optimization.
#### Strategy Risk
Although this strategy is well designed, it still has the following potential risks:
1. Trend reversal risk: In the case of a strong trend reversal, even with the Martingale mechanism, you may still face large losses. The solution is to add trend confirmation indicators, such as MACD, RSI, etc., or introduce a stop loss mechanism.
2. Risk of running out of funds: In extreme market conditions, if the price continues to fall beyond the preset maximum Martingale times, the strategy will be unable to continue to add positions. It is recommended to set a cap on the total use of funds and maintain an emergency fund.
3. Parameter sensitivity: Strategy performance is highly sensitive to parameter settings (especially moving average periods and Martingale multiples), and different market environments may require different parameters. It is recommended to determine the optimal parameter combination through backtesting and regularly check the parameter effectiveness.
4. Impact of slippage and commission: In real trading, slippage and commission may significantly affect the profitability of the strategy, especially when positions are frequently added. It is recommended to include reasonable transaction cost estimates in backtesting.
5. Liquidity risk: In low-liquidity markets, large orders may result in severe slippage or failure to be executed. It is recommended to implement this strategy in highly liquid markets or limit the size of single trades.
#### Strategy optimization direction
Based on the current implementation, the strategy can be optimized from the following aspects:
1. Dynamic stop loss mechanism: Introduce dynamic stop loss based on ATR (average true range) to limit the maximum loss under extreme market conditions and protect the safety of funds. This optimization can provide the final safety net for the strategy while retaining the advantages of Martingale.
2. Dynamic profit target: The current fixed profit target of 1% is relatively conservative. You can consider automatically adjusting the profit target according to market volatility, keeping it conservative in low-volatility markets, and raising the target in high-volatility markets.
3. Trend strength filtering: Add a trend strength evaluation mechanism, such as the ADX indicator, to enable strategies only when the trend is clear to avoid frequent signals in volatile markets.
4. Market environment adaptability: Add a market environment identification module to automatically adjust strategy parameters or suspend strategy operation in different market stages (trends, shocks, extreme fluctuations).
5. Fund management optimization: Improve the current fixed multiple increase model and adopt a more flexible fund allocation method, such as Kelly's formula or dynamic adjustment based on account equity.
6. Multi-cycle confirmation: Adding a multi-cycle confirmation mechanism requires a higher time frame and also presents a long arrangement, improving the reliability of entry signals.
7. Machine learning optimization: Use machine learning technology to automatically identify the best parameter combination and predict the performance of the strategy in different market environments based on historical patterns.
#### Summary
The VWMA-EMA moving average crossover Martingale strategy is a quantitative trading system that combines technical analysis signals with advanced fund management. Use the long arrangement of VWMA and EMA to cooperate with price breakthroughs to confirm the trend direction, and use the Martingale method based on the Fibonacci sequence to intelligently increase positions during callbacks, and finally make profits with a fixed profit target. This strategy focuses on risk control in design, and protects the safety of funds by limiting the maximum number of additions and setting up an exit mechanism.
Although there are potential risks such as trend reversal and fund exhaustion, the robustness and adaptability of the strategy can be significantly improved by introducing optimization measures such as dynamic stop loss and trend strength filtering. Especially in a market environment with a clear upward trend, this strategy can effectively capture callback buying opportunities and improve overall profitability through a downward shift in average costs.
For quantitative trading practitioners, this strategy provides a framework for balancing risks and returns. Under the premise of appropriate parameter optimization and risk control, it can be used as an effective component of a medium- and long-term investment portfolio. The strategy's concise and clear logic and flexible parameter settings also make it an excellent example for learning quantitative trading and fund management. || #### Overview
The VWMA-EMA Crossover Martingale Strategy is a quantitative trading system based on technical analysis, combining volume-weighted moving average (VWMA) and exponential moving average (EMA) crossover signals with a Fibonacci-based Martingale money management approach. This strategy primarily utilizes the bullish alignment of VWMA (shorter period) and EMA (longer period), along with price breakouts above VWMA to determine market trend direction. It implements a Martingale method to progressively increase positions during price retracements to lower average cost, ultimately achieving profit through a fixed percentage profit target.
#### Strategy Principles
The core principles of this strategy can be divided into three main components: signal generation, position management, and profit taking.

1. Signal Generation:
   - The strategy calculates VWMA (default period 100) and EMA (default period 200)
   - Entry conditions consist of two key factors:
     a) VWMA positioned above EMA (bullish alignment)
     b) Price breaking above VWMA (momentum confirmation)
   - This combination ensures entries only occur in an overall uptrend and uses price breakouts as trigger signals

2. Position Management (Martingale System):
   - Initial entry uses a set percentage of capital (default 10%)
   - Additional buy orders are triggered when price drops by specific percentages
   - Implements Fibonacci-style percentage drops: 1%, 2%, 3%, 6%, 12%, 24%
   - Each additional position increases in size by a set multiplier (default 2x)
   - System limits maximum Martingale operations (default 7) to control risk
   - Average position cost is recalculated after each buy

3. Profit Taking:
   - All positions are closed when price rises to a specific percentage (default 1%) above average entry cost
   - All state variables are reset after closing positions, preparing for the next trading cycle

#### Strategy Advantages
Through deep analysis of the code implementation, this strategy demonstrates the following significant advantages:

1. Dual Trend Confirmation Mechanism: The combination of VWMA-EMA relative positioning and price breakouts above VWMA effectively filters false breakouts and improves entry quality.

2. Intelligent Risk Management: The Fibonacci sequence-style percentage drops progressively raise the threshold for additional buys as retracement magnitude increases, aligning with market volatility characteristics and avoiding premature additions.

3. High Capital Efficiency: Initially uses only a portion of funds (default 10%), reserving the majority for potential additional positions and preventing premature capital depletion.

4. Low Psychological Burden: The strategy operates fully automatically, eliminating psychological pressure during drawdowns and avoiding emotional interference.

5. Flexible Parameter System: Provides multiple adjustable parameters (moving average periods, profit targets, Martingale multipliers, etc.) that can be optimized for different market environments and trading instruments.

6. Visual Monitoring: Incorporates a built-in status table displaying real-time key information (current positions, average cost, profit/loss status, next trigger price, etc.), facilitating strategy execution monitoring.

7. Clear Trade Markers: Annotates all operation points on the chart (initial entries, additional buys, profit-taking), aiding backtest analysis and strategy optimization.

#### Strategy Risks
Despite its sophisticated design, the strategy still presents the following potential risks:

1. Trend Reversal Risk: In strong trend reversal scenarios, even with the Martingale mechanism, significant losses may occur. Solutions include adding trend confirmation indicators like MACD or RSI, or implementing stop-loss mechanisms.

2. Capital Depletion Risk: In extreme market conditions, if prices continue to fall beyond the preset maximum Martingale iterations, the strategy cannot add more positions. It's advisable to set a total capital usage limit and maintain emergency funds.

3. Parameter Sensitivity: Strategy performance is highly sensitive to parameter settings (especially moving average periods and Martingale multipliers), with different market environments potentially requiring different parameters. Backtesting is recommended to determine optimal parameter combinations with periodic validation.

4. Slippage and Commission Impact: In live trading, slippage and commissions can significantly affect profitability, especially with frequent position additions. Including reasonable transaction cost estimates in backtests is advised.

5. Liquidity Risk: In low-liquidity markets, large orders may cause severe slippage or fail to execute. This strategy is best implemented in highly liquid markets, or with limited transaction sizes.

#### Strategy Optimization Directions
Based on the current implementation, the strategy can be optimized in the following ways:

1. Dynamic Stop-Loss Mechanism: Introduce ATR (Average True Range) based dynamic stop-losses to limit maximum losses in extreme market conditions, protecting capital. This optimization provides a safety net while preserving Martingale advantages.

2. Dynamic Profit Targets: The current fixed 1% profit target is relatively conservative. Consider automatically adjusting profit targets based on market volatility – maintaining conservatism in low-volatility markets and increasing targets in high-volatility markets.

3. Trend Strength Filtering: Add trend strength assessment mechanisms, such as the ADX indicator, to activate the strategy only during clear trends, avoiding frequent signals in ranging markets.

4. Market Environment Adaptability: Incorporate market environment recognition modules to automatically adjust strategy parameters or pause operations in different market phases (trending, ranging, extreme volatility).

5. Money Management Optimization: Improve the current fixed multiplier position sizing model by adopting more flexible capital allocation methods, such as the Kelly formula or dynamic adjustments based on account equity.

6. Multi-timeframe Confirmation: Add multi-timeframe confirmation mechanisms, requiring bullish alignment in higher timeframes as well, improving entry signal reliability.

7. Machine Learning Optimization: Utilize machine learning techniques to automatically identify optimal parameter combinations and predict strategy performance across different market environments based on historical patterns.

#### Summary
The VWMA-EMA Crossover Martingale Strategy is a quantitative trading system combining technical analysis signals with advanced money management. It confirms trend direction through VWMA-EMA bullish alignment and price breakouts, intelligently increases positions during retracements using a Fibonacci-based Martingale method, and takes profits at fixed targets. The strategy design emphasizes risk control by limiting maximum additional entries and implementing exit mechanisms to protect capital.

Despite potential risks such as trend reversals and capital depletion, the strategy's robustness and adaptability can be significantly enhanced by introducing dynamic stop-losses, trend strength filtering, and other optimization measures. Particularly in well-defined uptrends, this strategy effectively captures buying opportunities during retracements and improves overall profitability by lowering average costs.

For quantitative trading practitioners, this strategy provides a framework balancing risk and reward. With appropriate parameter optimization and risk controls, it can serve as an effective component of medium to long-term investment portfolios. The strategy's clear logic and flexible parameter settings also make it an excellent example for learning quantitative trading and money management principles.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-04 00:00:00
end: 2025-03-03 08:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

// VWMA-EMA Martingale Long Strategy
// @version=5
strategy("VWMA-EMA Martingale Long Strategy", overlay=true, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// Parameter settings
vwmaLength = input.int(100, "VWMA Period", minval=1)
emaLength = input.int(200, "EMA Period", minval=1)
profitPercent = input.float(1.0, "Take Profit (%)", minval=0.1, step=0.1)
maxMartingaleEntries = input.int(7, "Max Martingale Entries", minval=1, maxval=10)
martingaleMultiplier = input.float(2.0, "Martingale Multiplier", minval=1.1, step=0.1)
initialPositionSize = input.float(10.0, "Initial Position Size (%)", minval=1.0, maxval=100.0, step=1.0)

// Indicator calculations
vwma100 = ta.vwma(close, vwmaLength)
ema200 = ta.ema(close, emaLength)

// Plot indicators
plot(vwma100, "VWMA 100", color=color.blue, linewidth=2)
plot(ema200, "EMA 200", color=color.red, linewidth=2)

// Entry conditions - modified!
vwmaAboveEma = vwma100 > ema200  // VWMA and EMA in bullish alignment
vwmaCrossover = ta.crossover(close, vwma100)  // Close crosses above VWMA

// Variables for managing Martingale state
var int martingaleCount = 0
var float entryPrice = 0.0
var float averageEntryPrice = 0.0
var float totalQuantity = 0.0
var float totalCost = 0.0
var bool inPosition = false
var float positionSize = initialPositionSize

// Long entry condition - modified!
longCondition = vwmaAboveEma and vwmaCrossover and martingaleCount < maxMartingaleEntries

// Take profit condition
takeProfitCondition = inPosition and close >= averageEntryPrice * (1 + profitPercent / 100)

// Additional entry conditions (Martingale)
// Fibonacci-based drop percentage (1%, 2%, 3%, 6%, 12%, 24%)
getFibDropPercent(count) =>
    if count == 1
        1.0  // 1% drop
    else if count == 2
        2.0  // 2% drop
    else if count == 3
        3.0  // 3% drop
    else if count == 4
        6.0  // 6% drop
    else if count == 5
        12.0  // 12% drop
    else if count == 6
        24.0  // 24% drop
    else
        100.0  // High value (failsafe)

// Calculate drop threshold for the current Martingale step
currentDropPercent = getFibDropPercent(martingaleCount)
dropThreshold = entryPrice * (1 - currentDropPercent / 100)

// Define additional buy conditions
martingaleAddCondition = inPosition and close < dropThreshold and martingaleCount < maxMartingaleEntries

// Order execution
if (longCondition and not inPosition)
    // Initial entry
    entryPrice := close
    averageEntryPrice := close
    totalQuantity := strategy.equity * positionSize / 100 / close
    totalCost := totalQuantity * close
    martingaleCount := 1
    inPosition := true
    strategy.entry("Long #" + str.tostring(martingaleCount), strategy.long, qty=totalQuantity)
    positionSize := initialPositionSize

if (martingaleAddCondition)
    // Martingale additional buy
    martingaleCount := martingaleCount + 1
    positionSize := positionSize * martingaleMultiplier
    
    // Calculate additional quantity
    additionalQuantity = strategy.equity * positionSize / 100 / close
    
    // Recalculate average entry price
    totalQuantity := totalQuantity + additionalQuantity
    totalCost := totalCost + (additionalQuantity * close)
    averageEntryPrice := totalCost / totalQuantity
    entryPrice := close
    
    // Place additional buy order
    strategy.entry("Long #" + str.tostring(martingaleCount), strategy.long, qty=additionalQuantity)

if (takeProfitCondition)
    // Take profit
    strategy.close_all("Take Profit +1%")
    martingaleCount := 0
    inPosition := false
    positionSize := initialPositionSize

// Display current status in a table
var table statusTable = table.new(position.top_right, 2, 9, bgcolor = color.new(color.black, 70))

// Table update function
updateTable() =>
    table.cell(statusTable, 0, 0, "Status", text_color = color.white, bgcolor = color.new(color.blue, 90))
    table.cell(statusTable, 1, 0, inPosition ? "In Position" : "No Position", text_color = inPosition ? color.green : color.white)
    
    table.cell(statusTable, 0, 1, "Martingale Count", text_color = color.white)
    table.cell(statusTable, 1, 1, str.tostring(martingaleCount) + "/" + str.tostring(maxMartingaleEntries), text_color = color.white)
    
    table.cell(statusTable, 0, 2, "Avg Entry Price", text_color = color.white)
    table.cell(statusTable, 1, 2, inPosition ? str.tostring(averageEntryPrice, "#.##") : "-", text_color = color.white)
    
    table.cell(statusTable, 0, 3, "Current Profit", text_color = color.white)
    if inPosition
        currentProfit = (close - averageEntryPrice) / averageEntryPrice * 100
        profitColor = currentProfit >= 0 ? color.green : color.red
        table.cell(statusTable, 1, 3, str.tostring(currentProfit, "#.##") + "%", text_color = profitColor)
    else
        table.cell(statusTable, 1, 3, "-", text_color = color.white)
    
    table.cell(statusTable, 0, 4, "Take Profit Target", text_color = color.white)
    table.cell(statusTable, 1, 4, inPosition ? str.tostring(averageEntryPrice * (1 + profitPercent / 100), "#.##") : "-", text_color = color.white)
    
    table.cell(statusTable, 0, 5, "Total Quantity", text_color = color.white)
    table.cell(statusTable, 1, 5, inPosition ? str.tostring(totalQuantity, "#.##") : "-", text_color = color.white)
    
    table.cell(statusTable, 0, 6, "Next Buy Size", text_color = color.white)
    table.cell(statusTable, 1, 6, inPosition ? str.tostring(positionSize, "#.##") + "%" : "-", text_color = color.white)
    
    // Display next buy trigger price
    table.cell(statusTable, 0, 7, "Next Buy Trigger", text_color = color.white)
    if inPosition and martingaleCount < maxMartingaleEntries
        nextDropPercent = getFibDropPercent(martingaleCount)
        nextTriggerPrice = entryPrice * (1 - nextDropPercent / 100)
        table.cell(statusTable, 1, 7, str.tostring(nextTriggerPrice, "#.##") + " (" + str.tostring(nextDropPercent) + "%↓)", text_color = color.orange)
    else
        table.cell(statusTable, 1, 7, "-", text_color = color.white)
        
    // Display bullish alignment status
    table.cell(statusTable, 0, 8, "Bullish Alignment", text_color = color.white)
    table.cell(statusTable, 1, 8, vwmaAboveEma ? "Bullish ✓" : "Bearish ✗", text_color = vwmaAboveEma ? color.green : color.red)

// Update the table on every bar
updateTable()

// Entry/Take profit markers
plotshape(series=longCondition and not inPosition[1], title="Long Entry", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(series=takeProfitCondition, title="Take Profit", location=location.abovebar, color=color.blue, style=shape.triangledown, size=size.small)
plotshape(series=martingaleAddCondition, title="Martingale Add", location=location.belowbar, color=color.yellow, style=shape.circle, size=size.tiny)

```

> Detail

https://www.fmz.com/strategy/484920

> Last Modified

2025-03-05 10:16:07

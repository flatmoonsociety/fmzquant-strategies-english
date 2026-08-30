
> Name

Four-Period-SMA-Breakthrough-Trading-Strategy-with-Dynamic-Profit-Loss-Management-System
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/199a69c7a17b732cecb.png)

[trans]
#### Overview
This is a trading strategy system based on a four-period simple moving average that integrates a dynamic stop-profit and stop-loss management mechanism. This strategy captures turning points in the market trend by monitoring the intersection of price and short-term moving averages, and uses a percentage approach to set take-profit and stop-loss for risk management. The core of the strategy is to use the characteristics of short-period moving averages to quickly respond to the market, combined with strict fund management rules, to achieve robust trading results.
#### Strategy Principle
The strategy operation is based on the following core logic: first, calculate the 4-period simple moving average (SMA) as the main indicator. When the price crosses the SMA upward, the system identifies it as a bullish signal and opens a long position; when the price crosses the SMA downward, the system identifies it as a bearish signal and opens a short position. Each transaction is set with a dynamic take-profit and stop-loss point based on the opening price. The default take-profit is 2% and the default stop-loss is 1%. This setup ensures a profit-loss ratio of 2:1, in line with professional money management principles.
#### Strategic Advantages
1. Fast response: Using a 4-period short-term moving average, it can quickly capture market fluctuations and is suitable for short-term trading.
2. Strict risk control: A dynamic stop-profit and stop-loss mechanism is integrated, and each transaction has a clear exit point.
3. The strategy logic is simple: using the classic moving average crossover method, it is easy to understand and execute.
4. The parameters are highly adjustable: the take-profit and stop-loss percentages can be flexibly adjusted according to different market characteristics.
5. Two-way trading: Supports long and short two-way operations, allowing you to fully seize market opportunities.
#### Strategy Risk
1. Risk of volatile markets: In sideways volatile markets, false signals are easily generated, leading to frequent trading.
2. Slippage risk: Due to the use of short-period moving averages and higher trading frequency, you may face greater slippage losses.
3. Systemic risk: When the market fluctuates violently, stop loss may not be executed in time.
4. Parameter sensitivity: The strategy effect is relatively sensitive to parameter settings and requires continuous optimization.
#### Strategy optimization direction
1. Add trend filter: You can add long-period moving averages as trend filter conditions to reduce false signals that shock the market.
2. Optimize take-profit and stop-loss: The take-profit and stop-loss ratio can be dynamically adjusted according to market volatility.
3. Add trading volume indicator: Use trading volume as an auxiliary indicator to improve the reliability of entry signals.
4. Set time filtering: Add trading time period filtering to avoid operating during periods that are not suitable for trading.
#### Summary
This is a quantitative trading strategy with complete structure and clear logic. It captures market momentum through short-term moving averages, supplemented by strict risk control mechanisms, and is suitable for traders who pursue steady returns. Although there is some room for optimization, the basic framework of the strategy has good scalability. Through continuous optimization and adjustment, it is expected to achieve better trading results. ||
#### Overview
This is a trading strategy system based on a four-period simple moving average, integrated with dynamic stop-loss and take-profit management mechanisms. The strategy captures market trend turning points by monitoring price crossovers with short-term moving averages and implements percentage-based stop-loss and take-profit levels for risk management. The core strength lies in utilizing the quick response characteristics of short-period moving averages, combined with strict money management rules to achieve stable trading results.

#### Strategy Principles
The strategy operates on the following core logic: First, it calculates a 4-period Simple Moving Average (SMA) as the primary indicator. When price crosses above the SMA, the system recognizes it as a bullish signal and enters a long position; when price crosses below the SMA, it identifies a bearish signal and enters a short position. Each trade is set with dynamic take-profit and stop-loss points based on the entry price, with default values of 2% for take-profit and 1% for stop-loss. This setup ensures a 2:1 reward-to-risk ratio, adhering to professional money management principles.

#### Strategy Advantages
1. Quick Response: Using a 4-period short-term moving average enables rapid capture of market movements, suitable for short-term trading.
2. Strict Risk Control: Integrated dynamic stop-loss and take-profit mechanisms provide clear exit points for each trade.
3. Simple Logic: Uses classic moving average crossover method, easy to understand and execute.
4. Adjustable Parameters: Profit and loss percentages can be flexibly adjusted for different market characteristics.
5. Bilateral Trading: Supports both long and short operations, maximizing market opportunities.

#### Strategy Risks
1. Consolidation Market Risk: Prone to false signals in sideways markets, leading to frequent trading.
2. Slippage Risk: Due to short-period moving average usage, high trading frequency may result in significant slippage losses.
3. Systemic Risk: Stop-losses may not execute timely during extreme market volatility.
4. Parameter Sensitivity: Strategy performance is highly sensitive to parameter settings, requiring continuous optimization.

#### Strategy Optimization Directions
1. Add Trend Filter: Incorporate longer-period moving averages as trend filters to reduce false signals in consolidating markets.
2. Optimize Stop Levels: Dynamically adjust profit and loss ratios based on market volatility.
3. Include Volume Indicators: Integrate volume as a supplementary indicator to improve entry signal reliability.
4. Implement Time Filters: Add trading session filters to avoid operations during unsuitable trading periods.

#### Summary
This is a well-structured quantitative trading strategy with clear logic. It captures market momentum through short-term moving averages, supplemented by strict risk control mechanisms, suitable for traders seeking stable returns. While there is room for optimization, the strategy's basic framework offers good scalability, and through continuous improvement and adjustment, it has the potential to achieve better trading results.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-28 00:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("4SMA Strategy with Targets and Stop Loss", overlay=true)

// Input parameters for SMA
smaLength = input.int(4, title="SMA Length", minval=1)

// Input parameters for stop loss and take profit
takeProfitPercent = input.float(2.0, title="Take Profit (%)", step=0.1)  // Default: 2%
stopLossPercent = input.float(1.0, title="Stop Loss (%)", step=0.1)  // Default: 1%

// Calculate 4-period SMA
sma = ta.sma(close, smaLength)

// Plot SMA
plot(sma, color=color.blue, title="4SMA Line")

// Entry Conditions
longCondition = ta.crossover(close, sma)  // Price crosses above SMA (bullish signal)
shortCondition = ta.crossunder(close, sma)  // Price crosses below SMA (bearish signal)

// Strategy Logic
if (longCondition)
    strategy.entry("Long", strategy.long)  // Enter long position

if (shortCondition)
    strategy.entry("Short", strategy.short)  // Enter short position

// Calculate Take Profit and Stop Loss
longTakeProfit = strategy.position_avg_price * (1 + takeProfitPercent / 100)  // TP for long
longStopLoss = strategy.position_avg_price * (1 - stopLossPercent / 100)      // SL for long

shortTakeProfit = strategy.position_avg_price * (1 - takeProfitPercent / 100) // TP for short
shortStopLoss = strategy.position_avg_price * (1 + stopLossPercent / 100)     // SL for short

// Exit for Long
if (strategy.position_size > 0)  // If in a long position
    strategy.exit("Long TP/SL", from_entry="Long", limit=longTakeProfit, stop=longStopLoss)

// Exit for Short
if (strategy.position_size < 0)  // If in a short position
    strategy.exit("Short TP/SL", from_entry="Short", limit=shortTakeProfit, stop=shortStopLoss)

```

> Detail

https://www.fmz.com/strategy/473401

> Last Modified

2024-11-29 16:44:42

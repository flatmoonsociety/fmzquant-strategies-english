
> Name

Adaptive Moving Average Crossover Dynamic Position Risk Management Strategy-Adaptive-EMA-Crossover-Dynamic-Position-Risk-Management-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d82a291a1fcd8087e74b.png)
![IMG](https://www.fmz.com/upload/asset/2d88f3a8dcadf18f0ec9f.png)



[trans]
#### Overview
This strategy is a trading system based on medium- and long-term exponential moving average (EMA) crossovers, which combines dynamic position management and risk control mechanisms. The strategy identifies market trends through the 21-period and 55-period EMA crossovers, and dynamically adjusts the trading position size based on the user-defined risk-return ratio and risk percentage, achieving precise risk control.
#### Strategy Principle
The core logic of the strategy is based on the EMA crossover signal of two time periods. When the 21-period EMA crosses the 55-period EMA upwards, the system identifies an upward trend and triggers a long signal; when the 21-period EMA crosses the 55-period EMA downwards, the system identifies a downward trend and triggers a short signal. The stop loss position is set based on the lowest point (long) or the highest point (short) of the past two K lines, and the stop profit position is dynamically calculated based on the risk-return ratio set by the user. The position size is dynamically calculated based on the total account funds, risk percentage and current stop loss distance to ensure that the risk of each transaction is controlled within the preset range.
#### Strategic Advantages
1. Dynamic risk management: By dynamically calculating the position size, ensure that the risk of each transaction is strictly controlled within the set percentage range.
2. Strong adaptability: EMA indicator can adapt to market fluctuations and reduce false signals.
3. Adjustable risk-return ratio: Users can set the risk-return ratio according to their own risk preferences.
4. Scientific position management: dynamically adjust positions based on account size and risk distance to avoid excessive leverage.
5. Fully automated operation: The strategy can run continuously 24/7 without manual intervention.
#### Strategy Risk
1. Risk of volatile market: In a volatile market, EMA crossover signals may produce frequent false signals.
2. Slippage risk: In rapid market conditions, the actual transaction price may deviate greatly from the signal price.
3. Fund management risk: Although risk controls are set up, continuous losses may still have a significant impact on the account.
4. Systemic risk: Sudden major events in the market may cause stop loss to be invalid.
#### Strategy optimization direction
1. Add trend filter: Introduce ADX or trend strength indicator to filter sideways and oscillating market conditions.
2. Optimize the stop loss method: Consider using ATR to dynamically adjust the stop loss distance and improve the adaptability of the stop loss.
3. Add volatility adjustment: dynamically adjust risk parameters based on market volatility.
4. Time filtering: Add trading time filtering to avoid low liquidity periods.
5. Introduce volume energy indicators: combine with trading volume indicators to verify the validity of the trend.
#### Summary
This strategy builds a complete trading system by combining EMA trend signals and dynamic risk management. The core advantage of the strategy lies in its scientific position management and risk control mechanism, but it still requires appropriate parameter optimization based on the market environment and personal risk preferences. Through the suggested optimization directions, the stability and profitability of the strategy are expected to be further improved. ||
#### Overview
This strategy is a trading system based on medium and long-term Exponential Moving Average (EMA) crossovers, incorporating dynamic position management and risk control mechanisms. The strategy identifies market trends through the crossover of 21-period and 55-period EMAs while dynamically adjusting position sizes based on user-defined risk-reward ratios and risk percentages, achieving precise risk control.

#### Strategy Principles
The core logic is built on EMA crossover signals from two time periods. When the 21-period EMA crosses above the 55-period EMA, the system identifies an uptrend and triggers a long signal; when the 21-period EMA crosses below the 55-period EMA, it identifies a downtrend and triggers a short signal. Stop-loss levels are set at the lowest point (for longs) or highest point (for shorts) of the past two candles, while take-profit levels are dynamically calculated based on the user-defined risk-reward ratio. Position sizing is dynamically calculated based on total account equity, risk percentage, and current stop-loss distance, ensuring risk control within preset parameters.

#### Strategy Advantages
1. Dynamic Risk Management: Position sizes are dynamically calculated to ensure strict risk control within set percentage parameters.
2. High Adaptability: EMA indicators adapt to market volatility, reducing false signals.
3. Adjustable Risk-Reward Ratio: Users can set risk-reward ratios according to their risk preferences.
4. Scientific Position Management: Positions are dynamically adjusted based on account size and risk distance, avoiding excessive leverage.
5. Fully Automated Operation: Strategy can run 24/7 without manual intervention.

#### Strategy Risks
1. Choppy Market Risk: EMA crossover signals may generate frequent false signals in ranging markets.
2. Slippage Risk: Actual execution prices may significantly differ from signal prices in fast-moving markets.
3. Money Management Risk: Despite risk controls, consecutive losses may still significantly impact the account.
4. Systemic Risk: Sudden market events may render stop-losses ineffective.

#### Strategy Optimization Directions
1. Add Trend Filters: Incorporate ADX or trend strength indicators to filter ranging market conditions.
2. Optimize Stop-Loss Method: Consider using ATR for dynamic stop-loss adjustment to improve adaptability.
3. Incorporate Volatility Adjustment: Dynamically adjust risk parameters based on market volatility.
4. Time Filtering: Add trading time filters to avoid low liquidity periods.
5. Include Volume Indicators: Integrate volume indicators to validate trend validity.

#### Summary
This strategy constructs a complete trading system by combining EMA trend signals with dynamic risk management. Its core advantages lie in scientific position management and risk control mechanisms, but it still requires appropriate parameter optimization based on market conditions and individual risk preferences. Through the suggested optimization directions, the strategy's stability and profitability can be further enhanced.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-21 00:00:00
end: 2024-07-11 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Carlos Humberto Rodríguez Arias

//@version=5
strategy("EMA Crossover Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// EMA periods
MT_EMA = input.int(21, title="Medium Term EMA")
LT_EMA = input.int(55, title="Long Term EMA")
RR = input.float(2.0, title="Risk-Reward Ratio") // User-defined RR
RiskPercent = input.float(1.0, title="Risk Percentage") // User-defined risk percentage

// Calculate EMAs
Signal_MT_EMA = ta.ema(close, MT_EMA)
Signal_LT_EMA = ta.ema(close, LT_EMA)

// Plot EMAs
plot(Signal_MT_EMA, title="Medium Term EMA", color=color.orange, linewidth=2)
plot(Signal_LT_EMA, title="Long Term EMA", color=color.blue, linewidth=2)

// Determine trend conditions
uptrend = ta.crossover(Signal_MT_EMA, Signal_LT_EMA)
downtrend = ta.crossunder(Signal_MT_EMA, Signal_LT_EMA)

// Stop-Loss Calculations
longStopLoss = ta.lowest(low, 2) // SL for buy = lowest low of last 2 candles
shortStopLoss = ta.highest(high, 2) // SL for sell = highest high of last 2 candles

// Take-Profit Calculations
longTakeProfit = close + (close - longStopLoss) * RR
shortTakeProfit = close - (shortStopLoss - close) * RR

// Calculate Position Size based on Risk Percentage
capital = strategy.equity * (RiskPercent / 100)
longPositionSize = capital / (close - longStopLoss)
shortPositionSize = capital / (shortStopLoss - close)

// Execute Buy Order
if uptrend
    strategy.entry("Long", strategy.long, qty=longPositionSize)
    strategy.exit("Long Exit", from_entry="Long", stop=longStopLoss, limit=longTakeProfit)

// Execute Sell Order
if downtrend
    strategy.entry("Short", strategy.short, qty=shortPositionSize)
    strategy.exit("Short Exit", from_entry="Short", stop=shortStopLoss, limit=shortTakeProfit)

```

> Detail

https://www.fmz.com/strategy/482849

> Last Modified

2025-02-27 17:36:00

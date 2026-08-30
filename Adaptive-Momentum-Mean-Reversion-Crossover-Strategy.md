
> Name

Adaptive-Momentum-Mean-Reversion-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/78c29bf7eac55628031fed8aff2538dfe4b2258e390c17a9d654de318107cea3.png)

[trans]
#### Overview
This strategy is a hybrid trading system that combines momentum and mean reversion theory. It uses the rate of change (ROC) indicator and Bollinger Bands to identify overbought and oversold conditions in the market, triggering trading signals when specific thresholds are crossed. The core of the strategy is to gain profits by detecting momentum transition points and exploiting the property of price reversion to the mean.
#### Strategy Principle
The strategy uses the 2-period ROC indicator to calculate short-term price changes, and uses two sets of Bollinger Bands with different parameters: short-term Bollinger Bands (18 periods, 1.7 standard deviation) to determine oversold conditions and entry signals, and long-term Bollinger Bands (21 periods, 2.1 standard deviation) to determine overbought conditions and exit signals. When ROC crosses the lower Bollinger Bands upwards, it indicates that the price momentum has turned from weak to strong, and the system opens a long position; when ROC crosses the upper Bollinger Bands downwards, it indicates that the momentum weakens, and the system closes the position and exits. The strategy also marks overbought and oversold areas by background color, with green indicating oversold (likely to go up) and red indicating overbought (likely to go down).
#### Strategic Advantages
1. Strong adaptability: Bollinger Bands will automatically adjust the bandwidth according to market volatility and remain effective in different market environments.
2. Improved risk control: disable pyramiding (pyramiding=0) and ensure that you only hold one position at a time
3. High signal reliability: Combining momentum and mean reversion strategies can better grasp market turning points
4. Highly practical: taking into account transaction costs and slippage, it is more in line with the actual trading environment
#### Strategy Risk
1. Volatile market risk: Frequent transactions may result in losses during range-bound market fluctuations.
2. False breakthrough risk: ROC indicator may generate false breakthrough signals
3. Parameter sensitivity: The parameter settings of Bollinger Bands and ROC have a greater impact on strategy performance.
4. Dependence on market environment: The strategy performs better in markets with obvious trends, but may fail during violent fluctuations.
#### Strategy optimization direction
1. Introducing trend filters: Long-term moving averages can be added to filter the main market trends and improve the accuracy of trading directions.
2. Optimize parameter settings: You can find the optimal ROC cycle and Bollinger Band parameter combination through historical data backtesting
3. Add a stop loss mechanism: set a fixed stop loss or trailing stop loss to control risks
4. Increase trading volume confirmation: Combine with trading volume indicators to verify the effectiveness of price breakthroughs
#### Summary
The adaptive momentum mean reversion crossover strategy combines the ROC indicator and double Bollinger Bands to build a trading system that can adapt to different market environments. The strategy maintains flexibility while also focusing on risk control, which has good practical value. Through continuous optimization and improvement, the strategy is expected to achieve better performance in actual trading. ||
#### Overview
This strategy is a hybrid trading system that combines momentum and mean reversion theories. It identifies market overbought and oversold conditions using the Rate of Change (ROC) indicator and Bollinger Bands, triggering trades when specific thresholds are crossed. The core concept is to detect momentum shifts and capitalize on price reversions to their mean.

#### Strategy Principles
The strategy employs a 2-period ROC indicator to calculate short-term price changes, along with two sets of Bollinger Bands: short-term (18-period, 1.7 standard deviations) for oversold conditions and entry signals, and long-term (21-period, 2.1 standard deviations) for overbought conditions and exit signals. Long positions are initiated when ROC crosses above the lower Bollinger Band, indicating a shift from weak to strong momentum, and positions are closed when ROC crosses below the upper Bollinger Band, signaling weakening momentum. The strategy also uses background colors to highlight overbought (red) and oversold (green) zones.

#### Strategy Advantages
1. High Adaptability: Bollinger Bands automatically adjust their width based on market volatility, maintaining effectiveness across different market conditions
2. Robust Risk Control: Pyramiding is disabled (pyramiding=0), ensuring only one position at a time
3. Reliable Signals: Combination of momentum and mean reversion strategies provides better market turning point identification
4. Practicality: Includes transaction costs and slippage considerations for real-world trading conditions

#### Strategy Risks
1. Choppy Market Risk: May generate frequent trades leading to losses in range-bound markets
2. False Breakout Risk: ROC indicator may produce false breakthrough signals
3. Parameter Sensitivity: Strategy performance heavily depends on Bollinger Bands and ROC parameter settings
4. Market Environment Dependency: Strategy performs better in trending markets but may fail during extreme volatility

#### Strategy Optimization Directions
1. Introduce Trend Filter: Add long-term moving averages to filter market trends and improve directional accuracy
2. Optimize Parameters: Conduct historical data backtesting to find optimal ROC period and Bollinger Bands parameter combinations
3. Add Stop-Loss Mechanisms: Implement fixed or trailing stop-losses for risk control
4. Include Volume Confirmation: Incorporate volume indicators to validate price breakouts

#### Summary
The Adaptive Momentum Mean-Reversion Crossover Strategy builds a trading system capable of adapting to different market environments by combining ROC indicators and dual Bollinger Bands. While maintaining flexibility, the strategy emphasizes risk control and demonstrates practical value. Through continuous optimization and improvement, this strategy shows promise for better performance in actual trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2025-01-08 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("Adaptive Momentum Reversion Strategy ", overlay=false, initial_capital=50000, pyramiding=0, commission_type=strategy.commission.cash_per_contract, commission_value=0.05, slippage=1)

// Input: ROC Period
rocPeriod = input.int(2, title="ROC Period", minval=1)

// Input: Bollinger Bands Settings (Lower Band)
bbLowerLength = input.int(18, title="Lower Bollinger Band Length", minval=1)
bbLowerStdDev = input.float(1.7, title="Lower Bollinger Band StdDev", minval=0.1, step=0.1)

// Input: Bollinger Bands Settings (Upper Band)
bbUpperLength = input.int(21, title="Upper Bollinger Band Length", minval=1)
bbUpperStdDev = input.float(2.1, title="Upper Bollinger Band StdDev", minval=0.1, step=0.1)

// ROC Calculation
rocValue = (close - close[rocPeriod]) / close[rocPeriod] * 100

// Bollinger Bands Calculation
bbLowerBasis = ta.sma(rocValue, bbLowerLength)  // Basis for Lower Band
bbLower = bbLowerBasis - bbLowerStdDev * ta.stdev(rocValue, bbLowerLength)  // Lower Band

bbUpperBasis = ta.sma(rocValue, bbUpperLength)  // Basis for Upper Band
bbUpper = bbUpperBasis + bbUpperStdDev * ta.stdev(rocValue, bbUpperLength)  // Upper Band

// Plot ROC
plot(rocValue, color=color.blue, linewidth=2, title="ROC Value")

// Plot Bollinger Bands
plot(bbLowerBasis, color=color.gray, linewidth=1, title="Lower BB Basis (SMA)")
plot(bbLower, color=color.green, linewidth=1, title="Lower Bollinger Band")
plot(bbUpperBasis, color=color.gray, linewidth=1, title="Upper BB Basis (SMA)")
plot(bbUpper, color=color.red, linewidth=1, title="Upper Bollinger Band")

// Add Zero Line for Reference
hline(0, "Zero Line", color=color.gray, linestyle=hline.style_dotted)

// Entry Condition: Long when ROC crosses above the lower Bollinger Band
longCondition = ta.crossover(rocValue, bbLower)
if (longCondition)
    strategy.entry("Long", strategy.long)

// Exit Condition: Exit on Upper Bollinger Band Cross or ROC drops below Lower Band again
exitCondition = ta.crossunder(rocValue, bbUpper)
if (exitCondition)
    strategy.close("Long")

// Background Color for Extreme Conditions
bgcolor(rocValue > bbUpper ? color.new(color.red, 80) : na, title="Overbought (ROC above Upper BB)")
bgcolor(rocValue < bbLower ? color.new(color.green, 80) : na, title="Oversold (ROC below Lower BB)")
```

> Detail

https://www.fmz.com/strategy/477952

> Last Modified

2025-01-10 15:26:18

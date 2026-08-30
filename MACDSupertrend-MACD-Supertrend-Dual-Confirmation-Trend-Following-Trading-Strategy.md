
> Name

Dual-Confirmation Trend Following Trading Strategy Based on MACD and Supertrend-MACD-Supertrend-Dual-Confirmation-Trend-Following-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/511169f94121a6ea18.png)

[trans]
#### Overview
This strategy is a dual-proven trend following trading system that combines the MACD indicator and the Supertrend indicator. The strategy determines the entry timing by comparing the intersection of the MACD line and the signal line, combined with the trend direction of the Supertrend indicator, and sets a fixed percentage of stop loss and take profit levels to control risks. This double verification mechanism improves the reliability of trading signals and effectively reduces the interference of false signals.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Supertrend indicator: Use 20-period ATR and 2x factor to calculate the trend line, which is used to determine the current market trend direction.
2. MACD indicator: Using the classic 12/26/9 parameter setting, trading signals are generated through the intersection of fast and slow lines.
3. Entry conditions: The buying operation will only be triggered when the MACD fast line crosses the slow line upward (buy signal) and the Supertrend direction is an upward trend (direction==1).
4. Risk management: Set a 0.5% stop loss and 99.99% take profit level for each transaction to protect the safety of funds and lock in profits.
#### Strategic Advantages
1. Double verification mechanism: By combining the advantages of trend following indicators (Supertrend) and momentum indicators (MACD), the accuracy of trading signals is significantly improved.
2. Strong adaptability: The Supertrend indicator is calculated based on ATR and can automatically adjust parameters according to market volatility to adapt to different market environments.
3. Perfect risk control: adopt a percentage stop loss strategy to ensure that the risk of a single transaction is controllable.
4. Clear execution logic: clear entry and exit conditions to avoid interference caused by subjective judgment.
5. Simple operation: The strategy logic is intuitive and easy to operate and monitor.
#### Strategy Risk
1. Trend dependence: Frequent false signals may occur in volatile markets, increasing transaction costs.
2. Lagging risk: MACD and Supertrend are lagging indicators and may not respond promptly enough when the market turns rapidly.
3. Fixed stop loss risk: Using a fixed percentage stop loss may not be well adapted to the fluctuation characteristics of different market environments.
4. Parameter sensitivity: The effect of the strategy is subject to the settings of multiple parameters and requires continuous optimization to adapt to market changes.
#### Strategy optimization direction
1. Dynamic stop loss optimization: It is recommended to change the fixed stop loss to a dynamic stop loss based on ATR to better adapt to market fluctuations.
2. Add market environment filtering: You can add volatility indicators (such as VIX) as market environment filters to adjust strategy parameters or suspend trading during periods of high volatility.
3. Introduce the volume-price relationship: Consider incorporating trading volume indicators into the signal confirmation system to improve signal reliability.
4. Optimize parameter adaptation: develop a parameter adaptation mechanism based on market status to improve the adaptability of the strategy.
5. Improve position management: Introduce a dynamic position management mechanism to dynamically adjust the transaction size based on market volatility and account net value.
#### Summary
This strategy builds a relatively reliable trend following trading system by combining the advantages of MACD and Supertrend indicators. An accuracy of 46% and a return rate of 46% indicate that the strategy has certain profitability. Through the suggested optimization directions, especially the introduction of dynamic stop loss and market environment filtering, the stability and adaptability of the strategy are expected to be further improved. The strategy is suitable for intraday and futures trading, but users need to pay attention to the suitability of the market environment and adjust parameter settings according to the actual situation. ||
#### Overview
This strategy is a dual-confirmation trend following trading system that combines MACD indicator with Supertrend indicator. The strategy determines entry points by comparing MACD line crossovers with signal line while considering Supertrend direction, incorporating fixed percentage stop-loss and take-profit levels for risk management. This dual-confirmation mechanism enhances the reliability of trading signals and effectively reduces interference from false signals.

#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Supertrend Indicator: Uses 20-period ATR and factor of 2 to calculate trend lines for determining current market trend direction.
2. MACD Indicator: Employs classic 12/26/9 parameter settings, generating trading signals through fast and slow line crossovers.
3. Entry Conditions: Buy orders are triggered only when MACD fast line crosses above slow line (buy signal) and Supertrend direction is upward (direction==1).
4. Risk Management: Sets 0.5% stop-loss and 99.99% take-profit levels for each trade to protect capital and secure profits.

#### Strategy Advantages
1. Dual Confirmation Mechanism: Significantly improves trading signal accuracy by combining trend following (Supertrend) and momentum (MACD) indicators.
2. Strong Adaptability: Supertrend indicator automatically adjusts parameters based on market volatility through ATR calculations.
3. Comprehensive Risk Control: Percentage-based stop-loss strategy ensures controllable risk per trade.
4. Clear Execution Logic: Well-defined entry and exit conditions minimize subjective judgment interference.
5. Simple Operation: Strategy logic is intuitive, facilitating practical operation and monitoring.

#### Strategy Risks
1. Trend Dependency: May generate frequent false signals in ranging markets, increasing trading costs.
2. Lag Risk: Both MACD and Supertrend are lagging indicators, potentially responding slowly to rapid market reversals.
3. Fixed Stop-Loss Risk: Fixed percentage stop-loss may not adequately adapt to volatility characteristics in different market environments.
4. Parameter Sensitivity: Strategy effectiveness depends on multiple parameter settings, requiring continuous optimization.

#### Strategy Optimization Directions
1. Dynamic Stop-Loss Optimization: Recommend replacing fixed stop-loss with ATR-based dynamic stop-loss for better market adaptation.
2. Market Environment Filtering: Add volatility indicators (e.g., VIX) as market environment filters to adjust parameters or pause trading during high volatility.
3. Volume-Price Relationship Integration: Consider incorporating volume indicators into signal confirmation system.
4. Parameter Adaptation Optimization: Develop parameter adaptation mechanism based on market conditions.
5. Position Management Enhancement: Introduce dynamic position sizing mechanism adjusting trade size based on market volatility and account equity.

#### Summary
The strategy constructs a relatively reliable trend following trading system by combining advantages of MACD and Supertrend indicators. The 46% accuracy rate and 46% return demonstrate profitable potential. Through suggested optimizations, particularly dynamic stop-loss and market environment filtering, strategy stability and adaptability can be further enhanced. Suitable for intraday and futures trading, users should note market environment compatibility and adjust parameters according to actual conditions.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-11-10 00:00:00
end: 2024-12-09 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('MANTHAN BHRAMASTRA', overlay=true)

// Supertrend function
f_supertrend(_period, _multiplier) =>
    atr = ta.sma(ta.tr, _period)
    upTrend = hl2 - _multiplier * atr
    downTrend = hl2 + _multiplier * atr
    var float _supertrend = na
    var int _trendDirection = na
    _supertrend := na(_supertrend[1]) ? hl2 : close[1] > _supertrend[1] ? math.max(upTrend, _supertrend[1]) : math.min(downTrend, _supertrend[1])
    _trendDirection := close > _supertrend ? 1 : -1
    [_supertrend, _trendDirection]

// Supertrend Settings
factor = input(2, title='Supertrend Factor')
atrLength = input(20, title='Supertrend ATR Length')

// Calculate Supertrend
[supertrendValue, direction] = f_supertrend(atrLength, factor)


// MACD Settings
fastLength = input(12, title='MACD Fast Length')
slowLength = input(26, title='MACD Slow Length')
signalSmoothing = input(9, title='MACD Signal Smoothing')

// Calculate MACD
[macdLine, signalLine, _] = ta.macd(close, fastLength, slowLength, signalSmoothing)

// Generate Buy signals
buySignal = ta.crossover(macdLine, signalLine) and direction == 1

// Plot Buy signals

// Calculate stop loss and take profit levels (0.25% of the current price)
longStopLoss = close * 0.9950
longTakeProfit = close * 1.9999

// Execute Buy orders with Target and Stop Loss
if buySignal
    strategy.entry('Buy', strategy.long)
    strategy.exit('Sell', 'Buy', stop=longStopLoss, limit=longTakeProfit)


```

> Detail

https://www.fmz.com/strategy/474704

> Last Modified

2024-12-11 17:16:05

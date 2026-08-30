
> Name

Parabolic SAR Indicator Divergence Trading Strategy-Parabolic-SAR-Divergence-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/13927233d8b434248ea.png)

[trans]
#### Overview
This strategy is a trading system based on the divergence relationship between the Parabolic SAR indicator and price. By monitoring the divergence between the SAR indicator and price trends, you can identify potential trend reversal points and capture market turning opportunities. The strategy uses the classic parabolic SAR indicator as the core technical indicator, combined with the divergence analysis method, to build a complete trend following trading system.
#### Strategy Principle
The core logic of the strategy includes the following key elements:
1. Use the Parabolic SAR indicator to track price trends. This indicator has the characteristics of dynamically adjusting the acceleration factor.
2. Detect the divergence between price and SAR indicator by setting a lookback period (lookback)
3. When there is a bullish divergence (the price hits a new low but the SAR does not hit a new low), a long signal is triggered.
4. When there is a bearish divergence (the price reaches a new high but the SAR does not reach a new high), a short signal is triggered.
5. The system marks trading signals on the chart through shape.triangleup and shape.triangledown
6. Integrated alert function to promptly notify traders when trading signals occur
#### Strategic Advantages
1. Scientific selection of indicators
- Parabolic SAR is a mature indicator that has been tested by the market
- Indicator parameters can be flexibly adjusted according to different market characteristics
2. The signaling mechanism is reliable
- Divergence signals have strong trend prediction capabilities
- Combine price trends and indicator trends to reduce false signals
3. Complete system design
- Contains complete signal generation, execution and monitoring mechanisms
- Integrated graphical interface and alarm function for easy operation
#### Strategy Risk
1. Parameter sensitivity
- Improper setting of SAR parameters may lead to over-trading
- Deviation detection period selection will affect signal quality
2. Market adaptability
- False signals may occur in highly volatile markets
- Invalid signals may appear frequently in sideways markets
3. Insufficient risk control
- Lack of stop loss mechanism
- No position management system
#### Strategy optimization direction
1. Enhance signal filtering
- Add trend filter to only trade in the main trend direction
- Combined with trading volume indicators to verify signal validity
2. Improve risk control
-Add dynamic stop loss mechanism
- Design warehouse management system
3. Optimize parameter adjustment
- Develop adaptive parameter systems
- Dynamically adjust parameters according to different market conditions
#### Summary
This is a trend following strategy based on classic technical indicators that captures market turning points through divergence analysis. The strategic design ideas are clear, the implementation method is simple, and it has good operability. However, in practical applications, it still needs to be optimized according to specific market characteristics, especially in terms of risk control, which needs to be further improved. By adding a filtering mechanism and improving the risk control system, this strategy is expected to achieve more stable trading performance.
|| 

#### Overview
This strategy is a trading system based on divergence relationships between the Parabolic SAR indicator and price movement. By monitoring divergence phenomena between SAR indicator and price trends, it identifies potential trend reversal points to capture market turning opportunities. The strategy employs the classic Parabolic SAR indicator as its core technical indicator, combined with divergence analysis methods to construct a complete trend-following trading system.

#### Strategy Principles
The core logic includes several key elements:
1. Uses Parabolic SAR indicator to track price trends, featuring dynamic adjustment of acceleration factors
2. Detects divergence between price and SAR indicator through a set lookback period
3. Triggers long signals when bullish divergence occurs (price makes new lows while SAR doesn't)
4. Triggers short signals when bearish divergence occurs (price makes new highs while SAR doesn't)
5. Marks trading signals on charts using shape.triangleup and shape.triangledown
6. Integrates alert functionality to notify traders of trading signals promptly

#### Strategy Advantages
1. Scientific Indicator Selection
- Parabolic SAR is a market-tested mature indicator
- Indicator parameters can be flexibly adjusted for different market characteristics
2. Reliable Signal Mechanism
- Divergence signals have strong trend prediction capability
- Combines price and indicator trends to reduce false signals
3. Complete System Design
- Includes comprehensive signal generation, execution, and monitoring mechanisms
- Integrates graphical interface and alert functions for easy operation

#### Strategy Risks
1. Parameter Sensitivity
- Improper SAR parameter settings may lead to overtrading
- Divergence detection period selection affects signal quality
2. Market Adaptability
- May generate false signals in volatile markets
- Frequent invalid signals may occur in ranging markets
3. Insufficient Risk Control
- Lacks stop-loss mechanism
- No position management system

#### Strategy Optimization Directions
1. Enhanced Signal Filtering
- Add trend filters to trade only in main trend direction
- Incorporate volume indicators to verify signal validity
2. Improved Risk Control
- Add dynamic stop-loss mechanism
- Design position management system
3. Optimized Parameter Adjustment
- Develop adaptive parameter system
- Dynamically adjust parameters based on market conditions

#### Summary
This is a trend-following strategy based on classic technical indicators, capturing market turning points through divergence analysis. The strategy design is clear, implementation methods are concise, and it has good operability. However, in practical application, it still needs optimization according to specific market characteristics, especially in risk control aspects. Through adding filtering mechanisms and improving the risk control system, this strategy has the potential to achieve more stable trading performance.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-11 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("SAR Divergence Strategy", overlay=true)

// --- Inputs ---
length = input.int(14, title="SAR Length", minval=1)
accelerationFactor = input.float(0.02, title="Acceleration Factor", minval=0.01)
maximumFactor = input.float(0.2, title="Maximum Factor", minval=0.01)

// --- SAR Calculation ---
sar = ta.sar(length, accelerationFactor, maximumFactor)

// --- Divergence Detection ---
lookback = 5

// Bullish Divergence
bullCond = close[lookback] < close[lookback + 1] and sar[lookback] > sar[lookback + 1]

// Bearish Divergence
bearCond = close[lookback] > close[lookback + 1] and sar[lookback] < sar[lookback + 1]

// --- Strategy Logic ---
if (bullCond)
    strategy.entry("Long", strategy.long)

if (bearCond)
    strategy.entry("Short", strategy.short)

// --- Plotting ---
plot(sar, color=color.blue, linewidth=2, title="Parabolic SAR")

plotshape(bullCond, style=shape.triangleup, color=color.green, size=size.small, title="Bullish Divergence")
plotshape(bearCond, style=shape.triangledown, color=color.red, size=size.small, title="Bearish Divergence")

// --- Alerts ---
alertcondition(bullCond, title="Bullish SAR Divergence", message="Bullish Divergence detected")
alertcondition(bearCond, title="Bearish SAR Divergence", message="Bearish Divergence detected")
```

> Detail

https://www.fmz.com/strategy/471696

> Last Modified

2024-11-12 15:12:33

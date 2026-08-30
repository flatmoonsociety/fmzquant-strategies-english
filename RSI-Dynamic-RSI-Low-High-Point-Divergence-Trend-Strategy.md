
> Name

Dynamic RSI low-high point divergence trend strategy-Dynamic-RSI-Low-High-Point-Divergence-Trend-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/80c0c079c99e75a7c2e2f75844b8d691e97448d017d720686d72ba6061dcc493.png)
![IMG](assets/images/516ed30162980678340ccad9da5f3d3662da31d88908a21dc7c48475677f7434.png)




[trans]
#### Overview
This article details a low-high divergence trend trading strategy based on the Relative Strength Index (RSI). This strategy captures potential trend reversal opportunities by identifying divergences between price and the RSI indicator, providing traders with accurate entry and exit signals. The strategy uniquely combines visual signals and technical indicator analysis to improve the accuracy and timeliness of trading decisions.
#### Strategy Principle
The core principle of the strategy is based on the low-high divergence theory of the Relative Strength Index (RSI). The specific implementation includes the following key steps:
1. Calculate the RSI indicator: Use the 14-period RSI length to evaluate the current overbought and oversold status of the market.
2. Identify price extremes: determine lows and highs through lookback periods.
3. Deviation judgment mechanism:
   - Bullish divergence: Price makes a new low, while the RSI indicator does not fall in tandem
   - Bearish divergence: Price makes a new high while the RSI indicator does not rise in tandem
4. Signal generation:
   - Bullish divergence in oversold zone (below 30)
   - Bearish divergence in the overbought zone (above 70)
#### Strategic Advantages
1. High-precision signal identification: filtering through strict deviation conditions to reduce false signals.
2. Visual signal presentation: Use large triangle markers and background highlights to improve signal readability.
3. High flexibility: RSI parameters, lookback period and overbought and oversold thresholds can be adjusted.
4. Multi-time frame adaptability: performs best in the 1 hour to 4 hour period.
5. Debugging function: Built-in debugging form to facilitate verification of key indicators.
#### Strategy Risk
1. Risk of misjudgment: divergence signals are not 100% accurate, and there is a certain probability of false signals.
2. Severe market volatility: In strongly trending markets, divergence strategies may perform poorly.
3. Parameter sensitivity: Improper settings of RSI parameters and lookback periods may reduce the strategy effect.
4. Transaction costs: Frequent transactions may incur higher handling fees and slippage costs.
#### Strategy optimization direction
1. Multi-indicator confirmation: Combined with moving average, MACD and other indicators to improve signal accuracy.
2. Dynamic parameter adjustment: Intelligently adjust RSI parameters according to market volatility.
3. Stop loss mechanism: Introduce a dynamic stop loss strategy based on ATR.
4. Machine learning optimization: Use machine learning algorithms to dynamically optimize entry and exit points.
5. Risk management: Adjust position size according to market volatility.
#### Summarize
The dynamic RSI low-high point divergence trend strategy provides traders with a relatively efficient trend trading method through precise technical indicator analysis and visual signals. Through continuous optimization and risk management, the strategy is expected to maintain stable performance in different market environments.
|| 

#### Overview

This article elaborates on a trend trading strategy based on the Relative Strength Index (RSI) low-high point divergence. The strategy captures potential trend reversal opportunities by identifying divergences between price and RSI indicators, providing traders with precise entry and exit signals. The strategy uniquely combines visual signals and technical indicator analysis to enhance the accuracy and timeliness of trading decisions.

#### Strategy Principles

The core principle is based on the RSI low-high point divergence theory. Key implementation steps include:

1. RSI Calculation: Using 14-period RSI length to assess market overbought and oversold states.
2. Price Extreme Identification: Determining low and high points through lookback period.
3. Divergence Judgment Mechanism:
   - Bullish Divergence: Price makes a new low, but RSI does not synchronously decline
   - Bearish Divergence: Price makes a new high, but RSI does not synchronously rise
4. Signal Generation:
   - Bullish divergence in oversold zone (below 30)
   - Bearish divergence in overbought zone (above 70)

#### Strategy Advantages

1. High-precision Signal Identification: Reduce false signals through strict divergence conditions.
2. Visualization of Signals: Large triangular markers and background highlighting enhance readability.
3. High Flexibility: Adjustable RSI parameters, lookback periods, and overbought/oversold thresholds.
4. Multi-timeframe Adaptability: Best performance on 1-hour to 4-hour periods.
5. Debugging Functionality: Built-in debug table for verifying key indicators.

#### Strategy Risks

1. Misjudgment Risk: Divergence signals are not 100% accurate.
2. Market Volatility: May underperform in strongly trending markets.
3. Parameter Sensitivity: Improper RSI and lookback period settings can reduce strategy effectiveness.
4. Transaction Costs: Frequent trading may incur high commission and slippage expenses.

#### Strategy Optimization Directions

1. Multi-indicator Confirmation: Incorporate moving averages, MACD to improve signal accuracy.
2. Dynamic Parameter Adjustment: Intelligently adjust RSI parameters based on market volatility.
3. Stop-loss Mechanism: Introduce ATR-based dynamic stop-loss strategy.
4. Machine Learning Optimization: Use machine learning algorithms to optimize entry and exit points.
5. Risk Management: Adjust position sizes based on market volatility.

#### Summary

The Dynamic RSI Low-High Point Divergence Trend Strategy provides traders with an efficient trend trading method through precise technical indicator analysis and visual signals. Continuous optimization and risk management can help maintain stable performance across different market environments.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-31 00:00:00
end: 2025-03-29 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=6
strategy("RSI Divergence Strategy - Visible Signals", overlay=true)

// 1. Basic Inputs (Keep it simple)
rsiLength = input.int(14, "RSI Length")
lookback = input.int(10, "Lookback Period", minval=5)
oversold = input.int(30, "Oversold Level")
overbought = input.int(70, "Overbought Level")

// 2. Calculate Indicators
rsi = ta.rsi(close, rsiLength)
priceLow = ta.lowest(low, lookback)
priceHigh = ta.highest(high, lookback)
rsiLow = ta.lowest(rsi, lookback)
rsiHigh = ta.highest(rsi, lookback)

// 3. Simple Divergence Detection
bullishDiv = low == priceLow and rsi > rsiLow and rsi < oversold
bearishDiv = high == priceHigh and rsi < rsiHigh and rsi > overbought

// 4. Visual Signals (Large and Clear)
plotshape(bullishDiv, "Buy", shape.triangleup, location.belowbar, 
     color=color.new(color.green, 0), size=size.large)
plotshape(bearishDiv, "Sell", shape.triangledown, location.abovebar, 
     color=color.new(color.red, 0), size=size.large)

// 5. Optional: Add Background for Better Visibility
bgcolor(bullishDiv ? color.new(color.green, 90) : bearishDiv ? color.new(color.red, 90) : na)

// 6. Basic Strategy Execution
if bullishDiv
    strategy.entry("Long", strategy.long)
    
if bearishDiv
    strategy.entry("Short", strategy.short)

// 7. Debugging Table (To verify values)
var table debugTable = table.new(position.top_right, 4, 1)
if barstate.islast
    table.cell(debugTable, 0, 0, "RSI: " + str.tostring(rsi))
    table.cell(debugTable, 1, 0, "Price Low: " + str.tostring(priceLow))
    table.cell(debugTable, 2, 0, "RSI Low: " + str.tostring(rsiLow))
    table.cell(debugTable, 3, 0, "Signal: " + (bullishDiv ? "BUY" : bearishDiv ? "SELL" : "NONE"))
    // Test Settings (paste these above the strategy call)
//rsiLength := 5
//lookback := 5
//oversold := 20
//overbought := 80
```

> Detail

https://www.fmz.com/strategy/488907

> Last Modified

2025-03-31 17:24:27

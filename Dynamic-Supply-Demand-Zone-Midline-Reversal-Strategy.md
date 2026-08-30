
> Name

Dynamic supply and demand zone midline reversal strategy-Dynamic-Supply-Demand-Zone-Midline-Reversal-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/4530580817feee75d5dfa756596fb07b8d6d9a2c8855cd16ac45676ef9ca00d5.png)
![IMG](assets/images/ad13350c1c41d0f4cf9ed34f1a8213558fd3aa478b908b1b1426092d5e62fc27.png)



[trans]
#### Overview
This strategy is a trading system based on supply and demand ranges and midline reversals, operating on the 5-minute time frame. It trades by identifying reversal signals when the trend pulls back to the midline position and placing take profits and stops at predetermined supply and demand areas. The strategy combines moving averages (SMA) to determine trend direction, identifying supply and demand intervals through high and low points, and using the midpoint of the interval as an important price reference level.
#### Strategy Principle
The core logic of the strategy includes the following key elements:
1. Determination of supply and demand range: Use the highest price and lowest price of the user-defined period (default 50 periods) to determine the supply area (resistance level) and demand area (support level)
2. Midline calculation: Take the midpoint of the supply and demand interval as an important reference position for price reversal
3. Trend judgment: Use a simple moving average (default period 20) to judge the current trend direction.
4. Admission conditions:
   - Long: Price is above the moving average (uptrend) and a bullish candle pattern appears below the midpoint
   - Short: Price is below the moving average (downtrend) and a bearish candle pattern appears above the midpoint
5. Take profit and stop loss settings:
   - Long: Take profit is set in the supply area, and stop loss is set in the demand area.
   - Short position: Take profit is set in the demand area, stop loss is set in the supply area
#### Strategic Advantages
1. Clear logic: a complete trading system is constructed by combining trends, price structures and candlestick patterns.
2. Perfect risk management: Set profit and loss points based on the market structure, in line with the law of price movement
3. Strong adaptability: can adapt to different market environments through parameter adjustment
4. Visual support: visually display trading signals and key price levels through marks and lines
5. High degree of automation: clear entry and exit conditions enable fully automated trading
#### Strategy Risk
1. False breakthrough risk: Prices may fluctuate back and forth within the supply and demand range, generating false signals.
2. Parameter sensitivity: Different parameter settings may lead to significantly different trading results.
3. Market environment dependence: may perform poorly in violently volatile or sideways markets
4. Impact of slippage: In a market with poor liquidity, the actual transaction price may deviate greatly from the signal price.
5. Overtrading: Frequent range breakouts can lead to overtrading
#### Strategy optimization direction
1. Signal filtering:
   - Add volume confirmation
   - Introduce volatility indicator to screen trading environment
2. Dynamic parameters:
   - Adaptively adjust parameters based on market volatility
   -Introduction of adaptive moving average
3. Risk management optimization:
   - Implement dynamic position management
   - Added P/L ratio filter
4. Market environment identification:
   - Develop market status classification system
   - Use different parameter settings in different market conditions
#### Summary
The dynamic supply and demand range midline reversal strategy is a trading system that combines multiple dimensions of technical analysis to capture market opportunities through the cooperation of supply and demand ranges, trends and price patterns. The core advantage of this strategy lies in its clear logical framework and complete risk management system, but it also requires traders to pay close attention to changes in the market environment and adjust parameter settings in a timely manner. Through the proposed optimization direction, the stability and adaptability of the strategy are expected to be further improved.
|| 

#### Overview
This strategy is a trading system based on supply-demand zones and midline reversal, operating on a 5-minute timeframe. It generates trading signals when price retraces to the midline during trends, with take-profit and stop-loss levels set at pre-identified supply and demand zones. The strategy combines Simple Moving Average (SMA) for trend direction, identifies supply-demand zones through highs and lows, and uses the zone midpoint as a crucial price reference level.

#### Strategy Principles
The core logic includes several key elements:
1. Supply-Demand Zone Identification: Uses user-defined period (default 50) highs and lows to determine supply (resistance) and demand (support) zones
2. Midline Calculation: Takes the midpoint of supply-demand zones as a key price reversal reference
3. Trend Determination: Employs Simple Moving Average (default 20 periods) to determine current trend direction
4. Entry Conditions:
   - Long: Price above SMA (uptrend) with bullish candlestick pattern below midpoint
   - Short: Price below SMA (downtrend) with bearish candlestick pattern above midpoint
5. Take-Profit and Stop-Loss Setup:
   - Long: Take-profit at supply zone, stop-loss at demand zone
   - Short: Take-profit at demand zone, stop-loss at supply zone

#### Strategy Advantages
1. Clear Logic: Combines trend, price structure, and candlestick patterns into a complete trading system
2. Robust Risk Management: Sets profit targets and stops based on market structure
3. High Adaptability: Can be adjusted through parameters for different market conditions
4. Visual Support: Provides clear visualization of trading signals and key price levels
5. High Automation: Clear entry and exit conditions enable fully automated trading

#### Strategy Risks
1. False Breakout Risk: Price may oscillate within supply-demand zones, generating false signals
2. Parameter Sensitivity: Different parameter settings may lead to significantly different trading results
3. Market Environment Dependency: May underperform in highly volatile or ranging markets
4. Slippage Impact: Actual execution prices may deviate significantly from signal prices in less liquid markets
5. Overtrading: Frequent zone breakouts may lead to excessive trading

#### Strategy Optimization Directions
1. Signal Filtering:
   - Add volume confirmation
   - Incorporate volatility indicators for market condition filtering
2. Dynamic Parameters:
   - Implement adaptive parameter adjustment based on market volatility
   - Introduce adaptive moving averages
3. Risk Management Enhancement:
   - Implement dynamic position sizing
   - Add risk-reward ratio filters
4. Market Environment Recognition:
   - Develop market state classification system
   - Use different parameter settings for different market states

#### Summary
The Dynamic Supply-Demand Zone Midline Reversal Strategy is a trading system that combines multiple dimensions of technical analysis, capturing market opportunities through the interplay of supply-demand zones, trends, and price patterns. Its core strengths lie in its clear logical framework and comprehensive risk management system, but traders need to closely monitor market environment changes and adjust parameters accordingly. Through the suggested optimization directions, the strategy's stability and adaptability can be further enhanced.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-02-16 00:00:00
end: 2025-02-23 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © bommytarton

//@version=6
strategy("Midline Rejection Entry with TP/SL at Supply/Demand", overlay=true)

// User inputs for Swing Length and Length for Supply/Demand Zones
length = input.int(50, title="Swing Length", minval=1)
midlineLength = input.int(20, title="Midline Length for Trend", minval=1)  // Moving average length for trend

// Identify swing highs (Supply Zone) and swing lows (Demand Zone)
supplyZone = ta.highest(high, length) // Supply Zone (resistance)
demandZone = ta.lowest(low, length) // Demand Zone (support)

// Calculate the midpoint between supply and demand zones
midpoint = (supplyZone + demandZone) / 2

// Trend Detection: Use a simple moving average (SMA) for trend direction
smaTrend = ta.sma(close, midlineLength)

// Variables to store Supply/Demand Zones at the time of entry
var float entrySupplyZone = na
var float entryDemandZone = na
var float entryMidpoint = na

// Entry Conditions
// 1. Price in an uptrend (close above SMA)
longCondition = close > smaTrend and close < midpoint and close > open and open < close[1] and close[1] < open[1]

// 1. Price in a downtrend (close below SMA)
shortCondition = close < smaTrend and close > midpoint and close < open and open > close[1] and close[1] > open[1]

// Close any open trades before opening a new one
if (longCondition or shortCondition)
    strategy.close_all()

// Execute the entry logic
if (longCondition)
    entrySupplyZone := supplyZone  // Store Supply Zone for Take Profit
    entryDemandZone := demandZone  // Store Demand Zone for Stop Loss
    entryMidpoint := midpoint      // Store Midpoint
    strategy.entry("Long", strategy.long)
    label.new(bar_index, low, "Open Long", color=color.green, textcolor=color.white, style=label.style_label_up, size=size.small)

if (shortCondition)
    entrySupplyZone := supplyZone  // Store Supply Zone for Stop Loss
    entryDemandZone := demandZone  // Store Demand Zone for Take Profit
    entryMidpoint := midpoint      // Store Midpoint
    strategy.entry("Short", strategy.short)
    label.new(bar_index, high, "Open Short", color=color.red, textcolor=color.white, style=label.style_label_down, size=size.small)

// Define Take Profit and Stop Loss Levels for Long/Short Trades
if (strategy.opentrades > 0)
    // For Long trades, use Supply Zone for Take Profit and Demand Zone for Stop Loss
    if (strategy.position_size > 0)
        strategy.exit("Take Profit", "Long", limit=entrySupplyZone)  // Take Profit at Supply Zone
        strategy.exit("Stop Loss", "Long", stop=entryDemandZone)    // Stop Loss at Demand Zone


    // For Short trades, use Demand Zone for Take Profit and Supply Zone for Stop Loss
    if (strategy.position_size < 0)
        strategy.exit("Take Profit", "Short", limit=entryDemandZone)  // Take Profit at Demand Zone
        strategy.exit("Stop Loss", "Short", stop=entrySupplyZone)     // Stop Loss at Supply Zone


// Re-Plot Supply, Midpoint, and Demand Zones after Trade Closure
plot(supplyZone, title="Supply Zone", color=color.red, linewidth=2, style=plot.style_line)
plot(demandZone, title="Demand Zone", color=color.green, linewidth=2, style=plot.style_line)
plot(midpoint, title="Midpoint", color=color.blue, linewidth=1, style=plot.style_line)

```

> Detail

https://www.fmz.com/strategy/483514

> Last Modified

2025-02-24 16:00:34

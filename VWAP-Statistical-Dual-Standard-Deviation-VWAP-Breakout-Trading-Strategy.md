
> Name

Double-standard deviation dynamic VWAP shock breakout trading strategy based on quantitative statistics-Statistical-Dual-Standard-Deviation-VWAP-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/0be5b612315f6ed9c939cb24b51fab3fd8f5720c13ffcffaf94124c45b488a7a.png)

[trans]
#### Overview
This strategy is a trend breakout strategy based on VWAP (Volume Weighted Average Price) and standard deviation channels. It constructs a dynamic price fluctuation range by calculating VWAP and upper and lower standard deviation channels, which is used to capture trading opportunities when prices break upward. The strategy mainly relies on trading on breakout signals of the standard deviation band, and sets profit targets and order intervals to control risks.
#### Strategy Principle
1. Calculation of core indicators:
- Calculate VWAP using intraday HL2 price and volume
- Calculate standard deviation based on price fluctuations
- Set the upper and lower channels to 1.28 times the standard deviation
2. Transaction logic:
- Entry conditions: The price crosses the lower track and then rises to the upper level
- Exit conditions: reaching the preset profit target
- Set minimum order interval to avoid frequent transactions
#### Strategic Advantages
1. Basics of Statistics
- Price hub reference based on VWAP
- Measure volatility using standard deviation
- Dynamically adjust trading ranges
2. Risk control
- Set fixed profit targets
- Control transaction frequency
- Only do long strategies to reduce risk
#### Strategy Risk
1. Market risk
- Severe fluctuations may lead to false breakouts
- It is difficult to accurately grasp the trend turning point
- Increased losses due to unilateral falling market conditions
2. Parameter risk
- Standard deviation multiple setting is sensitive
- Profit target setting needs to be optimized
- Trading interval affects income performance
#### Optimization direction
1. Signal optimization
- Added trend judgment filter
-Confirm based on changes in trading volume
- Add other technical indicator verification
2. Risk management optimization
- Dynamically set stop loss positions
- Adjust positions based on volatility
- Improve order management mechanism
#### Summary
This is a quantitative trading strategy that combines statistical principles and technical analysis. Through the cooperation of VWAP and standard deviation band, a relatively reliable trading system is constructed. The core advantage of the strategy lies in its scientific statistical basis and complete risk control mechanism, but it still needs to continuously optimize parameters and trading logic in practical applications.
||
#### Overview
This strategy is a trend breakout system based on VWAP (Volume Weighted Average Price) and standard deviation channels. It constructs a dynamic price range by calculating VWAP and standard deviation bands to capture upward breakout opportunities. The strategy mainly relies on standard deviation band breakthrough signals for trading, with profit targets and order intervals to control risk.
#### Strategy Principles
1. Core Indicator Calculation:
- Calculate VWAP using intraday HL2 prices and volume
- Compute standard deviation based on price volatility
- Set 1.28 times standard deviation upper and lower bands

2. Trading Logic:
- Entry condition: price crosses below lower band then rises above it
- Exit condition: reaches preset profit target
- Minimum order interval to avoid frequent trading

#### Strategy Advantages
1. Statistical Foundation
- VWAP-based price center reference
- Volatility measurement using standard deviation
- Dynamic trading range adjustment

2. Risk Control
- Fixed profit target setting
- Trading frequency control
- Long-only strategy reduces risk

#### Strategy Risks
1. Market Risks
- False breakouts during high volatility
- Difficulty in accurately timing trend reversals
- Increased losses in downtrend markets

2. Parameter Risks
- Sensitivity to standard deviation multiplier settings
- Profit target optimization needed
- Trading interval affects performance

#### Optimization Directions
1. Signal Optimization
- Add trend filter
- Incorporate volume change confirmation
- Include additional technical indicators

2. Risk Management Optimization
- Dynamic stop-loss placement
- Position sizing based on volatility
- Enhanced order management system

#### Summary
This is a quantitative trading strategy combining statistical principles and technical analysis. Through the combination of VWAP and standard deviation bands, it builds a relatively reliable trading system. The core advantages lie in its scientific statistical foundation and comprehensive risk control mechanisms, but continuous optimization of parameters and trading logic is still needed in practical applications.
[/trans]



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
strategy("VWAP Stdev Bands Strategy (Long Only)", overlay=true)

// Standard Deviation Inputs
devUp1 = input.float(1.28, title="Stdev above (1)")
devDn1 = input.float(1.28, title="Stdev below (1)")

// Show Options
showPrevVWAP = input(false, title="Show previous VWAP close?")
profitTarget = input.float(2, title="Profit Target ($)", minval=0) // Profit target for closing orders
gapMinutes = input.int(15, title="Gap before new order (minutes)", minval=0) // Gap for placing new orders

// VWAP Calculation
var float vwapsum = na
var float volumesum = na
var float v2sum = na
var float prevwap = na // Track the previous VWAP
var float lastEntryPrice = na // Track the last entry price
var int lastEntryTime = na // Track the time of the last entry

start = request.security(syminfo.tickerid, "D", time)
newSession = ta.change(start)

vwapsum := newSession ? hl2 * volume : vwapsum[1] + hl2 * volume
volumesum := newSession ? volume : volumesum[1] + volume
v2sum := newSession ? volume * hl2 * hl2 : v2sum[1] + volume * hl2 * hl2

myvwap = vwapsum / volumesum
dev = math.sqrt(math.max(v2sum / volumesum - myvwap * myvwap, 0))

// Calculate Upper and Lower Bands
lowerBand1 = myvwap - devDn1 * dev
upperBand1 = myvwap + devUp1 * dev

// Plot VWAP and Bands with specified colors
plot(myvwap, style=plot.style_line, title="VWAP", color=color.green, linewidth=1)
plot(upperBand1, style=plot.style_line, title="VWAP Upper (1)", color=color.blue, linewidth=1)
plot(lowerBand1, style=plot.style_line, title="VWAP Lower (1)", color=color.red, linewidth=1)

// Trading Logic (Long Only)
longCondition = close < lowerBand1 and close[1] >= lowerBand1 // Price crosses below the lower band

// Get the current time in minutes
currentTime = timestamp("GMT-0", year(timenow), month(timenow), dayofmonth(timenow), hour(timenow), minute(timenow))

// Check if it's time to place a new order based on gap
canPlaceNewOrder = na(lastEntryTime) or (currentTime - lastEntryTime) >= gapMinutes * 60 * 1000

// Close condition based on profit target
if (strategy.position_size > 0)
    if (close - lastEntryPrice >= profitTarget)
        strategy.close("B")
        lastEntryTime := na // Reset last entry time after closing

// Execute Long Entry
if (longCondition and canPlaceNewOrder)
    strategy.entry("B", strategy.long)
    lastEntryPrice := close // Store the entry price
    lastEntryTime := currentTime // Update the last entry time

    // Add label for the entry
    label.new(bar_index, close, "B", style=label.style_label_down, color=color.green, textcolor=color.white, size=size.small)

// Optional: Plot previous VWAP for reference
prevwap := newSession ? myvwap[1] : prevwap[1]
plot(showPrevVWAP ? prevwap : na, style=plot.style_circles, color=close > prevwap ? color.green : color.red)
```

> Detail

https://www.fmz.com/strategy/477602

> Last Modified

2025-01-06 16:31:36

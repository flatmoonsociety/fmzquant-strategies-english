
> Name

QFL Oscillation Conditional Stop-Loss Moving Average Strategy-QFL-Oscillation-Stop-Loss-Moving-Average-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/6ec93b794c2df6160390c49a431c865a577eba5e4df39cc5a13c14a3eda5338f.png)

[trans]
#### Overview
This strategy is a trading system based on the idea of Jackson QFL (Quick finger Luc). It mainly builds positions by identifying the timing of panic decline in the market, and carries out stop-profit and stop-loss management through the moving average system. The core of the strategy is to capture the trading opportunities brought about by short-term violent fluctuations, confirm the entry timing through multiple technical indicators, and achieve the goal of building a low position.
#### Strategy Principle
The strategy uses the ATR (Average True Range) indicator and customized Base Level and Rebound Level as the main trading signals. When the price falls in a panic and breaks through the baseline, a long signal is triggered. The system determines whether there is a panic drop by calculating the recent K-line fluctuation range and combining it with the ATR multiple. There are three modes of take profit: average price, first entry price and batch take profit, which can be flexibly selected according to different market environments. The system also sets a cooling-off period to avoid frequent transactions.
#### Strategic Advantages
1. The trading logic is clear, and the timing of entry is determined quantitatively through technical indicators to reduce the interference of subjective factors.
2. Multiple confirmation mechanism improves transaction reliability, including ATR filtering, baseline breakthrough and panic drop confirmation
3. Flexible profit-taking mechanism, different profit-taking methods can be selected according to market conditions
4. Equipped with protective mechanisms, including transaction interval control and stop loss settings, to effectively control risks
5. The system has a high degree of automation and can realize fully automatic transactions and reduce human intervention.
#### Strategy Risk
1. False signals may be triggered frequently in volatile markets, increasing transaction costs.
2. Relying on historical data to calculate the baseline may become invalid when the market suddenly changes.
3. The take-profit setting may exit a strong market prematurely and miss greater profits.
4. In a market with insufficient liquidity, the judgment of panic decline may be inaccurate.
5. Parameter optimization involves the risk of over-fitting and needs to be repeatedly verified in different market environments.
#### Strategy optimization direction
1. Introduce trading volume indicators to enhance the accuracy of judgment on panic declines
2. Develop an adaptive parameter system and dynamically adjust it according to market fluctuation characteristics
3. Add the trend judgment module to adjust strategy parameters in obvious trending markets
4. Improve the take-profit mechanism, consider introducing trailing stop-loss and dynamically adjust the take-profit ratio
5. Add market environment classification and adopt different parameter configurations according to different market characteristics.
#### Summary
The QFL shock conditional stop-loss moving average strategy is a comprehensive trading system that captures panic market decline opportunities through multiple technical indicators. The strategy design takes into account actual combat needs and includes complete entry, stop-profit and stop-loss and risk control mechanisms. Although there are certain limitations, through continuous optimization and improvement, it is expected to achieve stable returns in actual transactions. It is recommended that investors conduct sufficient historical data backtesting before applying the real offer, and adjust parameter settings according to specific market characteristics. ||
#### Overview
This strategy is a trading system based on Jackson QFL (Quick finger Luc) philosophy, which primarily identifies market panic sell-offs for position building and manages profit-taking and stop-loss through a moving average system. The core strategy is to capture trading opportunities brought by short-term violent fluctuations, confirming entry timing through multiple technical indicators to achieve low-position building.

#### Strategy Principles
The strategy uses the ATR (Average True Range) indicator and custom Base Level and Rebound Level as primary trading signals. Long positions are triggered when prices show panic selling and break through the base level. The system determines panic selling by calculating recent candlestick volatility ranges combined with ATR multiples. Three profit-taking modes are set: average price, first entry price, and batch profit-taking, which can be flexibly chosen based on different market environments. The system also includes a cooldown period to avoid frequent trading.

#### Strategy Advantages
1. Clear trading logic, using technical indicators to quantify entry timing, reducing subjective interference
2. Multiple confirmation mechanisms improve trading reliability, including ATR filtering, base level breakthrough, and panic selling confirmation
3. Flexible profit-taking mechanisms, allowing different methods based on market conditions
4. Protective mechanisms including trade interval control and stop-loss settings for effective risk control
5. High system automation level, enabling fully automated trading with reduced human intervention

#### Strategy Risks
1. May trigger frequent false signals in oscillating markets, increasing trading costs
2. Base level calculations depend on historical data, potentially failing during market changes
3. Profit-taking settings may exit strong trends too early, missing larger gains
4. Panic selling judgment may be inaccurate in markets with insufficient liquidity
5. Parameter optimization faces overfitting risks, requiring repeated validation in different market environments

#### Strategy Optimization Directions
1. Introduce volume indicators to enhance panic selling judgment accuracy
2. Develop adaptive parameter systems that dynamically adjust based on market volatility characteristics
3. Add trend judgment modules to adjust strategy parameters in clear trend markets
4. Improve profit-taking mechanisms, considering trailing stops and dynamic profit ratio adjustments
5. Enhance market environment classification to use different parameter configurations for different market characteristics

#### Summary
The QFL Oscillation Stop-Loss Moving Average Strategy is a comprehensive trading system that captures market panic selling opportunities through multiple technical indicators. The strategy design considers practical needs, including complete entry, profit-taking, stop-loss, and risk control mechanisms. While it has certain limitations, continuous optimization and improvement show promise for stable returns in actual trading. Investors are advised to conduct thorough historical data backtesting before live implementation and adjust parameters according to specific market characteristics.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-19 00:00:00
end: 2025-02-17 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("Jackson Quickfingersluc (QFL) Strategy", overlay=true)

// Parameters
baseLevelMultiplier = input.float(1, title="Base Level Multiplier", minval=0.1, maxval=1.0, step=0.05)
reboundMultiplier = input.float(0.8, title="Rebound Level Multiplier", minval=0.0001, maxval=1.0, step=0.01) // Multiplier for range of past candles
lookBackPeriod = input.int(50, title="Look-back Period", minval=10)
atrPeriod = input.int(14, title="ATR Period", minval=1)
atrMultiplier = input.float(1.2, title="Panic Sell ATR Multiplier", minval=0.1, maxval=5.0, step=0.1) // Multiplier for ATR threshold
exitProfitThreshold = input.float(0.01, title="Exit Profit Threshold", minval=0.001, maxval=0.1, step=0.001) // Minimum profit threshold (e.g., 1%)
panicSellPercentage = input.float(0.005, title="Panic Sell Percentage Below Base Level", step=0.0001) // Percentage below base level for panic sell
showLabels = input.bool(true, title="Show Buy/Sell Labels") // Toggle for showing labels
takeProfitOption = input.string("avg_price", title="Take Profit Option", options=["avg_price", "first_entry", "each_position"]) // TP option selection
rangeBars = input.int(3, title="Number of Bars for Range Calculation", minval=1) // Input for number of bars for range calculation
cooldownBars = input.int(5, title="Cooldown Period (Bars)", minval=1) // Input for cooldown period after a buy

// Calculate Base Level
lowestClose = ta.lowest(close, lookBackPeriod)
baseLevel = lowestClose[1] * baseLevelMultiplier

// Calculate Rebound Level as a multiplier of the range of the last 'rangeBars' bars
rangeLastBars = ta.highest(high, rangeBars) - ta.lowest(low, rangeBars)
reboundLevel = reboundMultiplier * rangeLastBars + baseLevel

// Plotting base and rebound levels
plot(baseLevel, color=color.green, linewidth=2, title="Base Level")
plot(reboundLevel, color=color.red, linewidth=2, title="Rebound Level")

// Calculate ATR
atrValue = ta.atr(atrPeriod)

// Factorial average and panic sell movement calculation
var bool panicSellMovement = false

// Loop through each range and check for panic sell condition
for bar_i = 1 to rangeBars+1
    currentBarRange = high[bar_i - 1] - low[bar_i - 1]  // Current bar range
    rangeOfLastXBars = ta.highest(high, bar_i) - ta.lowest(low, bar_i)  // Range of the last `bar_i` bars
    
    // Condition 1: Check if the average range of the last `bar_i` bars exceeds ATR multiplier
    if (rangeOfLastXBars / bar_i) > atrMultiplier * atrValue
        panicSellMovement := true
        break  // Exit the loop immediately
    
    // Condition 2: Check if the current bar range exceeds ATR multiplier
    if currentBarRange > atrMultiplier * atrValue
        panicSellMovement := true
        break  // Exit the loop immediately

// Define the adjusted base level threshold for panic sell (base level - percentage)
panicSellThreshold = baseLevel[0] * (1 - panicSellPercentage)

// Define panic sell condition with base level check and the panic sell percentage threshold
isPanicSell = low < panicSellThreshold and panicSellMovement

// Define rebound condition
isRebound = close > reboundLevel

// Track the last entry bar index
var float lastEntryBar = na

// Store entry prices for each position in an array
var float[] entryPrices = na
var float[] entrySizes = na

bool exit_cond = false
if (na(entryPrices))
    entryPrices := array.new_float(0)
if (na(entrySizes))
    entrySizes := array.new_float(0)

// Strategy to simulate buys and sells (for backtesting purposes)
entry_cond = isPanicSell and (na(lastEntryBar) or (bar_index - lastEntryBar) > cooldownBars)
if entry_cond
    strategy.entry("Buy", strategy.long)
    lastEntryBar := bar_index  // Set last entry bar to current bar index
    // Store the entry price and size for this new position
    array.push(entryPrices, close)
    array.push(entrySizes, strategy.position_size)

    // Trigger BUY alert
    alert("BUY ALERT: Panic Sell condition triggered", alert.freq_once_per_bar)

isTakeProfitCondition(entryPrice) =>
    profitPercentage = (close - entryPrice) / entryPrice
    profitCondition = profitPercentage >= exitProfitThreshold
    reboundCondition = isRebound
    profitCondition and reboundCondition

// Check TP condition based on selected option
if takeProfitOption == "avg_price"
    avgEntryPrice = strategy.position_avg_price
    if isTakeProfitCondition(avgEntryPrice)
        exit_cond := true
        strategy.close("Buy")
else if takeProfitOption == "first_entry"
    firstEntryPrice = strategy.opentrades.entry_price(0)
    if isTakeProfitCondition(firstEntryPrice)
        exit_cond := true
        strategy.close("Buy")
else if takeProfitOption == "each_position"
    // Ensure we only check when there is at least one entry
    if array.size(entryPrices) > 0
        // Loop until there are no more entries left
        i = 0
        while i < array.size(entryPrices)
            entryPrice = array.get(entryPrices, i)
            positionSize = array.get(entrySizes, i)
            
            // Check profit condition for each position
            if isTakeProfitCondition(entryPrice)
                exit_cond := true
                // Remove the entry price and size from the arrays once the position is closed
                array.remove(entryPrices, i)
                array.remove(entrySizes, i)
                strategy.close("Buy", qty=positionSize) // Close only the position that reached the target
            else
                // Only increment the index if the current entry is not closed
                i := i + 1

// Buy and Sell signals with labels and alerts
if showLabels and isPanicSell
    label.new(bar_index, low, "BUY", style=label.style_label_up, color=color.green, textcolor=color.white, size=size.small)

if showLabels and exit_cond
    label.new(bar_index, high, "SELL", style=label.style_label_down, color=color.rgb(213, 20, 20), textcolor=color.white, size=size.small)

// Trigger SELL alert
if exit_cond
    alert("SELL ALERT: Exit condition met (take profit or rebound)", alert.freq_once_per_bar)
```

> Detail

https://www.fmz.com/strategy/482512

> Last Modified

2025-02-18 18:18:01

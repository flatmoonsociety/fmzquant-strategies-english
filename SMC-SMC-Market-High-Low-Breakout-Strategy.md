
> Name

SMC Market High-Low Breakout Strategy-SMC-Market-High-Low-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1888debaa889488dfd3.png)

[trans]
#### Overview
The SMC market high and low breakout strategy is a quantitative trading strategy based on the principles of Advanced Market Concepts (SMC). This strategy identifies important buying and selling pressure areas (order blocks) in high-level time frames and looks for the best breakout points to enter in the current time frame. This is consistent with the SMC principle that these blocks often act as support or resistance levels. The strategy also considers the trend direction, induced patterns and risk-reward ratio to optimize the entry point and profit-loss ratio.
#### Strategy Principle
1. Identify uptrends and downtrends on high-level time frames such as the 1-hour chart. An uptrend is defined as a closing price higher than the closing price of the previous period and a low higher than the low of the previous period. The opposite is true for a downward trend.
2. Look for inducing patterns on high-level time frames. The bullish induction pattern is that in an upward trend, the high point of the previous period is higher than the high points of the previous two periods and the previous three periods. The short-induced pattern is in a downward trend, and the low of the previous cycle is lower than the low of the previous two and three cycles. 
3. Identify order blocks in high-level time frames. After the bull induction pattern, the highest price and lowest price of the cycle are defined as the upper and lower boundaries of the order block. The opposite is true for bearish inducing patterns.
4. Find the best entry point in the current time frame (such as the 15-minute chart). The long entry is when the current closing price breaks through the lower edge of the order block, and the closing price of the previous period is within the block. Short entry occurs when the closing price falls below the upper edge of the order block.
5. Set stop loss and take profit. The stop-loss position is the boundary of the order block, and the take-profit is calculated based on the set risk-reward ratio (such as 1:1.5).
#### Strategic Advantages
1. Based on the SMC principle, capture the main trends and key support and resistance levels in high-level time frames, avoiding market noise interference in low-level time frames.
2. The identification of induced patterns helps to judge the strength and sustainability of the trend, and provides more basis for entering the market.
3. Make accurate breakthroughs and entries in the current time frame to reduce the risk of invalid signals and retracements.
4. Flexible risk-reward ratio settings that can be adjusted according to personal risk preferences.
#### Strategy Risk
1. In a volatile market or early stage of trend reversal, this strategy may face a certain risk of retracement.
2. Under extreme market conditions (such as sudden rises and falls), the order block may become invalid, causing the stop loss level to be too loose.
3. Only considering price behavior and ignoring other important indicators such as trading volume, the judgment may be biased.
#### Strategy optimization direction
1. Introduce more high-level time frames (such as daily and weekly) as filters to ensure capturing long-term trends.
2. When identifying trends and induced patterns, moving average systems, momentum indicators, etc. can be combined to improve the accuracy of judgment.
3. Dynamically optimize order block boundaries, such as considering ATR (average true range) or channel width, to cope with different market conditions.
4. After entering the market, you can set a trailing stop loss, such as tracking ATR or SAR (parabolic indicator), to reduce the risk of holding a position.
5. Consider market sentiment indicators (such as VIX) or macroeconomic data to identify possible trend reversals or black swan events.
#### Summary
The SMC market high and low breakout strategy is a quantitative trading strategy based on SMC principles. It identifies key pressure areas in high-level time frames and finds the best breakthrough points to enter the market in the current time frame. This strategy comprehensively considers the trend direction, induced patterns and risk-reward ratio to optimize the entry point and profit-loss ratio. The advantage of the strategy is to filter noise based on high-level time frames, accurately capture trends, and have flexible risk management functions. However, in a volatile market or early stage of trend reversal, the strategy may face a certain risk of retracement. In the future, optimization can be done by introducing more time frames, optimizing order block boundaries, dynamic stop loss, and considering market sentiment to improve the robustness and adaptability of the strategy.
|| 

#### Overview
The SMC Market High-Low Breakout Strategy is a quantitative trading strategy based on the principles of Superior Market Concepts (SMC). It identifies significant buying/selling pressure areas (order blocks) on higher timeframes and seeks optimal breakout entry points on the current timeframe. This aligns with the SMC principle that these blocks often act as support or resistance levels. The strategy considers trend direction, inducement patterns, and risk-reward ratio to optimize entry levels and profit targets.

#### Strategy Principles
1. Identify uptrends and downtrends on the higher timeframe (e.g., 1-hour chart). An uptrend is defined as a higher close and higher low compared to the previous period. A downtrend is the opposite.
2. Look for inducement patterns on the higher timeframe. A bullish inducement occurs in an uptrend when the previous high is higher than the highs of the past two and three periods. A bearish inducement occurs in a downtrend when the previous low is lower than the lows of the past two and three periods.
3. Identify order blocks on the higher timeframe. After a bullish inducement, the high and low of that period define the upper and lower boundaries of the order block. The opposite applies to a bearish inducement.
4. Find optimal entry points on the current timeframe (e.g., 15-minute chart). A long entry occurs when the current close breaks above the lower boundary of the order block, and the previous close is within the block. A short entry occurs when the close breaks below the upper boundary.
5. Set stop-loss and take-profit levels. The stop-loss is placed at the boundary of the order block, while the take-profit is calculated based on the set risk-reward ratio (e.g., 1:1.5).

#### Strategy Advantages
1. Based on SMC principles, it captures major trends and key support/resistance levels on higher timeframes, avoiding noise interference on lower timeframes.
2. Identifying inducement patterns helps gauge trend strength and sustainability, providing more basis for entry.
3. Precise breakout entries on the current timeframe reduce false signals and drawdown risks.
4. Flexible risk-reward ratio settings can be adjusted according to individual risk preferences.

#### Strategy Risks
1. During market consolidation or early trend reversals, the strategy may face drawdown risks.
2. In extreme market conditions (e.g., sharp rises or falls), order blocks may become invalid, leading to overly loose stop-losses.
3. Considering only price action and ignoring other important indicators like volume may lead to biased judgments.

#### Strategy Optimization Directions
1. Introduce more higher timeframes (e.g., daily, weekly) for filtering to ensure capturing long-term trends.
2. Combine moving average systems, momentum indicators, etc., to improve the accuracy of trend and inducement pattern identification.
3. Dynamically optimize order block boundaries, such as considering Average True Range (ATR) or channel width, to adapt to different market conditions.
4. Implement trailing stop-losses after entry, such as tracking ATR or Parabolic SAR, to reduce holding risks.
5. Consider market sentiment indicators (e.g., VIX) or macroeconomic data to identify potential trend reversals or black swan events.

#### Summary
The SMC Market High-Low Breakout Strategy is a quantitative trading strategy based on SMC principles. It identifies key pressure areas on higher timeframes and seeks optimal breakout entry points on the current timeframe. The strategy comprehensively considers trend direction, inducement patterns, and risk-reward ratio to optimize entry levels and profit targets. Its advantages lie in filtering out noise based on higher timeframes, precisely capturing trends, and providing flexible risk management features. However, the strategy may face drawdown risks during market consolidation or early trend reversals. Future optimizations can introduce more timeframes, optimize order block boundaries, implement dynamic stop-losses, and consider market sentiment to improve the strategy's robustness and adaptability.
[/trans]



> Source (PineScript)

``` pinescript
//@version=5
strategy("SMC Indian Market Strategy", overlay=true)

// Input Parameters
htf = input.timeframe("60", title="Higher Timeframe")  // For Inducement & Order Block
riskRewardRatio = input.float(1.5, title="Risk:Reward Ratio", minval=0.1)

// Higher Timeframe Data
[htfOpen, htfHigh, htfLow, htfClose] = request.security(syminfo.tickerid, htf, [open, high, low, close])

// Trend Identification (HTF)
bool htfUptrend = htfClose > htfClose[1] and htfLow > htfLow[1]  // Price action
bool htfDowntrend = htfClose < htfClose[1] and htfHigh < htfHigh[1]

// Inducement Identification (HTF)
bool htfInducementHigh = htfUptrend and high[1] > high[2] and high[1] > high[3] 
bool htfInducementLow = htfDowntrend and low[1] < low[2] and low[1] < low[3]
float inducementLevel = htfInducementHigh ? high[1] : htfInducementLow ? low[1] : na

// Order Block Identification (HTF)
var float htfOBHigh = na // Highest high within the order block
var float htfOBLow = na  // Lowest low within the order block

if htfInducementHigh
    htfOBHigh := htfHigh
    htfOBLow := htfLow
else if htfInducementLow
    htfOBHigh := htfHigh
    htfOBLow := htfLow

// Optimal Entry (Current Timeframe)
bool longEntry = htfUptrend and close > htfOBLow and close[1] < htfOBLow  // Break of OB low
bool shortEntry = htfDowntrend and close < htfOBHigh and close[1] > htfOBHigh  // Break of OB high

// Stop Loss and Take Profit
float longSL = htfOBLow
float longTP = close + (close - longSL) * riskRewardRatio
float shortSL = htfOBHigh
float shortTP = close - (shortSL - close) * riskRewardRatio

// Strategy Execution
if longEntry
    strategy.entry("Long", strategy.long, stop=longSL, limit=longTP)
else if shortEntry
    strategy.entry("Short", strategy.short, stop=shortSL, limit=shortTP)

```

> Detail

https://www.fmz.com/strategy/452277

> Last Modified

2024-05-23 18:04:59

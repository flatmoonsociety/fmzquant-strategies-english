
> Name

Triple-Supertrend-and-Bollinger-Bands-Multi-Indicator-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/bb85840aed8f14d50e.png)

[trans]
#### Overview
This strategy uses a combination of Bollinger Bands and Triple Supertrend indicators for trading. Through the judgment of the Bollinger Bands' fluctuation range and the trend confirmation of the triple super trend, a robust trend tracking system is formed. Bollinger Bands are used to identify extreme price movements, while Triple Supertrends provide multiple confirmations of trend direction with different parameter settings. Only trade when all signals are consistent to reduce the risk of false signals. This combination method not only retains the advantages of trend following, but also increases the reliability of trading.
#### Strategy Principle
The core logic of the strategy includes the following key parts:
1. Use 20-period Bollinger Bands with a standard deviation multiple of 2.0 to determine price fluctuations
2. Set three super trend lines, with periods of 10 and parameters of 3.0, 4.0 and 5.0 respectively.
3. Bull entry conditions: the price breaks through the Bollinger Band upper limit and the three super-trend lines all show an upward trend.
4. Short entry conditions: the price falls below the lower Bollinger Band and the three super-trend lines all show a downward trend.
5. When any super trend line changes direction, close the current position
6. Use the middle price line as a filling reference to enhance the visual effect
#### Strategic Advantages
1. Multiple confirmation mechanism: Through the combination of Bollinger Bands and triple super trends, false signals are greatly reduced
2. Strong trend tracking ability: The progressive parameter setting of the super-trend indicator can effectively capture trends at different levels.
3. Perfect risk control: quickly close positions when the trend shows signs of turning and control drawdowns
4. Strong parameter adjustability: various indicator parameters can be optimized according to different market characteristics
5. High degree of automation: the strategy logic is clear and easy to implement systematically
#### Strategy Risk
1. Risk of volatile market: False breakthrough signals may frequently occur in a volatile market.
2. Impact of slippage: During periods of severe fluctuations, you may face larger slippage losses.
3. Delay risk: Multiple confirmation mechanism may lead to late entry timing
4. Parameter sensitivity: Different parameter combinations may lead to large differences in strategy performance
5. Market environment dependence: Strategies perform better in markets with obvious trends
#### Strategy optimization direction
1. Introduce trading volume indicators: confirm the effectiveness of price breakthroughs through trading volume
2. Optimize the stop loss mechanism: you can add a trailing stop or a dynamic stop based on ATR
3. Add time filtering: prohibit transactions during specific time periods to avoid inefficient fluctuations
4. Add volatility filtering: adjust positions or suspend trading during periods of excessive volatility
5. Develop parameter adaptive mechanism: dynamically adjust parameters according to market conditions
#### Summary
This is a trend following strategy that combines Bollinger Bands and triple supertrends to improve the reliability of trading through the confirmation of multiple technical indicators. The strategy has strong trend capturing and risk control capabilities, but it is also necessary to pay attention to the impact of the market environment on strategy performance. Through continuous optimization and improvement, the strategy is expected to maintain stable performance under different market conditions. It is recommended to conduct sufficient backtesting and parameter optimization before real trading, and make appropriate adjustments based on the actual market conditions. ||
#### Overview
This strategy combines Bollinger Bands with Triple Supertrend indicators for trading. It creates a robust trend-following system by utilizing Bollinger Bands for volatility range assessment and Triple Supertrend for trend confirmation. The Bollinger Bands identify extreme price movements, while the Triple Supertrend provides multiple confirmations of trend direction through different parameter settings. Trades are executed only when all signals align, reducing the risk of false signals. This combination maintains the advantages of trend following while enhancing trading reliability.

#### Strategy Principles
The core logic includes the following key components:
1. Uses 20-period Bollinger Bands with 2.0 standard deviation multiplier for volatility judgment
2. Implements three Supertrend lines with period 10 and factors 3.0, 4.0, and 5.0
3. Long entry conditions: price breaks above upper Bollinger Band and all three Supertrend lines show uptrend
4. Short entry conditions: price breaks below lower Bollinger Band and all three Supertrend lines show downtrend
5. Positions are closed when any Supertrend line changes direction
6. Uses middle price line as fill reference for enhanced visualization

#### Strategy Advantages
1. Multiple confirmation mechanism: Combination of Bollinger Bands and Triple Supertrend significantly reduces false signals
2. Strong trend-following capability: Progressive Supertrend parameters effectively capture trends at different levels
3. Comprehensive risk control: Quick position closure when trend reversal signs appear
4. High parameter adaptability: All indicator parameters can be optimized for different market characteristics
5. High automation level: Clear strategy logic facilitates systematic implementation

#### Strategy Risks
1. Choppy market risk: May generate frequent false breakout signals in sideways markets
2. Slippage impact: May face significant slippage losses during volatile periods
3. Delay risk: Multiple confirmation mechanism may lead to delayed entries
4. Parameter sensitivity: Different parameter combinations may result in varying strategy performance
5. Market environment dependence: Strategy performs better in trending markets

#### Strategy Optimization Directions
1. Incorporate volume indicators: Confirm price breakout validity through volume analysis
2. Optimize stop-loss mechanism: Add trailing stops or ATR-based dynamic stops
3. Add time filters: Restrict trading during specific periods to avoid inefficient volatility
4. Implement volatility filters: Adjust position sizes or pause trading during excessive volatility
5. Develop parameter adaptation mechanism: Dynamically adjust parameters based on market conditions

#### Summary
This is a trend-following strategy combining Bollinger Bands and Triple Supertrend, enhancing trading reliability through multiple technical indicator confirmations. The strategy demonstrates strong trend capture capability and risk control, but market conditions significantly impact its performance. Through continuous optimization and refinement, the strategy can maintain stable performance across different market conditions. It is recommended to conduct thorough backtesting and parameter optimization before live trading, and make appropriate adjustments based on actual market conditions.[/trans]



> Source (PineScript)

``` pinescript
//@version=5
strategy("Demo GPT - Bollinger + Triple Supertrend Combo", overlay=true, commission_type=strategy.commission.percent, commission_value=0.1, slippage=3)

// -------------------------------
// User Input for Date Range
// -------------------------------
startDate = input(title="Start Date", defval=timestamp("2018-01-01 00:00:00"))
endDate   = input(title="End Date",   defval=timestamp("2069-12-31 23:59:59"))

// -------------------------------
// Bollinger Band Inputs
// -------------------------------
lengthBB = input.int(20, "Bollinger Length")
multBB   = input.float(2.0, "Bollinger Multiplier")

// -------------------------------
// Supertrend Inputs for 3 lines
// -------------------------------
// Line 1
atrPeriod1 = input.int(10, "ATR Length (Line 1)", minval = 1)
factor1    = input.float(3.0, "Factor (Line 1)", minval = 0.01, step = 0.01)

// Line 2
atrPeriod2 = input.int(10, "ATR Length (Line 2)", minval = 1)
factor2    = input.float(4.0, "Factor (Line 2)", minval = 0.01, step = 0.01)

// Line 3
atrPeriod3 = input.int(10, "ATR Length (Line 3)", minval = 1)
factor3    = input.float(5.0, "Factor (Line 3)", minval = 0.01, step = 0.01)

// -------------------------------
// Bollinger Band Calculation
// -------------------------------
basis = ta.sma(close, lengthBB)
dev   = multBB * ta.stdev(close, lengthBB)
upperBand = basis + dev
lowerBand = basis - dev

// Plot Bollinger Bands
plot(upperBand, "Upper BB", color=color.new(color.blue, 0))
plot(basis,     "Basis",    color=color.new(color.gray, 0))
plot(lowerBand, "Lower BB", color=color.new(color.blue, 0))

// -------------------------------
// Supertrend Calculation Line 1
// -------------------------------
[supertrendLine1, direction1] = ta.supertrend(factor1, atrPeriod1)
supertrendLine1 := barstate.isfirst ? na : supertrendLine1

upTrend1   = plot(direction1 < 0 ? supertrendLine1 : na, "Up Trend 1",   color = color.green, style = plot.style_linebr)
downTrend1 = plot(direction1 < 0 ? na : supertrendLine1, "Down Trend 1", color = color.red,   style = plot.style_linebr)

// -------------------------------
// Supertrend Calculation Line 2
// -------------------------------
[supertrendLine2, direction2] = ta.supertrend(factor2, atrPeriod2)
supertrendLine2 := barstate.isfirst ? na : supertrendLine2

upTrend2   = plot(direction2 < 0 ? supertrendLine2 : na, "Up Trend 2",   color = color.new(color.green, 0), style = plot.style_linebr)
downTrend2 = plot(direction2 < 0 ? na : supertrendLine2, "Down Trend 2", color = color.new(color.red, 0),   style = plot.style_linebr)

// -------------------------------
// Supertrend Calculation Line 3
// -------------------------------
[supertrendLine3, direction3] = ta.supertrend(factor3, atrPeriod3)
supertrendLine3 := barstate.isfirst ? na : supertrendLine3

upTrend3   = plot(direction3 < 0 ? supertrendLine3 : na, "Up Trend 3",   color = color.new(color.green, 0), style = plot.style_linebr)
downTrend3 = plot(direction3 < 0 ? na : supertrendLine3, "Down Trend 3", color = color.new(color.red, 0),   style = plot.style_linebr)

// -------------------------------
// Middle line for fill (used as a reference line)
// -------------------------------
bodyMiddle = plot(barstate.isfirst ? na : (open + close) / 2, "Body Middle", display = display.none)

// Fill areas for each supertrend line
fill(bodyMiddle, upTrend1,   color.new(color.green, 90), fillgaps = false)
fill(bodyMiddle, downTrend1, color.new(color.red,   90), fillgaps = false)

fill(bodyMiddle, upTrend2,   color.new(color.green, 90), fillgaps = false)
fill(bodyMiddle, downTrend2, color.new(color.red,   90), fillgaps = false)

fill(bodyMiddle, upTrend3,   color.new(color.green, 90), fillgaps = false)
fill(bodyMiddle, downTrend3, color.new(color.red,   90), fillgaps = false)

// Alerts for the first line only (as an example)
alertcondition(direction1[1] > direction1, title='Downtrend to Uptrend (Line 1)', message='Supertrend Line 1 switched from Downtrend to Uptrend')
alertcondition(direction1[1] < direction1, title='Uptrend to Downtrend (Line 1)', message='Supertrend Line 1 switched from Uptrend to Downtrend')
alertcondition(direction1[1] != direction1, title='Trend Change (Line 1)', message='Supertrend Line 1 switched trend')

// -------------------------------
// Strategy Logic
// -------------------------------
inDateRange = true

// Long Conditions
longEntryCondition = inDateRange and close > upperBand and direction1 < 0 and direction2 < 0 and direction3 < 0
longExitCondition = direction1 > 0 or direction2 > 0 or direction3 > 0

// Short Conditions
shortEntryCondition = inDateRange and close < lowerBand and direction1 > 0 and direction2 > 0 and direction3 > 0
shortExitCondition = direction1 < 0 or direction2 < 0 or direction3 < 0

// Execute Long Trades
if longEntryCondition and strategy.position_size <= 0
    strategy.entry("Long", strategy.long)

if strategy.position_size > 0 and longExitCondition
    strategy.close("Long")

// Execute Short Trades
if shortEntryCondition and strategy.position_size >= 0
    strategy.entry("Short", strategy.short)

if strategy.position_size < 0 and shortExitCondition
    strategy.close("Short")

```

> Detail

https://www.fmz.com/strategy/475596

> Last Modified

2024-12-20 14:28:58

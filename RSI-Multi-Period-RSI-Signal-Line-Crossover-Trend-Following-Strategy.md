
> Name

Multi-Period-RSI-Signal-Line-Crossover-Trend-Following-Strategy based on RSI signal line crossover
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/52ebafa7c070d9ffb1e35077ce5f28494867a69beb67877ffdd54873e6b3ad0d.png)

[trans]
#### Overview
This strategy is a trend following trading system based on the enhanced Relative Strength Index (RSI). It captures trend reversal opportunities in different market cycles by calculating a modified version of RSI and combining it with its signal lines. This strategy not only calculates the indicator value, but also visually displays the overbought and oversold areas to help traders judge the market status more intuitively.
#### Strategy Principle
The core principle of the strategy is to identify market trends through the calculation of the Enhanced RSI (ARSI). Specifically include:
1. Calculate the highest price and lowest price within the specified period to obtain the price range
2. Calculate the difference based on price changes
3. Smooth the differences using optional moving average methods (EMA, SMA, RMA, TMA)
4. Standardize the results to a range of 0-100
5. A long signal is generated when ARSI crosses the signal line below 50
6. A short signal is generated when ARSI falls below the signal line above 50
#### Strategic Advantages
1. Complete signal confirmation mechanism - ensuring signal reliability through the intersection of ARSI and signal lines and central axis filtering
2. Strong adaptability - supports multiple moving average methods and can be adjusted according to different market characteristics
3. Reasonable risk control - adopt position percentage management method to effectively control the risk of each transaction
4. Outstanding visualization effect - overbought and oversold areas are clearly displayed through color filling to facilitate quick judgment.
5. Reverse position management - existing positions will be automatically closed when a reverse signal occurs to avoid the risk of two-way positions.
#### Strategy Risk
1. Volatile market risk - Frequent false signals may occur in sideways and volatile markets.
2. Lagging risk - Due to the use of moving average calculations, the signal will have a certain lag.
3. Parameter sensitivity - different parameter settings may lead to large differences in strategy performance
4. Market adaptability risk - the performance of strategies may differ significantly in different market environments
5. Fund management risk - fixed percentage position management may bring greater risks during severe fluctuations
#### Strategy optimization direction
1. Introduce volatility filtering - ATR indicator can be added to filter trading signals in low volatility environment
2. Add trend confirmation indicators - combine with longer period trend indicators to improve signal reliability
3. Optimize position management - dynamically adjust position proportions based on market volatility
4. Add a stop loss mechanism - set a dynamic stop loss based on ATR to better control risks
5. Develop adaptive parameters - study dynamic optimization methods of parameters to improve strategy adaptability
#### Summary
This is a trend following strategy with complete structure and clear logic. Through the innovative calculation method of enhanced RSI, combined with the advantages of multiple technical indicators, a reliable trading system is formed. Although there are some inherent risks, through reasonable optimization and risk management measures, this strategy has good practical application prospects. It is recommended that traders need to fully test the parameter settings when using it in real trading, and adjust the strategy configuration in a timely manner based on the market environment.
|| 

#### Overview
This strategy is a trend-following trading system based on an enhanced Relative Strength Index (RSI). It captures trend reversal opportunities across different market cycles by calculating an improved version of RSI and combining it with its signal line. The strategy not only computes indicator values but also provides visual representation of overbought and oversold areas to help traders make more intuitive market judgments.

#### Strategy Principles
The core principle revolves around identifying market trends through an Augmented RSI (ARSI) calculation, including:
1. Calculating highest and lowest prices within a specified period to determine price range
2. Computing differences based on price changes
3. Smoothing the differences using selectable moving average methods (EMA, SMA, RMA, TMA)
4. Normalizing results to a 0-100 range
5. Generating long signals when ARSI crosses above its signal line below 50
6. Generating short signals when ARSI crosses below its signal line above 50

#### Strategy Advantages
1. Robust Signal Confirmation - Ensures reliability through ARSI crossovers and midline filtering
2. High Adaptability - Supports multiple moving average methods for different market characteristics
3. Reasonable Risk Control - Employs position percentage management for effective risk control
4. Outstanding Visualization - Clearly displays overbought/oversold areas through color filling
5. Reverse Position Management - Automatically closes existing positions on contrary signals

#### Strategy Risks
1. Oscillation Market Risk - May generate frequent false signals in sideways markets
2. Lag Risk - Signals have inherent lag due to moving average calculations
3. Parameter Sensitivity - Different parameter settings may lead to significant performance variations
4. Market Adaptability Risk - Strategy performance may vary significantly across different market environments
5. Money Management Risk - Fixed percentage position sizing may pose risks during high volatility

#### Optimization Directions
1. Volatility Filtering - Add ATR indicator to filter signals in low volatility environments
2. Additional Trend Confirmation - Incorporate longer-period trend indicators to improve signal reliability
3. Position Management Optimization - Dynamically adjust position sizes based on market volatility
4. Stop Loss Implementation - Develop ATR-based dynamic stop-loss for better risk control
5. Adaptive Parameters - Research dynamic parameter optimization methods to improve adaptability

#### Summary
This is a well-structured trend-following strategy with clear logic. Through innovative ARSI calculation methods and the combination of various technical indicators' advantages, it forms a reliable trading system. While inherent risks exist, the strategy shows good practical application potential through reasonable optimization and risk management measures. Traders are advised to thoroughly test parameter settings and adjust strategy configuration according to market conditions when implementing in live trading.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-19 00:00:00
end: 2025-02-16 08:00:00
period: 4h
basePeriod: 4h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("Ultimate RSI [LuxAlgo] Strategy", shorttitle="ULT RSI Strat", overlay=false, initial_capital=10000, currency=currency.USD, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

//------------------------------------------------------------------------------
// Settings
//------------------------------------------------------------------------------
length    = input.int(14, minval=2, title="RSI Length")
smoType1  = input.string("RMA", title="Method", options=["EMA", "SMA", "RMA", "TMA"])
src       = input(close, title="Source")

arsiCss   = input.color(color.silver, "RSI Color", inline="rsicss")
autoCss   = input.bool(true, "Auto", inline="rsicss")

// Signal Line settings
smooth    = input.int(14, minval=1, title="Signal Smooth", group="Signal Line")
smoType2  = input.string("EMA", title="Method", options=["EMA", "SMA", "RMA", "TMA"], group="Signal Line")
signalCss = input.color(color.new(#ff5d00, 0), "Signal Color", group="Signal Line")

// Overbought/Oversold style
obValue     = input.float(80, "Overbought", inline="ob", group="OB/OS Style")
obCss       = input.color(color.new(#089981, 0), "", inline="ob", group="OB/OS Style")
obAreaCss   = input.color(color.new(#089981, 80), "", inline="ob", group="OB/OS Style")

osValue     = input.float(20, "Oversold", inline="os", group="OB/OS Style")
osCss       = input.color(color.new(#f23645, 0), "", inline="os", group="OB/OS Style")
osAreaCss   = input.color(color.new(#f23645, 80), "", inline="os", group="OB/OS Style")

//------------------------------------------------------------------------------
// Function: Moving Average (selectable type)
//------------------------------------------------------------------------------
ma(x, len, maType)=>
    switch maType
        "EMA" => ta.ema(x, len)
        "SMA" => ta.sma(x, len)
        "RMA" => ta.rma(x, len)
        "TMA" => ta.sma(ta.sma(x, len), len)
 
//------------------------------------------------------------------------------
// Augmented RSI Calculation
//------------------------------------------------------------------------------
upper = ta.highest(src, length)
lower = ta.lowest(src, length)
r     = upper - lower

d     = src - src[1]
diff  = upper > upper[1] ? r : lower < lower[1] ? -r : d

num   = ma(diff, length, smoType1)
den   = ma(math.abs(diff), length, smoType1)
arsi  = den != 0 ? num / den * 50 + 50 : 50  // safeguard against division by zero

signal = ma(arsi, smooth, smoType2)

//------------------------------------------------------------------------------
// Strategy Entry Conditions
//------------------------------------------------------------------------------
// Long entry: Ultimate RSI crosses above its signal when it is below 50 (lower half)
// Short entry: Ultimate RSI crosses below its signal when it is above 50 (upper half)
longCondition  = ta.crossover(arsi, signal) and arsi < 50
shortCondition = ta.crossunder(arsi, signal) and arsi > 50

// Close opposite positions when conditions occur
if shortCondition
    strategy.close("Long")
if longCondition
    strategy.close("Short")

// Place new entries based on the conditions
if longCondition
    strategy.entry("Long", strategy.long)
if shortCondition
    strategy.entry("Short", strategy.short)

// //------------------------------------------------------------------------------
// // Plots and Constant Lines
// //------------------------------------------------------------------------------
// // Plot the Ultimate RSI and its Signal
// plot_rsi = plot(arsi, title="Ultimate RSI",
//      color = arsi > obValue ? obCss : arsi < osValue ? osCss : autoCss ? chart.fg_color : arsiCss,
//      linewidth=2)
// plot(signal, title="Signal Line", color=signalCss, linewidth=2)

// // Instead of using hline, create constant plots for OB, Midline, and OS
// plot_ob  = plot(obValue, title="Overbought", color=obCss, style=plot.style_line, linewidth=1)
// plot_mid = plot(50, title="Midline", color=color.gray, style=plot.style_line, linewidth=1)
// plot_os  = plot(osValue, title="Oversold", color=osCss, style=plot.style_line, linewidth=1)

// //------------------------------------------------------------------------------
// // Fill OB/OS Areas for Visual Clarity
// //------------------------------------------------------------------------------
// fill(plot_rsi, plot_ob, color=arsi > obValue ? obAreaCss : na)
// fill(plot_os, plot_rsi, color=arsi < osValue ? osAreaCss : na)

```

> Detail

https://www.fmz.com/strategy/482453

> Last Modified

2025-02-18 15:04:49

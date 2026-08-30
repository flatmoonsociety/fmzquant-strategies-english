
> Name

Improved-Ichimoku-Cloud-Trading-Strategy-with-Dynamic-Crossover-Signals
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d895a5f44f778d51a43a.png)
![IMG](https://www.fmz.com/upload/asset/2d8441b437b6d93ecf473.png)




[trans]
#### Overview
This strategy is based on an improved version of the classic Ichimoku Kinko Hyo system, which identifies trading signals through the dynamic crossing of the conversion line and the baseline. Based on the traditional market cloud system, the strategy adds the generation and execution logic of automatic trading signals, and cooperates with visual labels to improve the readability of market trends.
#### Strategy Principle
The core of the strategy is based on the five main curves of the city cloud system: conversion line (9 periods), baseline (26 periods), leading line A, leading line B (52 periods) and lag line. One of the most critical trading signals comes from the intersection of the conversion line and the base line. When the conversion line crosses the baseline, a long signal is generated, and when it crosses below, the position is closed. The strategy uses dynamic Donchian channels to calculate each line, reflecting price fluctuations by taking the average of the highest and lowest prices.
#### Strategic Advantages
1. Systematic trend tracking - through a combination of indicators in multiple time frames, market trends can be comprehensively captured.
2. Visually intuitive - using color labels and cloud display, trading signals are clearly visible.
3. Risk management integration - has a built-in stop-loss mechanism that automatically closes positions when the market reverses.
4. Strong adaptability - parameters are adjustable and can adapt to different market environments.
5. Signal stability - Use moving average crossovers to filter out false signals and improve trading quality.
#### Strategy Risk
1. Trend reversal delay - Due to the use of moving averages, there is a certain lag.
2. Not applicable to volatile markets - false signals may be generated during sideways trading phases.
3. Parameter sensitivity - Different parameter settings will significantly affect strategy performance.
4. Cloud pattern complexity - The interweaving of multiple lines can make signal interpretation difficult.
#### Strategy optimization direction
1. Introducing volatility filtering - ATR indicator can be added to adjust position size.
2. Optimize entry timing - Use momentum indicators such as RSI to confirm trading signals.
3. Improve the stop loss mechanism - you can set a dynamic stop loss based on the cloud chart support level.
4. Added transaction volume confirmation - check the transaction volume when the signal is generated to improve reliability.
5. Add market environment filtering - select the appropriate trading environment through the trend strength indicator.
#### Summary
This strategy builds a complete trend tracking trading system by improving the traditional market cloud system. Although there is a certain lag, through optimization of signal filtering and risk management, stable performance can be achieved in trending markets. It is recommended that traders adjust parameters based on the market environment and personal risk preferences when using real trading, and continue to monitor the performance of the strategy. ||
#### Overview
This strategy is an enhanced version of the classic Ichimoku Kinko Hyo system, utilizing dynamic crossovers between the Conversion and Base lines to identify trading signals. It incorporates automated trading signal generation and execution logic, along with visual labels to improve trend readability.

#### Strategy Principles
The strategy is built upon the five main lines of the Ichimoku system: Conversion Line (9 periods), Base Line (26 periods), Leading Span A, Leading Span B (52 periods), and Lagging Span. The primary trading signals are generated from crossovers between the Conversion and Base lines. Long positions are entered when the Conversion Line crosses above the Base Line and closed when it crosses below. The strategy employs dynamic Donchian channels to calculate each line by averaging the highest and lowest prices to reflect price volatility.

#### Strategy Advantages
1. Systematic Trend Following - Combines multiple timeframe indicators for comprehensive trend capture.
2. Visual Clarity - Utilizes color labels and cloud visualization for clear signal identification.
3. Integrated Risk Management - Features built-in stop-loss mechanisms for automatic position closure on market reversals.
4. High Adaptability - Adjustable parameters allow adaptation to different market conditions.
5. Signal Stability - Uses moving average crossovers to filter false signals and improve trade quality.

#### Strategy Risks
1. Trend Reversal Delay - Inherent lag due to moving average calculations.
2. Poor Performance in Ranging Markets - May generate false signals during consolidation phases.
3. Parameter Sensitivity - Strategy performance significantly affected by parameter settings.
4. Cloud Complexity - Multiple intersecting lines may complicate signal interpretation.

#### Optimization Directions
1. Volatility Filtering - Incorporate ATR indicator for position sizing adjustment.
2. Entry Timing Enhancement - Integrate momentum indicators like RSI for signal confirmation.
3. Stop-Loss Refinement - Implement dynamic stop-loss based on cloud support levels.
4. Volume Confirmation - Add volume analysis for signal validation.
5. Market Environment Filtering - Include trend strength indicators for market condition selection.

#### Summary
This strategy enhances the traditional Ichimoku system to create a comprehensive trend-following trading system. While it exhibits some lag, optimization through signal filtering and risk management enables stable performance in trending markets. Traders should adjust parameters based on market conditions and risk preferences while continuously monitoring strategy performance.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-22 00:00:00
end: 2024-12-16 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=6

strategy(title="Ichimoku Cloud with Lables", shorttitle="Ichimoku", overlay=true)
conversionPeriods = input.int(9, minval=1, title="Conversion Line Length")
basePeriods = input.int(26, minval=1, title="Base Line Length")
laggingSpan2Periods = input.int(52, minval=1, title="Leading Span B Length")
displacement = input.int(26, minval=1, title="Lagging Span")
donchian(len) => math.avg(ta.lowest(len), ta.highest(len))
conversionLine = donchian(conversionPeriods)
baseLine = donchian(basePeriods)
leadLine1 = math.avg(conversionLine, baseLine)
leadLine2 = donchian(laggingSpan2Periods)
plot(conversionLine, color=#2962FF, title="Conversion Line")
plot(baseLine, color=#B71C1C, title="Base Line")





plot(close, offset = -displacement + 1, color=#43A047, title="Lagging Span", display = display.none)
p1 = plot(leadLine1, offset = displacement - 1, color=#A5D6A7,
	 title="Leading Span A")
p2 = plot(leadLine2, offset = displacement - 1, color=#EF9A9A,
	 title="Leading Span B")
plot(leadLine1 > leadLine2 ? leadLine1 : leadLine2, offset = displacement - 1, title = "Kumo Cloud Upper Line", display = display.none) 
plot(leadLine1 < leadLine2 ? leadLine1 : leadLine2, offset = displacement - 1, title = "Kumo Cloud Lower Line", display = display.none) 
fill(p1, p2, color = leadLine1 > leadLine2 ? color.rgb(67, 160, 71, 90) : color.rgb(244, 67, 54, 90))

if barstate.islast
    label.new(bar_index+5,baseLine,style=label.style_none,xloc=xloc.bar_index,text="Base",color=color.white,textcolor=#B71C1C)
    label.new(bar_index +8, conversionLine,style=label.style_none,xloc=xloc.bar_index,text="Conversion",color=color.white,textcolor=#2962FF)
	label.new(bar_index+(displacement-1)+5,leadLine1,style=label.style_none,xloc=xloc.bar_index,text="Lead1",color=color.white,textcolor=#A5D6A7)
	label.new(bar_index+(displacement-1)+5,leadLine2,style=label.style_none,xloc=xloc.bar_index,text="Lead2",color=color.white,textcolor=#EF9A9A)

// --- TRADING LOGIC ---

// 1) Detect bullish cross (Conversion crosses above Base)
longSignal = ta.crossover(conversionLine, baseLine)

// 2) Detect bearish cross (Conversion crosses below Base)
closeSignal = ta.crossunder(conversionLine, baseLine)

// 3) If bullish cross occurs, open a new long
if longSignal
    strategy.entry("LongTK", strategy.long)

// 4) If bearish cross occurs, close the open long
if closeSignal
    // Closes all orders opened with the ID "LongTK"
    strategy.close("LongTK")

```

> Detail

https://www.fmz.com/strategy/483042

> Last Modified

2025-02-21 10:41:00

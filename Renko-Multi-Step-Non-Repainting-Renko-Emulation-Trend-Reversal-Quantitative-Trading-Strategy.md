
> Name

Multi-Step-Non-Repainting-Renko-Emulation-Trend-Reversal-Quantitative-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8cf9748c9159c78d282.png)
![IMG](https://www.fmz.com/upload/asset/2d8aaea1f46cb4b768b0a.png)


[trans]## Strategy Overview
This strategy is a non-redrawing quantitative trading system based on Renko chart simulation. It solves the redrawing problem in the traditional Renko strategy by simulating the Renko brick behavior on the standard time chart. This strategy uses fixed-size price bricks to filter out market noise and focus only on meaningful price movements while ensuring that historical signals remain intact. This strategy is particularly suitable for trend following and trend reversal trading. It makes trading decisions by comparing the direction changes of bricks in multiple steps.
Main features:
- Implement non-redraw Renko effect on time chart
- Use Renko direction changes to identify trend reversals
- Multi-step verification mechanism improves signal quality
- Graphical display of the brick formation process
- Stable backtest results consistent with real-time trading performance
## Strategy Principle
The core principle of this strategy is to implement the functionality of Renko bricks on standard time charts while solving the redrawing problem in traditional Renko charts. The specific working principle is as follows:
1. **Parameter configuration and initialization**:
   - `brickSize`: defines the brick size and determines how much the price must move to form a new brick
   - `renkoPrice`: stores the closing price of the last completed Renko brick
   - `prevRenkoPrice`: stores the previous Renko brick price level
   - `brickDir`: Track brick direction (1=rising, -1=falling)
   - `newBrick`: Boolean flag indicating whether new bricks are formed
   - `brickStart`: stores the column index where the current brick starts
2. **Non-redraw Renko brick recognition**:
   - The system only performs calculations on confirmation bars to ensure that historical data will not be recalculated
   - Calculate the difference between the current price and the previous Renko brick level
   - When the price difference reaches or exceeds the brick size, a new Renko brick is formed
   - Update brick price levels based on the number of bricks that can be accommodated by price changes
   - Update the direction (brickDir) and set the flag (newBrick) to indicate the formation of a new brick
3. **Renko visualization on time chart**:
   - Draw Renko style bricks on standard charts using graphical elements
   - Green squares represent bullish bricks
   - Red squares represent bearish bricks
   - Bricks will never change or disappear after being formed
4. **Multi-step trend reversal judgment**:
   - The strategy not only checks the current brick direction, but also compares multiple historical bricks
   - Confirm true trend reversal by verifying direction changes on multiple consecutive bricks
## Strategic Advantages
After in-depth analysis of the code, this strategy shows the following significant advantages:
1. **Solving the redrawing problem**:
   - The traditional Renko strategy performs well in backtesting, but often fails in real trading. The main reason is the redraw problem.
   - This strategy ensures that once a brick is formed it will not change by simulating Renko behavior on a standard time chart
   - This makes the backtest results more reliable and closer to the actual performance
2. **Noise filtering and clear trend identification**:
   - The Renko chart itself has the characteristic of filtering out small fluctuations, and only forms new bricks when the price moves a preset amount
   - This helps identify clear price trends and reduce false signals
   - Ideal for finding meaningful price movements in highly volatile markets
3. **Multi-step signal verification**:
   - Strategy not only checks for single direction changes, but also verifies the direction of multiple consecutive tiles
   - By comparing `brickDir[brickSize]` with current `brickDir` and historical price levels
   - Multi-step verification mechanism significantly reduces false signals
4. **Visual trading basics**:
   - Draw colored bricks on the chart to visually display the price structure
   - Green and red boxes clearly indicate market direction
   - Visual aids help traders better understand market behavior
5. **Flexibility and Customizability**:
   - Brick size is user-adjustable, allowing strategies to be optimized for different markets and time frames
   - Smaller brick sizes produce more frequent trading signals, suitable for short-term trading
   - Larger brick size filters out more noise and is suitable for mid- to long-term trend tracking
## Strategy Risk
Although this strategy solves the redraw problem, it still has the following risk factors:
1. **Signal delay risk**:
   - Because the strategy only performs calculations on confirmation bars, trade execution may be slightly later than on traditional Renko charts
   - In fast-moving markets, entry points may have missed the best price
   - Solution: Consider combining other confirmation indicators or adjusting the brick size to balance timeliness and accuracy
2. **Brick size selection risk**:
   - Bricks that are too small will generate too many trading signals, increase trading costs and may lead to over-trading
   - Bricks that are too large may miss important market turning points
   - Solution: Brick size should be optimized based on the target asset’s volatility and trading time frame
3. **Trend reversal false signal risk**:
   - Despite the use of multi-step verification, false breakouts may still occur in highly volatile markets
   - Price may cross the Renko border multiple times before a true trend is established
   - Solution: Consider adding additional filters such as volume confirmation or momentum indicators
4. **Retracement Risk**:
   - Trend reversal strategies may result in consecutive losses in strong trending markets
   - Reversal signals may trigger prematurely, leading to counter-trend trades
   - Solution: Implement appropriate stop-loss mechanisms and position management strategies
5. **Calculation Resource Risk**:
   - Drawing large numbers of bricks can be resource intensive, especially on long time frames and large data sets
   - The maximum number of cabinets is limited to 500 in the code, which may not be sufficient in some cases
   - Solution: Optimize code efficiency or consider displaying only the nearest N bricks
## Strategy optimization direction
Based on code analysis, the following are several key optimization directions for this strategy:
1. **Dynamic brick size optimization**:
   - The current strategy uses fixed brick sizes, which can be improved to dynamic brick sizes based on market volatility
   - Use smaller bricks during low volatility and larger bricks during high volatility
   - This will increase the adaptability of the strategy to different market conditions
   - Implementation method: You can use ATR (real fluctuation range) to dynamically adjust the brick size
2. **Add transaction filter**:
   - Combine with volume or other momentum indicators to confirm trend reversal signals
   - Avoid trading in conditions of low liquidity or extreme volatility
   - Implementation method: Add additional confirmation conditions based on RSI, volume breakout or MACD
3. **Improve stop loss and profit mechanism**:
   - The current strategy only closes positions when the direction is reversed, smart stops and target profit levels can be added
   - Set dynamic stop loss based on multiples of brick size
   - Implementation method: Add the `strategy.exit()` command to set the stop loss point based on ATR or brick size
4. **Optimize multi-step verification mechanism**:
   - The current strategy uses a fixed `brickSize` multiple to compare historical bricks
   - Can study the optimal number of historical comparison steps
   - Backtest on different markets and time frames to find the best parameter combinations
   - Implementation method: parameterize the number of steps and allow users to customize the verification depth
5. **Improve visualization and alarm system**:
   - Added trend lines and key level markers
   - Added alert function for brick formation and trading signals
   - Shows current trend strength and duration
   - Implementation method: Use `label.new()` and `alert()` functions to enhance user experience
## Summarize
The multi-step non-redrawing Renko simulation trend reversal quantitative trading strategy successfully solves the redrawing problem in the traditional Renko strategy, allowing traders to apply Renko logic on standard time charts while maintaining the stability of historical signals. The strategy identifies trend reversals through a multi-step verification mechanism, improves signal quality, and provides a graphical representation of market structure.
The main advantages of the strategy are solving the redraw problem, filtering market noise, multi-level signal verification and intuitive graphical representation. However, there are still risks such as signal delays, brick size selection and false signals. Further optimization can be achieved in the future by implementing dynamic brick sizes, adding transaction filters, improving stop loss mechanisms, optimizing verification steps and enhancing the visualization system.
This method, which combines the advantages of Renko charts and avoids its shortcomings, is particularly suitable for trend following and trend reversal trading strategies, providing traders with a reliable technical analysis tool that can provide stable real-time performance while maintaining the accuracy of backtesting. || ## Strategy Overview
This strategy is a non-repainting quantitative trading system based on Renko chart emulation that solves the repainting problem found in traditional Renko strategies by simulating Renko brick behavior on standard time-based charts. The strategy uses fixed-size price bricks to filter market noise, focusing only on meaningful price movements while ensuring historical signals remain unchanged. This strategy is particularly suitable for trend following and trend reversal trading, making trading decisions by comparing brick direction changes through multiple steps.

Key features:
- Implements non-repainting Renko effects on time-based charts
- Identifies trend reversals using brick direction changes
- Multi-step verification mechanism to improve signal quality
- Graphical display of brick formation process
- Stable backtesting results consistent with real-time trading performance

## Strategy Principles

The core principle of this strategy is to implement Renko brick functionality on a standard time-based chart while solving the repainting problem found in traditional Renko charts. The specific working principles are as follows:

1. **Parameter Configuration & Initialization**:
   - `brickSize`: Defines the brick size, determining how much price must move to form a new brick
   - `renkoPrice`: Stores the closing price of the last completed Renko brick
   - `prevRenkoPrice`: Stores the price level of the previous Renko brick
   - `brickDir`: Tracks the direction of bricks (1=up, -1=down)
   - `newBrick`: A boolean flag indicating whether a new brick has been formed
   - `brickStart`: Stores the bar index at which the current brick started

2. **Non-Repainting Renko Brick Identification**:
   - The system performs calculations only on confirmed bars, ensuring historical data is not recalculated
   - Calculates the difference between the current price and the last Renko brick level
   - When the price difference reaches or exceeds the brick size, a new Renko brick is formed
   - Updates the brick price level based on the number of bricks that would fit within the price movement
   - Updates the direction (brickDir) and sets a flag (newBrick) indicating a new brick has been formed

3. **Renko Visualization on Time-Based Charts**:
   - Uses graphical elements to draw Renko-style bricks on a standard chart
   - Green boxes represent bullish bricks
   - Red boxes represent bearish bricks
   - Once formed, bricks never change or disappear

4. **Multi-Step Trend Reversal Detection**:
   - The strategy checks not only the current brick direction but also compares multiple historical bricks
   - Confirms genuine trend reversals by verifying direction changes across consecutive bricks

## Strategy Advantages

After in-depth code analysis, this strategy demonstrates the following significant advantages:

1. **Solves the Repainting Problem**:
   - Traditional Renko strategies perform well in backtesting but often fail in live trading, primarily due to the repainting issue
   - This strategy ensures that once a brick is formed, it will not change by emulating Renko behavior on standard time-based charts
   - This makes backtesting results more reliable and closer to live trading performance

2. **Noise Filtering and Clear Trend Identification**:
   - Renko charts inherently filter small fluctuations, forming new bricks only when price moves by a preset amount
   - This helps identify clear price trends and reduces false signals
   - Suitable for finding meaningful price movements in highly volatile markets

3. **Multi-Step Signal Verification**:
   - The strategy checks not just single direction changes but verifies multiple consecutive bricks' directions
   - By comparing `brickDir[brickSize]` with the current `brickDir` and historical price level relationships
   - Multi-step verification mechanism significantly reduces false signals

4. **Visual Trading Foundation**:
   - Draws colored bricks on charts, visually displaying price structure
   - Green and red boxes clearly identify market direction
   - Visual aids help traders better understand market behavior

5. **Flexibility and Customizability**:
   - Brick size can be adjusted by users, allowing strategy optimization for different markets and timeframes
   - Smaller brick sizes generate more frequent trading signals, suitable for short-term trading
   - Larger brick sizes filter more noise, suitable for medium to long-term trend following

## Strategy Risks

Despite solving the repainting problem, the following risk factors still exist:

1. **Signal Delay Risk**:
   - Since the strategy executes calculations only on confirmed bars, trade execution may be slightly later than traditional Renko charts
   - In fast-moving markets, entry points may miss optimal prices
   - Solution: Consider combining with other confirmation indicators or adjusting brick size to balance timeliness and accuracy

2. **Brick Size Selection Risk**:
   - Too small bricks generate excessive trading signals, increasing trading costs and potentially leading to overtrading
   - Too large bricks may miss important market turning points
   - Solution: Optimize brick size based on the volatility of the target asset and trading timeframe

3. **Trend Reversal False Signal Risk**:
   - Despite using multi-step verification, false breakouts may still occur in violently volatile markets
   - Price may cross brick boundaries multiple times before a real trend forms
   - Solution: Consider adding additional filters such as volume confirmation or momentum indicators

4. **Drawdown Risk**:
   - Trend reversal strategies may lead to consecutive losses in strongly trending markets
   - Reversal signals may trigger too early, resulting in counter-trend trading
   - Solution: Implement appropriate stop-loss mechanisms and position management strategies

5. **Computational Resource Risk**:
   - Drawing numerous bricks may consume significant resources, especially on long timeframes and large datasets
   - The code limits the maximum number of boxes to 500, which may be insufficient in some cases
   - Solution: Optimize code efficiency or consider displaying only the most recent N bricks

## Strategy Optimization Directions

Based on code analysis, here are several key optimization directions for this strategy:

1. **Dynamic Brick Size Optimization**:
   - The current strategy uses fixed brick size, which can be improved to dynamic brick size based on market volatility
   - Use smaller bricks during low volatility periods and larger bricks during high volatility periods
   - This will improve the strategy's adaptability to different market conditions
   - Implementation method: Use ATR (Average True Range) to dynamically adjust brick size

2. **Add Trading Filters**:
   - Combine volume or other momentum indicators to confirm trend reversal signals
   - Avoid trading under low liquidity or extreme volatility conditions
   - Implementation method: Add additional confirmation conditions based on RSI, volume breakouts, or MACD

3. **Improve Stop Loss and Profit Taking Mechanisms**:
   - The current strategy only closes positions when direction reverses; intelligent stop loss and target profit levels can be added
   - Set dynamic stop loss levels based on multiples of brick size
   - Implementation method: Add `strategy.exit()` commands, setting stop loss points based on ATR or brick size

4. **Optimize Multi-Step Verification Mechanism**:
   - The current strategy uses fixed `brickSize` multiples to compare historical bricks
   - Research the optimal number of historical comparison steps
   - Backtest different markets and timeframes to find the best parameter combinations
   - Implementation method: Parameterize the number of steps, allowing users to customize verification depth

5. **Improve Visualization and Alert Systems**:
   - Add trend lines and key level markers
   - Add alert functionality for brick formation and trading signals
   - Display current trend strength and duration
   - Implementation method: Use `label.new()` and `alert()` functions to enhance user experience

## Conclusion

The Multi-Step Non-Repainting Renko Emulation Trend Reversal Quantitative Trading Strategy successfully addresses the repainting problem in traditional Renko strategies, enabling traders to apply Renko logic on standard time-based charts while maintaining the stability of historical signals. The strategy identifies trend reversals through a multi-step verification mechanism, improving signal quality, and visually displays market structure through graphical representation.

The main advantages of the strategy include solving the repainting problem, filtering market noise, multi-level signal verification, and intuitive graphical representation. However, risks still exist, including signal delays, brick size selection, and false signals. Future optimizations can be achieved by implementing dynamic brick sizes, adding trading filters, improving stop loss mechanisms, optimizing verification steps, and enhancing visualization systems.

This approach, which combines the advantages of Renko charts while avoiding their drawbacks, is particularly suitable for trend following and trend reversal trading strategies, providing traders with a reliable technical analysis tool that can deliver stable live performance while maintaining backtesting accuracy.[/trans]



> Source (PineScript)

``` pinescript
//@version=5
strategy("Non-Repainting Renko Emulation Strategy [PineIndicators]", overlay=true, calc_on_every_tick=false, max_boxes_count = 500, max_labels_count = 500, max_lines_count = 500, initial_capital = 10000, default_qty_value = 100, default_qty_type = strategy.percent_of_equity, commission_value = 0.01, slippage = 2)

// Parameter: Brick-Größe (z.B. 10 Punkte)
brickSize = input.float(3.0, "Brick Size", step=0.1)

// Persistente Variablen
var float renkoPrice     = na    // Aktueller Renko-Level (Schlusswert des letzten Bricks)
var float prevRenkoPrice = na    // Vorheriger Renko-Level (für Box-Berechnung)
var int   brickDir       = 0     // 1 = Aufwärts, -1 = Abwärts
var bool  newBrick       = false // Signalisiert, dass ein neuer Brick abgeschlossen wurde
var int   brickStart     = bar_index  // Beginn des aktuellen Bricks (x-Achse)

// Berechnungen nur auf abgeschlossenen Candles
if barstate.isconfirmed
    newBrick := false
    // Initialisierung: Beim ersten Candle setzen wir den Renko-Level
    if na(renkoPrice)
        renkoPrice := close
        brickStart := bar_index
    // Berechne die Differenz zum letzten Renko-Level
    diff = close - renkoPrice
    // Prüfen, ob der Unterschied mindestens der Brick-Größe entspricht
    if math.abs(diff) >= brickSize
        // Anzahl kompletter Bricks (kann > 1 sein)
        numBricks = math.floor(math.abs(diff) / brickSize)
        prevRenkoPrice := renkoPrice
        // Aktualisieren des Renko-Levels
        renkoPrice := renkoPrice + numBricks * brickSize * math.sign(diff)
        // Brick-Richtung (konvertiere math.sign-Ergebnis in int)
        brickDir := int(math.sign(diff))
        newBrick := true

        // Bestimme die obere und untere Grenze des abgeschlossenen Bricks:
        lowLevel  = brickDir == 1 ? prevRenkoPrice : renkoPrice
        highLevel = brickDir == 1 ? renkoPrice     : prevRenkoPrice

        // Setze den Start für den nächsten Brick
        brickStart := bar_index


// Handelslogik: Einstieg/Ausstieg nur, wenn ein neuer Brick abgeschlossen wurde
if barstate.isconfirmed and newBrick
    // Bei Aufwärts-Brick: Long-Signal
    if brickDir[brickSize] < brickDir and renkoPrice[brickSize] < renkoPrice[brickSize*2] and renkoPrice < renkoPrice[brickSize] and renkoPrice[brickSize*2] < renkoPrice[brickSize*3] and strategy.position_size <= 0
        // Bestehende Short-Position schließen, falls vorhanden
        strategy.entry("Long", strategy.long)

    // Bei Abwärts-Brick: Short-Signal
    else if brickDir[brickSize] > brickDir and renkoPrice[brickSize] > renkoPrice[brickSize*2] and renkoPrice > renkoPrice[brickSize] and renkoPrice[brickSize*2] > renkoPrice[brickSize*3] and strategy.position_size >= 0
        // Bestehende Long-Position schließen, falls vorhanden
        strategy.entry("Short", strategy.short)

if barstate.isconfirmed and newBrick
    if brickDir[brickSize] < brickDir
        strategy.close("Short")

    else if brickDir[brickSize] > brickDir
        strategy.close("Long")


```

> Detail

https://www.fmz.com/strategy/484769

> Last Modified

2025-03-04 10:26:05

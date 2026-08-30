
> Name

Dynamic-Fair-Value-Gap-Intraday-Trading-Strategy-A-Multi-Timeframe-Backtesting-System-Based-on-Smart-Money-Concept-Theory
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d89d0207e49d0e89b3e5.png)
![IMG](https://www.fmz.com/upload/asset/2d8ab333626ddfd156dc2.png)


[trans]
#### Overview
The dynamic fair value gap intraday trading strategy is a quantitative trading system based on market structure theory that focuses on identifying and trading the fair value gap (FVG) in the price. This strategy utilizes three candlestick patterns to detect supply and demand imbalances in price action and place trades when price retests these areas. The strategy adopts a fixed risk-reward ratio for risk management and sets a forced liquidation mechanism at specific times every day to avoid overnight risks. This approach is derived from the Smart Money Concept (SMC) theory, which focuses on institutional funding behavior and changes in market microstructure. By systematically identifying and trading these high-probability return areas, the strategy is designed to capture intraday price fluctuations while maintaining tight risk control measures.
#### Strategy Principle
The core principle of the fair value gap trading strategy is based on the "unfilled area" or "gap" left when price moves quickly. These areas represent severe imbalances in supply and demand and are typically "filled in" or "retested" in the future. Specifically, the strategy works in the following ways:
1. **Gap Detection Mechanism**: The strategy uses the three candlestick pattern to identify two types of FVG:
   - Bullish FVG: The lowest price of the current candle is higher than the highest price two candles ago, and the closing price of the previous candle is higher than the highest price two candles ago.
   - Bearish FVG: The high price of the current candle is lower than the low price two candles ago, and the close price of the previous candle is lower than the low price two candles ago.
2. **Backtest entry logic**: The strategy will not enter the market immediately when FVG is formed, but waits for the price to backtest these areas:
   - Bullish FVG: A long signal is triggered when the price falls back to the upper boundary (high) of the FVG zone.
   - Bearish FVG: A short signal is triggered when the price rebounds to the lower border (low) of the FVG zone.
3. **Risk Management**:
   - Stop loss is set at the border of the corresponding FVG (low of bullish FVG or high of bearish FVG).
   - The profit target adopts a risk-reward ratio of 1:2, calculated as: entry price ± (entry price - stop loss) × 2.
4. **End-of-day closing**: The strategy automatically closes all positions at 3:15 pm (Indian Standard Time) every day and clears all FVG arrays to prepare for the next trading day.
5. **Pyramiding**: The strategy allows up to 5 stacking transactions (pyramiding), which means that multiple positions can be held in the same direction, thereby amplifying gains in strong trending markets.
This approach utilizes discontinuities in market structure and price action theory to attempt to capture the predictable behavior of prices as they fill these areas of imbalance.
#### Strategic Advantages
A deeper analysis of the code reveals several advantages of this strategy:
1. **Objective Trading Standards**: The strategy uses clearly defined mathematical conditions to identify FVG and entry points, eliminating subjective judgment and improving trading discipline and consistency.
2. **Market Structure-Based Trading**: By trading fair value gaps, strategies focus on areas of the market with true supply and demand imbalances, rather than relying on signals from traditional indicators, which tend to lag price action.
3. **Risk Control Mechanism**:
   - Preset stops specify the maximum risk for each trade.
   - A fixed risk-reward ratio ensures a reasonable win rate required for long-term profitability.
   - End-of-day liquidation eliminates overnight risk.
4. **Compound Gain Potential**: By allowing stacked trades (up to 5 positions), the strategy can significantly increase returns in strong trending markets, while controlling the risk of each position through stop losses.
5. **Adaptability**: The strategy does not rely on fixed price levels, but dynamically identifies key areas under current market conditions, making it adaptable in different market environments and instruments.
6. **Programming efficiency**: The code uses arrays to store FVG information and effectively manage multiple potential trading opportunities, ensuring that the system can track and respond to multiple price levels.
7. **Visual Assistance**: The strategy visually displays the FVG area on the chart (green is bullish FVG, red is bearish FVG) to help traders understand the decision-making process of the system.
#### Strategy Risk
While this strategy has a solid theoretical foundation and several advantages, there are several risk factors to be aware of:
1. **False breakthrough risk**: In a consolidating market, the price may hit the FVG boundary multiple times without forming a sustained trend, resulting in multiple stops and exits. Solutions could include adding additional market environment filters or trend confirmation indicators.
2. **Stacked Trading Risk**: Allowing up to 5 positions in the same direction may result in overexposure in the wrong direction, especially if the trend suddenly reverses. It is recommended to implement overall risk limits, such that the maximum risk for all positions does not exceed a specific percentage of the account.
3. **Limitations of Fixed Risk-Reward Ratio**: Using a fixed 1:2 risk-reward ratio may not be suitable for all market conditions. In low-volatility markets, such goals may be difficult to achieve; in high-volatility markets, profitable trades may be exited prematurely. Consider adjusting profit targets based on market volatility.
4. **Lack of market environment filtering**: The strategy generates signals under all market conditions without regard to the overall trend or volatility state. Trading counter-trend FVG in a strong trend environment can result in consecutive losses. Adding a trend filter can significantly improve performance.
5. **Lack of Volume Confirmations**: The strategy is based solely on price action and does not take into account volume confirmations, which can lead to false signals in low volume areas. Integrating volume analysis can improve signal quality.
6. **Potential problems with fixed-time exits**: Exiting at specific times of the day may result in premature exits in favorable positions or missed better exit opportunities in unfavorable positions. Consider incorporating exit conditions based on price action.
7. **Reliance on Historical Backtesting Assumptions**: The strategy assumes that future FVG behavior will be similar to patterns observed in the past. Market dynamics may change, reducing the effectiveness of these models. It is important to regularly re-optimize parameters and validate assumptions.
#### Strategy optimization direction
Based on an in-depth analysis of the code, here are several possible optimization directions:
1. **Market Structure Filter**:
   - Implement a higher level trend identification system to only trade FVG in the direction of the trend.
   - Possibility to add a simple moving average directional filter or more complex market structure analysis.
   - Such a filter can significantly reduce losses from contrarian trades.
2. **Volatility Adjustment**:
   - Implement dynamic stop-loss and take-profit targets based on current market volatility rather than using a fixed risk-reward ratio.
   - Expand targets in high volatility environments and tighten targets in low volatility environments.
   - Volatility can be quantified using ATR (Average True Range) or similar indicators.
3. **Transaction volume confirmation**:
   - Add trading volume conditions to ensure sufficient trading volume support during FVG formation and backtesting.
   - This can reduce false signals in low liquidity environments.
4. **Adaptive position size**:
   - Dynamic position sizing based on historical win rate, current volatility and specific FVG characteristics.
   - For "cleaner" FVGs (clearer three-candle pattern) or FVGs formed in a strong trend, it is possible to increase the position size.
5. **Multiple Time Frame Analysis**:
   - Integrate FVG analysis of higher time frames, prioritizing signals aligned with higher time frame FVG.
   - This approach improves signal quality and overall success rate.
6. **Intelligent overlay transaction**:
   - Modified overlay trading logic to be based on trend strength and success of previous trades.
   - The possibility of stacking trades can be increased after profitable trades and reduced after losing trades.
7. **Machine Learning Enhancement**:
   - Implement machine learning algorithms to identify FVG features most likely to succeed.
   - This can include analysis of FVG size, speed of formation, market environment and other factors.
8. **Statistical backtesting framework**:
   - Develop a more comprehensive backtesting framework to evaluate strategy performance under different market conditions.
   - Use Monte Carlo simulation to evaluate expected results under different parameter combinations and market conditions.
#### Summarize
The dynamic fair value gap day trading strategy provides a systematic approach to identifying and trading areas of supply and demand imbalances in the market. By utilizing the three-candle FVG pattern and clear backtest entry rules, the strategy is both theoretically sound and practical. Its powerful risk management framework, including pre-defined stops, fixed risk-to-reward ratios and end-of-day closing mechanisms, provides a solid foundation for trading discipline.
The strategy's key strengths are its objectivity and market structure-based approach, allowing it to remain relevant in different market environments. However, the effectiveness of the strategy may be significantly improved by implementing the suggested optimization directions, in particular adding market environment filtering, volatility-based adjustments and volume confirmation.
It is important to note that any trading strategy, no matter how perfect, is not guaranteed to succeed. Successful trading requires not only a sound strategy, but also strict execution discipline, proper money management and a deep understanding of the market. The Dynamic Fair Value Gap strategy provides a good starting point that traders can further customize and optimize based on their own risk tolerance and market views. ||
#### Overview

The Dynamic Fair Value Gap Intraday Trading Strategy is a quantitative trading system based on market structure theory, focusing on identifying and trading Fair Value Gaps (FVGs) in price action. The strategy employs a three-candle pattern to detect supply-demand imbalances in price behavior and enters trades when price retests these areas. It implements risk management with a fixed risk-reward ratio and includes a forced exit mechanism at a specific time each day to avoid overnight risk. This approach is derived from Smart Money Concept (SMC) theory, which focuses on institutional money behavior and changes in market microstructure. By systematically identifying and trading these high-probability-reward zones, the strategy aims to capture intraday price movements while maintaining strict risk control measures.

#### Strategy Principles

The core principle of the Fair Value Gap trading strategy is based on "unfilled areas" or "gaps" left when price moves rapidly. These areas represent significant supply-demand imbalances that will typically be "filled" or "retested" in the future. Specifically, the strategy works as follows:

1. **Gap Detection Mechanism**: The strategy uses a three-candle pattern to identify two types of FVGs:
   - Bullish FVG: Current candle's low is higher than the high of the candle two periods ago, AND the previous candle's close is higher than the high of the candle two periods ago.
   - Bearish FVG: Current candle's high is lower than the low of the candle two periods ago, AND the previous candle's close is lower than the low of the candle two periods ago.

2. **Retest Entry Logic**: The strategy doesn't enter immediately when an FVG forms but waits for price to retest these areas:
   - Bullish FVG: Long entry is triggered when price drops back to the upper boundary (high) of the FVG area.
   - Bearish FVG: Short entry is triggered when price bounces up to the lower boundary (low) of the FVG area.

3. **Risk Management**:
   - Stop loss is placed at the boundary of the respective FVG (low of bullish FVG or high of bearish FVG).
   - Profit target uses a 1:2 risk-reward ratio, calculated as: entry price ± (entry price - stop loss) × 2.

4. **End-of-Day Exit**: The strategy automatically closes all positions at 3:15 PM IST each day and clears all FVG arrays, preparing for the next trading day.

5. **Pyramiding**: The strategy allows up to 5 pyramiding trades, meaning multiple positions can be held in the same direction, amplifying gains in strong trending markets.

This approach leverages discontinuities in market structure and price action theory to capture predictable behavior as price fills these imbalance areas.

#### Strategy Advantages

Upon deep analysis of the code, the strategy demonstrates several advantages:

1. **Objective Trading Criteria**: The strategy uses clearly defined mathematical conditions to identify FVGs and entry points, eliminating subjective judgment and improving trading discipline and consistency.

2. **Market Structure-Based Trading**: By trading Fair Value Gaps, the strategy focuses on genuine supply-demand imbalance areas in the market rather than relying on signals from traditional indicators, which often lag price action.

3. **Risk Control Mechanisms**:
   - Predefined stop losses clearly define the maximum risk for each trade.
   - Fixed risk-reward ratio ensures a reasonable win rate needed for long-term profitability.
   - End-of-day forced exit eliminates overnight risk.

4. **Compound Profit Potential**: By allowing pyramiding (up to 5 positions), the strategy can significantly increase returns in strongly trending markets while controlling risk on each position through stop losses.

5. **Adaptability**: The strategy doesn't depend on fixed price levels but dynamically identifies key areas in current market conditions, making it adaptable across different market environments and instruments.

6. **Programming Efficiency**: The code uses arrays to store FVG information and efficiently manages multiple potential trade opportunities, ensuring the system can track and respond to multiple price levels.

7. **Visual Assistance**: The strategy visually displays FVG areas on the chart (green for bullish FVGs, red for bearish FVGs), helping traders understand the system's decision-making process.

#### Risk Analysis

Despite its solid theoretical foundation and numerous advantages, the strategy also presents several risk factors that need attention:

1. **False Breakout Risk**: In ranging markets, price may touch FVG boundaries multiple times without forming sustained trends, leading to multiple stop-outs. Solutions might include adding additional market environment filters or trend confirmation indicators.

2. **Pyramiding Risk**: Allowing up to 5 positions in the same direction could lead to excessive exposure in the wrong direction, especially during sudden trend reversals. Consider implementing overall risk limits, such as maximum risk across all positions not exceeding a specific percentage of the account.

3. **Fixed Risk-Reward Ratio Limitations**: Using a fixed 1:2 risk-reward ratio may not be optimal for all market conditions. In less volatile markets, such targets might be difficult to achieve; in highly volatile markets, it might exit profitable trades too early. Consider adjusting profit targets based on market volatility.

4. **Lack of Market Environment Filtering**: The strategy generates signals in all market conditions regardless of the overall trend or volatility state. Trading counter-trend FVGs in strong trending environments can lead to consecutive losses. Adding trend filters could significantly improve performance.

5. **Absence of Volume Confirmation**: The strategy relies solely on price action without considering volume confirmation, which might lead to false signals in low-volume areas. Integrating volume analysis could improve signal quality.

6. **Fixed-Time Exit Potential Issues**: Exiting at a specific time daily might lead to premature exits from favorable positions or missed better exit opportunities in unfavorable ones. Consider combining price action-based exit conditions.

7. **Reliance on Historical Backtesting Assumptions**: The strategy assumes future FVG behavior will be similar to patterns observed in the past. Market dynamics may change, weakening the effectiveness of these patterns. Regular parameter re-optimization and hypothesis validation is important.

#### Strategy Optimization Directions

Based on deep analysis of the code, here are several potential optimization directions:

1. **Market Structure Filtering**:
   - Implement higher-level trend identification systems to trade FVGs only in the trend direction.
   - Simple moving average direction filters or more complex market structure analysis could be added.
   - Such filtering could significantly reduce losses from counter-trend trades.

2. **Volatility Adjustment**:
   - Implement dynamic stop losses and profit targets based on current market volatility instead of using fixed risk-reward ratios.
   - Widen targets in high-volatility environments and tighten them in low-volatility ones.
   - ATR (Average True Range) or similar indicators could be used to quantify volatility.

3. **Volume Confirmation**:
   - Add volume conditions to ensure sufficient volume supports FVG formation and retests.
   - This can reduce false signals in low-liquidity environments.

4. **Adaptive Position Sizing**:
   - Implement dynamic position sizing based on historical win rates, current volatility, and specific FVG characteristics.
   - Increase position size for "cleaner" FVGs (more distinct three-candle pattern) or those forming within strong trends.

5. **Multiple Timeframe Analysis**:
   - Integrate FVG analysis from higher timeframes, prioritizing signals that align with higher timeframe FVGs.
   - This approach can improve signal quality and overall success rate.

6. **Smart Pyramiding**:
   - Modify the pyramiding logic to base it on trend strength and previous trade success.
   - Increase the likelihood of pyramiding after profitable trades and reduce it after losing ones.

7. **Machine Learning Enhancement**:
   - Implement machine learning algorithms to identify FVG characteristics most likely to succeed.
   - This could include analyzing FVG size, formation speed, market environment, etc.

8. **Statistical Backtesting Framework**:
   - Develop a more comprehensive backtesting framework to assess strategy performance across different market conditions.
   - Use Monte Carlo simulations to evaluate expected outcomes under different parameter combinations and market conditions.

#### Conclusion

The Dynamic Fair Value Gap Intraday Trading Strategy offers a systematic approach to identifying and trading supply-demand imbalance areas in the market. Through the use of the three-candle FVG pattern and clear retest entry rules, the strategy provides both theoretical soundness and practical operability. Its robust risk management framework, including predefined stop losses, fixed risk-reward ratios, and end-of-day exit mechanisms, provides a solid foundation for trading discipline.

The strategy's main strengths lie in its objectivity and market structure-based approach, allowing it to remain relevant across different market environments. However, its effectiveness could be significantly enhanced through the implementation of suggested optimization directions, particularly market environment filtering, volatility-based adjustments, and volume confirmation.

It's worth noting that no trading strategy, no matter how sophisticated, can guarantee success. Successful trading requires not only a sound strategy but also strict execution discipline, proper money management, and a deep understanding of the markets. The Dynamic Fair Value Gap strategy provides a good starting point that traders can further customize and optimize according to their risk tolerance and market views.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-26 00:00:00
end: 2025-03-25 00:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

//@version=6
strategy("Intraday FVG", overlay=true, pyramiding=5, max_bars_back=500, default_qty_type=strategy.percent_of_equity, commission_type=strategy.commission.percent)

// 2. FVG Detection (Three-Candle Pattern)
var bullFVGHigh = array.new_float()
var bullFVGLow = array.new_float()
var bullFVGIndex = array.new_int()
var bearFVGHigh = array.new_float()
var bearFVGLow = array.new_float()
var bearFVGIndex = array.new_int()

detectFVG() =>

    // Bullish FVG: Current low > prior high AND next high < current low
    bullCondition = low > high[2] and close[1] > high[2]
    // Bearish FVG: Current high < prior low AND next low > current high
    bearCondition = high < low[2] and close[1] < low[2]


    if bullCondition 
        // log.info("bull condition met: {0} {0} {0}", high[2], close[1], low)
        array.push(bullFVGHigh, low)
        array.push(bullFVGLow, low[2])
        array.push(bullFVGIndex, bar_index)

    
    if bearCondition
        // log.info("bear condition met: {0} {0} {0}", low[2], close[1], high)
        array.push(bearFVGHigh, high[2])
        array.push(bearFVGLow, high)
        array.push(bearFVGIndex, bar_index)

detectFVG()

// 3. Retest Execution Logic
checkRetests(arrayHigh, arrayLow, barIndex, direction) =>
    // log.info("{0} : {1}", bar_index, time)
    i = array.size(arrayHigh) - 1
    
    while i >= 0

        // log.info("barIndex : {0}" , array.get(barIndex, i))
        // log.info("bar_index : {0}" , bar_index)
        
        if array.get(barIndex, i) <  bar_index
            
            fvgHigh = array.get(arrayHigh, i)
            fvgLow = array.get(arrayLow, i)
            // log.info("visting : {0} : {1} : {2} : {3} ", array.get(barIndex, i), bar_index, fvgHigh, fvgLow)
            
            if direction == "long" and low <= fvgHigh
                // log.info("entering long")
                sl = array.get(arrayLow, i)  // Previous candle's low
                entry = close
                tp = entry + (entry - sl)*2
                strategy.entry("L"+str.tostring(array.get(barIndex, i)), strategy.long)
                strategy.exit("XL"+str.tostring(array.get(barIndex, i)), "L"+str.tostring(array.get(barIndex, i)), stop=sl, limit=tp)
                array.remove(arrayHigh, i)
                array.remove(arrayLow, i)
                array.remove(barIndex, i)
            
            if direction == "short" and high >= fvgLow
                // log.info("entering short")
                sl = array.get(arrayHigh, i)   // Previous candle's low
                entry = close
                tp = entry - (sl - entry)*2
                strategy.entry("S"+str.tostring(array.get(barIndex, i)), strategy.short)
                strategy.exit("XS"+str.tostring(array.get(barIndex, i)), "S"+str.tostring(array.get(barIndex, i)), stop=sl, limit=tp)
                array.remove(arrayHigh, i)
                array.remove(arrayLow, i)
                array.remove(barIndex, i)
        
        i := i - 1


checkRetests(bullFVGHigh, bullFVGLow, bullFVGIndex, "long")
checkRetests(bearFVGHigh, bearFVGLow, bearFVGIndex,"short")

// 5. Daily Exit at 3:15 PM IST
exitTime = hour == 15 and minute >= 15
if exitTime
    strategy.close_all()
    array.clear(bullFVGHigh)
    array.clear(bullFVGLow)
    array.clear(bearFVGHigh)
    array.clear(bearFVGLow)
    array.clear(bullFVGIndex)
    array.clear(bearFVGIndex)

```

> Detail

https://www.fmz.com/strategy/488280

> Last Modified

2025-03-26 15:27:29

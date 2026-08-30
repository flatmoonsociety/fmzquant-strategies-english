
> Name

Automated-Market-Reversal-Trading-Strategy-Based-on-Stochastic-Indicator-and-Candlestick-Patterns
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d982dceb5163579c25f0.png)
![IMG](https://www.fmz.com/upload/asset/2d8861af0afa3bdb304b6.png)

[trans]
#### Overview
The automated market reversal trading strategy based on stochastic indicators and candlestick patterns is a quantitative trading system that combines classic candlestick pattern recognition in technical analysis with stochastic indicator trend confirmation. The core design concept of this strategy is to capture potential trend turning opportunities in overbought or oversold areas by identifying key market reversal points. The strategy is written using Pine Script and implements a complete automated trading process on the TradingView platform, including signal generation, risk management and chart marking functions. This strategy can identify a variety of classic candlestick patterns, such as hammers, shooting stars, engulfing patterns, morning stars, etc., and confirm trends through stochastic indicators, providing higher reliability and accuracy for trading. The system has a built-in dynamic stop-profit and stop-loss mechanism based on ATR (average true volatility), which effectively controls the risk of a single transaction and improves the efficiency of fund management.
#### Strategy Principle
The strategy is based on two core technical principles: candlestick pattern recognition and trend confirmation filtering.
First of all, in terms of candlestick pattern identification, the strategy analyzes the structure of each K line through precise mathematical calculations, including the proportional relationship between the entity, the upper shadow line and the lower shadow line. The system defines a series of parameters to quantify the characteristics of different forms. For example, the hammer line requires that the length of the lower shadow line exceeds twice the length of the real body, and the real body accounts for no more than 50% of the total length, and the upper shadow line is almost non-existent. Forms of strategy identification include:
- Bull signals: Hammer, Inverted Hammer, Bullish Engulfing and Bullish Tweezer Bottom
- Bearing signals: Hanging Man, Shooting Star, Bearish Engulfing and Tweezer Top
Secondly, the strategy introduces the Stochastic as a trend confirmation tool to ensure that reversal signals are captured only in overbought or oversold areas. By setting the threshold (default 80), when the stochastic indicator is above the threshold area, it is considered an overbought area (bearish area), and when it is below (100-threshold), it is considered an oversold area (bullish area). The strategy also uses a smoothing algorithm to process random indicators to reduce noise interference and enhance signal reliability.
The transaction execution logic is as follows:
1. Long signal: When a bullish candlestick pattern is recognized in the oversold zone (bearZone), the system enters a long position
2. Short signal: When a bearish candlestick pattern is recognized in the overbought zone (bullZone), the system enters a short position
In terms of risk management, the strategy adopts a dynamic stop-profit and stop-loss mechanism based on ATR:
- Long trading: Take profit = entry price + (ATR × 1.5), stop loss = entry price - (ATR × 1.0)
- Short trade: Take Profit = Entry Price - (ATR × 1.5), Stop Loss = Entry Price + (ATR × 1.0)
This design allows the stop-profit and stop-loss points to automatically adapt to market volatility, automatically expand the protection scope in volatile markets, and narrow the protection scope in markets with low volatility, ensuring that the risk-to-return ratio remains at 1:1.5.
#### Strategic Advantages
Through in-depth analysis of the code, this strategy demonstrates the following significant advantages:
1. **Multi-dimensional signal verification mechanism**: The strategy not only relies on candlestick patterns, but also combines stochastic indicators for trend confirmation. Double filtering greatly reduces false signals and improves the winning rate of transactions. Analysis shows that when using candlestick patterns alone, a large number of false signals may be generated, but when trend confirmation is added, the quality of effective signals is significantly improved.
2. **Adaptive Risk Management**: By dynamically setting stop-profit and stop-loss through ATR, the strategy can intelligently adapt to different market environments and fluctuation conditions, and the protection scope can be adjusted without manual intervention. This mechanism ensures that the protection scope is automatically expanded during periods of high volatility, while parameters are tightened during periods of low volatility to avoid stop losses being triggered by small fluctuations.
3. **Highly customizable**: The strategy provides multiple parameters for users to adjust, including ATR period, take-profit and stop-loss ratio, trend lookback period, reversal threshold, smoothing factor, etc. Each candlestick pattern can also be turned on or off individually, allowing traders to customize the system based on different market characteristics or personal preferences.
4. **Visual trading signals**: The strategy automatically marks trading signals on the chart, such as "HAM" (hammer line), "STAR" (shooting star line), etc., allowing traders to intuitively identify market status and facilitate backtest analysis and real-time monitoring.
5. **Fund Management Integration**: The strategy uses 10% of the account equity as the fund allocation for each transaction by default, which can be adjusted according to needs, realizing complete fund management functions and avoiding excessive trading and capital risks.
6. **Commission cost consideration**: The strategy has built-in commission calculation (default 0.1%), which makes the backtest results closer to the actual trading environment and helps traders fully consider transaction costs when evaluating strategy performance.
#### Strategy Risk
Although the strategy is comprehensively designed, in-depth analysis still reveals the following potential risk points:
1. **Reversal Failure Risk**: Market reversal signals are not 100% reliable. Even if the candlestick pattern and stochastic indicator conditions are met at the same time, there is still the possibility of reversal failure. In strong trending markets, reversal signals can lead to consecutive losses. Solution: It is recommended to confirm the overall trend direction in a higher time period and only look for reversal signals in the direction of the general trend.
2. **Parameter optimization trap**: Over-optimizing parameters may cause the strategy to perform well on historical data, but have poor results in real trading. Solution: Use the Out-of-Sample method to verify the robustness of the parameters and avoid overfitting.
3. **Signal congestion**: In a highly volatile market, multiple trading signals may be generated in a short period of time, resulting in frequent entry and exit of the market and increased transaction costs. Solution: Add a signal confirmation mechanism, such as requiring two consecutive K lines to confirm, or increase the trading interval limit.
4. **Fixed risk ratio**: Although the strategy uses dynamic ATR to set take profit and stop loss, the fixed ratio (1.5:1) may not be suitable for all market environments. Solution: Dynamically adjust the risk-return ratio according to different market cycles and fluctuation characteristics.
5. **Stochastic indicator lag**: The stochastic indicator itself has a certain lag, which may lead to unsatisfactory timing of signal generation. Solution: Consider using a more sensitive indicator such as the RSI or combining it with a moving average for trend confirmation.
6. **Single time period limitation**: The strategy is only based on the current time period analysis and lacks multi-time period confirmation. Solution: Introduce multi-timeframe analysis, requiring both higher-level and lower-level timeframes to confirm signals.
#### Strategy optimization direction
Based on code analysis, the following are the key directions in which this strategy can be further optimized:
1. **Introduction of multi-time period analysis**: Combined with higher time period trend confirmation, the signal quality can be greatly improved. It is recommended to add a high time frame trend judgment function, and only execute transactions when complying with the high-level trend direction to avoid generating false signals when the big trend conflicts with the small trend.
2. **Optimize stochastic indicator parameters**: The current use of a fixed threshold (80) may not be suitable for all markets. It is recommended to implement an adaptive threshold mechanism to automatically adjust the overbought and oversold thresholds according to market fluctuation characteristics, or to perform cross-confirmation in conjunction with the Relative Strength Index (RSI).
3. **Improved risk management mechanism**: A dynamic risk adjustment system can be implemented to expand positions when there are continuous profits, reduce positions when there are continuous losses, or automatically adjust the risk-return ratio based on market volatility. It is recommended to add a trailing stop function to protect the profits made after the trend is established.
4. **Enhance the accuracy of candlestick pattern recognition**: The current pattern recognition algorithm is relatively simple, and more complex pattern recognition technology can be introduced, such as machine learning algorithms to identify more candlestick combination patterns, or combined with trading volume to confirm signal validity.
5. **Market environment adaptation**: Add market status classification (shock/trend/breakthrough), and use different trading strategy parameters for different market environments. In periods of high volatility, the reversal threshold requirements can be increased, while in low-volatility markets, the requirements can be lowered to achieve intelligent matching of strategies and market conditions.
6. **Add filter conditions**: Introduce additional filter conditions such as transaction volume confirmation, support and resistance levels, and key price levels to reduce false signals. In particular, reversal signals at important price levels (such as previous highs and lows, integer levels) are more meaningful.
7. **Backtest Optimization**: Improve the backtest framework, add slippage simulation, different market conditions testing, stress testing and other functions to comprehensively evaluate strategy performance. It is recommended to implement segmented backtesting to compare the performance differences of strategies in different market cycles.
#### Summary
The automated market reversal trading strategy based on stochastic indicators and candlestick patterns is a complete trading system that combines classic technical analysis concepts with modern quantitative trading techniques. By identifying classic candlestick reversal patterns and using stochastic indicators for trend confirmation, this strategy is able to capture potential market reversal points in overbought and oversold areas, and protect trading funds through a dynamic risk management mechanism based on ATR.
The main feature of the strategy is to mathematically and systematize traditional candlestick analysis, achieving precise pattern recognition and automatic trade execution, while retaining a high degree of customizability. The system's built-in chart marking function enhances the visualization of the trading process and facilitates analysis and monitoring. Compared with the traditional single technical indicator system, this strategy significantly improves the quality of trading signals through the multiple confirmation mechanism.
However, any trading strategy has limitations, and the main challenges faced by this strategy include the risk of reversal failure, difficulty in parameter optimization, signal congestion, etc. By introducing multi-time period analysis, optimizing indicator parameters, improving risk management mechanisms and other measures, the stability and profitability of the strategy can be further improved.
Overall, this strategy provides a framework that balances automation and flexibility and is suitable for investors who are familiar with technical analysis and want systematic trade execution. Through reasonable parameter adjustment and necessary optimization, this strategy can become a practical tool to effectively capture market reversal opportunities. ||
#### Overview
The Automated Market Reversal Trading Strategy Based on Stochastic Indicator and Candlestick Patterns is a quantitative trading system that combines classic candlestick pattern recognition with stochastic indicator trend confirmation. The core design concept of this strategy is to identify key market reversal points by capturing potential trend turning opportunities in overbought or oversold areas. Implemented in Pine Script on the TradingView platform, this strategy provides a complete automated trading process including signal generation, risk management, and chart labeling functions. The strategy can identify multiple classic candlestick patterns such as hammer, shooting star, engulfing patterns, and more, while using the stochastic oscillator for trend confirmation, providing higher reliability and precision for trading decisions. The system incorporates a dynamic stop-loss and take-profit mechanism based on ATR (Average True Range), effectively controlling individual trade risk and improving capital management efficiency.

#### Strategy Principles
This strategy is based on two core technical principles: candlestick pattern recognition and trend confirmation filtering.

First, for candlestick pattern recognition, the strategy analyzes the structure of each candlestick through precise mathematical calculations, including the proportional relationships between the body, upper shadow, and lower shadow. The system defines a series of parameters to quantify the characteristics of different patterns, such as requiring the hammer pattern to have a lower shadow length exceeding twice the body length, with the body occupying less than 50% of the total length, and minimal upper shadow. The patterns identified include:
- Bullish signals: Hammer, Inverted Hammer, Bullish Engulfing, and Tweezer Bottom
- Bearish signals: Hanging Man, Shooting Star, Bearish Engulfing, and Tweezer Top

Second, the strategy introduces the Stochastic Oscillator as a trend confirmation tool, ensuring that reversal signals are only captured in overbought or oversold zones. By setting a threshold (default 80), when the stochastic indicator is above the threshold, it's considered an overbought zone (bearish area), and when below (100-threshold), it's considered an oversold zone (bullish area). The strategy also employs a smoothing algorithm to process the stochastic indicator, reducing noise interference and enhancing signal reliability.

The trade execution logic is as follows:
1. Long signals: When bullish candlestick patterns are identified in oversold areas (bearZone), the system enters a long position
2. Short signals: When bearish candlestick patterns are identified in overbought areas (bullZone), the system enters a short position

For risk management, the strategy employs an ATR-based dynamic stop-loss and take-profit mechanism:
- Long trades: Take Profit = Entry Price + (ATR × 1.5), Stop Loss = Entry Price - (ATR × 1.0)
- Short trades: Take Profit = Entry Price - (ATR × 1.5), Stop Loss = Entry Price + (ATR × 1.0)

This design allows the stop-loss and take-profit levels to automatically adapt to market volatility, expanding protection ranges in highly volatile markets and narrowing them in less volatile markets, ensuring a risk-to-reward ratio of 1:1.5.

#### Strategy Advantages
Through in-depth code analysis, this strategy demonstrates the following significant advantages:

1. **Multi-dimensional Signal Validation Mechanism**: The strategy relies not only on candlestick patterns but also combines stochastic indicators for trend confirmation. This dual filtering significantly reduces false signals and improves win rates. Analysis shows that using candlestick patterns alone may generate numerous erroneous signals, while adding trend confirmation notably enhances effective signal quality.

2. **Adaptive Risk Management**: By dynamically setting stop-loss and take-profit levels based on ATR, the strategy can intelligently adapt to different market environments and volatility conditions without manual intervention. This mechanism ensures automatic expansion of protection ranges during high volatility periods and tightening of parameters during low volatility periods, avoiding stop-loss triggers from minor fluctuations.

3. **High Customizability**: The strategy provides multiple parameters for user adjustment, including ATR period, profit-loss ratio, trend lookback period, reversal threshold, and smoothing factor. Each candlestick pattern can also be individually enabled or disabled, allowing traders to customize the system according to different market characteristics or personal preferences.

4. **Visualized Trading Signals**: The strategy automatically marks trading signals on the chart, such as "HAM" (hammer), "STAR" (shooting star), etc., allowing traders to visually identify market conditions, facilitating backtesting analysis and real-time monitoring.

5. **Integrated Capital Management**: The strategy defaults to allocating 10% of account equity for each trade, which can be adjusted as needed, implementing complete capital management functionality and avoiding overtrading and capital risk.

6. **Commission Cost Consideration**: The strategy includes commission calculation (default 0.1%), making backtesting results closer to actual trading environments and helping traders fully consider transaction costs when evaluating strategy performance.

#### Strategy Risks
Despite its comprehensive design, the following potential risk points were identified after in-depth analysis:

1. **Reversal Failure Risk**: Market reversal signals are not 100% reliable. Even when both candlestick patterns and stochastic indicator conditions are met, there remains a possibility of reversal failure. In strong trending markets, reversal signals may lead to consecutive losses. Solution: It's recommended to confirm the overall trend direction in higher timeframes and only look for reversal signals in the direction of the larger trend.

2. **Parameter Optimization Trap**: Excessive parameter optimization may cause the strategy to perform excellently on historical data but poorly in live trading. Solution: Use Out-of-Sample testing methods to verify parameter robustness and avoid overfitting.

3. **Signal Congestion**: In highly volatile markets, multiple trading signals may be generated in a short period, leading to frequent market entries and exits that increase transaction costs. Solution: Add signal confirmation mechanisms, such as requiring confirmation from two consecutive candlesticks, or implementing trade interval restrictions.

4. **Fixed Risk Ratio**: Although the strategy uses dynamic ATR settings for stop-loss and take-profit, the fixed ratio (1.5:1) may not be suitable for all market environments. Solution: Dynamically adjust the risk-reward ratio based on different market cycles and volatility characteristics.

5. **Stochastic Indicator Lag**: The stochastic indicator itself has a certain lag, which may lead to suboptimal signal timing. Solution: Consider using more sensitive indicators like RSI or combining moving averages for trend confirmation.

6. **Single Timeframe Limitation**: The strategy is based solely on the current timeframe analysis, lacking multi-timeframe confirmation. Solution: Introduce multi-timeframe analysis, requiring signal confirmation from both higher and lower timeframe frameworks.

#### Strategy Optimization Directions
Based on code analysis, the following are key directions for further optimization of this strategy:

1. **Introduce Multi-timeframe Analysis**: Combining higher timeframe trend confirmation can significantly improve signal quality. It's recommended to add higher timeframe trend judgment functionality, executing trades only when aligned with the higher-level trend direction, avoiding erroneous signals when major and minor trends conflict.

2. **Optimize Stochastic Indicator Parameters**: The current fixed threshold (80) may not be suitable for all markets. It's recommended to implement an adaptive threshold mechanism that automatically adjusts overbought/oversold thresholds based on market volatility characteristics, or to cross-confirm with the Relative Strength Index (RSI).

3. **Improve Risk Management Mechanism**: A dynamic risk adjustment system can be implemented, expanding positions during consecutive profits and reducing positions during consecutive losses, or automatically adjusting the risk-reward ratio based on market volatility. Adding trailing stop-loss functionality is recommended to protect profits after a trend is established.

4. **Enhance Candlestick Pattern Recognition Precision**: The current pattern recognition algorithm is relatively simple. More complex pattern recognition techniques can be introduced, such as machine learning algorithms to identify more candlestick combination patterns, or combining volume to confirm signal validity.

5. **Market Environment Adaptation**: Add market state classification (oscillation/trend/breakout) and use different trading strategy parameters for different market environments. In high volatility periods, reversal threshold requirements can be increased, while in low volatility markets, requirements can be reduced, achieving intelligent matching between strategy and market states.

6. **Add Filtering Conditions**: Introduce additional filtering conditions such as volume confirmation, support and resistance levels, key price levels, etc., to reduce erroneous signals. Reversal signals at important price levels (such as previous highs and lows, round numbers) are particularly meaningful.

7. **Backtesting Optimization**: Improve the backtesting framework by adding slippage simulation, testing under different market conditions, stress testing, and other functionalities for comprehensive strategy performance evaluation. Implementing segmented backtesting is recommended to compare strategy performance differences across different market cycles.

#### Summary
The Automated Market Reversal Trading Strategy Based on Stochastic Indicator and Candlestick Patterns is a complete trading system that combines classic technical analysis concepts with modern quantitative trading technology. By identifying classic candlestick reversal patterns and using stochastic indicators for trend confirmation, this strategy can capture potential market reversal points in overbought and oversold areas, while protecting trading capital safety through ATR-based dynamic risk management mechanisms.

The main feature of the strategy is the mathematical and systematic implementation of traditional candlestick analysis, achieving precise pattern recognition and automatic trade execution while maintaining high customizability. The built-in chart marking functionality enhances the visualization of the trading process, facilitating analysis and monitoring. Compared to traditional single technical indicator systems, this strategy significantly improves trading signal quality through multiple confirmation mechanisms.

However, like any trading strategy, limitations exist. The main challenges faced by this strategy include reversal failure risk, parameter optimization difficulties, signal congestion issues, etc. The stability and profitability of the strategy can be further enhanced through measures such as introducing multi-timeframe analysis, optimizing indicator parameters, and improving risk management mechanisms.

Overall, this strategy provides a framework that balances automation and flexibility, suitable for investors familiar with technical analysis who desire systematized trade execution. With reasonable parameter adjustments and necessary optimizations, this strategy can become an effective tool for capturing market reversal opportunities.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-02-23 00:00:00
end: 2025-02-25 07:00:00
period: 2m
basePeriod: 2m
exchanges: [{"eid":"Futures_Binance","currency":"ETH_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © tradingbauhaus

//@version=6
strategy("Bauhaus Reversal Master", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10, commission_type=strategy.commission.percent, commission_value=0.1)

// Yo! Let's set some user controls
atrLen = input.int(14, title="ATR Period for Risk")
profitTarget = input.float(1.5, title="Profit Target (ATR x)")
stopLoss = input.float(1.0, title="Stop Loss (ATR x)")
trendLen = input.int(14, "Trend Lookback", minval=2)
thresh = input.float(80, "Reversal Threshold", minval=0, maxval=100)
smoothPeriod = input.float(20, "Smoothing Warmup", minval=1)

// Candlestick toggles because we love options
bullStuff = "Bullish Vibes"
bearStuff = "Bearish Blues"
hammerOn = input.bool(true, "Hammer Time", group=bullStuff, inline="b1")
invHammerOn = input.bool(true, "Upside-Down Hammer", group=bullStuff, inline="b2")
bullEngulfOn = input.bool(true, "Bullish Munch", group=bullStuff, inline="b3")
tweezerBotOn = input.bool(true, "Bottom Tweezers", group=bullStuff, inline="b4")
hangManOn = input.bool(true, "Hanging Dude", group=bearStuff, inline="r1")
shootStarOn = input.bool(true, "Falling Star", group=bearStuff, inline="r2")
bearEngulfOn = input.bool(true, "Bearish Gobble", group=bearStuff, inline="r3")
tweezerTopOn = input.bool(true, "Top Tweezers", group=bearStuff, inline="r4")

// Trend magic
var float smoothK = 0.0
alphaSmooth = 2 / (smoothPeriod + 1)
kTrend = ta.stoch(close, close, close, trendLen)
smoothK := kTrend > 50 ? smoothK + (100 - smoothK) * alphaSmooth : kTrend < 50 ? smoothK + (0 - smoothK) * alphaSmooth : kTrend
bullZone = kTrend >= thresh and smoothK >= thresh
bearZone = kTrend <= (100 - thresh) and smoothK <= (100 - thresh)

// Candle math because we’re nerds
redCandle = close < open
greenCandle = close > open
candleTop = math.max(open, close)
candleBot = math.min(open, close)
fullRange = high - low
bodySize = candleTop - candleBot
upperWickP = ((high - candleTop) / fullRange) * 100
lowerWickP = ((candleBot - low) / fullRange) * 100
bodyP = (bodySize / fullRange) * 100
isDoji = math.round_to_mintick(close) == math.round_to_mintick(open)

// Bullish signals, let’s catch that bounce
hammerSig = hammerOn and (lowerWickP > (bodyP * 2) and bodyP < 50 and upperWickP < 2 and not isDoji) and bearZone
invHammerSig = invHammerOn and (upperWickP > (bodyP * 2) and bodyP < 50 and lowerWickP < 2 and not isDoji) and bearZone
bullEngulfSig = bullEngulfOn and redCandle[1] and greenCandle and (bodySize > (bodySize[1] / 2)) and (open < close[1]) and candleTop > candleTop[1] and bearZone[1]
tweezerBotSig = tweezerBotOn and (math.round_to_mintick(low) - math.round_to_mintick(low[1]) == 0) and greenCandle and redCandle[1] and bearZone[1]

// Bearish signals, time to drop
shootStarSig = shootStarOn and (upperWickP > (bodyP * 2) and bodyP < 50 and lowerWickP < 2 and not isDoji) and bullZone
hangManSig = hangManOn and (lowerWickP > (bodyP * 2) and bodyP < 50 and upperWickP < 2 and not isDoji) and bullZone
bearEngulfSig = bearEngulfOn and greenCandle[1] and redCandle and (bodySize > (bodySize[1] / 2)) and (open > close[1]) and candleBot < candleBot[1] and bullZone[1]
tweezerTopSig = tweezerTopOn and (math.round_to_mintick(high) - math.round_to_mintick(high[1]) == 0) and redCandle and greenCandle[1] and bullZone[1]

// Risk management, keep the cash safe
atrVal = ta.atr(atrLen)
longProfit = close + atrVal * profitTarget
longStop = close - atrVal * stopLoss
shortProfit = close - atrVal * profitTarget
shortStop = close + atrVal * stopLoss

// Let’s trade, baby!
if hammerSig or invHammerSig or bullEngulfSig or tweezerBotSig
    strategy.entry("GoLong", strategy.long)
    strategy.exit("LongExit", "GoLong", limit=longProfit, stop=longStop)

if shootStarSig or hangManSig or bearEngulfSig or tweezerTopSig
    strategy.entry("GoShort", strategy.short)
    strategy.exit("ShortExit", "GoShort", limit=shortProfit, stop=shortStop)

// Slap some labels on this chart
if hammerSig
    label.new(bar_index, low, "HAM", color=color(na), textcolor=color.green, style=label.style_label_up, size=size.tiny)
if invHammerSig
    label.new(bar_index, low, "INV", color=color(na), textcolor=color.green, style=label.style_label_up, size=size.tiny)
if bullEngulfSig
    label.new(bar_index, low, "BULL", color=color(na), textcolor=color.green, style=label.style_label_up, size=size.tiny)
if tweezerBotSig
    label.new(bar_index, low, "TWZB", color=color(na), textcolor=color.green, style=label.style_label_up, size=size.tiny)
if shootStarSig
    label.new(bar_index, high, "STAR", color=color(na), textcolor=color.red, style=label.style_label_down, size=size.tiny)
if hangManSig
    label.new(bar_index, high, "HANG", color=color(na), textcolor=color.red, style=label.style_label_down, size=size.tiny)
if bearEngulfSig
    label.new(bar_index, high, "BEAR", color=color(na), textcolor=color.red, style=label.style_label_down, size=size.tiny)
if tweezerTopSig
    label.new(bar_index, high, "TWZT", color=color(na), textcolor=color.red, style=label.style_label_down, size=size.tiny)
```

> Detail

https://www.fmz.com/strategy/484582

> Last Modified

2025-03-03 10:03:52

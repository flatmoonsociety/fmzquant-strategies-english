
> Name

Triple-Moving-Average-Trend-Following-and-Momentum-Integration-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1184187f636090839af.png)

[trans]
#### Overview
This is a quantitative trading strategy based on a combination of trend following and momentum analysis. This strategy utilizes the Triple Exponential Moving Average (TEMA), Multiple Moving Average Crossovers, and MACD variant indicators to identify market trends and entry opportunities. The strategy adopts a strict risk control mechanism, including fixed stop loss, profit target and trailing stop loss, to achieve the optimal balance of risk and return.
#### Strategy Principle
The strategy mainly determines trading signals through three core technical indicator systems:
1. The Triple Exponential Moving Average (TEMA) system is used to confirm the overall trend direction. The trend strength is judged by calculating the three-layer EMA and combining its dynamic changes.
2. The fast and slow moving average crossover system uses 9-period and 15-period EMA to capture the turning point of the mid-term trend.
3. The intersection of the price and the 5-period EMA serves as the final confirmation signal and is used to accurately grasp the timing of entry.
The triggering of trading signals needs to meet the following conditions at the same time:
- The MACD indicator forms a golden cross with its signal line and the TEMA trend is upward
- Short-term EMA crosses above long-term EMA
- Price crossed above the 5-period EMA
#### Strategic Advantages
1. The multiple confirmation mechanism greatly reduces the impact of false signals and improves the accuracy of transactions.
2. Combining the advantages of trend tracking and momentum analysis, it can grasp the general trend without missing short-term opportunities.
3. A complete stop-loss mechanism is adopted, including fixed stop-loss points and dynamic trailing stop-loss, to effectively control risks.
4. The strategy parameters are highly adjustable and can adapt to different market environments.
5. The entry logic is clear and easy to understand and execute.
#### Strategy Risk
1. The multiple confirmation mechanism may lead to slower entry and miss some opportunities in fast market conditions.
2. The fixed stop loss point needs to be adjusted according to different market volatility, otherwise it may be stopped prematurely.
3. Frequent false signals may occur in sideways and volatile markets.
4. Trailing stops can exit high-quality trends prematurely when the market moves violently.
#### Strategy optimization direction
1. Introduce volatility indicators to dynamically adjust stop loss and profit targets to make them more consistent with market conditions.
2. Add trading volume indicators as auxiliary confirmation to improve signal reliability.
3. Add a market environment identification mechanism and use different parameter combinations under different market conditions.
4. Develop a mechanism for adding positions against the trend, and appropriately build positions during corrections to increase returns.
5. Optimize the trailing stop loss algorithm to better adapt to market fluctuations.
#### Summary
This strategy builds a robust trading system by integrating multiple technical indicator systems. Its core advantage lies in the multiple confirmation mechanism and complete risk control system. Although there is a certain risk of hysteresis, the strategy still has room for improvement through parameter optimization and function expansion. Suitable for traders who pursue steady returns. ||
#### Overview
This is a quantitative trading strategy that combines trend following and momentum analysis. The strategy utilizes Triple Exponential Moving Average (TEMA), multiple moving average crossovers, and a MACD variant to identify market trends and entry points. It implements strict risk control mechanisms, including fixed stop-loss, profit targets, and trailing stops to optimize risk-reward balance.

#### Strategy Principles
The strategy determines trading signals through three core technical indicator systems:
1. Triple Exponential Moving Average (TEMA) system confirms overall trend direction. It calculates three layers of EMA and combines their dynamic changes to judge trend strength.
2. Fast/Slow MA crossover system uses 9-period and 15-period EMAs to capture medium-term trend reversal points.
3. Price crossing with 5-period EMA serves as final confirmation signal for precise entry timing.

Trade signals are triggered when all conditions are met:
- MACD crosses above its signal line with upward TEMA trend
- Short-term EMA crosses above long-term EMA
- Price crosses above 5-period EMA

#### Strategy Advantages
1. Multiple confirmation mechanisms greatly reduce false signals and improve trading accuracy.
2. Combines benefits of trend following and momentum analysis to capture both major trends and short-term opportunities.
3. Implements comprehensive stop-loss mechanisms including fixed stops and dynamic trailing stops for effective risk control.
4. High parameter adaptability for different market environments.
5. Clear entry logic that's easy to understand and execute.

#### Strategy Risks
1. Multiple confirmation requirements may lead to delayed entries, missing opportunities in fast-moving markets.
2. Fixed stop-loss points need adjustment for different market volatilities to avoid premature exits.
3. May generate frequent false signals in range-bound, choppy markets.
4. Trailing stops might exit quality trends too early during severe market fluctuations.

#### Optimization Directions
1. Introduce volatility indicators for dynamic adjustment of stops and profit targets to better match market conditions.
2. Add volume indicators as auxiliary confirmation to improve signal reliability.
3. Implement market environment recognition for different parameter combinations in various market states.
4. Develop counter-trend position building mechanism for moderate accumulation during pullbacks.
5. Optimize trailing stop algorithm for better adaptation to market volatility.

#### Summary
The strategy builds a robust trading system by integrating multiple technical indicator systems. Its core strengths lie in multiple confirmation mechanisms and comprehensive risk control systems. While there are certain lag risks, the strategy has significant improvement potential through parameter optimization and functional expansion. Suitable for traders seeking stable returns.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-10-01 00:00:00
end: 2024-10-31 23:59:59
period: 2h
basePeriod: 2h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("ITG Scalper Strategy", shorttitle="lokesh_ITG_Scalper_Strategy", overlay=true)

// General inputs
len = input(14, title="TEMA period")
FfastLength = input.int(13, title="Filter fast length")
FslowLength = input.int(18, title="Filter slow length")
FsignalLength = input.int(14, title="Filter signal length")
sl_points = 7 // 5 points stop loss
tp_points = 100 // 100 points target profit
trail_points = 15 // Trailing stop loss every 10 points

// Validate input
if FfastLength < 1
    FfastLength := 1
if FslowLength < 1
    FslowLength := 1
if FsignalLength < 1
    FsignalLength := 1

// Get real close price
realC = close

// Triple EMA definition
ema1 = ta.ema(realC, len)
ema2 = ta.ema(ema1, len)
ema3 = ta.ema(ema2, len)

// Triple EMA trend calculation
avg = 3 * (ema1 - ema2) + ema3

// Filter formula
Fsource = close
FfastMA = ta.ema(Fsource, FfastLength)
FslowMA = ta.ema(Fsource, FslowLength)
Fmacd = FfastMA - FslowMA
Fsignal = ta.sma(Fmacd, FsignalLength)

// Plot EMAs for visual reference
shortema = ta.ema(close, 9)
longema = ta.ema(close, 15)
yma = ta.ema(close, 5)
plot(shortema, color=color.green)
plot(longema, color=color.red)
plot(yma, color=#e9f72c)

// Entry conditions
firstCrossover = ta.crossover(Fmacd, Fsignal) and avg > avg[1]
secondCrossover = ta.crossover(shortema, longema)  // Assuming you meant to cross shortema with longema
thirdCrossover = ta.crossover(close, yma)

var bool entryConditionMet = false

if (firstCrossover)
    entryConditionMet := true

longSignal = entryConditionMet and secondCrossover and thirdCrossover

// Strategy execution
if (longSignal)
    strategy.entry("Long", strategy.long)
    entryConditionMet := false  // Reset the entry condition after taking a trade

// Calculate stop loss and take profit prices
var float long_sl = na
var float long_tp = na

if strategy.position_size > 0  // Long position
    long_sl := close - sl_points
    long_tp := close + tp_points
    
    // Adjust stop loss with trailing logic
    if (close - long_sl > trail_points)
        long_sl := close - trail_points
        
    strategy.exit("Exit Long", "Long", stop=long_sl, limit=long_tp)

// Plotting Buy signals
plotshape(series=longSignal, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.small, title="Buy Signal")

// Alerts
alertcondition(longSignal, title="Buy Signal", message="Buy Signal")

```

> Detail

https://www.fmz.com/strategy/473145

> Last Modified

2024-11-27 16:08:16

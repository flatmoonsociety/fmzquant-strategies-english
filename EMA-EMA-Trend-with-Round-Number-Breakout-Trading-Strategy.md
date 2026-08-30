
> Name

EMA trend combined with round breakout trading strategy-EMA-Trend-with-Round-Number-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/deb58225b936ed5401.png)

[trans]
#### Overview
This is a quantitative trading strategy that combines EMA trends, reincarnation level breakthroughs and trading session filters. The strategy is mainly based on the judgment of the moving average trend direction, and uses the breakthrough pattern of price at key cycle positions as trading signals. At the same time, trading period filtering is introduced to improve the quality of trading. The strategy uses a percentage stop-loss and take-profit method for risk control.
#### Strategy Principle
The core logic of the strategy includes the following key elements:
1. Use the 20-day EMA as a trend judgment tool, only go long when the price is above the moving average, and go short when the price is below the moving average.
2. Look for the engulfing pattern as a trading signal near the key cycle level (the integer mark of $5)
3. Open positions only during London and New York trading hours and avoid periods of low volatility
4. Bullish signals must meet the following requirements at the same time: bullish engulfing pattern, price above EMA, and in a valid trading period
5. The short signal must meet the following requirements at the same time: bearish engulfing pattern, price below EMA, and in a valid trading period
6. Use a risk-return ratio of 1% stop loss and 1.5% take profit for transaction management.
#### Strategic Advantages
1. Multiple signal confirmation mechanism significantly improves transaction reliability
2. Combine technical analysis and price psychology to improve your winning rate
3. Time period filtering ensures trading during active market periods to avoid false breakthroughs
4. Fixed percentage stop loss and take profit facilitate risk management
5. The strategy has clear logic and is easy to understand and execute.
6. Suitable for volatile market environments
#### Strategy Risk
1. A sideways market may generate too many false signals
2. Fixed stop loss and take profit are not flexible enough and may miss the big market trend.
3. Relying only on technical indicators without considering fundamental factors
4. Possible risk of slippage when important news is announced
5. Trading session restrictions may miss good opportunities in other sessions
#### Strategy optimization direction
1. Introduce an adaptive stop-loss and stop-profit mechanism to dynamically adjust according to market volatility
2. Increase trading volume confirmation indicators and improve the credibility of breakthroughs
3. Add trend strength filter to avoid trading in weak trends
4. Consider introducing market sentiment indicators to optimize entry timing
5. Develop a more intelligent reincarnation bit recognition algorithm
#### Summary
This strategy builds a logically rigorous trading system by combining multiple mechanisms such as moving average trends, price patterns, and period filters. Although there are certain limitations, through continuous optimization and improvement, it is expected to further improve the stability and profitability of the strategy. The strategy is suitable as the basic framework of the mid- to long-term trend tracking system and can be customized and improved according to actual trading needs.
|| 

#### Overview
This is a quantitative trading strategy that combines EMA trend, round number breakout, and trading session filtering. The strategy primarily relies on EMA trend direction, coupled with price breakout patterns at key round number levels as trading signals, while incorporating session filtering to enhance trade quality. The strategy employs percentage-based stop-loss and take-profit for risk management.

#### Strategy Principles
The core logic includes the following key elements:
1. Uses 20-day EMA as a trend identification tool, only going long above EMA and short below
2. Looks for engulfing patterns near key round numbers ($5 intervals)
3. Only trades during London and New York sessions to avoid low volatility periods
4. Long signals require: bullish engulfing pattern, price above EMA, active trading session
5. Short signals require: bearish engulfing pattern, price below EMA, active trading session
6. Implements 1% stop-loss and 1.5% take-profit risk-reward ratio for trade management

#### Strategy Advantages
1. Multiple signal confirmation mechanism significantly improves trade reliability
2. Combines technical analysis with psychological price levels for higher win rate
3. Session filtering ensures trading during active market periods, avoiding false breakouts
4. Fixed percentage stop-loss and take-profit facilitates risk management
5. Clear strategy logic, easy to understand and execute
6. Suitable for markets with higher volatility

#### Strategy Risks
1. May generate excessive false signals in ranging markets
2. Fixed stop-loss and take-profit lack flexibility, might miss larger moves
3. Relies solely on technical indicators, ignoring fundamental factors
4. Subject to slippage risk during major news releases
5. Session restrictions might miss opportunities in other periods

#### Optimization Directions
1. Introduce adaptive stop-loss and take-profit mechanisms based on market volatility
2. Add volume confirmation indicators to enhance breakout reliability
3. Incorporate trend strength filters to avoid trading in weak trends
4. Consider adding market sentiment indicators to optimize entry timing
5. Develop more intelligent round number level identification algorithms

#### Summary
The strategy constructs a logically rigorous trading system by combining multiple mechanisms including EMA trends, price patterns, and session filtering. While it has certain limitations, continuous optimization and refinement can potentially enhance the strategy's stability and profitability. The strategy serves as a solid foundation for a medium to long-term trend following system, suitable for customization based on specific trading requirements.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-17 00:00:00
end: 2025-01-16 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT","balance":49999}]
*/


//@version=6
strategy("The Gold Box Strategy", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=200)

// Inputs
roundNumberInterval = input.int(5, title="Round Number Interval ($)", minval=1)
useEMA = input.bool(true, title="Use 20 EMA for Confluence")
emaLength = input.int(20, title="EMA Length")

// Session times for London and NY
londonSession = input("0300-1200", title="London Session (NY Time)")
nySession = input("0800-1700", title="New York Session (NY Time)")

// EMA Calculation
emaValue = ta.ema(close, emaLength)

// Plot Round Number Levels
roundLow = math.floor(low / roundNumberInterval) * roundNumberInterval
roundHigh = math.ceil(high / roundNumberInterval) * roundNumberInterval

// for level = roundLow to roundHigh by roundNumberInterval
//     line.new(x1=bar_index - 1, y1=level, x2=bar_index, y2=level, color=color.new(color.gray, 80), extend=extend.both)

// Session Filter
inLondonSession = not na(time("1", londonSession))
inNYSession = not na(time("1", nySession))
inSession = true

// Detect Bullish and Bearish Engulfing patterns
bullishEngulfing = close > open[1] and open < close[1] and close > emaValue and inSession
bearishEngulfing = close < open[1] and open > close[1] and close < emaValue and inSession

// Entry Conditions
if bullishEngulfing
    strategy.entry("Long", strategy.long, comment="Bullish Engulfing with EMA Confluence")
if bearishEngulfing
    strategy.entry("Short", strategy.short, comment="Bearish Engulfing with EMA Confluence")

// Stop Loss and Take Profit
stopLossPercent = input.float(1.0, title="Stop Loss (%)", minval=0.1) / 100
takeProfitPercent = input.float(1.5, title="Take Profit (%)", minval=0.1) / 100

strategy.exit("Exit Long", "Long", stop=close * (1 - stopLossPercent), limit=close * (1 + takeProfitPercent))
strategy.exit("Exit Short", "Short", stop=close * (1 + stopLossPercent), limit=close * (1 - takeProfitPercent))

```

> Detail

https://www.fmz.com/strategy/478736

> Last Modified

2025-01-17 16:17:10

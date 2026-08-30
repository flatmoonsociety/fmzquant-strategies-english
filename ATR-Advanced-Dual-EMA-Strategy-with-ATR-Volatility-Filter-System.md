
> Name

Advanced-Dual-EMA-Strategy-with-ATR-Volatility-Filter-System
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1dcf19219e18a6c34c3.png)

[trans]
#### Overview
This is a quantitative trading strategy that combines an exponential moving average (EMA) crossover and an average true range (ATR) filter. The strategy effectively improves the strategy's Sharpe ratio and overall performance by identifying strong trends and trading in higher-volatility market environments. The strategy uses 50-period and 200-period EMAs to capture mid- to long-term trends, while using the ATR indicator to assess market volatility, and only trades when volatility exceeds a specific threshold.
#### Strategy Principle
The core logic of the strategy consists of two main parts: trend judgment and volatility filtering. In terms of trend judgment, the strategy uses the 50-period EMA as the fast line and the 200-period EMA as the slow line. When the fast line crosses the slow line, a long signal is generated, and when it crosses below, a short signal is generated. In terms of volatility filtering, the strategy calculates the 14-period ATR value and converts it into a percentage of the price, allowing positions to be opened only when the ATR percentage exceeds a preset threshold (default is 2%). This design ensures that the strategy only trades in market environments with sufficient volatility, effectively reducing false signals in volatile markets.
#### Strategic Advantages
1. The volatility filtering mechanism significantly improves the stability of the strategy and improves the winning rate by only trading in high volatility environments.
2. Use the percentage method to calculate ATR so that the volatility filter can be adapted to varieties in different price ranges
3. Combined with medium and long-term moving averages, it can effectively capture the general trend and reduce the impact of short-term noise.
4. The strategy logic is simple and clear, with relatively few parameters, which reduces the risk of over-fitting.
5. Effectively control risks by setting up reasonable position management (10% position)
#### Strategy Risk
1. The EMA indicator has hysteresis, which may cause delays in entry and exit timing in violently volatile markets.
2. In a volatile market, even with ATR filtering, frequent false breakthroughs may still occur
3. Fixed ATR thresholds may not apply to all market environments
4. It does not take into account cyclical changes in the market, and parameters may need to be adjusted at different market stages.
It is recommended to use dynamic stop loss and gradual position opening to manage these risks
#### Strategy optimization direction
1. Introduce a dynamic ATR threshold and adjust it adaptively according to market conditions.
2. Add trend strength confirmation indicators, such as DMI or ADX
3. Implement a batch opening and closing mechanism to reduce the risks caused by a single entry and exit.
4. Add seasonal analysis module and use different parameter settings in different market cycles
5. Develop an adaptive moving average period selection mechanism to improve the adaptability of the strategy
#### Summary
This is a strategy that combines classic technical indicators with modern risk management concepts. Capturing trends through EMA crosses and using ATR filters to control trading timing, the strategy maintains simplicity while also being highly practical. Although there are some inherent risks, this strategy still has good application value through reasonable optimization and risk management measures. It is recommended that traders make appropriate parameter adjustments based on specific market characteristics and their own risk preferences in practical applications. ||
#### Overview
This is a quantitative trading strategy that combines Exponential Moving Average (EMA) crossovers with an Average True Range (ATR) filter. The strategy aims to identify strong trends and execute trades in high-volatility market conditions, effectively improving the Sharpe ratio and overall performance. It utilizes 50-period and 200-period EMAs to capture medium to long-term trends, while using the ATR indicator to assess market volatility, only trading when volatility exceeds a specific threshold.

#### Strategy Principles
The core logic consists of two main components: trend determination and volatility filtering. For trend determination, the strategy uses a 50-period EMA as the fast line and a 200-period EMA as the slow line, generating long signals when the fast line crosses above the slow line and short signals when it crosses below. For volatility filtering, the strategy calculates the 14-period ATR value and converts it to a percentage of price, only allowing positions when the ATR percentage exceeds a preset threshold (default 2%). This design ensures that the strategy only trades in markets with sufficient volatility, effectively reducing false signals in ranging markets.

#### Strategy Advantages
1. Volatility filtering mechanism significantly improves strategy stability by trading only in high-volatility environments
2. Using percentage-based ATR calculations makes the volatility filter adaptable to instruments at different price levels
3. Combination of medium and long-term moving averages effectively captures major trends while reducing short-term noise
4. Simple and clear strategy logic with relatively few parameters, reducing overfitting risk
5. Effective risk control through appropriate position management (10% position size)

#### Strategy Risks
1. EMA indicators have inherent lag, potentially causing delayed entry and exit timing in volatile markets
2. False breakouts may still occur in ranging markets, even with ATR filtering
3. Fixed ATR thresholds may not be suitable for all market conditions
4. Market cyclicality is not considered, parameters may need adjustment in different market phases
It is recommended to use dynamic stop-losses and gradual position building to manage these risks

#### Strategy Optimization Directions
1. Introduce dynamic ATR thresholds that adapt to market conditions
2. Add trend strength confirmation indicators like DMI or ADX
3. Implement graduated position building and closing mechanisms to reduce single entry/exit risks
4. Add seasonal analysis modules to use different parameters in different market cycles
5. Develop adaptive moving average period selection mechanisms to improve strategy adaptability

#### Summary
This strategy combines classic technical indicators with modern risk management concepts. By using EMA crossovers to capture trends while employing an ATR filter to control trade timing, the strategy maintains simplicity while achieving strong practicality. While some inherent risks exist, the strategy still holds good application value through proper optimization and risk management measures. Traders are advised to adjust parameters according to specific market characteristics and their own risk preferences in practical applications.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-11-27 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA Crossover with ATR Filter", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// Inputs for Moving Averages
fastLength = input.int(50, title="Fast EMA Length")
slowLength = input.int(200, title="Slow EMA Length")

// Inputs for ATR Filter
atrLength = input.int(14, title="ATR Length")
atrMultiplier = input.float(1.5, title="ATR Multiplier")
atrThreshold = input.float(0.02, title="ATR Threshold (%)")

// Calculate EMAs
fastEMA = ta.ema(close, fastLength)
slowEMA = ta.ema(close, slowLength)

// Calculate ATR
atr = ta.atr(atrLength)

// Convert ATR to a percentage of price
atrPct = atr / close

// Define Long Condition (Cross and ATR filter)
longCondition = ta.crossover(fastEMA, slowEMA) and atrPct > atrThreshold / 100

// Define Short Condition
shortCondition = ta.crossunder(fastEMA, slowEMA) and atrPct > atrThreshold / 100

// Define Exit Conditions
exitConditionLong = ta.crossunder(fastEMA, slowEMA)
exitConditionShort = ta.crossover(fastEMA, slowEMA)

// Long Entry
if (longCondition)
    strategy.entry("Long", strategy.long)

// Short Entry
if (shortCondition)
    strategy.entry("Short", strategy.short)

// Long Exit
if (exitConditionLong)
    strategy.close("Long")

// Short Exit
if (exitConditionShort)
    strategy.close("Short")

// Plot EMAs for visual reference
plot(fastEMA, title="50 EMA", color=color.blue)
plot(slowEMA, title="200 EMA", color=color.red)

// Plot ATR for reference
plot(atrPct, title="ATR Percentage", color=color.orange, style=plot.style_line)
hline(atrThreshold / 100, "ATR Threshold", color=color.green)
```

> Detail

https://www.fmz.com/strategy/473387

> Last Modified

2024-11-29 16:14:30

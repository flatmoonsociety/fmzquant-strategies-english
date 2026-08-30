
> Name

Awesome-Oscillator-Double-Stochastic-Filtered-Divergence-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14a73ad1069582e20af.png)
[trans]
### Overview
The Double Stochastic Filter Sharp Dispersion Strategy identifies potential buying and selling opportunities by detecting divergences between the Dispersion Analysis Index (AO) and price action, combined with the overbought and oversold status of the Stochastic indicator as an additional filter.
### Strategy Principles
The strategy consists of the following components:
1. Calculation of Dispersion Analysis (AO): AO is the difference between the simple moving average (SMA) of 5-period and 34-period HL2, which is used to identify the push and pull dynamics of market momentum.
2. Stochastic: The stochastic indicator measures momentum and its potential reversal points by comparing closing prices to price ranges over a period. Here, the 14-period stochastic indicator (stochK) and its 3-period SMA (stochD) are used to identify overbought and oversold conditions.
3. Divergence detection logic: When the price moves in one direction (up or down) and AO moves in the opposite direction, it is determined that there is a divergence. A simplified departure detection logic is used here.
4. Stochastic indicator filtering: The signal is filtered by the stochastic indicator status. It is required that the sell signal is overbought and the buy signal is oversold.
5. Signal drawing: Draw filtered confirmed trading signals on the chart by shapes.
6. Strategic entry: go long when the long entry signal is confirmed, and go short when the short entry signal is confirmed.
### Advantage Analysis
This strategy combines the advantages of trend following and reversal identification, and has high reliability. The specific advantages are as follows:
1. AO helps identify changes in short-term trends in the market, and deviates from price as a source of strategic signals, with high reliability.
2. Check the status of the stochastic indicator to avoid generating false signals when it is not overbought or oversold.
3. Use a variety of indicators to combine and comprehensively judge the market status with good reliability.
4. The strategic entry signal is clear, the operating rules are simple, and it is easy to implement.
5. The selection of indicators and parameters is reasonable, the backtest performance is good, and the real-time verification effect is good.
### Risk Analysis
This strategy also has some risks, mainly including:
1. The judgment of divergence signals is too simple and misjudgments may occur. The risk of misjudgment can be reduced by optimizing entry logic.
2. Indicator parameters are set statically, and the effects may vary under different market conditions. It can be improved through parameter optimization or adaptive parameter settings.
3. Stochastic indicator filtering may miss some trading opportunities. Filters can be adjusted to capture more opportunities.
4. The control of long and short positions is not strict, and losses cannot be well controlled. You can set stop loss conditions or optimize position management rules.
### Optimization direction
This strategy can be further optimized from the following aspects:
1. Optimize the identification logic of divergence signals and improve signal quality.
2. Test different parameter combinations to find the best parameters.
3. Add stop-loss strategies and strictly control single losses.
4. Optimize the opening size and position management strategy.
5. Introduce machine learning algorithms to achieve dynamic optimization of parameters and rules.
6. Add more data sources to achieve multi-factor driving.
### Summarize
The dual stochastic filter sharp discrete analysis strategy combines AO and price divergence signals with stochastic indicator filtering to achieve an effective combination of trend capture and reversal identification. The operation rules of this strategy are clear, the backtest performance is good, and it has strong practical value. Through continuous optimization, it is expected to obtain better simulated trading and real trading effects.
||

### Overview  

The Awesome Oscillator Double Stochastic Filtered Divergence trading strategy identifies potential buy and sell opportunities through detecting divergences between the Awesome Oscillator (AO) and price action, filtered by Stochastic Oscillator’s overbought and oversold conditions to improve signal reliability.

### Strategy Logic  

The strategy consists of the following components:

1. Awesome Oscillator (AO) Calculation: AO is the difference between 5-period and 34-period SMAs of midpoint (HL2) to identify market momentum dynamics. 

2. Stochastic Oscillator: Used to gauge momentum and potential reversal points by comparing closing price to price range over a period. Uses 14-period Stochastic (stochK) and 3-period SMA (stochD) to detect overbought/oversold levels.

3. Divergence Detection Logic: Simplified to when price is moving in one direction while AO moves in opposite direction. Real-world divergence detection involves more nuanced analysis. 

4. Stochastic Filtering: Signals filtered by Stochastic overbought condition for selling and oversold for buying.

5. Signal Plotting: Confirmed signals after filtering plotted on chart as shapes.

6. Entry Rules: Long entry on confirmed bullish signal, short entry on confirmed bearish signal.

### Advantage Analysis   

The strategy combines following trend and identifying reversals, with reliable signals. Advantages include:

1. AO helps identify short-term trend changes, divergence with price provides reliable signal source.  

2. Stochastic filters avoid false signals without overbought/oversold confirmation.

3. Combining indicators provides robust market assessment and reliability. 

4. Clear entry signals and rules, easy implementation.

5. Reasonable indicator selection and parameters, good backtest and live performance.

### Risk Analysis

Potential risks include:

1. Simplistic divergence detection risks misjudging signals. Optimization can reduce misjudging likelihood.

2. Static parameter settings may underperform across changing market conditions. Adaptive parameters could improve performance.

3. Stochastic filtering may miss some profitable opportunities. Adjusting filters could capture more trades. 

4. No strict loss control mechanisms for open positions. Stop losses or position sizing rules could control risk better.


### Optimization Directions

Areas for further optimization:

1. Improve divergence signal identification logic for higher quality signals.  

2. Test different parameter combinations to find optimum parameters.

3. Incorporate stop loss strategies to control downside on individual trades.

4. Optimize entry sizing rules and open position management.

5. Introduce machine learning for dynamic parameter and logic optimization.  

6. Add more data sources for multivariate factor driving.


### Summary

The AO Double Stochastic Filtered Divergence strategy effectively combines trend following and reversal identification through AO divergence and Stochastic filtering. Clear rules, good backtest results, with strong practical potential. Further optimizations can yield improved simulation and live performance.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 4h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Fixed AO Divergence Strategy", shorttitle="Fixed AO+Stoch", overlay=true)

// Calculate Awesome Oscillator
ao() => ta.sma(hl2, 5) - ta.sma(hl2, 34)
aoVal = ao()

// Stochastic Oscillator
stochK = ta.stoch(close, high, low, 14)
stochD = ta.sma(stochK, 3)

// Simplify the divergence detection logic
// For educational purposes, we will define a basic divergence detection mechanism
// Real-world application would require more sophisticated logic

// Detect bullish and bearish divergences based on AO and price action
bullishDivergence = (close > close[1]) and (aoVal < aoVal[1])
bearishDivergence = (close < close[1]) and (aoVal > aoVal[1])

// Stochastic Overbought/Oversold conditions
stochOverbought = (stochK > 80) and (stochD > 80)
stochOversold = (stochK < 20) and (stochD < 20)

// Filtered signals
confirmedBullishSignal = bullishDivergence and stochOversold
confirmedBearishSignal = bearishDivergence and stochOverbought

// Plot signals
plotshape(series=confirmedBullishSignal, style=shape.triangleup, location=location.belowbar, color=color.green, title="Bullish Divergence", text="BUY")
plotshape(series=confirmedBearishSignal, style=shape.triangledown, location=location.abovebar, color=color.red, title="Bearish Divergence", text="SELL")

// Strategy Entry
if (confirmedBullishSignal)
    strategy.entry("Long", strategy.long, comment="Long Entry")

if (confirmedBearishSignal)
    strategy.entry("Short", strategy.short, comment="Short Entry")

```

> Detail

https://www.fmz.com/strategy/442946

> Last Modified

2024-02-27 15:51:44

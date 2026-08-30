
> Name

Enhanced-Momentum-Oscillator-and-Stochastic-Divergence-Quantitative-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/ae4177fe07564ef345.png)

[trans]
#### Overview
This strategy is a quantitative trading system that combines the Accelerating Oscillator (AC) and Stochastic. It captures shifts in market momentum by identifying divergences between price and technical indicators, thereby predicting potential trend reversals. The strategy also integrates moving averages (SMA) and relative strength indicators (RSI) to enhance signal reliability, and sets fixed take-profit and stop-loss to control risk.
#### Strategy Principle
The core logic of the strategy is based on the synergy of multiple technical indicators. First, calculate the accelerating oscillator (AC), which is calculated by taking the difference between the 5-period and 34-period moving averages of the median price, and then subtracting its N-period moving average. At the same time, the K value and D value of the stochastic indicator are calculated to confirm the divergence signal. When the price makes a new low and the AC indicator moves higher, a bullish divergence is formed; when the price makes a new high and the AC indicator moves lower, a bearish divergence is formed. The strategy also introduces RSI as an auxiliary confirmation indicator to improve the accuracy of the signal through cross-validation of multiple indicators.
#### Strategic Advantages
1. Multi-indicator collaboration: Through the cooperation of three indicators, AC, Stochastic and RSI, false signals can be effectively filtered
2. Automated risk control: built-in fixed-point stop-profit and stop-loss settings, which can effectively control the risk of each transaction
3. Visual tips: Clearly mark the buying and selling signals on the chart to facilitate traders to quickly identify opportunities.
4. Strong flexibility: The parameters are highly adjustable and suitable for different market environments and trading cycles.
5. Real-time warning: Integrated real-time warning system to ensure that no trading opportunities are missed
#### Strategy Risk
1. False breakthrough risk: False divergence signals may occur in volatile markets
2. Slippage risk: Due to the use of fixed points for stop-profit and stop-loss, you may face greater slippage when the market fluctuates violently.
3. Parameter sensitivity: Different parameter combinations may lead to large differences in strategy performance
4. Dependence on the market environment: In markets where the trend is not obvious, the strategy may not be effective.
5. Signal lag: Due to the use of moving average calculations, there may be a certain lag in the signal.
#### Strategy optimization direction
1. Dynamic stop-profit and stop-loss: The stop-profit and stop-loss points can be dynamically adjusted according to market volatility.
2. Introduce trading volume indicators: enhance signal reliability through volume confirmation
3. Market environment filtering: Add a trend judgment module and adopt different trading strategies in different market environments.
4. Optimize parameter selection: Use machine learning methods to optimize the combination of each indicator parameter
5. Add time filtering: consider market time characteristics to avoid trading during unfavorable periods
#### Summary
This is a quantitative trading strategy that integrates multiple technical indicators to capture market turning points through divergence signals. The advantage of the strategy lies in the cross-validation of multiple indicators and a complete risk control system, but it is also necessary to pay attention to issues such as false breakthroughs and parameter optimization. Through continuous optimization and improvement, this strategy is expected to maintain stable performance in different market environments. ||
#### Overview
This strategy is a quantitative trading system that combines the Accelerator Oscillator (AC) and Stochastic indicators. It captures market momentum shifts by identifying divergences between price and technical indicators to predict potential trend reversals. The strategy also incorporates Simple Moving Averages (SMA) and Relative Strength Index (RSI) to enhance signal reliability, with fixed take-profit and stop-loss levels for risk control.

#### Strategy Principle
The core logic is based on the synergy of multiple technical indicators. The AC is calculated using the difference between 5-period and 34-period SMAs of price midpoints, minus its N-period moving average. Stochastic K and D values are calculated to confirm divergence signals. Bullish divergence forms when price makes new lows while AC rises; bearish divergence forms when price makes new highs while AC falls. RSI is incorporated as an additional confirmation indicator, using cross-validation of multiple indicators to improve signal accuracy.

#### Strategy Advantages
1. Multiple indicator synergy: Effectively filters false signals through the combination of AC, Stochastic, and RSI
2. Automated risk control: Built-in fixed take-profit and stop-loss settings effectively control risk per trade
3. Visual cues: Clear buy and sell signals marked on charts for quick opportunity identification
4. High flexibility: Strong parameter customization suitable for different market conditions and timeframes
5. Real-time alerts: Integrated alert system ensures no trading opportunities are missed

#### Strategy Risks
1. False breakout risk: May generate false divergence signals in ranging markets
2. Slippage risk: Fixed pip take-profit and stop-loss may face significant slippage in volatile markets
3. Parameter sensitivity: Different parameter combinations may lead to varying strategy performance
4. Market environment dependency: Strategy may underperform in markets lacking clear trends
5. Signal lag: Some lag may exist due to moving average calculations

#### Strategy Optimization Directions
1. Dynamic take-profit/stop-loss: Adjust levels based on market volatility
2. Volume indicator integration: Enhance signal reliability through volume confirmation
3. Market environment filtering: Add trend assessment module for different market conditions
4. Parameter optimization: Use machine learning methods to optimize indicator parameter combinations
5. Time filtering: Consider market time characteristics to avoid unfavorable trading periods

#### Summary
This is a quantitative trading strategy integrating multiple technical indicators, capturing market turning points through divergence signals. Its strengths lie in cross-validation of multiple indicators and comprehensive risk control system, while attention must be paid to false breakouts and parameter optimization. Through continuous optimization and improvement, the strategy shows promise for maintaining stable performance across different market environments.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-09 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This Pine Script™ code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © JayQwae


//@version=5
strategy("Enhanced AC Divergence Strategy with Stochastic Divergence", overlay=true)

// Input settings
tp_pips = input.float(0.0020, "Take Profit (in price)", step=0.0001)
sl_pips = input.float(0.0040, "Stop Loss (in price)", step=0.0001)  // 40 pips
ac_length = input.int(5, "AC Length")
rsi_length = input.int(14, "RSI Length")
stoch_k = input.int(14, "Stochastic K Length")
stoch_d = input.int(3, "Stochastic D Smoothing")
stoch_ob = input.float(80, "Stochastic Overbought Level")
stoch_os = input.float(20, "Stochastic Oversold Level")

// Accelerator Oscillator Calculation
high_low_mid = (high + low) / 2
ao = ta.sma(high_low_mid, 5) - ta.sma(high_low_mid, 34)
ac = ao - ta.sma(ao, ac_length)

// RSI Calculation
rsi = ta.rsi(close, rsi_length)

// Stochastic Oscillator Calculation
k = ta.sma(ta.stoch(close, high, low, stoch_k), stoch_d)
d = ta.sma(k, stoch_d)

// Stochastic Divergence Detection
stoch_bull_div = ta.lowest(close, 5) < ta.lowest(close[1], 5) and ta.lowest(k, 5) > ta.lowest(k[1], 5)
stoch_bear_div = ta.highest(close, 5) > ta.highest(close[1], 5) and ta.highest(k, 5) < ta.highest(k[1], 5)

// Main Divergence Detection
bullish_div = ta.lowest(close, 5) < ta.lowest(close[1], 5) and ac > ac[1] and stoch_bull_div
bearish_div = ta.highest(close, 5) > ta.highest(close[1], 5) and ac < ac[1] and stoch_bear_div

// Plot divergences
plotshape(bullish_div, title="Bullish Divergence", location=location.belowbar, color=color.green, style=shape.triangleup, size=size.small)
plotshape(bearish_div, title="Bearish Divergence", location=location.abovebar, color=color.red, style=shape.triangledown, size=size.small)

// Strategy rules
if (bullish_div)
    strategy.entry("Buy", strategy.long)
    strategy.exit("Take Profit/Stop Loss", "Buy", limit=close + tp_pips, stop=close - sl_pips)

if (bearish_div)
    strategy.entry("Sell", strategy.short)
    strategy.exit("Take Profit/Stop Loss", "Sell", limit=close - tp_pips, stop=close + sl_pips)

// Alerts
if (bullish_div)
    alert("Bullish Divergence detected! Potential Buy Opportunity", alert.freq_once_per_bar)

if (bearish_div)
    alert("Bearish Divergence detected! Potential Sell Opportunity", alert.freq_once_per_bar)




```

> Detail

https://www.fmz.com/strategy/474709

> Last Modified

2024-12-11 17:34:01

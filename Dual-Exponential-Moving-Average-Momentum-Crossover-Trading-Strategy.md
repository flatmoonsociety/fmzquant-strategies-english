
> Name

Dual-Exponential-Moving-Average-Momentum-Crossover-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/130a2aac3f995676066.png)

[trans]
#### Overview
This strategy is a trend following trading system based on the Triple Exponential Moving Average (TEMA). The strategy captures market trends by comparing short-term and long-term TEMA cross signals, and combines volatility stops to manage risks. The strategy operates on a 5-minute timeframe, using the 300 and 500 period TEMA indicators as the basis for signal generation.
#### Strategy Principle
The core logic of the strategy is based on the following key elements:
1. Use the TEMA indicator with two different periods (300 and 500) to identify the trend direction
2. When the short-term TEMA crosses the long-term TEMA upward, the system generates a long signal
3. When the short-term TEMA crosses the long-term TEMA downward, the system generates a short signal
4. Use the highest and lowest prices of 10 periods to set the stop loss position
5. After entering the market, hold the position until a reverse signal appears before closing the position.
#### Strategic Advantages
1. Strong signal stability: Using TEMA with a longer period can effectively filter market noise and reduce false signals.
2. Improved risk control: combined with fluctuation stop loss, single transaction risks can be effectively controlled
3. Strong ability to grasp trends: TEMA responds to trends faster than traditional moving averages
4. Complete closed trading loop: including clear entry, stop loss and profit-taking conditions
5. Highly adjustable parameters: all key parameters can be flexibly adjusted according to market characteristics
#### Strategy Risk
1. Volatile market risk: In a volatile market, it is easy to generate false signals, leading to continuous losses.
2. Slippage risk: The 5-minute period may face large slippage during violent fluctuations
3. Fund management risk: Fixed point stop loss may result in excessive losses during periods of severe fluctuations.
4. Signal lag: The TEMA indicator itself has a certain lag and may miss the best entry point.
5. Parameter sensitivity: The optimal parameters vary greatly under different market environments.
#### Strategy optimization direction
1. Increase market environment identification: add trend strength indicators and use different parameters in different market environments
2. Optimize the stop loss method: consider using ATR dynamic stop loss to improve the adaptability of the stop loss
3. Improve position management: dynamically adjust the number of positions opened according to the strength of the trend
4. Add an early warning mechanism: send early warning signals at key price positions in advance
5. Add trading volume indicator: combine the trading volume to confirm the validity of the signal
#### Summary
This strategy is a complete trend tracking system that captures trends through the intersection of TEMA indicators and manages risks with dynamic stop loss. The strategy logic is clear, simple to implement, and has good practicality. However, in real trading, attention needs to be paid to the identification of market environment and risk control. It is recommended to optimize parameters based on actual market conditions based on backtest verification. ||
#### Overview
This strategy is a trend-following trading system based on the Triple Exponential Moving Average (TEMA). It captures market trends by analyzing crossover signals between short-term and long-term TEMA indicators, incorporating volatility-based stop-loss for risk management. The strategy operates on a 5-minute timeframe, utilizing 300 and 500-period TEMA indicators as the foundation for signal generation.

#### Strategy Principles
The core logic of the strategy is based on the following key elements:
1. Uses two different period TEMAs (300 and 500) to identify trend direction
2. Generates long signals when short-term TEMA crosses above long-term TEMA
3. Generates short signals when short-term TEMA crosses below long-term TEMA
4. Uses 10-period high and low prices to set stop-loss levels
5. Holds positions until a reverse signal appears

#### Strategy Advantages
1. Signal Stability: Longer-period TEMAs effectively filter market noise and reduce false signals
2. Robust Risk Control: Incorporates volatility-based stop-loss for effective single-trade risk control
3. Strong Trend Capture: TEMA responds faster to trends than traditional moving averages
4. Complete Trading Loop: Includes clear entry, stop-loss, and profit-taking conditions
5. High Parameter Adaptability: Key parameters can be flexibly adjusted based on market characteristics

#### Strategy Risks
1. Sideways Market Risk: Prone to false signals in range-bound markets leading to consecutive losses
2. Slippage Risk: 5-minute timeframe may face significant slippage during volatile periods
3. Money Management Risk: Fixed-point stop-loss may result in excessive losses during high volatility
4. Signal Lag: TEMA indicators have inherent lag, potentially missing optimal entry points
5. Parameter Sensitivity: Optimal parameters vary significantly across different market environments

#### Strategy Optimization
1. Add Market Environment Recognition: Incorporate trend strength indicators for parameter adaptation
2. Optimize Stop-Loss: Consider implementing ATR-based dynamic stop-loss
3. Improve Position Sizing: Dynamically adjust position size based on trend strength
4. Enhanced Alert System: Implement early warning signals at key price levels
5. Include Volume Analysis: Confirm signal validity with volume indicators

#### Summary
This strategy is a comprehensive trend-following system that captures trends through TEMA crossovers while managing risk with dynamic stop-loss. The strategy logic is clear, implementation is straightforward, and it demonstrates good practicality. However, when trading live, attention must be paid to market environment identification and risk control. It is recommended to optimize parameters based on actual market conditions after backtesting verification.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2025-01-04 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("TEMA Strategy for Gold", overlay=true)

// Inputs
tema_short_length = input.int(300, title="Short TEMA Length")
tema_long_length = input.int(500, title="Long TEMA Length")
pip_value = input.float(0.10, title="Pip Value (10 pips = 1 point for Gold)")

// Calculate TEMA
tema_short = ta.ema(2 * ta.ema(close, tema_short_length) - ta.ema(ta.ema(close, tema_short_length), tema_short_length), tema_short_length)
tema_long = ta.ema(2 * ta.ema(close, tema_long_length) - ta.ema(ta.ema(close, tema_long_length), tema_long_length), tema_long_length)

// Plot TEMA
plot(tema_short, color=color.blue, title="300 TEMA")
plot(tema_long, color=color.red, title="500 TEMA")

// Crossover conditions
long_condition = ta.crossover(tema_short, tema_long)
short_condition = ta.crossunder(tema_short, tema_long)

// Calculate recent swing high/low
swing_low = ta.lowest(low, 10)
swing_high = ta.highest(high, 10)

// Convert pips to price
pip_adjustment = pip_value * syminfo.mintick

// Long entry logic
if (long_condition and strategy.position_size == 0)
    stop_loss_long = swing_low - pip_adjustment
    strategy.entry("Long", strategy.long)
    label.new(bar_index, swing_low, style=label.style_label_down, text="Buy", color=color.green)

// Short entry logic
if (short_condition and strategy.position_size == 0)
    stop_loss_short = swing_high + pip_adjustment
    strategy.entry("Short", strategy.short)
    label.new(bar_index, swing_high, style=label.style_label_up, text="Sell", color=color.red)

// Exit logic
if (strategy.position_size > 0 and short_condition)
    strategy.close("Long")
    label.new(bar_index, high, style=label.style_label_up, text="Exit Long", color=color.red)

if (strategy.position_size < 0 and long_condition)
    strategy.close("Short")
    label.new(bar_index, low, style=label.style_label_down, text="Exit Short", color=color.green)

```

> Detail

https://www.fmz.com/strategy/477556

> Last Modified

2025-01-06 13:53:11

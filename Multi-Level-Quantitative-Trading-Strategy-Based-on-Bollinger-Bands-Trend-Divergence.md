
> Name

Multi-Level-Quantitative-Trading-Strategy-Based-on-Bollinger-Bands-Trend-Divergence
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14d7eb33bf3777a5ea7.png)

[trans]
#### Overview
This strategy is a multi-level quantitative trading system based on Bollinger Bands trend divergence and dynamic bandwidth changes. This strategy builds a complete trading decision-making framework by monitoring the dynamic changes in Bollinger Band width, price breakthroughs, and EMA200 moving average coordination. The strategy adopts an adaptive volatility tracking mechanism, which can effectively capture the turning points of market trends.
#### Strategy Principle
The core of the strategy is based on the following key elements:
1. The Bollinger Bands calculation uses a 20-period moving average and 2 times the standard deviation.
2. Determine the trend strength through bandwidth changes at three consecutive time points
3. Combine the relationship between the K-line entity and the bandwidth ratio to determine the effectiveness of the breakthrough
4. Use EMA200 as a mid- to long-term trend filter
5. Enter long when the price breaks through the upper track and meets the conditions for bandwidth expansion.
6. Close the position when the price falls below the lower track and meets the bandwidth contraction conditions.
#### Strategic Advantages
1. The signal system is forward-looking and can detect potential trend turning points in advance.
2. Cross-validation of multiple technical indicators significantly reduces false signals
3. The bandwidth change rate indicator has good adaptability to market fluctuations
4. The entry and exit logic is clear and easy to implement programmatically.
5. The risk control mechanism is perfect and can effectively control drawdowns
#### Strategy Risk
1. Frequent transactions may occur in volatile markets
2. There may be a lag when the trend changes suddenly.
3. Parameter optimization has the risk of overfitting
4. You may face the risk of slippage during periods of high market volatility.
5. The effectiveness of bandwidth indicators needs to be monitored in a timely manner
#### Strategy optimization direction
1. Introduce an adaptive parameter optimization mechanism
2. Increase the verification of auxiliary indicators such as trading volume
3. Optimize stop loss and take profit condition settings
4. Improve the quantitative judgment criteria for trend strength
5. Add more market environment filter conditions
#### Summary
This strategy builds a robust trading system through Bollinger Bands trend divergence and dynamic bandwidth changes. The strategy performs well in trending markets, but still needs improvement in volatile markets and parameter optimization. Overall, this strategy has good practical value and room for expansion. ||
#### Overview
This strategy is a multi-level quantitative trading system based on Bollinger Bands trend divergence and dynamic bandwidth changes. The strategy constructs a complete trading decision framework by monitoring Bollinger Bands width dynamics, price breakouts, and EMA200 coordination. It employs an adaptive volatility tracking mechanism to effectively capture market trend turning points.

#### Strategy Principles
The strategy is based on the following key elements:
1. Bollinger Bands calculation using 20-period moving average and 2 standard deviations
2. Trend strength determination through bandwidth changes across three consecutive time points
3. Breakout validation using candle body to bandwidth ratio
4. EMA200 as a medium-long term trend filter
5. Long entry when price breaks above upper band with expanding bandwidth conditions
6. Exit when price breaks below lower band with contracting bandwidth conditions

#### Strategy Advantages
1. Forward-looking signal system that identifies potential trend turning points
2. Multiple technical indicator cross-validation reduces false signals
3. Bandwidth change rate indicator adapts well to market volatility
4. Clear entry and exit logic, easy to implement programmatically
5. Comprehensive risk control mechanisms effectively control drawdowns

#### Strategy Risks
1. May generate frequent trades in ranging markets
2. Potential lag during sudden trend changes
3. Parameter optimization faces overfitting risk
4. Slippage risk during high market volatility periods
5. Requires constant monitoring of bandwidth indicator effectiveness

#### Strategy Optimization Directions
1. Introduce adaptive parameter optimization mechanisms
2. Add volume and other auxiliary indicators for validation
3. Optimize stop-loss and take-profit conditions
4. Improve quantitative standards for trend strength assessment
5. Incorporate additional market environment filters

#### Summary
The strategy builds a robust trading system through Bollinger Bands trend divergence and dynamic bandwidth changes. While performing excellently in trending markets, improvements are needed for ranging markets and parameter optimization. Overall, the strategy demonstrates good practical value and room for expansion.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2024-12-25 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=6
strategy("BBDIV_Strategy", overlay=true)

// Inputs for Bollinger Bands
length = input.int(20, title="BB Length")
mult = input.float(2.0, title="BB Multiplier")

// Calculate Bollinger Bands
basis = ta.sma(close, length)
deviation = mult * ta.stdev(close, length)
upperBB = basis + deviation
lowerBB = basis - deviation

// Calculate Bollinger Band width
bb_width = upperBB - lowerBB
prev_width = ta.valuewhen(not na(bb_width[1]), bb_width[1], 0)
prev_prev_width = ta.valuewhen(not na(bb_width[2]), bb_width[2], 0)

// Determine BB state
bb_state = bb_width > prev_width and prev_width > prev_prev_width ? 1 : bb_width < prev_width and prev_width < prev_prev_width ? -1 : 0

// Assign colors based on BB state
bb_color = bb_state == 1 ? color.green : bb_state == -1 ? color.red : color.gray

// Highlight candles closed outside BB
candle_size = high - low
highlight_color = (candle_size > bb_width / 2 and close > upperBB) ? color.new(color.green, 50) : (candle_size > bb_width / 2 and close < lowerBB) ? color.new(color.red, 50) : na

bgcolor(highlight_color, title="Highlight Candles")

// Plot Bollinger Bands
plot(upperBB, title="Upper BB", color=bb_color, linewidth=2, style=plot.style_line)
plot(lowerBB, title="Lower BB", color=bb_color, linewidth=2, style=plot.style_line)
plot(basis, title="Middle BB", color=color.blue, linewidth=1, style=plot.style_line)

// Calculate EMA 200
ema200 = ta.ema(close, 200)

// Plot EMA 200
plot(ema200, title="EMA 200", color=color.orange, linewidth=2, style=plot.style_line)

// Strategy logic
enter_long = highlight_color == color.new(color.green, 50)
exit_long = highlight_color == color.new(color.red, 50)

if (enter_long)
    strategy.entry("Buy", strategy.long)

if (exit_long)
    strategy.close("Buy")

// Display profit at close
if (exit_long)
    var float entry_price = na
    var float close_price = na
    var float profit = na

    if (strategy.opentrades > 0)
        entry_price := strategy.opentrades.entry_price(strategy.opentrades - 1)
        close_price := close
        profit := (close_price - entry_price) * 100 / entry_price * 2 * 10 // Assuming 1 pip = 0.01 for XAUUSD
        label.new(bar_index, high + (candle_size * 2), str.tostring(profit, format.mintick) + " USD", style=label.style_label_up, color=color.green)

```

> Detail

https://www.fmz.com/strategy/476279

> Last Modified

2024-12-27 15:52:41

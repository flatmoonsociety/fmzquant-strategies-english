
> Name

Multi-Order-Breakout-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/12571119aac50b1588c.png)

[trans]
#### Overview
The multi-order breakout trend following strategy is a quantitative trading strategy based on technical analysis indicators, designed to capture market trends and make multiple entries at favorable opportunities. This strategy combines multiple indicators such as Bollinger Bands, Average True Range (ATR), Parabolic Reversal Index (SAR) and Exponential Moving Average (EMA), and determines entry and exit timing through multiple conditional screening. The core idea of ​​the strategy is to open a long position when it breaks through the upper Bollinger Band and meets other conditions, while using dynamic position management and fixed percentage stop loss to control risks. In addition, the strategy also sets a limit on the maximum number of positions to avoid excessive concentration risks.
#### Strategy Principle
1. Admission conditions:
   - Price breaks above the upper Bollinger Band
   - Price is higher than the SAR indicator
   - Price is above EMA
   - ATR is above its 100-period simple moving average
   - The current open position quantity is less than the maximum allowed position number
2. Entry conditions:
   - Price fell below the middle track of Bollinger Bands
   - Price falls below the SAR indicator
3. Position management:
   - Dynamic position calculation based on account equity, risk percentage for each trade and stop loss ratio
   -Set maximum opening quantity limit
4. Risk control:
   - Set a fixed percentage stop loss on each order
   - Use the ATR indicator to filter low volatility markets
5. Indicator application:
   - Bollinger Bands: used to determine price breakthroughs and pullbacks
   - SAR: assists in judging trend direction and exit timing
   - EMA: used to confirm mid- to long-term trends
   - ATR: Determine market volatility and filter low-volatility markets
#### Strategic Advantages
1. Multiple confirmation mechanism: By combining multiple technical indicators, the reliability of entry signals is improved and the risk of false breakthroughs is reduced.
2. Dynamic position management: Dynamically adjust the position size based on account equity, risk tolerance and market volatility, which can not only effectively control risks, but also obtain greater returns in favorable market conditions.
3. Balancing trend tracking and risk control: While tracking the trend, the strategy controls risks by setting stop losses and maximum positions, achieving a balance between returns and risks.
4. Strong adaptability: Through parametric design, the strategy can be flexibly adjusted according to different market environments and traders' risk preferences.
5. Volatility filtering: Using the ATR indicator to filter low-volatility markets helps avoid frequent trading when the market lacks a clear direction.
6. Multiple entry opportunities: multiple positions are allowed in the same trend, which is conducive to obtaining more profits in a strong trend.
#### Strategy Risk
1. Over-trading risk: In a volatile market, frequent false breakthrough signals may occur, leading to over-trading and increased transaction costs.
2. Slippage and liquidity risk: In rapid market conditions, you may face severe slippage or insufficient liquidity, which will affect the effectiveness of strategy execution.
3. Trend reversal risk: Although stop loss is set, you may still suffer large losses in a violent trend reversal.
4. Parameter sensitivity: Strategy performance may be more sensitive to parameter settings, and parameters may need to be adjusted frequently under different market environments.
5. Systemic risk: Holding multiple highly correlated positions at the same time may suffer systemic risks when the market fluctuates violently.
6. Retracement risk: In long-term sideways or volatile markets, you may face greater retracement risk.
#### Strategy optimization direction
1. Introduce market regime recognition: Develop a market status recognition module to dynamically adjust strategy parameters or switch trading modes according to different market environments (trends, shocks, high volatility, etc.).
2. Optimize the exit mechanism: Consider introducing trailing stop or dynamic stop loss based on ATR to better lock in profits and adapt to market fluctuations.
3. Add trading time filtering: analyze the market characteristics of different time periods, avoid inefficient trading times, and improve the overall efficiency of the strategy.
4. Add counter-trend operations: On the basis of the main trend strategy, increase the certainty of short-term reversal, such as considering reverse trading when hitting the lower Bollinger Band.
5. Optimize position management: Consider dynamically adjusting positions according to trend strength, increasing positions in stronger trends and reducing positions in weak trends.
6. Introduce fundamental factors: Combine with fundamental indicators (such as economic data releases, major events, etc.) to filter or enhance trading signals.
7. Multi-period analysis: Introduce multi-period analysis to ensure that it is consistent with the trend direction in a larger time frame.
8. Correlation management: Develop a module to monitor and manage the correlation between different trading varieties to better diversify risks.
9. Machine learning optimization: Use machine learning algorithms to optimize parameter selection and signal generation processes to improve the adaptability and performance of the strategy.
#### Summarize
The multi-order breakout trend following strategy is a quantitative trading system that combines multiple technical indicators. Through strict entry conditions and risk management measures, it aims to capture market trends and control risks. The core advantages of this strategy are its multiple confirmation mechanism, dynamic position management and adaptability to market fluctuations. However, it also faces challenges such as over-trading, parameter sensitivity and systemic risks.
Through further optimization, such as introducing market regime recognition, improving the exit mechanism, adding trading time filtering, etc., the robustness and profitability of the strategy can be improved. At the same time, adding fundamental factors and using machine learning technology is expected to make the strategy better adaptable to different market environments.
Overall, this strategy provides a good starting point for trend following trading, and with continued monitoring, backtesting, and optimization, it has the potential to become a reliable quantitative trading strategy. However, when using this strategy, investors still need to carefully assess their risk tolerance and conduct sufficient simulation tests before real trading.
|| 

#### Overview

The Multi-Order Breakout Trend Following Strategy is a quantitative trading strategy based on technical analysis indicators, designed to capture market trends and enter positions multiple times during favorable conditions. This strategy combines several indicators including Bollinger Bands, Average True Range (ATR), Parabolic SAR, and Exponential Moving Average (EMA) to determine entry and exit points through multiple condition screenings. The core idea is to open long positions when the price breaks above the upper Bollinger Band and meets other conditions, while employing dynamic position sizing and fixed percentage stop-loss to control risk. Additionally, the strategy sets a maximum limit on the number of open positions to avoid excessive concentration of risk.

#### Strategy Principles

1. Entry Conditions:
   - Price breaks above the upper Bollinger Band
   - Price is above the SAR indicator
   - Price is above the EMA
   - ATR is above its 100-period simple moving average
   - Current number of open positions is less than the maximum allowed

2. Exit Conditions:
   - Price falls below the middle Bollinger Band
   - Price falls below the SAR indicator

3. Position Management:
   - Uses dynamic position sizing based on account equity, risk per trade, and stop-loss percentage
   - Sets a maximum limit on the number of open positions

4. Risk Control:
   - Applies a fixed percentage stop-loss for each order
   - Uses the ATR indicator to filter out low volatility market conditions

5. Indicator Application:
   - Bollinger Bands: Used to judge price breakouts and retracements
   - SAR: Assists in determining trend direction and exit timing
   - EMA: Confirms medium to long-term trends
   - ATR: Judges market volatility and filters out low volatility conditions

#### Strategy Advantages

1. Multiple Confirmation Mechanism: By combining multiple technical indicators, it increases the reliability of entry signals and reduces risks from false breakouts.

2. Dynamic Position Sizing: Adjusts position size dynamically based on account equity, risk tolerance, and market volatility, effectively controlling risk while allowing for larger gains in favorable market conditions.

3. Balance Between Trend Following and Risk Control: The strategy tracks trends while controlling risk through stop-losses and maximum position limits, achieving a balance between returns and risk.

4. High Adaptability: Through parameterized design, the strategy can be flexibly adjusted according to different market environments and trader risk preferences.

5. Volatility Filtering: Uses the ATR indicator to filter out low volatility market conditions, helping to avoid frequent trading when the market lacks clear direction.

6. Multiple Entry Opportunities: Allows for multiple entries within the same trend, beneficial for capturing more profits in strong trend movements.

#### Strategy Risks

1. Overtrading Risk: In oscillating markets, frequent false breakout signals may lead to overtrading and increased transaction costs.

2. Slippage and Liquidity Risk: In fast-moving markets, severe slippage or insufficient liquidity issues may affect strategy execution effectiveness.

3. Trend Reversal Risk: Although stop-losses are set, significant losses may still occur during severe trend reversals.

4. Parameter Sensitivity: Strategy performance may be sensitive to parameter settings, potentially requiring frequent adjustments in different market environments.

5. Systemic Risk: Holding multiple highly correlated positions simultaneously may expose the strategy to systemic risk during extreme market volatility.

6. Drawdown Risk: In long-term sideways or oscillating markets, the strategy may face significant drawdown risks.

#### Strategy Optimization Directions

1. Introduce Market Regime Recognition: Develop a market state recognition module to dynamically adjust strategy parameters or switch trading modes based on different market environments (trending, oscillating, high volatility, etc.).

2. Optimize Exit Mechanism: Consider introducing trailing stops or ATR-based dynamic stop-losses to better lock in profits and adapt to market volatility.

3. Add Trading Time Filters: Analyze market characteristics during different time periods to avoid inefficient trading times and improve overall strategy efficiency.

4. Incorporate Counter-Trend Operations: On the basis of the main trend strategy, add capabilities to capture short-term reversals, such as considering counter-trend trades when touching the lower Bollinger Band.

5. Enhance Position Management: Consider dynamically adjusting positions based on trend strength, increasing positions in stronger trends and reducing them in weaker ones.

6. Integrate Fundamental Factors: Combine fundamental indicators (such as economic data releases, major events) to filter or enhance trading signals.

7. Multi-Timeframe Analysis: Introduce multi-timeframe analysis to ensure trend alignment in larger time frames.

8. Correlation Management: Develop a module to monitor and manage correlations between different trading instruments for better risk diversification.

9. Machine Learning Optimization: Utilize machine learning algorithms to optimize parameter selection and signal generation processes, improving strategy adaptability and performance.

#### Conclusion

The Multi-Order Breakout Trend Following Strategy is a quantitative trading system that combines multiple technical indicators, aiming to capture market trends and control risk through strict entry conditions and risk management measures. The core advantages of this strategy lie in its multiple confirmation mechanisms, dynamic position management, and adaptability to market volatility. However, it also faces challenges such as overtrading, parameter sensitivity, and systemic risks.

Through further optimization, such as introducing market regime recognition, improving exit mechanisms, and adding trading time filters, the strategy's robustness and profitability can be enhanced. Additionally, incorporating fundamental factors and leveraging machine learning techniques holds the promise of better adapting the strategy to different market environments.

Overall, this strategy provides a good starting point for trend following trading. Through continuous monitoring, backtesting, and optimization, it has the potential to become a reliable quantitative trading strategy. However, investors using this strategy should still carefully assess their own risk tolerance and conduct thorough simulated testing before live trading.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-06-29 00:00:00
end: 2024-07-29 00:00:00
period: 3h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Multi-Order Breakout Strategy", overlay=true)

// Parameters
risk_per_trade = input.float(1.0, "Risk Per Trade")
lookback = input(20, "Lookback Period")
breakout_mult = input.float(2.0, "Breakout Multiplier")
stop_loss_percent = input.float(2.0, "Stop Loss Percentage")
max_positions = input(5, "Maximum Open Positions")
atr_period = input(14, "ATR Period")
ma_len = input(100, "MA Length")

// Calculate Bollinger Bands and other indicators
[middle, upper, lower] = ta.bb(close, lookback, breakout_mult)
atr = ta.atr(atr_period)
sar = ta.sar(0.02, 0.02, 0.2)

ma = ta.ema(close, ma_len)
plot(ma, color=color.white)

// Entry conditions
long_condition = close > upper and close > sar and close > ma

// Exit conditions
exit_condition = ta.crossunder(close, middle) or ta.crossunder(close, sar)

// Count open positions
var open_positions = 0

// Dynamic position sizing
position_size = (strategy.equity * risk_per_trade/100) / (close * stop_loss_percent / 100)


// Strategy execution
if (long_condition and open_positions < max_positions and atr > ta.sma(atr, 100) and position_size > 0)
    strategy.entry("Long " + str.tostring(open_positions + 1), strategy.long, qty=position_size)
    open_positions := open_positions + 1

// Apply fixed stop loss to each position
for i = 1 to max_positions
    strategy.exit("SL " + str.tostring(i), "Long " + str.tostring(i), stop=strategy.position_avg_price * (1 - stop_loss_percent/100))

// Close all positions on exit condition
if (exit_condition and open_positions > 0)
    strategy.close_all()
    open_positions := 0

// Plot
plot(upper, "Upper BB", color.blue)
plot(lower, "Lower BB", color.blue)
plot(middle, "Middle BB", color.orange)
plot(sar, "SAR", color.purple, style=plot.style_cross)
```

> Detail

https://www.fmz.com/strategy/458200

> Last Modified

2024-07-30 17:18:11

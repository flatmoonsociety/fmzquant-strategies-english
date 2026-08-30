
> Name

Trend-Detection-Strategy-Based-on-Gaussian-Channel-and-Stochastic-RSI-Filter
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d8885839dcde31be1d7a.png)
![IMG](https://www.fmz.com/upload/asset/2d818261c73a59de1f53c.png)



[trans]
#### Overview
This strategy is a trend following trading system that combines Gaussian Channels and Stochastic RSI. The Gaussian Channel is used to identify price trends and ranges, while the Stochastic RSI acts as a filter to confirm overbought and oversold conditions, thereby increasing the accuracy of trading signals. The strategy generates trading signals by observing price crossings of Gaussian channel boundaries and the position of the Stochastic RSI.
#### Strategy Principle
The core logic of the strategy is based on the following key components:
1. Gaussian channel calculation: Use Gaussian filter to calculate the center line, and set the upper and lower channel bands based on the multiplier. Gaussian filter uses exponential smoothing method, which can effectively reduce price noise.
2. Stochastic RSI indicator: combines the advantages of stochastic indicator and RSI, and identifies overbought and oversold conditions through two smooth lines of %K and %D.
3. Admission conditions:
   - Bulls: Price breaks below the lower band of the Gaussian Channel and Stochastic RSI is in oversold territory
   - Bears: The price breaks below the upper band of the Gaussian Channel and the Stochastic RSI is in the overbought zone
4. Entry conditions:
   - When price crosses the center line of the Gaussian Channel
   - Or Stochastic RSI reaches opposite overbought and oversold levels
#### Strategic Advantages
1. High signal reliability: combined with trend and momentum indicators, it can effectively filter out false signals
2. Improved risk control: using the Gaussian channel as a dynamic support pressure level provides a good risk management framework
3. Strong parameter adjustability: channel width and RSI parameters can be adjusted according to different market characteristics
4. High computational efficiency: Gaussian filter requires less calculation and is suitable for real-time trading.
5. Strong adaptability: can be used in different time periods and market environments
#### Strategy Risk
1. Risk of market shock: Frequent false breakthrough signals may occur in sideways markets
2. Hysteresis risk: Indicator smoothing will cause a certain signal delay
3. Parameter sensitivity: Different parameter combinations may lead to significantly different trading results.
4. Dependence on market environment: It performs better in strong trending markets, but may cause larger retracements in rapidly reversing markets.
#### Strategy optimization direction
1. Dynamic parameter optimization:
   - Adaptively adjust channel width based on market volatility
   - Dynamically adjust Stochastic RSI parameters based on market cycle characteristics
2. Signal confirmation mechanism:
   - Added volume confirmation indicator
   - Introduced trend strength filter
3. Enhanced risk management:
   - Implement dynamic stop loss and take profit
   - Added position management module
4. Market environment identification:
   - Develop market state classifiers
   - Adjust strategy parameters according to different market conditions
#### Summary
This strategy combines Gaussian Channel and Stochastic RSI to build a trading system with both trend following and momentum characteristics. The strategy design is reasonable and has good scalability and adaptability. Through the suggested optimization direction, the stability and profitability of the strategy can be further improved. In practical applications, it is recommended to fully test different parameter combinations and carry out targeted optimization according to specific market characteristics. ||
#### Overview
This strategy is a trend-following trading system that combines Gaussian Channel and Stochastic RSI. The Gaussian Channel is used to identify price trends and volatility ranges, while the Stochastic RSI serves as a filter to confirm overbought/oversold conditions, thereby improving the accuracy of trading signals. The strategy generates trading signals by observing price crosses with Gaussian Channel boundaries and Stochastic RSI positions.

#### Strategy Principle
The core logic of the strategy is based on the following key components:
1. Gaussian Channel Calculation: Uses Gaussian filter to calculate the midline and sets channel bands based on multipliers. The Gaussian filter employs exponential smoothing to effectively reduce price noise.
2. Stochastic RSI Indicator: Combines the advantages of Stochastic and RSI indicators, using %K and %D smoothed lines to identify overbought/oversold conditions.
3. Entry Conditions:
   - Long: Price breaks above the lower Gaussian band and Stochastic RSI is in oversold territory
   - Short: Price breaks below the upper Gaussian band and Stochastic RSI is in overbought territory
4. Exit Conditions:
   - When price crosses the Gaussian Channel midline
   - Or when Stochastic RSI reaches opposite overbought/oversold levels

#### Strategy Advantages
1. High Signal Reliability: Combines trend and momentum indicators to effectively filter false signals
2. Robust Risk Control: Uses Gaussian Channel as dynamic support/resistance levels, providing a solid risk management framework
3. Strong Parameter Adaptability: Can adjust channel width and RSI parameters for different market characteristics
4. High Computational Efficiency: Gaussian filter requires minimal computation, suitable for real-time trading
5. Strong Adaptability: Can be used across different timeframes and market environments

#### Strategy Risks
1. Choppy Market Risk: May generate frequent false breakout signals in sideways markets
2. Lag Risk: Indicator smoothing leads to certain signal delays
3. Parameter Sensitivity: Different parameter combinations may lead to significantly different trading results
4. Market Environment Dependency: Performs well in strong trends but may experience larger drawdowns in quick reversal markets

#### Strategy Optimization Directions
1. Dynamic Parameter Optimization:
   - Adapt channel width based on market volatility
   - Dynamically adjust Stochastic RSI parameters based on market cycle characteristics
2. Signal Confirmation Mechanism:
   - Add volume confirmation indicators
   - Introduce trend strength filters
3. Risk Management Enhancement:
   - Implement dynamic stop-loss and take-profit
   - Add position management module
4. Market Environment Recognition:
   - Develop market state classifier
   - Adjust strategy parameters based on different market states

#### Summary
The strategy builds a trading system combining trend-following and momentum characteristics through the integration of Gaussian Channel and Stochastic RSI. The strategy design is reasonable, with good scalability and adaptability. Through the suggested optimization directions, the strategy's stability and profitability can be further improved. In practical application, it is recommended to thoroughly test different parameter combinations and optimize specifically according to market characteristics.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-01-21 00:00:00
end: 2025-02-20 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=6
strategy("Gaussian Channel + Stochastic RSI Filter", overlay=true, margin_long=100, margin_short=100)

// === INPUTS ===
input_length = input.int(100, title="Gaussian Channel Length", minval=1)
input_mult = input.float(2.0, title="Gaussian Channel Multiplier", minval=0.1, step=0.1)
stoch_rsi_period = input.int(14, title="Stochastic RSI Period", minval=1)
stoch_rsi_smoothK = input.int(3, title="Stochastic RSI Smooth K", minval=1)
stoch_rsi_smoothD = input.int(3, title="Stochastic RSI Smooth D", minval=1)
stoch_rsi_overbought = input.float(80.0, title="Stochastic RSI Overbought Level", minval=0, maxval=100)
stoch_rsi_oversold = input.float(20.0, title="Stochastic RSI Oversold Level", minval=0, maxval=100)

// === GAUSSIAN CHANNEL ===
// Gaussian filter calculation with proper initialization
gauss(src, len) =>
    b = math.exp(-1.414 * 3.14159 / len)
    a0 = 1 - b
    var float f = na
    f := na(f[1]) ? src : a0 * src + b * f[1]

// Calculate Gaussian channel
gaussian_channel_mid = gauss(close, input_length)
gaussian_channel_high = gaussian_channel_mid + gaussian_channel_mid * input_mult / 100
gaussian_channel_low = gaussian_channel_mid - gaussian_channel_mid * input_mult / 100

// Plot Gaussian Channel
plot(gaussian_channel_mid, color=color.blue, linewidth=2, title="Gaussian Channel Midline")
plot(gaussian_channel_high, color=color.green, linewidth=1, title="Gaussian Channel Upper Band")
plot(gaussian_channel_low, color=color.red, linewidth=1, title="Gaussian Channel Lower Band")

// === STOCHASTIC RSI ===
k = ta.sma(ta.stoch(close, high, low, stoch_rsi_period), stoch_rsi_smoothK)
d = ta.sma(k, stoch_rsi_smoothD)
is_oversold = k < stoch_rsi_oversold and d < stoch_rsi_oversold
is_overbought = k > stoch_rsi_overbought and d > stoch_rsi_overbought

// Plot Stochastic RSI
hline(stoch_rsi_overbought, "Overbought", color=color.red, linestyle=hline.style_dotted)
hline(stoch_rsi_oversold, "Oversold", color=color.green, linestyle=hline.style_dotted)
plot(k, color=color.blue, title="Stochastic RSI %K")
plot(d, color=color.orange, title="Stochastic RSI %D")

// === ENTRY AND EXIT LOGIC ===
// Long entry: Price crosses above Gaussian Channel lower band and Stochastic RSI is oversold
long_condition = ta.crossover(close, gaussian_channel_low) and is_oversold

// Short entry: Price crosses below Gaussian Channel upper band and Stochastic RSI is overbought
short_condition = ta.crossunder(close, gaussian_channel_high) and is_overbought

// Exit logic
long_exit = ta.crossunder(close, gaussian_channel_mid) or is_overbought
short_exit = ta.crossover(close, gaussian_channel_mid) or is_oversold

// Execute trades
if (long_condition)
    strategy.entry("Long", strategy.long)

if (short_condition)
    strategy.entry("Short", strategy.short)

if (long_exit)
    strategy.close("Long")

if (short_exit)
    strategy.close("Short")

// === SETTINGS ===
// Backtest date range
start_date = timestamp(2023, 1, 1, 0, 0)
end_date = timestamp(2069, 1, 1, 0, 0)
if (time < start_date or time > end_date)
    strategy.close_all()
```

> Detail

https://www.fmz.com/strategy/483073

> Last Modified

2025-02-21 11:42:36

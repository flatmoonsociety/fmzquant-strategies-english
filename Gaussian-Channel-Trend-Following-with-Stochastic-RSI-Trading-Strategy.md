
> Name

Gaussian-Channel-Trend-Following-with-Stochastic-RSI-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d87428f0719943d31996.png)
![IMG](https://www.fmz.com/upload/asset/2d8e546bc7dc4b1151ee9.png)



[trans]
#### Overview
This strategy is a trend following trading system that combines Gaussian Weighted Moving Average channels with the Stochastic RSI. The strategy constructs a price channel through the Gaussian weighting method, and combines the cross signals of the stochastic RSI indicator to determine the timing of entry and exit, so as to grasp the trend and confirm the momentum. This strategy has a good mathematical foundation and can effectively filter market noise and capture the main trends.
#### Strategy Principle
The core logic of the strategy consists of two main parts:
1. Gaussian Channel System: Construct price channels using Gaussian Weighted Moving Average (GWMA) and Gaussian Weighted Standard Deviation (GWSD). GWMA gives more weight to recent data, making the moving average more responsive to price changes. The upper and lower channel rails are determined by multiplying the GWSD by a multiplication factor.
2. Stochastic RSI system: Randomize the traditional RSI indicator and calculate the K value and D value. This processing method can better identify overbought and oversold areas and provide more accurate momentum signals.
Trading signals are generated based on the following conditions:
- Long entry: the price closes above the upper rail of the Gaussian channel and the K line of the stochastic RSI crosses the D line
- Closing signal: the price closes below the upper track of the Gaussian channel
#### Strategic Advantages
1. Solid mathematical foundation: The Gaussian weighting method is used to construct the price channel, which has a better theoretical foundation than the simple moving average.
2. High signal reliability: The dual verification mechanism combined with price breakthrough and momentum confirmation can effectively reduce false signals.
3. Strong adaptability: Gaussian weighting method can automatically adjust the channel width according to market fluctuations.
4. Improved risk control: Through fund management and commission setting, effective control of transaction costs and risks is achieved.
#### Strategy Risk
1. Trend dependence: Frequent false signals may occur in volatile markets, leading to over-trading.
2. Hysteresis effect: Due to the use of multiple moving average smoothing, signal lags may occur at trend turning points.
3. Parameter sensitivity: The effect of the strategy is greatly affected by parameter settings, and each parameter needs to be carefully optimized.
#### Strategy optimization direction
1. Market environment identification: Add a market environment judgment mechanism and use different parameter settings under different market conditions.
2. Stop loss optimization: Introduce dynamic stop loss mechanism, such as adaptive stop loss based on ATR or volatility.
3. Signal filtering: Add trading volume confirmation or other technical indicators as auxiliary filtering conditions.
4. Fund management: Implement a more flexible position management strategy and dynamically adjust the position ratio based on signal strength.
#### Summary
This strategy builds a trend following system with a solid mathematical foundation by combining the Gaussian Channel and the Stochastic RSI indicator. The strategy performs well in markets with obvious trends, but attention needs to be paid to parameter optimization and adaptability to the market environment. By implementing the recommended optimization measures, the stability and profitability of the strategy can be further improved. ||
#### Overview
This strategy combines a Gaussian Weighted Moving Average Channel with the Stochastic Relative Strength Index (Stochastic RSI) to create a trend-following trading system. The strategy uses Gaussian weighting methods to construct a price channel and combines it with Stochastic RSI crossover signals to determine entry and exit points, effectively capturing trends and confirming momentum. The strategy has a solid mathematical foundation and effectively filters market noise while capturing major trends.

#### Strategy Principles
The core logic consists of two main components:
1. Gaussian Channel System: Uses Gaussian Weighted Moving Average (GWMA) and Gaussian Weighted Standard Deviation (GWSD) to construct a price channel. GWMA assigns higher weights to recent data, making the moving average more responsive to price changes. The channel bands are determined by multiplying the GWSD by a factor.

2. Stochastic RSI System: Applies stochastic calculations to the traditional RSI indicator to compute K and D values. This processing method better identifies overbought and oversold areas, providing more accurate momentum signals.

Trading signals are generated based on the following conditions:
- Long Entry: Price closes above the upper Gaussian channel band AND Stochastic RSI K-line crosses above D-line
- Exit Signal: Price closes below the upper Gaussian channel band

#### Strategy Advantages
1. Solid Mathematical Foundation: Uses Gaussian weighting methods to construct price channels, providing better theoretical basis than simple moving averages.
2. High Signal Reliability: Combines price breakout and momentum confirmation as dual verification mechanism, effectively reducing false signals.
3. Strong Adaptability: Gaussian weighting method automatically adjusts channel width based on market volatility.
4. Comprehensive Risk Control: Implements effective control over trading costs and risks through money management and commission settings.

#### Strategy Risks
1. Trend Dependency: May generate frequent false signals in ranging markets, leading to overtrading.
2. Lag Effect: Multiple moving average smoothing may result in delayed signals at trend turning points.
3. Parameter Sensitivity: Strategy performance is highly dependent on parameter settings, requiring careful optimization.

#### Optimization Directions
1. Market Environment Recognition: Add market state identification mechanism to use different parameter settings in different market conditions.
2. Stop Loss Optimization: Introduce dynamic stop loss mechanism, such as ATR-based or volatility-based adaptive stops.
3. Signal Filtering: Add volume confirmation or other technical indicators as auxiliary filtering conditions.
4. Money Management: Implement more flexible position management strategies, adjusting position sizes dynamically based on signal strength.

#### Summary
This strategy combines Gaussian channels and Stochastic RSI indicators to build a trend-following system with solid mathematical foundations. The strategy performs excellently in trending markets but requires attention to parameter optimization and market environment adaptability. Through implementing the suggested optimization measures, the strategy's stability and profitability can be further enhanced.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-21 00:00:00
end: 2025-02-18 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("Gaussian Channel + Stoch RSI Strategy", overlay=true, margin_long=100, margin_short=100, initial_capital=100000, commission_type=strategy.commission.percent, commission_value=0.1, default_qty_type=strategy.percent_of_equity, default_qty_value=100, pyramiding=1)

// User Inputs
length     = input.int(20, "Gaussian Length", minval=5)
multiplier = input.float(2.0, "Channel Multiplier", step=0.1)
rsiLength  = input.int(14, "RSI Length", minval=1)
stochLength= input.int(14, "Stoch RSI Length", minval=1)
kLength    = input.int(3, "Stoch K Smoothing", minval=1)
dLength    = input.int(3, "Stoch D Smoothing", minval=1)

// Gaussian Weighted Moving Average Function
f_gaussian(source, length) =>
    half = (length - 1) / 2.0
    sum = 0.0
    norm = 0.0
    // Gaussian standard deviation chosen as length/6 for a smooth curve
    denom = (length / 6.0) * (length / 6.0)
    for i = 0 to length - 1
        x = i - half
        w = math.exp(-(x * x) / (2 * denom))
        sum += source[i] * w
        norm += w
    sum / norm

// Gaussian Weighted Standard Deviation Function
f_gaussian_std(source, length) =>
    half = (length - 1) / 2.0
    gavg = f_gaussian(source, length)
    sum = 0.0
    norm = 0.0
    denom = (length / 6.0) * (length / 6.0)
    for i = 0 to length - 1
        x = i - half
        w = math.exp(-(x * x)/(2*denom))
        diff = source[i] - gavg
        sum += diff * diff * w
        norm += w
    math.sqrt(sum/norm)

// Compute Gaussian Channel
gaussMid = f_gaussian(close, length)
gaussStd = f_gaussian_std(close, length)
gaussUpper = gaussMid + gaussStd * multiplier
gaussLower = gaussMid - gaussStd * multiplier

// Stochastic RSI Calculation
rsi = ta.rsi(close, rsiLength)
rsiLowest = ta.lowest(rsi, stochLength)
rsiHighest = ta.highest(rsi, stochLength)
stoch = 100 * (rsi - rsiLowest) / math.max(rsiHighest - rsiLowest, 1e-10)
k = ta.sma(stoch, kLength)
d = ta.sma(k, dLength)

// Conditions
// Long entry: Price closes above upper Gaussian line AND Stoch RSI K > D (stochastic is "up")
longCondition = close > gaussUpper and k > d

// Exit condition: Price closes below upper Gaussian line
exitCondition = close < gaussUpper

// Only trade in the specified date range
inDateRange = time >= timestamp("2018-01-01T00:00:00") and time < timestamp("2069-01-01T00:00:00")

// Submit Orders
if inDateRange
    if longCondition and strategy.position_size <= 0
        strategy.entry("Long", strategy.long)
    if exitCondition and strategy.position_size > 0
        strategy.close("Long")
        
// Plot Gaussian Channel
plot(gaussMid, "Gaussian Mid", color=color.new(color.yellow, 0))
plot(gaussUpper, "Gaussian Upper", color=color.new(color.green, 0))
plot(gaussLower, "Gaussian Lower", color=color.new(color.red, 0))

```

> Detail

https://www.fmz.com/strategy/482786

> Last Modified

2025-02-20 11:01:36

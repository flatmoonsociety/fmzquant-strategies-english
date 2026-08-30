
> Name

Multi-timeframe-Trend-Tracking-Strategy-Based-on-Impulse-MACD-and-Dual-Moving-Average-Crossover
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f0140b1aacffa692b4.png)

[trans]
#### Overview
This strategy uses a variety of moving average indicators, including SMMA, SMA, ZLEMA and EMA, and builds an improved MACD indicator (Impulse MACD) based on them, which generates trading signals through the intersection of Impulse MACD and its signal line. The main idea of ​​the strategy is to use moving averages on different time scales to capture market trends, while using Impulse MACD to confirm the strength and direction of the trend.
#### Strategy Principle
1. Calculate the SMMA and ZLEMA of the high price, low price and closing price with a length of 34, and get the Impulse MACD (MD).
2. Calculate the 9-period SMA of Impulse MACD as the signal line (SB).
3. Calculate the difference (SH) between the Impulse MACD and the signal line to reflect the trend strength.
4. A buy signal is generated when Impulse MACD crosses above the signal line, and the position is closed when it crosses below.
5. Based on the relationship between price, Impulse MACD, and high and low price SMMA, use different colors to draw the Impulse MACD histogram to intuitively reflect the strength of the trend.
#### Strategic Advantages
1. Multiple types of moving averages are used to more comprehensively reflect market trends.
2. The improved MACD indicator (Impulse MACD) takes into account the relative position of price and moving average, which can better reflect the strength of the trend.
3. The introduction of signal lines helps to filter out some false signals and improve signal quality.
4. Draw Impulse MACD in different colors according to the strength of the trend to facilitate intuitive judgment of market trends.
#### Strategy Risk
1. Improper parameter selection may lead to frequent or lagging signals, which need to be optimized according to different markets and cycles.
2. For volatile market conditions, this strategy may generate more false signals and lead to losses.
3. The strategy lacks a stop-loss mechanism and may face a large retracement when encountering violent market conditions.
#### Strategy optimization direction
1. Introduce trend judgment indicators, such as ADX, etc., and only trade when the trend is clear to reduce losses in volatile market conditions.
2. The generated trading signals can be combined with other indicators such as RSI, ATR, etc. for secondary confirmation to improve signal quality.
3. Set reasonable stop loss and take profit levels to control single transaction risks.
4. Optimize parameters, such as using genetic algorithms and other methods to find the optimal parameter combination.
#### Summary
This strategy builds an improved MACD indicator based on various types of moving averages, and uses its intersection with the signal line to generate trading signals. At the same time, it intuitively displays the strength of the trend. The overall idea is clear and the advantages are obvious. However, this strategy also has certain limitations, such as insufficient adaptability to volatile market conditions and lack of risk control measures. You can consider further improving the strategy in terms of trend judgment, signal confirmation, risk control, parameter optimization, etc. to enhance the robustness and profitability of the strategy.
|| 

#### Overview
This strategy utilizes various moving average indicators, including SMMA, SMA, ZLEMA, and EMA, and constructs an improved MACD indicator (Impulse MACD) based on them. It generates trading signals through the crossover of the Impulse MACD and its signal line. The main idea of the strategy is to capture market trends using moving averages of different time frames while confirming the strength and direction of the trend with the Impulse MACD.

#### Strategy Principle
1. Calculate the SMMA and ZLEMA of the high, low, and close prices with a length of 34 to obtain the Impulse MACD (MD).
2. Calculate the 9-period SMA of the Impulse MACD as the signal line (SB).
3. Calculate the difference between the Impulse MACD and the signal line (SH) to reflect the trend strength.
4. Generate a buy signal when the Impulse MACD crosses above the signal line, and close the position when it crosses below.
5. Plot the Impulse MACD histogram with different colors based on the relationship between the price, Impulse MACD, and the high/low price SMMA to visually reflect the trend strength.

#### Strategy Advantages
1. The use of multiple types of moving averages provides a more comprehensive reflection of market trends.
2. The improved MACD indicator (Impulse MACD) takes into account the relative position of price and moving averages, better reflecting the trend strength.
3. The introduction of the signal line helps filter out some false signals and improve signal quality.
4. Plotting the Impulse MACD with different colors based on trend strength facilitates intuitive judgment of market movements.

#### Strategy Risks
1. Improper parameter selection may lead to frequent or lagging signals, requiring optimization based on different markets and timeframes.
2. The strategy may generate more false signals and cause losses in choppy markets.
3. The strategy lacks a stop-loss mechanism and may face significant drawdowns in volatile markets.

#### Strategy Optimization Directions
1. Introduce trend identification indicators such as ADX to only trade when the trend is clear, reducing losses in choppy markets.
2. Confirm the generated trading signals with other indicators such as RSI and ATR to improve signal quality.
3. Set reasonable stop-loss and take-profit levels to control single-trade risk.
4. Optimize parameters using methods such as genetic algorithms to find the optimal parameter combination.

#### Summary
This strategy constructs an improved MACD indicator based on various types of moving averages and generates trading signals through its crossover with the signal line while intuitively displaying trend strength. The overall idea is clear, and the advantages are obvious. However, the strategy also has certain limitations, such as poor adaptability to choppy markets and a lack of risk control measures. Further improvements can be considered from aspects such as trend identification, signal confirmation, risk control, and parameter optimization to enhance the robustness and profitability of the strategy.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-05-11 00:00:00
end: 2024-05-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Impulse MACD Strategy [LazyBear]", shorttitle="IMACD_Strategy", overlay=false)

// Function to calculate SMMA
calc_smma(src, len) =>
    var float smma = na
    smma := na(smma[1]) ? ta.sma(src, len) : (smma[1] * (len - 1) + src) / len
    smma

// Function to calculate SMA
	ta.sma(src, len)
    sum = 0.0
    for i = 0 to len - 1
        sum := sum + src[i]
    sum / len

// Function to calculate ZLEMA
calc_zlema(src, length) =>
    var float ema1 = na
    var float ema2 = na
    var float d = na
    ema1 := ta.ema(src, length)
    ema2 := ta.ema(ema1, length)
    d := ema1 - ema2
    ema1 + d

// Function to calculate EMA
calc_ema(src, len) =>
    ema = 0.0
    ema := ta.ema(src, len)
    ema

// Inputs
lengthMA = input(34, title="Length of Moving Average")
lengthSignal = input(9, title="Length of Signal Line")

// Calculations
src = hlc3
hi = calc_smma(high, lengthMA)
lo = calc_smma(low, lengthMA)
mi = calc_zlema(src, lengthMA) 

md = mi > hi ? (mi - hi) : mi < lo ? (mi - lo) : 0
sb = ta.sma(md, lengthSignal)
sh = md - sb
mdc = src > mi ? src > hi ? color.lime : color.green : src < lo ? color.red : color.orange

// Plotting
plot(0, color=color.gray, linewidth=1, title="MidLine")
plot(md, color=mdc, linewidth=2, title="ImpulseMACD", style=plot.style_histogram)
plot(sh, color=color.blue, linewidth=2, title="ImpulseHisto", style=plot.style_histogram)
plot(sb, color=color.maroon, linewidth=2, title="ImpulseMACDCDSignal")

// Execute trades based on signals
if (ta.crossover(md, sb))
    strategy.entry("Buy", strategy.long)
if (ta.crossunder(md, sb))
    strategy.close("Buy")

```

> Detail

https://www.fmz.com/strategy/451730

> Last Modified

2024-05-17 15:33:02

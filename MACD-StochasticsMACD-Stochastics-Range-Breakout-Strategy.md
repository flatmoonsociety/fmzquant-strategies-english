
> Name

MACD-Stochastics Range Breakout Strategy MACD-Stochastics-Range-Breakout-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/14382de37dfd747d099.png)
[trans]

## Overview
The MACD Stochastics Oscillation Breakout Strategy is a quantitative trading strategy that combines the MACD indicator and the Stochastics indicator. This strategy attempts to identify the trend direction of a stock's price and enter a position when the price breaks out of a volatile range.
When entering a position, this strategy considers the signals of both MACD and Stochastics indicators to improve the quality of Entries. In addition, this strategy has preset stop-loss points and take-profit points, which can effectively control risks.
## Strategy Principle
MACD Stochastics band shock breakthrough strategy is mainly based on the following principles:
1. The MACD indicator can effectively identify the direction and strength of stock price trends.
2. The Stochastics indicator can identify whether a stock is overbought or oversold.
3. When the stock price fluctuates for a long time, it is likely to break through the previous price range and produce a larger directional market.
4. Combining the signals of MACD and Stochastics indicators, you can enter the market in time when the stock breaks through the swing range, improving the quality of entries.
Specifically, this strategy uses the intersection of the DIFF line and the DEA line of the MACD indicator as a signal to determine the direction of the price trend. When DIFF breaks through DEA ​​upward, a long signal is generated, otherwise a short signal is generated.
At the same time, trading signals will also be generated when the Stochastics K line crosses the D line upward or downward near the overbought and oversold areas (default 30 and 70).
This strategy will choose to enter when the MACD indicator and the Stochastics indicator give signals in the same direction at the same time. At this time, the stock price is likely to have a major breakthrough.
After entering the market, the strategy will set rational stop loss points and take profit points. A reasonable stop loss can effectively control a single loss, and a stop profit can lock in profits.

## Advantage Analysis
The MACD Stochastics swing breakout strategy has the following advantages:
1. Multi-indicator combination to improve signal quality
This strategy uses two indicators, MACD and Stochastics, to filter out some false signals and improve the quality of entries.
2. Seize the breakthrough market and follow the trend
The strategy is specifically designed to capture breakouts after long periods of volatile stock prices. This type of market range is usually larger.
3. Optimize the stop-loss and stop-profit mechanism to effectively control risks
The strategy has built-in stop-loss and take-profit settings, which can reasonably control single losses and lock in profits in a timely manner.
## Risk Analysis
Although the MACD Stochastics swing breakout strategy has been carefully designed, there are still certain risks:
1. Miss the opportunity to enter the market
There may be some false breakthroughs before the stock price breaks through. Improper entry timing may result in missing the best entry point.
2. Breakthrough failure
Although adequate preparations are made before the breakthrough, there is still the possibility that the breakthrough will fail. In this case losses will occur.
3. Improper parameter optimization
The parameter settings of the strategy can have a large impact on the results. If the parameters are set improperly, it will be greatly reduced.
In view of the above risks, optimization can be carried out in the following ways:
1. Combine other indicators to filter signals
2. Manual intervention ensures breakthrough position
3. Multiple sets of parameter optimization tests
## Optimization direction
The MACD Stochastics swing breakout strategy still has room for further optimization:
1. Optimize MACD parameters and find the best parameter combination
2. Optimize Stochastics parameters and find the best parameter combination
3. Add other indicator combinations, such as KDJ, BOLL, etc., to further improve the quality of Entries
4. Test different holding times and optimize stop-profit and stop-loss strategies
5. Test the difference in parameters of different trading targets
6. Add machine learning algorithm to automatically optimize parameters
## Summarize
The MACD Stochastics band shock breakthrough strategy comprehensively uses the two indicators MACD and Stochastics to enter the market with high quality when the band shock breaks through and follow the trend. At the same time, stop-loss and take-profit strategies are used to effectively control risks. This strategy captures the short-term trend of stock prices and has certain trading advantages. However, there is still room for exploration in parameter optimization and technical indicator combination, which needs to be further optimized.
||


## Overview

The MACD Stochastics Range Breakout Strategy combines the MACD and Stochastics indicators into a quantitative trading strategy. It attempts to identify the trend direction of stock prices and take positions when prices break out of ranging zones.

When taking positions, this strategy considers the signals from both MACD and Stochastics to improve the quality of entries. Also, preset stop loss and take profit points can effectively control risks.

## Strategy Logic

The MACD Stochastics Range Breakout Strategy is mainly based on the following principles:

1. MACD indicator can effectively identify the direction and momentum of price trends  
2. Stochastics indicator can spot overbought or oversold conditions of a stock
3. When stock price has been ranging for a period of time, a significant directional move after breaking previous range is likely to happen
4. Combining the signals from MACD and Stochastics on range breakouts allows timely entries and improves quality  

Specifically, the strategy uses the MACDDIFF line crossing over DEA line to determine bullish or bearish trend signals. When DIFF crosses over DEA upwards, it generates a bullish signal and vice versa.  

Meanwhile, crosses between Stochastics’s K line and D line around overbought/oversold areas (default 30 and 70) also produce trade signals.

When MACD and Stochastics give aligned signals, the strategy will take a position. At this point, a major price move is likely.  

After entering, stop loss and take profit points are set to rationally control single trade loss and lock in profits.


## Strengths  

The MACD Stochastics Range Breakout Strategy has the following strengths:

1. Combining indicators improves signal quality

   Utilizing both MACD and Stochastics filters out some fake signals and allows better entry quality.
   
2. Capturing breakout moves and trend trading 

   The strategy specializes in catching significant breakout moves after ranging. These moves tend to be huge.
   
3. Optimized stop loss/take profit mechanism effectively controls risks

   Built-in stop loss/take profit logic reasonably limits single trade loss and timely locks in gains. 


## Risks

Despite careful design, MACD Stochastics Range Breakout Strategy has some inherent risks:

1. Missing perfect entry timing 

   False breakouts are common before valid breakouts happen. Suboptimal entry timing may result in missed best entry price.  

2. Failed breakout

   While adequate preparations are made prior to entries, failed breakouts are still possible, leading to losses.

3. Improper parameter optimization

   Inappropriate parameter settings severely undermine strategy performance. 


To address the above risks, the following optimizations can be adopted:

1. Adding other indicators to filter signals

2. Manual intervention to ensure valid breakout  

3. Rigorous multi-set parameter optimization tests


## Optimization Directions   

There remains room for further optimization of the MACD Stochastics Range Breakout Strategy:

1. Optimize MACD parameters to find best combination

2. Optimize Stochastics parameters to find best combination  

3. Incorporate other indicators like KDJ, BOLL to improve entry quality

4. Test different holding periods, optimize stop loss/take profit  

5. Test cross-asset parameter differences 

6. Introduce machine learning algorithms for automated parameter optimization


## Conclusion

The MACD Stochastics Range Breakout Strategy capitalizes on range breakouts by entering based on aligned signals from both MACD and Stochastics. The stop loss/take profit mechanism further controls risks. It aims to capture short-term trends but still leaves room for parameter tuning and more indicator combinations for better performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|180|Fast Length|
|v_input_2|390|Slow Length|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_1|135|Signal Smoothing|
|v_input_string_1|0|Oscillator MA Type: EMA|SMA|
|v_input_string_2|0|Signal Line MA Type: EMA|SMA|
|v_input_int_2|14|%K Length|
|v_input_int_3|true|%K Smoothing|
|v_input_int_4|3|%D Smoothing|
|v_input_float_1|3|Long Take Profit (%)|
|v_input_float_2|3|Short Take Profit (%)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-04 00:00:00
end: 2023-12-10 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy(title="macd stoch strategy", shorttitle="benzo MACD stoch",overlay=true)
// Getting inputs
fast_length = input(title = "Fast Length", defval = 180)
slow_length = input(title = "Slow Length", defval = 390)
src = input(title = "Source", defval = close)
signal_length = input.int(title = "Signal Smoothing",  minval = 1, maxval = 500, defval = 135)
sma_source = input.string(title = "Oscillator MA Type",  defval = "EMA", options = ["SMA", "EMA"])
sma_signal = input.string(title = "Signal Line MA Type", defval = "EMA", options = ["SMA", "EMA"])
// Calculating
fast_ma = sma_source == "SMA" ? ta.sma(src, fast_length) : ta.ema(src, fast_length)
slow_ma = sma_source == "SMA" ? ta.sma(src, slow_length) : ta.ema(src, slow_length)
macd = fast_ma - slow_ma
signal = sma_signal == "SMA" ? ta.sma(macd, signal_length) : ta.ema(macd, signal_length)
hist = macd - signal

// hline(0, "Zero Line", color = color.new(#787B86, 50))
// plot(hist, title = "Histogram", style = plot.style_columns, color = (hist >= 0 ? (hist[1] < hist ? #26A69A : #B2DFDB) : (hist[1] < hist ? #FFCDD2 : #FF5252)))
// plot(macd,   title = "MACD",   color = #2962FF)

// plot(signal, title = "Signal", color = #FF6D00)

periodK = input.int(14, title="%K Length", minval=1)
smoothK = input.int(1, title="%K Smoothing", minval=1)
periodD = input.int(3, title="%D Smoothing", minval=1)
k = ta.sma(ta.stoch(close, high, low, periodK), smoothK)
d = ta.sma(k, periodD)
// plot(k, title="%K", color=#2962FF)
// plot(d, title="%D", color=#FF6D00)
// h0 = hline(80, "Upper Band", color=#787B86)
// hline(50, "Middle Band", color=color.new(#787B86, 50))
// h1 = hline(20, "Lower Band", color=#787B86)
// fill(h0, h1, color=color.rgb(33, 150, 243, 90), title="Background")


// Make inputs that set the take profit % (optional)
longProfitPerc = input.float(3, title="Long Take Profit (%)", minval=0.0, step=0.1) * 0.01

shortProfitPerc = input.float(3, title="Short Take Profit (%)",minval=0.0, step=0.1) * 0.01

// Calculate trading conditions
enterLong  = macd>signal and ta.crossover(k,30)
enterShort = macd<signal and ta.crossunder(k,70)

// Figure out take profit price
longExitPrice  = strategy.position_avg_price * (1 + longProfitPerc)
shortExitPrice = strategy.position_avg_price * (1 - shortProfitPerc)

// Plot take profit values for confirmation
plot(strategy.position_size > 0 ? longExitPrice : na,
     color=color.green, style=plot.style_circles,
     linewidth=3, title="Long Take Profit")

plot(strategy.position_size < 0 ? shortExitPrice : na,
     color=color.red, style=plot.style_circles,
     linewidth=3, title="Short Take Profit")

// Submit entry orders
if enterLong
    strategy.entry("long", strategy.long)

if enterShort
    strategy.entry("short", strategy.short)

// STEP 3:
// Submit exit orders based on take profit price
if strategy.position_size > 0
    strategy.exit("long TP", limit=longExitPrice)

if strategy.position_size < 0
    strategy.exit("short TP", limit=shortExitPrice)
```

> Detail

https://www.fmz.com/strategy/434960

> Last Modified

2023-12-11 11:48:27

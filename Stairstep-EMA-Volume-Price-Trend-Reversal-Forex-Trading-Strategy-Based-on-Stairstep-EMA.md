
> Name

Volume-Price-Trend-Reversal-Forex-Trading-Strategy-Based-on-Stairstep-EMA-
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/c3702aeed89a7b272ff4fcddb62cfc566b2f663b410fb6aaa149bf0f10cf9250.png)
[trans]


## Overview
This is a short-period (1-5 minutes) foreign exchange gold trading strategy that mainly uses the volume-price relationship in the tide level theory and multiple Stairstep EMA to predict trend reversal points and conduct short-period trend following transactions. This strategy is suitable for high-frequency trading.
## Principle
The trading signals of this strategy come from two parts:
1. Judgment of the volume-price relationship based on the average trading volume price. Specifically, the strategy determines changes in the long and short trends by calculating the average price EMA of trading volume in different periods (configurable). If the short-period EMA crosses above the longer-period EMA, it is considered a bullish signal; if the short-period EMA crosses below the longer-period EMA, it is considered a bearish signal.
2. Reversal signal based on Stairstep EMA judgment. Stairstep EMA refers to multiple EMA moving averages with different parameters, such as the 10-day line, the 20-day line, the 50-day line, etc., and the trend reversal is judged based on their order. If the short-term EMA turns before the long-term EMA, it means the trend is reversing.
The strategy will combine these two signals to decide the entry. Specifically, if the volume-price relationship is judged to be bullish, and the Stairstep EMA shows that the multiple EMAs have all turned bullish, then the market will be entered to go long; on the contrary, if the volume-price relationship is judged to be bearish, and the Stairstep EMA shows that the multiple EMAs have all turned bearish, then the market will be entered to go short.
## Advantages
This strategy combines the advantages of volume average price and multiple EMA, which can improve the accuracy and stability of signals:
1. Judging the volume-price relationship based on the average price of trading volume can be more accurate than judging the price EMA alone, and avoid being misled by enhanced price shocks.
2. Stairstep EMA can increase the dimension of judgment through the arrangement order of different parameter EMA and avoid the noise caused by a single EMA.
3. The combination of two signals can achieve mutual verification and reduce false signals.
4. Suitable for high-frequency and short-cycle trading, and can quickly capture small-scale reversal opportunities.
5. Strategy parameters can be flexibly configured to adapt to the optimization of different varieties and cycles.
## Risk
There are also some risks with this strategy:
1. Relying too much on technical indicators may lead to being misled by abnormal market movements.
2. Short-cycle operations are more sensitive to transaction costs, and slippage and handling fees need to be controlled.
3. Short-period EMA parameters need to be optimized frequently, otherwise they may fail.
4. The divergence between volume and price may not necessarily result in a reversal, and there is a risk of misjudgment.
5. The judgment of the order of multiple EMAs is not completely reliable and may cause misjudgments.
Countermeasures:
1. Make judgments based on more fundamental factors.
2. Adjust the position to ensure that the single stop loss is not too large.
3. Retest and optimize parameters regularly.
4. Trade near key support and resistance areas to increase your success rate.
5. Use in combination with other indicators for multi-dimensional verification.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Test different calculation methods for the volume-price relationship to find more stable parameters.
2. Add more levels of Stairstep EMA indicator judgment.
3. Filter in combination with other indicator signals, such as RSI, MACD, etc.
4. Optimize the stop loss mechanism, such as trailing stop loss, pending order stop loss, etc.
5. Optimize parameters according to the characteristics of different varieties and develop a parameter set suitable for the variety.
6. Add machine learning algorithms and use big data to train judgment models.
7. Explore different exit strategies, such as fixed exit, trend following exit, etc.
8. Introduce an adaptive parameter mechanism to automatically adjust parameters according to market changes.
## Summarize
This strategy comprehensively utilizes the advantages of two indicators, namely trading volume average price and Stairstep EMA, to conduct short-period trend following transactions. This strategy has high stability and accuracy, but it also requires attention to risk control and parameter optimization. If you continue to optimize and test, and use it in conjunction with other technical indicators, it can become an efficient short-cycle trading strategy.
||

# 

## Overview

This is a short-term (1-5 minutes) forex trading strategy that mainly utilizes the volume price relationship in tidal theory and multiple Stairstep EMAs to predict trend reversal points for short-term trend tracking trading. The strategy is suitable for high-frequency trading.

## Principle 

The trading signals of this strategy come from two parts:

1. Volume price relationship judgment based on volume average price. Specifically, the strategy calculates the EMA of volume average price of different periods (configurable) to judge the change in bullish and bearish trends. If the short period EMA crosses above the longer period EMA, it is considered a bullish signal. If the short period EMA crosses below the longer period EMA, it is considered a bearish signal.

2. Trend reversal signals judged by Stairstep EMA. Stairstep EMA refers to setting multiple EMAs with different parameters, such as 10-day, 20-day, 50-day, etc. Judging trend reversal according to their order. If the short period EMA turns ahead of the long period EMA, it means the trend is reversing.

The strategy will combine these two signals to determine entry. Specifically, if the volume price relationship is judged as bullish, and the Stairstep EMA shows that multiple EMAs have turned bullish, long positions will be taken. Conversely, if the volume price relationship is judged as bearish, and the Stairstep EMA shows multiple EMAs have turned bearish, short positions will be taken.

## Advantages

This strategy combines the advantages of volume average price and multiple EMAs, which can improve the accuracy and stability of signals:

1. Judging the volume price relationship based on volume average price can be more accurate than simply price EMA judgment, avoiding being misled by enhanced price fluctuations.

2. Stairstep EMA can increase the dimension of judgment by the order of different parameter EMAs, avoiding the noise of a single EMA. 

3. The combination of the two signals enables mutual verification and reduces false signals.

4. It is suitable for high-frequency short-term trading and can quickly capture small reversal opportunities within the range.

5. The strategy parameters can be flexibly configured to optimize for different varieties and frequencies.

## Risks

This strategy also has some risks:

1. Overly dependent on technical indicators, there is a possibility of being misled by erratic market conditions.

2. Short-term operations are relatively sensitive to trading costs, slippage and commissions need to be well controlled.

3. Short-term EMA parameters need frequent optimization, otherwise they may become invalid. 

4. Volume price divergence does not necessarily generate reversal, there is a risk of misjudgment.

5. The order of multiple EMAs is not completely reliable and may also cause misjudgments.

Countermeasures:

1. Combine more fundamental factors for judgment.

2. Adjust positions to ensure losses on single trades are not too large. 

3. Regularly retest and optimize parameters.

4. Trade near key support/resistance levels to increase success rate.

5. Use with other indicators for multi-dimensional verification.

## Optimization Directions

This strategy can also be optimized in the following aspects:

1. Test different methods of calculating volume price relationship to find more stable parameters.

2. Increase more levels of Stairstep EMA indicators.

3. Combine other indicator signals for filtering, such as RSI, MACD, etc.

4. Optimize stop loss mechanisms like moving stop loss, pending orders, etc.

5. Optimize parameters based on characteristics of different trading instruments to develop suitable parameter sets.

6. Introduce machine learning algorithms to train judgment models using big data.

7. Explore different exit strategies such as fixed exits, trend tracking exits, etc. 

8. Introduce adaptive parameter mechanisms to automatically adjust parameters based on market changes.

## Summary 

This strategy combines the advantages of volume average price and Stairstep EMA for short-term trend tracking trading. The strategy has high stability and accuracy, but risk control and parameter optimization need to be noted. With continuous optimization and testing, combined with other technical indicators, it can become an efficient short-term trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_int_1|2|(?Optimization Parameters)Period Fractals|
|v_input_1_hl2|0|Source for EMA's: hl2|high|low|open|close|hlc3|hlcc4|ohlc4|
|v_input_int_2|10|Length EMA 1|
|v_input_int_3|20|Length EMA 2|
|v_input_int_4|100|Length EMA 3|
|v_input_2|25|(?Risk Management)TP in PIPS|
|v_input_3|25|SL in PIPS|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-01 00:00:00
end: 2023-10-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © exlux99

//@version=5

strategy("Forex Fractal EMA Scalper", overlay=true)
// Define "n" as the number of periods and keep a minimum value of 2 for error handling.
n = input.int(title="Period Fractals", defval=2, minval=2, group="Optimization Parameters")

src = input(hl2, title="Source for EMA's", group="Optimization Parameters")
len1 = input.int(10, minval=1, title="Length EMA 1", group="Optimization Parameters")
out1 = ta.ema(src, len1)
len2 = input.int(20, minval=1, title="Length EMA 2", group="Optimization Parameters")
out2 = ta.ema(src, len2)
len3 = input.int(100, minval=1, title="Length EMA 3", group="Optimization Parameters")
out3 = ta.ema(src, len3)



// UpFractal
bool upflagDownFrontier = true
bool upflagUpFrontier0 = true
bool upflagUpFrontier1 = true
bool upflagUpFrontier2 = true
bool upflagUpFrontier3 = true
bool upflagUpFrontier4 = true

for i = 1 to n
    upflagDownFrontier := upflagDownFrontier and (high[n-i] < high[n])
    upflagUpFrontier0 := upflagUpFrontier0 and (high[n+i] < high[n])
    upflagUpFrontier1 := upflagUpFrontier1 and (high[n+1] <= high[n] and high[n+i + 1] < high[n])
    upflagUpFrontier2 := upflagUpFrontier2 and (high[n+1] <= high[n] and high[n+2] <= high[n] and high[n+i + 2] < high[n])
    upflagUpFrontier3 := upflagUpFrontier3 and (high[n+1] <= high[n] and high[n+2] <= high[n] and high[n+3] <= high[n] and high[n+i + 3] < high[n])
    upflagUpFrontier4 := upflagUpFrontier4 and (high[n+1] <= high[n] and high[n+2] <= high[n] and high[n+3] <= high[n] and high[n+4] <= high[n] and high[n+i + 4] < high[n])
flagUpFrontier = upflagUpFrontier0 or upflagUpFrontier1 or upflagUpFrontier2 or upflagUpFrontier3 or upflagUpFrontier4

upFractal = (upflagDownFrontier and flagUpFrontier)


// downFractal
bool downflagDownFrontier = true
bool downflagUpFrontier0 = true
bool downflagUpFrontier1 = true
bool downflagUpFrontier2 = true
bool downflagUpFrontier3 = true
bool downflagUpFrontier4 = true

for i = 1 to n
    downflagDownFrontier := downflagDownFrontier and (low[n-i] > low[n])
    downflagUpFrontier0 := downflagUpFrontier0 and (low[n+i] > low[n])
    downflagUpFrontier1 := downflagUpFrontier1 and (low[n+1] >= low[n] and low[n+i + 1] > low[n])
    downflagUpFrontier2 := downflagUpFrontier2 and (low[n+1] >= low[n] and low[n+2] >= low[n] and low[n+i + 2] > low[n])
    downflagUpFrontier3 := downflagUpFrontier3 and (low[n+1] >= low[n] and low[n+2] >= low[n] and low[n+3] >= low[n] and low[n+i + 3] > low[n])
    downflagUpFrontier4 := downflagUpFrontier4 and (low[n+1] >= low[n] and low[n+2] >= low[n] and low[n+3] >= low[n] and low[n+4] >= low[n] and low[n+i + 4] > low[n])
flagDownFrontier = downflagUpFrontier0 or downflagUpFrontier1 or downflagUpFrontier2 or downflagUpFrontier3 or downflagUpFrontier4

downFractal = (downflagDownFrontier and flagDownFrontier)

// plotshape(downFractal, style=shape.triangledown, location=location.belowbar, offset=-n, color=#F44336, size = size.small)
// plotshape(upFractal, style=shape.triangleup,   location=location.abovebar, offset=-n, color=#009688, size = size.small)


long= out1 > out2 and out2>out3 and upFractal
short= out1 < out2 and out2<out3 and downFractal


strategy.entry("long",strategy.long,when= short)
strategy.entry("short",strategy.short,when=long)

tp=input(25, title="TP in PIPS", group="Risk Management")*10
sl=input(25, title="SL in PIPS", group="Risk Management")*10


strategy.exit("X_long", "long", profit=tp,  loss=sl  )
strategy.exit("x_short", "short",profit=tp, loss=sl  )

```

> Detail

https://www.fmz.com/strategy/431426

> Last Modified

2023-11-07 17:03:57

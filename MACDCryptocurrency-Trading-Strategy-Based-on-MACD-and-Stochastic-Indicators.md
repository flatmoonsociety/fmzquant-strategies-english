
> Name

Cryptocurrency-Trading-Strategy-Based-on-MACD-and-Stochastic-Indicators
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/6d32d2638892606913.png)
[trans]
## Overview
This strategy is a cryptocurrency trading strategy based on a combination of MACD indicator and stochastic indicator. It generates trading signals by calculating the MACD indicator of Bitcoin price and applying the stochastic indicator to it to capture trend changes in the cryptocurrency market.
## Strategy Principle
The strategy first calculates the MACD indicator. MACD stands for Moving Average Convergence Divergence and is a trend following indicator. It consists of a fast line and a slow line. The fast line is a shorter-term exponential moving average, and the slow line is a longer-term exponential moving average. When the fast line crosses the slow line, it is a golden cross signal, indicating that the market has turned bullish; when the fast line crosses the slow line, it is a dead cross signal, indicating that the market has turned bearish.
After calculating the MACD indicator, this strategy applies the stochastic indicator %K to the MACD indicator itself. The calculation formula of the stochastic indicator %K is:
%K = (Current closing price - lowest price in N days) / (highest price in N days - lowest price in N days) * 100
Stochastics reflect changes in stock prices away from their recent range. Fluctuations in the %K value between 20 and 80 represent that the stock price trend is in a consolidation range. When %K crosses the 20 line from bottom to top, it is a buy signal. When %K crosses the 80 line from top to bottom, it is a sell signal.
This strategy combines the trading signals of the MACD indicator and the stochastic indicator %K to trade in the cryptocurrency market. A buy signal is generated when the stochastic indicator %K crosses 20 upwards; a sell signal is generated when the stochastic indicator %K crosses 80 downwards.
## Strategic Advantages
This strategy combines trend analysis and overbought and oversold indicators to effectively identify important turning points in the market. Compared with using MACD or stochastic indicator alone, the combined use of %K and MACD can increase the reliability of signals and reduce false signals.
In addition, this strategy applies technical indicators commonly used in the stock market to cryptocurrency trading, which is a cross-market application. This indicator works equally well in the digital currency market, and may even achieve better results due to the high volatility of digital currencies.
## Risks and Solutions
The biggest risk of this strategy is that the cryptocurrency market is highly volatile, which can easily generate false signals and lead to trading losses. In addition, when technical indicators send signals, the price may have already changed to a certain extent, and there is a risk that the early stage of the trend cannot be fully captured.
In order to control these risks, it is recommended to use trailing stop loss to lock in profits and avoid further expansion of losses. At the same time, parameters can also be adjusted appropriately and different cycle lengths can be used to explore more potential opportunities.
## Strategy optimization direction
First, the strategy can try to use moving averages in conjunction with volatility indicators, such as Bollinger Bands, and set volatility parameters to identify the effectiveness of breakouts and avoid false signals.
Second, machine learning models can be introduced to train historical data and establish random forest or LSTM neural network models to assist in judging the effectiveness of indicator signals.
Third, add a stop-loss mechanism. When the price moves in an adverse direction beyond a certain range, stop loss is automatically executed to control risks.
## Summarize
This strategy combines the MACD indicator and the stochastic indicator %K, and uses the two indicators to verify each other's signals to formulate a cryptocurrency trading strategy. This combination of indicator strategies can improve the accuracy of signals to a certain extent. But we also need to be wary of the noise and lagging effects that may be caused by too complex an indicator combination. Parameter setting and risk control are equally important and need to be adjusted and optimized according to different market environments in order to obtain better strategic performance.
||

## Overview

This strategy is a cryptocurrency trading strategy based on a combination of the MACD indicator and stochastic indicators. It generates trading signals by calculating the MACD indicator of bitcoin prices and applying stochastic indicators on it, in order to capture trend changes in the cryptocurrency market.

## Strategy Logic

The strategy first calculates the MACD indicator. MACD stands for Moving Average Convergence Divergence, which is a trend-following indicator. It consists of a fast line and a slow line, where the fast line is a shorter-term exponential moving average and the slow line is a longer-term exponential moving average. When the fast line crosses above the slow line, it generates a golden cross signal, indicating a bullish market. When the fast line crosses below the slow line, it generates a death cross signal, indicating a bearish market.  

After calculating the MACD indicator, the strategy applies the stochastic indicator %K on the MACD itself. The calculation formula for %K is:

%K = (Current Close - Lowest Low over N periods) / (Highest High over N periods - Lowest Low over N periods) * 100

The stochastic indicator reflects the price deviation from its recent range. The fluctuation of %K between 20-80 represents the price is trading in consolidation. When %K crosses above 20 from below, it generates a buy signal. When %K crosses below 80 from above, it generates a sell signal.

This strategy combines the trading signals from both the MACD and stochastic %K to trade in the cryptocurrency market. It generates a buy signal when %K crosses above 20 and a sell signal when %K crosses below 80.

## Advantages of the Strategy

This strategy combines trend analysis and overbought-oversold indicators, which can effectively identify important turning points in the market. Compared to using MACD or stochastic alone, the combination of %K and MACD increases the reliability of trading signals and reduces false signals.  

In addition, this strategy applies technical indicators commonly used in stock markets to cryptocurrency trading. This is a cross-market application. These indicators are equally applicable in the digital currency market, and may even perform better due to the high volatility of cryptocurrencies.

## Risks and Solutions

The biggest risk of this strategy is the high volatility in the cryptocurrency market, which easily produces false signals and leads to trading losses. In addition, when indicators generate signals, prices may have already moved substantially, posing the risk of missing early trend signals.

To control these risks, it is advisable to use moving stop loss to lock in profits and avoid further losses. At the same time, parameters can also be adjusted appropriately to discover more potential opportunities using different time frame lengths.

## Optimization Directions

Firstly, the strategy can try to combine moving averages with volatility indicators such as Bollinger Bands, setting volatility parameters to identify the validity of breakouts and avoid false signals.  

Secondly, machine learning models can be introduced to train on historical data and establish random forest or LSTM neural network models to assist in judging the effectiveness of indicator signals.

Thirdly, add a stop loss mechanism. When prices move more than a certain range in an unfavorable direction, automatically trigger stop loss to control risks.


## Conclusion  

This strategy combines the MACD indicator and the stochastic indicator %K, using the method of mutually verifying signals from two indicators to formulate a cryptocurrency trading strategy. This combination indicator strategy can improve the accuracy of signals to some extent. But we also need to be aware of the risk of over-complication of indicators, which may introduce noise and lagging effects. Proper parameter tuning and risk control according to different market environments are equally important for obtaining better strategy performance.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|23|MACD Fast Length|
|v_input_2|50|MACD Slow Length|
|v_input_3|10|Cycle Length|
|v_input_4|3|1st %D Length|
|v_input_5|3|2nd %D Length|
|v_input_6_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_7|true|Highlight Breakouts ?|
|v_input_8|75|upper|
|v_input_9|25|lower|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Schaff Trend Cycle Strategy", shorttitle="STC Backtest", overlay=true)

fastLength = input(title="MACD Fast Length",  defval=23)
slowLength = input(title="MACD Slow Length",  defval=50)
cycleLength = input(title="Cycle Length",  defval=10)
d1Length = input(title="1st %D Length",  defval=3)
d2Length = input(title="2nd %D Length",  defval=3)
src = input(title="Source", defval=close)
highlightBreakouts = input(title="Highlight Breakouts ?", type=bool, defval=true)

macd = ema(src, fastLength) - ema(src, slowLength)
k = nz(fixnan(stoch(macd, macd, macd, cycleLength)))
d = ema(k, d1Length)
kd = nz(fixnan(stoch(d, d, d, cycleLength)))

stc = ema(kd, d2Length)
stc := 	stc > 100 ? 100 : stc < 0 ? 0 : stc

upper = input(75, defval=75)
lower = input(25, defval=25)

long =  crossover(stc, lower) ? lower : na
short = crossunder(stc, upper) ? upper : na

long_filt = long and not short
short_filt = short and not long

prev = 0
prev := long_filt ? 1 : short_filt ? -1 : prev[1]

long_final = long_filt and prev[1] == -1
short_final = short_filt and prev[1] == 1

//alertcondition(long_final, "Long", message="Long")
//alertcondition(short_final,"Short", message="Short")

//plotshape(long_final, style=shape.arrowup, text="Long", color=green, location=location.belowbar)
//plotshape(short_final, style=shape.arrowdown, text="Short", color=red, location=location.abovebar)

strategy.entry("long", strategy.long, when = long )
strategy.entry("short", strategy.short, when = short)

```

> Detail

https://www.fmz.com/strategy/440703

> Last Modified

2024-02-01 11:52:15

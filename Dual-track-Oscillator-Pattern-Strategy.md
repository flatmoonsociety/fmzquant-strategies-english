
> Name

Dual-track-Oscillator-Pattern-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/7f52d9951aba286550fd12ea871bc557451fd08dcd9f8189db32b802da5d20f0.png)
[trans]

## Overview
The dual-track tracking shock typing strategy is a quantitative trading strategy based on Bollinger Bands and EMA indicators. The strategy attempts to capture short-term price fluctuations through identifying oscillator patterns based on Bollinger Bands and EMA.
## Strategy Principle
This strategy uses both Bollinger Bands and EMA as technical indicators. Bollinger Bands include the upper track, middle track and lower track, which can determine whether the price is in a shock range. EMA is a trend following indicator that can determine price trends.
This strategy first calculates the middle track of the Bollinger Bands, which is the n-day simple moving average of the price, where the n value defaults to 20 days. The upper and lower tracks of Bollinger Bands are respectively plus/minus two standard deviations from the middle track. Then calculate the 9-day EMA.
When the price crosses above the EMA, it is considered a buy signal; when the price crosses below the EMA, it is considered a sell signal. In this way, EMA, as a fast moving average, can capture the short-term price trend; while the Bollinger Bands middle track, as a slow moving average, can filter out some false signals.
Therefore, this strategy uses dual-track tracking of EMA and Bollinger Bands to capture short-term price shocks as much as possible. Buy when EMA crosses the middle rail, and sell when EMA crosses below the middle rail.
## Strategic advantage analysis
This dual-track tracking strategy has the following advantages:
1. Using EMA and Bollinger Bands mid-track dual-track tracking, you can judge trends and shocks at the same time, and capture short-term price fluctuations more accurately.
2. EMA serves as a fast moving average, and the middle track of Bollinger Bands serves as a slow moving average. The two can be used together to effectively filter out false signals and improve signal quality.
3. The indicator parameters can be adjusted, and the n value and Bollinger Band standard deviation can be adjusted according to the market, which is highly adaptable.
4. The strategic ideas are simple, clear and easy to implement, and are very suitable for short-term market fluctuations.
5. Parameters can be appropriately optimized and filtered in combination with other indicators to further improve the stability of the strategy.
## Risk Analysis
There are also some potential risks with this strategy:
1. The upper and lower rails of Bollinger Bands can easily form support and pressure, which may trigger stop loss in advance.
2. When the EMA crosses the middle track of the Bollinger Bands, the price may diverge and send out wrong signals.
3. When there is a sharp trend, EMA can easily form a 3-cup bottom buying point or a 3-cup bottom selling point, which may miss the trend.
4. When the volatile market weakens, trading signals will be significantly reduced and profits will not be sustained.
5. Improper parameter settings may lead to over-trading or missed trading opportunities.
6. Transaction fees will reduce actual profits, so position size needs to be controlled.
## Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Add indicators such as trading volume and filter out cross signals with poor signal quality.
2. Combine with overbought and oversold indicators such as RSI to avoid buying and selling points appearing in extreme areas.
3. Set stop loss and take profit based on the ATR value to make the stop loss more reasonable.
4. Increase the judgment of trends and avoid false signals under trending conditions.
5. Optimize parameters, such as EMA cycle, Bollinger Band parameters, etc., to make them more consistent with different market environments.
6. Use machine learning methods to dynamically optimize parameters to make the strategy more robust.
7. Adopt algorithmic trading, set stricter entry and exit conditions, and reduce human intervention.
## Summarize
The dual-track tracking shock type strategy uses both EMA and Bollinger Bands to track prices. Buy when EMA crosses above the middle track, and sell when EMA crosses below the middle track to capture short-term price shocks. It is a relatively simple and practical short-term strategy. This strategy has the advantages of trend judgment and filtering out false signals, but it also has certain risks. By continuously optimizing parameter settings, entry and exit conditions, etc., this strategy can become more stable and reliable, applicable to more market environments, and is a strategic idea worth learning and applying.
||


## Overview

The Dual-track Oscillator Pattern strategy is a quantitative trading strategy based on Bollinger Bands and EMA indicators. It attempts to capture short-term price fluctuations through identifying oscillator patterns based on Bollinger Bands and EMA.

## Strategy Logic

The strategy uses both Bollinger Bands and EMA as technical indicators. Bollinger Bands contain upper, middle and lower bands to judge if price is oscillating. EMA is a trend following indicator to determine price trend. 

First, the middle band of Bollinger Bands is calculated as the n-day simple moving average of price, where n defaults to 20 days. The upper and lower bands are middle band plus/minus two standard deviations. Then the 9-day EMA is calculated.

When price crosses above EMA, it is a buy signal. When price crosses below EMA, it is a sell signal. So EMA as a fast moving average captures short-term trend, while the middle band as a slow moving average filters some false signals.

By tracking dual bands of EMA and Bollinger Bands middle line, the strategy aims to capture short-term price oscillations. It buys when EMA crosses above middle line, and sells when EMA crosses below middle line.

## Advantage Analysis 

The dual-track strategy has the following advantages:

1. Using EMA and Bollinger Bands middle line dual tracks, it can judge both trend and oscillation, and more accurately capture short-term price fluctuations.

2. EMA as fast MA and middle band as slow MA work together to effectively filter false signals and improve signal quality. 

3. Indicator parameters are adjustable. The n value and Bollinger Bands standard deviation can be adjusted according to market conditions for better adaptability.

4. The strategy logic is simple and clear, very suitable for short-term oscillating markets. 

5. It can be optimized by adjusting parameters and incorporating other filters to further improve stability.

## Risk Analysis

The strategy also has some potential risks:

1. Bollinger Bands upper and lower bands can form support and resistance easily, triggering premature stop loss.

2. Divergence may happen between EMA and middle band when they cross, generating incorrect signals.

3. In strong trending markets, EMA may form W-bottoms and M-tops, missing the trend.

4. Trading signals will reduce significantly when oscillation weakens, unable to sustain profitability.

5. Inadequate parameter tuning may lead to overtrading or missing opportunities. 

6. Transaction costs erode actual profits, position sizing needs control.

## Optimization Directions

The strategy can be optimized in the following aspects:

1. Add volume to filter low quality crossover signals. 

2. Combine RSI to avoid buying/selling in overbought/oversold levels.

3. Use ATR to set more reasonable stop loss and take profit.

4. Add trend judgment to avoid wrong signals in trending markets.

5. Optimize parameters like EMA period and Bollinger Bands settings to suit different market environments.

6. Use machine learning to dynamically optimize parameters for robustness. 

7. Adopt algorithmic trading with strict entry and exit rules to minimize human interference.

## Summary

The Dual-track Oscillator Pattern strategy tracks price using dual bands of EMA and Bollinger Bands middle line. It buys when EMA crosses above middle band, and sells when EMA crosses below middle band, to capture short-term price oscillations. This simple short-term strategy has the advantage of filtering false signals and judging trends, but also has some risks. By continuously optimizing parameters, entry/exit rules etc., it can become more robust and applicable to more market environments, making it a worthwhile strategy approach to learn and apply.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|length|
|v_input_2|9|lengthEMA|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_4_close|0|Source EMA: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_5|2019|From Year|
|v_input_6|true|From Month|
|v_input_7|true|From Day|
|v_input_8|9999|To Year|
|v_input_9|12|To Month|
|v_input_10|31|To Day|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-07 00:00:00
end: 2023-11-13 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(shorttitle="BBXEMA", title="Bollinger Bands Cross EMA", default_qty_type=strategy.percent_of_equity, default_qty_value=100, overlay=true)
length = input(20, minval=1)
lengthEMA = input(9)
src = input(close, title="Source")
srcEMA = input(close, title="Source EMA")
//mult = input(2.0, minval=0.001, maxval=50)

// === INPUT BACKTEST RANGE ===
FromYear  = input(defval = 2019, title = "From Year", minval = 2009)
FromMonth = input(defval = 1, title = "From Month", minval = 1, maxval = 12)
FromDay   = input(defval = 1, title = "From Day", minval = 1, maxval = 31)
ToYear    = input(defval = 9999, title = "To Year", minval = 2009)
ToMonth   = input(defval = 12, title = "To Month", minval = 1, maxval = 12)
ToDay     = input(defval = 31, title = "To Day", minval = 1, maxval = 31)

// === FUNCTION EXAMPLE ===
start     = timestamp(FromYear, FromMonth, FromDay, 00, 00)  // backtest start window
finish    = timestamp(ToYear, ToMonth, ToDay, 23, 59)        // backtest finish window
window()  => true
basis = sma(src, length)
EMA = ema(srcEMA,lengthEMA)
//dev = mult * stdev(src, length)
//upper = basis + dev
//lower = basis - dev

Buy = crossover(EMA,basis)
Sell = crossunder(EMA,basis)

bb = plot(basis, color=color.red)
signal = plot(EMA, color=color.green)
//p1 = plot(upper, color=color.blue)
//p2 = plot(lower, color=color.blue)
//fill(p1, p2)

strategy.entry("Buy",true,when=window() and Buy)
strategy.close_all(when=window() and Sell)
```

> Detail

https://www.fmz.com/strategy/432096

> Last Modified

2023-11-14 14:12:16

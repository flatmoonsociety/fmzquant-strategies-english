
> Name

Dual-Stochastics-and-Volume-Weighted-Moving-Average-Combination-Indicator-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/9438a5d4a7647b6034.png)

[trans]

## Overview
This is a strategy that utilizes a combination of the Dual Stochastics indicator and the Volume Weighted Moving Average to identify trends. This strategy uses two Stochastics indicators with different periods, one is short-period and one is long-period, and is combined with the volume-weighted moving average to determine the current trend direction.
## Strategy Principle
This strategy mainly implements trend judgment through the following parts:
1. Calculate a short-period Stochastics indicator, the period length is input(30), and the smoothing parameter is 2
2. Calculate a long-period Stochastics indicator, the period length is input(90), and the smoothing parameter is 2
3. Add the short-period and long-period Stochastics indicators to get a comprehensive Stochastics curve ts
4. Calculate a volume-weighted moving average tsl for the ts curve, with a period length of input(30)
5. Compare the current value of tsl with the value 1 period ago. When tsl rises, it is considered an upward trend. When tsl falls, it is considered a downward trend.
6. Combined with the position of the Stochastics curve to determine whether it is a long or short signal
- When tsl rises and ts is in the middle zone, it is a long signal
- When tsl falls and ts is in the middle zone, it is a short signal
## Strategic advantage analysis
This strategy combines trend judgment and overbought and oversold judgment, and can identify the trend direction more reliably. The specific advantages are as follows:
1. The double Stochastics indicator can simultaneously reflect short-term and long-term overbought and oversold conditions to avoid missing certain signals.
2. Volume weighting can filter out some false breakthrough signals
3. The position of the Stochastics curve once again verifies the reliability of the trend signal
4. The parameters are adjustable and the cycle length can be adjusted appropriately according to different markets.
5. The strategic ideas are clear and concise, easy to understand and modify
## Risk and improvement analysis
There are also some risks to be aware of with this strategy:
1. Stochastics indicators are prone to sending out false signals and need to be filtered in conjunction with longer period indicators.
2. Fixed period parameters are not suitable for all market conditions, dynamic optimization parameters can be considered
3. Based only on technical indicators, it can be combined with fundamental factors to improve accuracy.
4. Inaccurate trading volume data will also affect the results, and the quality of the trading volume data needs to be verified.
5. Insufficient backtesting time and longer historical data is needed to verify the effect.
6. The entry point can be optimized. Now it is crosses under the lowest value to go long directly. A buffer zone can be set.
## Summarize
Generally speaking, this strategy uses double Stochastics indicators and volume-weighted moving averages to judge trends, and can theoretically identify trend turning points more reliably. However, parameter settings need to be optimized for specific markets, and there is a certain risk of false signals. It is recommended to make comprehensive judgments in combination with other factors such as fundamentals, long-term trends, etc., to improve the strategy Profit Factor. This strategy has a simple and clear idea, provides a template for quantitative trading, can be modified and optimized according to needs, and has strong application value.
||

## Overview

This is a strategy that utilizes a combination of dual Stochastics indicators and Volume Weighted Moving Average to identify trends. It uses two Stochastics indicators with different periods, one short-term and one long-term, combined with VWMA to determine the current trend direction.

## Strategy Logic

The strategy mainly implements trend identification through the following parts:

1. Calculate a short-period Stochastics indicator with period length input(30) and smooth parameter 2

2. Calculate a long-period Stochastics indicator with period length input(90) and smooth parameter 2

3. Add the short-period and long-period Stochastics together to get a combined Stochastics curve ts

4. Calculate a Volume Weighted Moving Average of ts curve with period length input(30)

5. Compare current tsl value with its value 1 period ago, when tsl rises, it indicates an uptrend, when tsl falls, it indicates a downtrend

6. Combine with Stochastics curve position to identify bullish or bearish signals

- When tsl rises and ts is in middle zone, it is a bullish signal 
- When tsl falls and ts is in middle zone, it is a bearish signal

## Advantage Analysis

The strategy combines trend identification and overbought-oversold analysis, which can identify trend direction quite reliably. The advantages are:

1. The dual Stochastics can reflect both short-term and long-term overbought/oversold situations, avoiding missing some signals

2. Volume weighted moving average can filter out some false breakout signals 

3. Stochastics curve position re-confirms the reliability of trend signals

4. Adjustable parameters suit different markets

5. Clear and simple logic, easy to understand and modify

## Risks and Improvements

There are also some risks to note for this strategy:

1. Stochastics may give false signals, needs filtering with longer-period indicators

2. Fixed periods may not suit all markets, dynamic optimization could help

3. Purely technical indicator based, fundamentals may improve accuracy

4. Inaccurate volume data affects results, need to verify data quality

5. Insufficient backtesting history, more data needed for validation

6. Entry points can be improved, rather than direct long on crosses under lowest

## Conclusion

In summary, this strategy identifies trends using dual Stochastics and VWMA, which can reliably identify trend reversals in theory. But parameter tuning is needed for specific markets, and false signals risk exists. Recommend combining other factors like fundamentals, long-term trends etc for judgment, to improve strategy Profit Factor. The logic is simple and clear, providing a template for quant trading, which can be modified as needed. It has great application value.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|30|periodK|
|v_input_2|90|periodK_two|
|v_input_3|30|VWMA Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-10-19 00:00:00
end: 2023-10-25 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title="Trend Finder V2", shorttitle="TFV2", format=format.price, precision=2, overlay = true)

//----------Indicator------------//

periodK = input(30)
periodD = 3
smoothK = 2

periodK_two = input(90)
periodD_two = 3
smoothK_two = 2

k = sma(stoch(close, high, low, periodK), smoothK)
d = sma(k, periodD)

k_two = sma(stoch(close, high, low, periodK_two), smoothK_two)
d_two = sma(k, periodD_two)

ts = k + k_two
tsl = vwma(ts, input(30, title = "VWMA Length"))

//--------Label parameter--------// 

up_label = tsl[1] < 100 and tsl > 100 ? 1 : 0
down_label = tsl[1] > 100 and tsl < 100 ? 1 : 0

//----------Color Code-----------//

//tsl_col = tsl > 100 and tsl > tsl[1] ? color.aqua : tsl > 100 and tsl < tsl[1] ? color.green : tsl < 100 and tsl > tsl[1] ? color.maroon : tsl < 100 and tsl < tsl[1] ? color.red : color.silver

//tsl_col = tsl > 100 and ts < 100 and ts > ts[1] ? color.aqua : tsl > 100 and ts > 100 and (ts > ts[1] or ts < ts[1]) ? color.green : tsl < 100 and ts > 100 and ts < ts[1] ? color.red : tsl < 100 and ts < 100 and (ts < ts[1] or ts > ts[1]) ? color.maroon : color.purple  

tsl_col = ts > ts[1] and tsl > tsl[1] ? color.lime : ts < ts[1] and tsl < tsl[1] ? color.red : color.yellow 

ts_col = (tsl_col == color.lime or tsl_col == color.maroon) and (k>k[1] and k < 30) ? color.lime :  (tsl_col == color.green or tsl_col == color.red) and (k < k[1] and k > 70)  ? color.red : color.silver

//-------------Plots-------------//

buy = tsl_col[1] == color.yellow and tsl_col == color.lime ? 1 : 0
sell = tsl_col[1] == color.yellow and tsl_col == color.red ? -1 : 0

plotcandle(open,high,low,close, color=tsl_col)

strategy.entry("Long", strategy.long,when=buy==1)
strategy.close("Long", when=sell==-1)

```

> Detail

https://www.fmz.com/strategy/430278

> Last Modified

2023-10-26 17:18:53

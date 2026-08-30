
> Name

Parabolic-SAR-and-CCI-Strategy-with-EMA-Exit-for-Gold-Trading Parabolic-SAR-and-CCI-Strategy-with-EMA-Exit-for-Gold-Trading
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/9a3b014917b9eb89a5240306bd97f3d40911142209f1bc8a455517221bb3c0e5.png)
[trans]

## Overview
This strategy is a gold M5 trading strategy based on a combination of SAR indicator, CCI indicator and EMA indicator. It uses a combination of three different technical indicators to identify gold's trend direction and overbought and oversold conditions to capture trading opportunities provided by intermediate pullbacks.
## Strategy Principle
1. The SAR indicator is used to determine the trend direction and possible reversal points of gold. When the SAR point falls across the price, it indicates the formation of a bullish trend; when the SAR point rises across the price, it indicates the formation of the short trend.
2. The CCI indicator is used to determine the overbought and oversold conditions of the market. When CCI is greater than 100, it indicates that the bullish trend has strengthened, and when CCI is less than -100, it indicates that the bearish trend has strengthened.
3. The EMA fast and slow line combination is used to determine the turning point of the price in the short and medium term. When the fast line rises, it is beneficial to go long, and when the fast line falls, it is conducive to short selling.
4. Specific entry rules: When the SAR indicator crosses the 5-minute EMA upwards and the CCI indicator is greater than 100, go long gold; when the SAR indicator crosses the 5-minute EMA downwards and the CCI index is less than -100, go short gold.
5. Stop-loss EXIT rules: The stop-profit point is the opening price plus 7 points, and the stop-loss point is the 1-minute EMA.
## Strategic advantage analysis
1. This strategy comprehensively uses three indicators to identify trend directions and important support and resistance, thereby increasing the probability of profit.
2. The CCI indicator can effectively filter out common false breakthroughs. SAR reversal points are combined with trend direction judgment to avoid repeated opening of positions in volatile markets.
3. The intersection of EMA fast and slow lines and the combined use with the SAR indicator can effectively identify low-risk trading opportunities provided by short-term price adjustments.
4. The strategy parameters have been optimized and are suitable for high-volatility varieties such as gold, and are also suitable for small accounts.
## Risk Analysis
1. This strategy is mainly based on technical indicators. If a major black swan event occurs, the probability of technical indicators failing is high.
2. Commodities such as gold fluctuate greatly, and the stop loss point is set to the EMA moving average. The stop loss may be exceeded, causing a large single loss to the account.
3. Both the CCI indicator and the SAR indicator may produce false signals, which may lead to unnecessary losses.
4. If you encounter violent market conditions, the probability of trading system platform failure will increase, which may result in the inability to stop losses.
## Optimization direction
1. Different parameter combinations can be tested to optimize the CCI indicator parameters to make them more consistent with the characteristics of gold.
2. You can combine more indicators, such as K-line patterns, Bollinger Bands, etc., to improve the stability of the strategy.
3. The parameters of the SAR indicator can be dynamically optimized through machine learning and other means to better adapt to market changes.
4. You can test different stop loss methods, such as trailing stop loss, to reduce the probability of stop loss being penetrated.
5. Position management can be optimized, such as fixed shares, dynamic adjustment of order volume, etc. to control single losses.

## Summarize
Overall, this strategy is a relatively stable gold trading strategy. It combines multiple indicators to identify gold's trend direction, important support and resistance levels, and overbought and oversold areas. Take advantage of gold's high volatility by opening a position during a pullback. At the same time, the strategy parameters have also been optimized and can be used for small account trading. However, this strategy also has certain risks, and appropriate risk management is recommended. If further optimized, the stability and profitability of this strategy still have a lot of room for improvement.
||

## Overview 

This is a gold trading strategy on M5 timeframe based on the combination of Parabolic SAR, CCI and EMA technical indicators. It utilizes three different indicators to identify the trend direction and overbought/oversold situations of gold to capture trading opportunities during market pullbacks.

## Strategy Logic

1. Parabolic SAR is used to determine the trend direction and potential reversal points of gold. When SAR dots start declining below the price, it indicates an upward trend; when SAR dots start rising above the price, it indicates a downtrend.

2. CCI indicates the overbought/oversold conditions of the market. CCI above 100 suggests a strengthening uptrend while CCI below -100 suggests a strengthening downtrend.

3. EMA crossovers signal short-term turning points of the price. Uptrend suggested when the fast line is rising and downtrend suggested when it is falling.  

4. Entry rules: Go long when SAR crosses above 5-min EMA in rising direction and CCI is greater than 100; Go short when SAR crosses below 5-min EMA in declining direction and CCI is less than -100.  

5. Exit rules: Take profit at Entry price + 7 ticks, Stop loss set at 1-min EMA line.

## Advantages

1. Utilizes 3 indicators to identify trends and key support/resistance levels, improving profitability.

2. CCI filters false breakouts efficiently. SAR reversals combined with trend direction avoids unnecessary entries during consolidations.

3. EMA crossovers with SAR offer low-risk entries during temporary pullbacks. 

4. Optimized parameters suitable for volatile commodity like gold and small accounts.

## Risks

1. Mainly relies on technical indicators which may fail during black swan events.  

2. Volatile commodity, EMA stop loss prone to being hit by spikes resulting in large losses.

3. Potential false signals from CCI and SAR leading to unnecessary losses.  

4. System failures during volatile moves can prevent effective stop loss execution.

## Enhancement Opportunities 

1. Test different parameter combinations to optimize CCI for gold's characteristics.

2. Incorporate more indicators like candlestick patterns, Bollinger Bands to improve robustness.  

3. Employ machine learning for dynamic optimization of SAR parameters adapting to changing markets.

4. Test different stop loss mechanisms e.g. trailing stops to reduce probability of being hit.

5. Optimize position sizing models e.g. fixed fractional, dynamic position sizing to control single trade loss amount.

## Conclusion

Overall a stable gold trading strategy combining multiple indicators to identify trends, key support/resistance levels and overbought/oversold zones for low risk entries during retracements. Optimized parameters allow small account trading capitalizing on gold’s high volatility. Has risks which can be addressed through proper risk management. Significant potential to further improve stability and profitability through enhancement.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|EMA Length|
|v_input_2|21|EMA Length 21|
|v_input_3|0.02|Acceleration Factor|
|v_input_4|0.2|Max Acceleration Factor|
|v_input_5|7|Take Profit Points|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-30 00:00:00
end: 2023-12-06 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Parabolic SAR and CCI Strategy with EMA Exit", overlay=true)

// Parameters
length = input(50, title="EMA Length")
length_21 = input(21, title="EMA Length 21")
acc = input(0.02, title="Acceleration Factor")
max_acc = input(0.2, title="Max Acceleration Factor")
takeProfitPoints = input(7, title="Take Profit Points")

// Variables
var float ep = 0.0
var float sar = 0.0
var float af = acc

// Calculating 5-minute EMA based on 1-minute data
var float sum_close = na
var float ema_5min = na
if (bar_index % 5 == 0)
    sum_close := 0.0
    for i = 0 to 4
        sum_close := sum_close + close[i]
    ema_5min := ema(sum_close / 5, length_21)

// Calculating 1-minute EMA
ema1 = ema(close, length)
cci = cci(close, 45)

// Custom Parabolic SAR Calculation
trendUp = close > ema1
trendDown = close < ema1

var float prev_sar = na
prev_sar := na(sar[1]) ? low[1] : sar[1]

if trendUp
    ep := high > ep ? high : ep
    af := min(af + acc, max_acc)
    sar := min(prev_sar, prev_sar + af * (ep - prev_sar))

if trendDown
    ep := low < ep ? low : ep
    af := min(af + acc, max_acc)
    sar := max(prev_sar, prev_sar + af * (ep - prev_sar))

// Entry Conditions
longCondition = sar > ema1 and ema1 > ema_5min and cci > 100
shortCondition = sar < ema1 and ema1 < ema_5min and cci < -100

// Exit Conditions
longTakeProfit = strategy.position_avg_price + takeProfitPoints * syminfo.mintick
longStopLoss = ema1
shortTakeProfit = strategy.position_avg_price - takeProfitPoints * syminfo.mintick
shortStopLoss = ema1

// Plotting Entry Points
plotshape(longCondition, style=shape.triangleup, location=location.belowbar, color=color.green, size=size.small)
plotshape(shortCondition, style=shape.triangledown, location=location.abovebar, color=color.red, size=size.small)

// Strategy Execution
if longCondition
    strategy.entry("Long", strategy.long)

if shortCondition
    strategy.entry("Short", strategy.short)

if strategy.position_size > 0
    strategy.exit("Take Profit/Stop Loss", "Long", limit=longTakeProfit, stop=longStopLoss)

if strategy.position_size < 0
    strategy.exit("Take Profit/Stop Loss", "Short", limit=shortTakeProfit, stop=shortStopLoss)

```

> Detail

https://www.fmz.com/strategy/434594

> Last Modified

2023-12-07 17:04:54

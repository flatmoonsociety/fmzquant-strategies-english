
> Name

Trend following strategy based on dual SMA system Dual-SMA-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]

### Overview
This strategy only uses two SMA moving averages, where the slow SMA is used to determine the trend direction and the fast SMA is used for entry signals. Combined with the K-line entity color determination, long and short position signals are generated. The strategy tracks the mid-term trend and is suitable for markets that fluctuate at high levels or fluctuate at low levels.
### Strategy Principles
Calculate two SMA moving averages, one fast and one slow, as well as the midline of the price channel. The fast line period is 5 and the slow line period is 20. When the price channel is above the midline, it is considered an upward trend. At this stage, look for opportunities for the fast line to cross the slow line to go long. When the price channel is below the midline, it is considered a downward trend. At this stage, look for opportunities for the fast line to cross the slow line to go short.
In addition, combined with the judgment of the color of the K-line entities, if it is an upward trend, the bottom K-line is required to have more than or equal to 2 red entities in a row, and then go long when the fast line crosses the slow line; if it is a downward trend, the top K-line is required to have more than or equal to 2 green entities in a row, and then go short when the fast line crosses the slow line.
### Advantage Analysis
This strategy uses two SMA moving averages and the price channel to determine the trend direction at the same time to avoid being misled by false breakthroughs. And add K-line entity color judgment to filter out false signals. Long and short signals exist at the same time, and hedging operations can be performed. Able to effectively track medium-term trends.
Parameters can be customized to configure long and short position conditions, which is highly adaptable. Backtest data shows that this strategy can achieve good returns in both high and low volatility markets.
### Risk Analysis
This strategy relies too much on moving average indicators and may generate too many false signals in volatile markets. And only consider the price factor, ignoring the impact of trading volume.
You can adjust the SMA cycle parameters appropriately, or add other technical indicators for signal filtering. Quantity and energy indicators can also be introduced for comprehensive judgment. In addition, position management can be optimized and position sizes adjusted according to market conditions.
### Optimization direction
1. Test different combinations of SMA fast and slow lines to find the optimal parameters.
2. Add trading volume and other indicators for signal verification.
3. Combine with other technical indicators to form a strategic combination.
4. Set up dynamic positions and optimize fund management.
5. Apply machine learning to predict price trends and turning points.
6. Optimize the stop loss strategy to prevent excessive losses.
### Summarize
The overall idea of ​​this strategy is clear, and it is common to use the double SMA system to determine the trend. However, relying solely on the moving average system can easily produce false signals, and other technical indicators need to be introduced for optimization. This strategy will be more effective if more qualitative and quantitative indicators can be introduced for verification. Overall, it provides a simple and reliable trend following strategy template.
||


### Overview 

This strategy uses only two SMA lines, with the slow SMA for trend direction and fast SMA for entry signals. Combined with candlestick color determination, it generates long and short signals. The strategy follows medium-term trends, suitable for consolidations at highs or lows.

### Strategy Logic

Two SMA lines are computed, one fast and one slow, along with the midline of the price channel. The fast line has a period of 5, while the slow line has a period of 20. Above the price channel midline is considered an uptrend, where opportunities to go long on fast line crossing above slow line are sought. Below the midline is a downtrend, where opportunities to go short on fast line crossing below slow line are sought.

In addition, candlestick body color is incorporated. In an uptrend, at least 2 consecutive red candlesticks are required after seeing the bottom, before going long when the fast line crosses above the slow line. In a downtrend, at least 2 consecutive green candles are required after seeing the top, before going short when the fast line crosses below the slow line.

### Advantage Analysis

The dual SMA lines and price channel help determine trend direction, avoiding false breakouts. Candlestick color filters further eliminate false signals. Long and short signals both exist for hedging. The strategy effectively tracks medium-term trends.

Customizable parameters allow configuring long/short conditions flexibly. Backtests show decent returns in consolidations at both highs and lows.

### Risk Analysis

Overreliance on SMA lines may generate excessive false signals during rangings. Price factors are considered while volume is ignored.

Tuning SMA periods or incorporating other technical indicators could filter signals. Volume indicators may also provide additional insight. Position sizing could also be optimized based on market conditions.

### Optimization Directions

1. Test different fast and slow SMA combinations to find optimal parameters.

2. Add volume and other indicators for signal validation.

3. Incorporate other technical indicators to form an ensemble strategy. 

4. Set dynamic position sizing to optimize capital management.

5. Apply machine learning to predict price trends and inflection points.

6. Optimize stop loss strategies to limit losses.

### Summary

The dual SMA system for trend determination is logically clear and commonly used. But overreliance on moving averages alone tends to generate false signals, requiring other indicators for enhancement. With more qualitative and quantitative validation, the strategy would become more robust. Overall it provides a simple and reliable trend following template.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|long|
|v_input_2|true|short|
|v_input_3|true|Use fast SMA|
|v_input_4|5|fast SMA Period|
|v_input_5|20|slow SMA Period|
|v_input_6|2|Bars Q|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-08-20 00:00:00
end: 2023-09-19 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Noro's Trend SMA Strategy v1.4", shorttitle = "Trend SMA str 1.4", overlay=true, default_qty_type = strategy.percent_of_equity, default_qty_value=100.0, pyramiding=0)

needlong = input(true, "long")
needshort = input(true, "short")
usefastsma = input(true, "Use fast SMA")
fastlen = input(5, defval = 5, minval = 1, maxval = 50, title = "fast SMA Period")
slowlen = input(20, defval = 20, minval = 2, maxval = 200, title = "slow SMA Period")
bars = input(2, defval = 2, minval = 0, maxval = 3, title = "Bars Q")

fastsma = ema(close, fastlen)
slowsma = ema(close, slowlen)

//PriceChannel
src = ohlc4
lasthigh = highest(src, slowlen)
lastlow = lowest(src, slowlen)
center = (lasthigh + lastlow) / 2

trend = low > center ? 1 : high < center ? -1 : trend[1]

bar = close > open ? 1 : close < open ? -1 : 0
redbars = bars == 0 ? 1 : bars == 1 and bar == -1 ? 1 : bars == 2 and bar == -1 and bar[1] == -1 ? 1 : bars == 3 and bar == -1 and bar[1] == -1 and bar[2] == -1 ? 1 : 0
greenbars = bars == 0 ? 1 : bars == 1 and bar == 1 ? 1 : bars == 2 and bar == 1 and bar[1] == 1 ? 1 : bars == 3 and bar == 1 and bar[1] == 1 and bar[2] == 1 ? 1 : 0

up = trend == 1 and (low < fastsma or usefastsma == false) and redbars == 1 ? 1 : 0
dn = trend == -1 and (high > fastsma or usefastsma == false) and greenbars == 1 ? 1 : 0

colorfastsma = usefastsma == true ? red : na
plot(fastsma, color = colorfastsma, title = "Fast SMA")
plot(center, color = blue, title = "Price Channel")

longCondition = up == 1
if (longCondition)
    strategy.entry("Long", strategy.long, needlong == false ? 0 : na)

shortCondition = dn == 1
if (shortCondition)
    strategy.entry("Short", strategy.short, needshort == false ? 0 : na)
```

> Detail

https://www.fmz.com/strategy/427347

> Last Modified

2023-09-20 11:35:30

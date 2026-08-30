
> Name

Kana-Candle-Breakout-Strategy-Based-on-Moving-Average-and-Support-Resistance
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1ccff99525065a65da5.png)
[trans]

## Overview
This strategy is a quick gapping strategy based on Japanese candle technical analysis, and combines moving average indicators and support and resistance indicators to determine trends and positions. The main idea is to wait for the price to quickly jump short and take profits quickly after the moving average and trend indicators are confirmed.
## Strategy Principle
This strategy uses a simple moving average SMA of length 20 and an exponential moving average EMA of length 200 to determine trend direction. When the price is in an uptrend (SMA is above the EMA), and the current closing price of the Japanese candle body is higher than the opening price (white real body), it indicates that the strength of the bulls is increasing; when the price is in a downtrend (the SMA is below the EMA), and the closing price of the current Japanese candle body is lower than the opening price (the black real body), it indicates that the strength of the shorts is increasing.
With trend and strength confirmed, this strategy waits for price to quickly gap up and enter the market. The so-called "gap" means that the price "crosses" the first channel line among the three preset ATR channels (channels calculated based on the 200-day ATR and coefficient) and enters within the second channel line. This is a high probability breakout signal.
After entering the market, the rules for taking profit or stop loss are very simple. As long as the price touches the outer edge of the channel (such as the rising take-profit line or the falling stop-loss line), the profit or loss will be taken immediately. This guarantees a quick profit for the strategy.
## Strategic Advantages
The biggest advantage of this strategy is that profits can be made quickly and conservatively. Use a quick gap to enter the market to avoid multiple position adjustments. The trend acceleration effect brought about by channel breakthroughs can lead to greater profits in a short period of time.
Compared with long-term holding, such an efficient opening and closing method can significantly reduce the short position rate of the strategy and further improve the efficiency of capital use. At the same time, the quick stop-profit and stop-loss mechanism can also effectively control single losses.
## Strategy Risk
This strategy mainly relies on moving average indicators to determine the trend direction, and there is a risk of callbacks and shocks. When the price fluctuates within the channel, it may lead to ultra-short-term reverse opening and losses.
In addition, this strategy relies too much on technical indicators and does not combine fundamentals and major event analysis. Once a black swan event occurs, the technical indicator QIAN will become invalid and the strategy may suffer large losses.
In order to control risks, the channel range can be appropriately relaxed and the frequency of opening positions can be reduced. Or add a position management module to dynamically adjust a single position according to the size of the funds.
## Strategy optimization
This strategy can be optimized from the following aspects:
1. Add a warehouse management module. According to the size of the account funds, the number of positions opened per order is dynamically adjusted to control the proportion of single losses.
2. Add fundamental filtering. When technical indicators trigger position opening conditions, judge the company's fundamentals and major events to avoid abnormal changes.
3. Combined with stock pool management. Set stock screening rules and dynamically adjust the stock pool. Select the optimal stock pool at different stages to improve stability.
4. Combined with machine learning models. Use AI to predict trends and key price points, and assist in determining channel ranges and opening opportunities.
## Summarize
This strategy is known for its simplicity and efficiency. Use moving averages to determine the general trend, Japanese candlesticks to determine the direction of power, jump into the market quickly, and quickly stop profits and losses. It can make profits in the short term and is suitable for high-frequency trading. But there are also risks of drawdowns and uncertainty. Through continuous optimization, the strategy can operate stably in different market environments.
||


## Overview

This is a fast breakout strategy based on Japanese candlestick technical analysis, combined with moving average indicators and support resistance indicators to determine trend and position. Its main idea is to wait for a fast price breakout and take profit quickly after the confirmation of moving average and trend indicators.  

## Strategy Logic

The strategy uses a 20-period simple moving average (SMA) and a 200-period exponential moving average (EMA) to determine the trend direction. When the price is in an uptrend (SMA above EMA), and the current Japanese candlestick real body closes above the open (white body), it indicates strengthened buying power. When the price is in a downtrend (SMA below EMA), and the current Japanese candlestick real body closes below the open (black body), it indicates strengthened selling pressure.

With the confirmation of trend and momentum, the strategy waits for a fast price breakout and enters the market. The so-called “breakout” means the price “crosses over” the first channel line of the three preset ATR channels (calculated based on 200-day ATR and coefficients) and enters the second channel line. This is a high probability breakout signal.

After entering the market, the profit taking and stop loss rules are very simple. As long as the price touches the outer bounds of the channel (such as take profit line or stop loss line), it will take profit or stop loss immediately. This ensures fast gains of the strategy.  

## Advantage Analysis 

The biggest advantage of this strategy is fast profit-taking with relatively small risk. By entering the market quickly after breakout, it avoids multiple adjustments of positions. And the accelerating effect brought by channel breakout allows large profits in a short period of time.  

Compared with long-term holding, such efficient opening and closing mechanics can significantly reduce the idling rate of the strategy and further improve capital efficiency. At the same time, the fast profit-taking and stop-loss mechanism can also effectively control single loss.

## Risk Analysis

The strategy mainly relies on moving average indicators to determine the trend direction, with the risk of pullback and consolidation. When the price oscillates within the channel, it may lead to ultra short-term reverse opening and loss. 

In addition, the strategy relies too much on technical indicators without combining fundamental and significant event analysis. In case of black swan events, the technical indicators would fail and the strategy may suffer major losses.

To control risks, we can appropriately expand the channel range to reduce opening frequency; or add position management module to dynamically adjust single position based on total capital.

## Optimization  

The strategy can be optimized in the following aspects:

1. Add position management module. Dynamically adjust single opening position based on account size to control single loss percentage.

2. Add fundamental filtering. When technical indicators trigger opening signals, check company fundamentals and significant events to avoid abnormalities. 

3. Combine stock pool management. Set rules to dynamically adjust stock pool. Select optimal stock pool in different stages to improve stability.  

4. Combine machine learning models. Use AI to predict trends and key price levels, assisting in determining channel range and entry timing.

## Conclusion  

The strategy features simplicity and efficiency. It determines major trend with moving averages, momentum direction with Japanese candles, enters with fast breakout, and exits with quick profit taking and stop loss. It allows short-term gains suitable for high frequency trading. But it also has the risk of drawdown and uncertainty. Continuous optimization can make the strategy stable under different market environments.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|20|Length|
|v_input_2|true|multiplier1|
|v_input_3|2|multiplier2|
|v_input_4|3|multiplier3|
|v_input_5|240|Support Resistance TimeFrame|
|v_input_6|true|Use Support/Resistance|
|v_input_7|0.5|Take Profit Percent|
|v_input_8|false|Use Take Profit|
|v_input_9_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-26 00:00:00
end: 2023-12-26 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy("Kana with S/R Strategy", title = "KANA with S/R", overlay=true)

len = input(20, minval=1, title="Length")
multiplier1 = input(1, minval=1, title="multiplier1")
multiplier2 = input(2, minval=1, title="multiplier2")
multiplier3 = input(3, minval=1, title="multiplier3") 
srTimeFrame = input(240, minval=1, title="Support Resistance TimeFrame")
useSR = input(true, type = bool, title="Use Support/Resistance")
tpPercent = input(0.5, type=float, title = "Take Profit Percent")
useTP = input(false, type=bool, title = "Use Take Profit")
tp = (close * tpPercent / 100) / syminfo.mintick

src = input(close, title="Source")
mid = sma(src, len)
plot(mid, title="SMA", color=blue)

trend = ema(close, 200)
plot(trend, title="Trend", color=green)


upper1 = mid + atr(200) * multiplier1
upper2 = mid + atr(200) * multiplier2
upper3 = mid + atr(200) * multiplier3

lower1 = mid - atr(200) * multiplier1
lower2 = mid - atr(200) * multiplier2
lower3 = mid - atr(200) * multiplier3

plot(upper1, color = orange)
plot(upper3, color = red)

plot(lower1, color = orange)
plot(lower3, color = red)

haClose = request.security(heikinashi(syminfo.tickerid), timeframe.period, close)
haOpen = request.security(heikinashi(syminfo.tickerid), timeframe.period, open)

resistance = request.security(syminfo.tickerid,tostring(srTimeFrame), high)
support  = request.security(syminfo.tickerid,tostring(srTimeFrame), low)
rsPos = (close - support[srTimeFrame]) / (resistance[srTimeFrame] - support[srTimeFrame])

MACD = ema(close, 120) - ema(close, 260)
aMACD = ema(MACD, 90)
hisline = MACD - aMACD

longCondition = (mid > trend) and (haOpen[1] < haClose[1]) and (mid > mid[1]) and (close < upper1) and hisline > 0 and (useSR == true ? (rsPos > 100) : true)
shortCondition = (mid < trend) and (haOpen[1] > haClose[1]) and (mid < mid[1]) and (close > lower1) and hisline < 0 and (useSR == true ? (rsPos < 0) : true)

longExit = (close > upper3 ) or (close < lower2)
shortExit = (close < lower3) or (close > upper2)

if (longCondition)
    strategy.entry("Long", strategy.long)
    if (useTP)
        strategy.exit("Exit Long", "Long", profit = tp)
        
if (longExit)
    strategy.close("Long")
    
if (shortCondition)
    strategy.entry("Short", strategy.short)
    if (useTP)
        strategy.exit("Exit Short", "Short", profit = tp)
    
if (shortExit)
    strategy.close("Short")
```

> Detail

https://www.fmz.com/strategy/436764

> Last Modified

2023-12-27 15:27:45

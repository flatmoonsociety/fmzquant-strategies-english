
> Name

Super-Trend-Dual-Moving-Average-Strategy based on Super-Trend Indicator and Simple Moving Average Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/121162c4b89b44f02e3.png)
 [trans]

## Overview
The supertrend double moving average strategy is a quantitative trading strategy based on supertrend indicators and simple moving averages. This strategy uses super-trend indicators to determine the direction of the market trend, and then filters it with the 200-day simple moving average to open long and short positions in the direction of the general trend.
## Strategy Principle
This strategy uses two indicators:
1. Supertrend indicator: It calculates the upper and lower rails based on the true amplitude ATR and a multiplier. When the closing price is higher than the upper band, it is bullish; when the closing price is lower than the lower band, it is bearish.
2. 200-day simple moving average: It takes the arithmetic average of the closing prices of the last 200 days. A closing price above this line indicates a bullish trend, and a closing price below this line indicates a bearish trend.
Strategy logic:
1. When the supertrend indicator is bullish (the supertrend indicator value is greater than 0) and the closing price is above the 200-day moving average, enter the market long.
2. When the supertrend indicator is bearish (the supertrend indicator value is less than 0) and the closing price is below the 200-day moving average, enter the market short.
3. Close the position when the supertrend indicator reverses the previous signal.
4. Stop loss is set to 25%.
## Advantage Analysis
This strategy combines super-trend indicators to determine short-term trends and 200-day moving averages to determine long-term trends, which can effectively filter out false breakthroughs, reduce trading frequency, and increase the winning rate. In a big market, the trend is clear enough, there is a lot of room for stop loss, and there is a lot of room for profit.
## Risk Analysis
The main risk of this strategy is that the stop loss range is large, and under high leverage conditions, it will increase the risk of forced liquidation. In addition, when the market is consolidating, super-trend indicators will generate redundant signals, thereby increasing trading frequency and costs.
Risks can be reduced by appropriately adjusting the ATR period, multiplier parameters and stop loss width.
## Optimization direction
This strategy can be optimized from the following aspects:
1. Adjust the ATR period and multiplier parameters, and optimize the parameters of the super trend indicator;
2. Try other moving average indicators, such as EMA, VIDYA, etc. to replace;
3. Add other auxiliary indicators, such as BOLL channel or KD indicator to further filter signals;
4. Optimize the stop loss strategy, such as moving to the break-even point or stopping loss with a large level.
## Summarize
This strategy is very practical overall. It takes into account both short-term and long-term trend judgments, and the stop loss setting is also relatively reasonable. Better results can still be obtained through parameter adjustment and optimization, which is worthy of actual verification and application.
||

## Overview

The Super Trend Dual Moving Average Strategy is a quantitative trading strategy based on the Super Trend indicator and simple moving average. This strategy uses the Super Trend indicator to determine the direction of the market trend, and then combines the 200-day simple moving average for filtering, opening long and short positions along the major trend direction.

## Strategy Logic

The strategy uses two indicators:  

1. Super Trend Indicator: It calculates the upper and lower rails based on the true volatility ATR and a multiplier. When the closing price is higher than the upper rail, it indicates a bullish view. When lower than the lower rail, it indicates a bearish view.

2. 200-day Simple Moving Average: It takes the arithmetic average of the closing prices over the past 200 days. When the closing price is higher than this line, it represents a major bullish trend. When lower than this line, it represents a major bearish trend.

Strategy Logic:

1. When the Super Trend indicator gives a bullish signal (Super Trend value greater than 0) and the closing price is higher than the 200-day MA, go long.  

2. When the Super Trend indicator gives a bearish signal (Super Trend value less than 0) and the closing price is lower than the 200-day MA, go short.

3. Close the position when the Super Trend indicator gives a reverse signal against the previous one.  

4. The stop loss is set at 25%.

## Advantage Analysis 

The strategy combines the Super Trend indicator to determine the short-term trend and the 200-day MA to determine the long-term trend, which can effectively filter false breakouts, reduce trading frequency while improving win rate. In a significant market trend, the trend is clear enough with large stop loss space and profit target.

## Risk Analysis

The main risk of this strategy is that the stop loss range is relatively large. It may increase the risk of forced liquidation in high leverage situations. In addition, when the market is range-bound, the Super Trend indicator will generate redundant signals, thus increasing transaction costs and trading frequency.

The risk can be reduced by appropriately adjusting the ATR period, multiplier parameters and stop loss range.

## Optimization Directions

The strategy can be optimized in the following aspects:  

1. Adjust the ATR period and multiplier parameters to optimize the Super Trend indicator.

2. Try other MA indicators such as EMA and VIDYA for replacement. 

3. Add other auxiliary indicators such as BOLL channel or KD indicator for further signal filtering.

4. Optimize stop loss strategy, such as moving it to breakeven point or trailing stop along with higher timeframe levels.

## Summary  

Overall, this strategy is very practical. It considers both short-term trend judgment and long-term trend judgment with reasonable stop loss settings. It can achieve better results through parameter adjustment and optimization, which is worth real trading verification and application.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|10|Lenght ATR|
|v_input_2|3|Mult.|
|v_input_3|200|Lenght SMA|
|v_input_float_1|25|% Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-16 00:00:00
end: 2024-01-15 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This work is licensed under a Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0) https://creativecommons.org/licenses/by-nc-sa/4.0/
// © wielkieef

//@version=5

strategy("Smart SuperTrend Strategy ", shorttitle="ST Strategy", overlay=true, pyramiding=1, initial_capital=10000, default_qty_type=strategy.percent_of_equity, default_qty_value=25, calc_on_order_fills=false, slippage=0, commission_type=strategy.commission.percent, commission_value=0.01)


// Parametry wskaźnika SuperTrend
atrLength = input(10, title="Lenght ATR")
factor = input(3.0, title="Mult.")

// Parametry dla SMA
lengthSMA = input(200, title="Lenght SMA")

// Parametry dla Stop Loss
sl = input.float(25.0, '% Stop Loss', step=0.1)

// Obliczanie ATR
atr = ta.atr(atrLength)

// Obliczanie podstawowej wartości SuperTrend
up = hl2 - (factor * atr)
dn = hl2 + (factor * atr)

// Obliczanie 200-SMA
sma200 = ta.sma(close, lengthSMA)

// Inicjalizacja zmiennych
var float upLevel = na
var float dnLevel = na
var int trend = na
var int trendWithFilter = na

// Logika SuperTrend
upLevel := close[1] > upLevel[1] ? math.max(up, upLevel[1]) : up
dnLevel := close[1] < dnLevel[1] ? math.min(dn, dnLevel[1]) : dn

trend := close > dnLevel[1] ? 1 : close < upLevel[1] ? -1 : nz(trend[1], 1)

// Filtr SMA i aktualizacja trendWithFilter
trendWithFilter := close > sma200 ? math.max(trend, 0) : math.min(trend, 0)

// Logika wejścia
longCondition = trend == 1  
shortCondition = trend == -1  

// Wejście w pozycje
if (longCondition) and  close > sma200
    strategy.entry("Long", strategy.long)
if (shortCondition) and close < sma200
    strategy.entry("Short", strategy.short)

// Warunki zamknięcia pozycji
Long_close = trend == -1 and close > sma200
Short_close = trend == 1  and close < sma200

// Zamknięcie pozycji
if (Long_close)
    strategy.close("Long")
if (Short_close)
    strategy.close("Short")

// Kolory superTrendu z filtrem sma200
trendColor = trendWithFilter == 1 ? color.green : trendWithFilter == -1 ? color.red : color.blue

//ploty
plot(trendWithFilter == 1 ? upLevel : trendWithFilter == -1 ? dnLevel : na, color=trendColor, title="SuperTrend")

// Stop Loss ( this code is from author RafaelZioni, modified by wielkieef )
per(procent) =>
    strategy.position_size != 0 ? math.round(procent / 100 * strategy.position_avg_price / syminfo.mintick) : float(na)
// --------------------------------------------------------------------------------------------------------------------

strategy.exit('SL',loss=per(sl))



//by wielkieef

```

> Detail

https://www.fmz.com/strategy/438944

> Last Modified

2024-01-16 15:19:09

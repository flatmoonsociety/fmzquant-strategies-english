
> Name

Dual-EMA-Crossover-Trend-Following-Strategy-with-ATR-and-ADX-Filters
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/4837975e130bbb71ac19b1e74207563a9dfab2937093872c60ffc459f9f51f42.png)
[trans]

## Overview
This strategy uses double EMA moving averages to form a classic trend following strategy of long golden crosses and short dead crosses, and uses the ATR indicator and ADX indicator for additional filtering to track strong trends and control risks during shocks.
## Strategy Principle
This strategy is mainly based on the following points:
1. Use the shorter-term 8-period EMA and the longer-term 20-period EMA to form golden cross and dead cross signals. The EMA moving average itself has trend following properties.
2. The ATR indicator reflects the recent fluctuation range. Through the normalization of the ATR indicator, the filtering conditions for EMA crossover can be dynamically adjusted, reducing the requirements when following a strong trend, and increasing the filtering requirements during volatile market conditions to control risks.
3. The ADX indicator determines the strength of the trend. When the ADX value is greater than 30, it is considered that a strong trend has emerged, and at this time, the loss should be stopped in time.
4. Judge the timing of long and short positions based on the rising and falling trends. In a bull market, the golden cross goes long, and in a bear market, the dead cross goes short.
5. Transaction volume filtering, enter the market when the transaction volume increases.
6. The USD index simply determines the strength of the US dollar. When the US dollar is strong, the stop loss and take profit ranges are expanded.
7. Combine with super trend indicators to judge the overall market trend and assist in judging the timing of long and short positions.
This strategy fully combines trend indicators and oscillators, and can dynamically adjust parameters to control risks while tracking trends.
## Strategic Advantages
1. Use the double EMA moving average system to judge trends. EMA has smoothness and can effectively filter out false breakthroughs.
2. The ATR indicator dynamically adjusts the EMA cross filtering conditions so that the strategy can flexibly adapt to different market environments.
3. The ADX indicator and trading volume are used as auxiliary judgment indicators to avoid being trapped in volatile market conditions.
4. Consider the US dollar index and super trend indicators to determine the general trend and improve the accuracy of decision-making.
5. Risk management parameters will be automatically adjusted according to the strength of the US dollar. When the US dollar is strong, the stop loss and take profit range will be enlarged.
6. Use simple and intuitive golden cross and dead cross trading signals and stop-loss and take-profit strategies, which are easy to implement and backtest.
## Strategy Risk
1. There is a lag in the judgment of the double EMA moving average system in removing the trend critical point.
2. Improper selection of ATR parameters may result in being too aggressive or conservative.
3. The ADX indicator parameters need to be optimized. Improper selection of ADX high points may miss the trend.
4. There may be errors in the judgment of the US dollar index and super trend indicators.
5. A stop loss that is too small may increase losses; a stop loss that is too wide may easily lead to traps.
## Optimization ideas
1. You can consider combining other indicators such as MACD to determine the trend critical point.
2. Use more historical data to train the ATR parameter space and find the optimal parameter range.
3. Test different ADX parameters and optimize ADX high point judgment.
4. Add more variables to determine the U.S. dollar index and overall market trends.
5. Calculate the optimal stop loss width based on backtest data.
6. You can consider changing the stop loss to a trailing stop loss or an oscillation stop loss.
7. Continue to optimize the size of the opening position and the position period.
## Summarize
This strategy integrates the classic double EMA moving average system and multiple auxiliary indicators, and realizes a more complete trend following strategy through automatic parameter optimization. It can flexibly adapt to changes in the market environment and control risks while tracking trends. However, further testing and optimization of stop loss and indicator parameters are still needed to obtain better stable returns. This strategic idea is worthy of reference and improvement.
||


## Overview

This strategy uses the classic dual EMA crossover system for trend following, with additional filters from the ATR and ADX indicators, to track strong trends and control risk during consolidations.

## Strategy Logic

The strategy is mainly based on the following:

1. Use a faster 8-period EMA and a slower 20-period EMA to generate crossover signals. EMAs themselves have trend-following properties.

2. The ATR indicator reflects recent volatility. Normalizing ATR allows dynamic adjustment of EMA crossover filter conditions, lowering requirements during strong trends and raising during consolidations to control risk.

3. The ADX indicator determines trend strength. An ADX reading above 30 suggests a strong trend, prompting timely stop loss. 

4. Combine with bull/bear trends to determine long/short entry timing. Go long on golden crosses in a bull market, and short on death crosses in a bear market.

5. Volume filter to enter when volume expands.

6. Use a simple USD index to determine USD strength, expanding stop and take profit range during strong USD.

7. Use the SuperTrend indicator to determine overall market direction for additional long/short timing aid.

The strategy combines trend and oscillation indicators to dynamically adjust parameters, tracking trends while controlling risk.

## Advantages of the Strategy

1. The dual EMA system provides trend determination, with EMA smoothness filtering false breaks.

2. ATR-normalized filters allow flexibility for different market environments.  

3. ADX and volume provide additional checks to avoid whipsaws during consolidations.

4. Considering USD and SuperTrend improves decision accuracy on the macro trend.

5. Risk management automatically adapts based on USD strength.

6. Simple golden/dead cross signals and stop/take profit logic make it easy to implement and backtest.

## Risks of the Strategy

1. Dual EMAs lag in detecting trend turning points. 

2. Poor ATR parameter selection may be too aggressive or conservative.

3. ADX parameters need optimization, improperly set high points could miss trends.

4. USD and SuperTrend trend determination could be inaccurate. 

5. Stop loss too tight increases losses, too wide risks whipsaws.

## Improvement Ideas

1. Consider adding indicators like MACD for better turnover point detection.

2. Optimize ATR parameters over more historical data. 

3. Test different ADX parameters and optimize high point thresholds.

4. Add more variables for USD and market trend analysis.

5. Calculate optimal stop loss percentage from backtest stats. 

6. Experiment with trailing or chandelier stops.

7. Continue optimizing entry size and holding period.

## Conclusion

This strategy integrates the classic dual EMA system with multiple auxiliary indicators, using parameterized optimization for a fairly robust trend following approach. It adapts flexibly to changing market environments, tracking trends while controlling risk. Further testing and optimization of stops and indicator parameters would improve results. The concepts are worth learning from and improving upon.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-10-15 00:00:00
end: 2023-11-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Refactored Advanced EMA Cross with Normalized ATR Filter, Controlling ADX", shorttitle="ALP V5", overlay=true)

// Initialize variables to track if a buy order has been placed and number of periods since the last buy
var bool hasBought = false
var int barCountSinceBuy = 0

// Define EMA periods
emaShort = ta.ema(close, 8)
emaLong = ta.ema(close, 20)

// Define ATR period and normalization
atrLength = 14
atrValue = ta.atr(atrLength)
maxHistoricalATR = ta.highest(atrValue, 20)
minHistoricalATR = ta.lowest(atrValue, 20)
normalizedATR = (atrValue - minHistoricalATR) / (maxHistoricalATR - minHistoricalATR)

// Define ADX parameters
adxValue = ta.rma(close, 14)
adxHighLevel = 30
isADXHigh = adxValue > adxHighLevel

// Initialize risk management variables
var float stopLossPercent = na
var float takeProfitPercent = na
var float trailingStop = na

// Calculate USD strength (simplified)
usd_strength = close / ta.ema(close, 50) - 1

// Adjust risk parameters based on USD strength
if (usd_strength > 0)
    stopLossPercent := 3
    takeProfitPercent := 6
else
    stopLossPercent := 4
    takeProfitPercent := 8

// Initialize position variable
var float positionPrice = na

// Volume filter
minVolume = ta.sma(volume, 14) * 1.5
isVolumeHigh = volume > minVolume



// Piyasa yönü için süper trend göstergesi
[supertrendValue, supertrendDirection] = ta.supertrend(4, 14)  // Use a factor of 3 and ATR period of 10
bool isBullMarket = supertrendDirection < 0
bool isBearMarket = supertrendDirection > 0

// Yükselen piyasa için alım koşulu
buyConditionBull = isBullMarket and ta.crossover(emaShort, emaLong) and normalizedATR > 0.2
// Düşen piyasa için alım koşulu
buyConditionBear = isBearMarket and ta.crossover(emaShort, emaLong) and normalizedATR > 0.5
// Genel alım koşulu
buyCondition = buyConditionBull or buyConditionBear

// Yükselen ve düşen piyasalar için farklı satış koşulları
sellConditionBull = isBullMarket and (ta.crossunder(emaShort, emaLong) or isADXHigh)
sellConditionBear = isBearMarket and (ta.crossunder(emaShort, emaLong) or isADXHigh)
// Genel satış koşulu
sellCondition = sellConditionBull or sellConditionBear


// Buy condition
if (buyCondition)
    strategy.entry("Buy", strategy.long)
    positionPrice := close
    hasBought := true // Set the flag to true when a buy order is placed
    barCountSinceBuy := 0 // Reset the bar counter when a buy order is placed

// Increase the bar counter if a buy has been executed
if (hasBought)
    barCountSinceBuy := barCountSinceBuy + 1

// Calculate stop-loss and take-profit levels
longStopLoss = positionPrice * (1 - stopLossPercent / 100)
longTakeProfit = positionPrice * (1 + takeProfitPercent / 100)


// Final Sell condition, now also checks if a buy has occurred before and if at least 5 periods have passed
finalSellCondition = sellCondition and hasBought and barCountSinceBuy >= 3 and isVolumeHigh

if (finalSellCondition)
    strategy.close("Buy")
    positionPrice := na
    hasBought := false // Reset the flag when a sell order is placed
    barCountSinceBuy := 0 // Reset the bar counter when a buy order is closed

// Implement stop-loss, take-profit, and trailing stop
strategy.exit("Stop Loss", "Buy", stop=longStopLoss)
strategy.exit("Take Profit", "Buy", limit=longTakeProfit)
//strategy.exit("Trailing Stop", "Buy", trail_price=close, trail_offset=trailingStop * close / 100)


var label l = na

if (buyCondition)
    l := label.new(bar_index, high, text="buy triggered " + str.tostring(usd_strength))
    label.delete(l[1])

if (finalSellCondition)
    l := label.new(bar_index, high, text="sell triggered " + str.tostring(usd_strength))
    label.delete(l[1])

// Plot signals
plotshape(series=buyCondition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="Buy")
plotshape(series=finalSellCondition, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="Sell")

```

> Detail

https://www.fmz.com/strategy/432212

> Last Modified

2023-11-15 15:53:57

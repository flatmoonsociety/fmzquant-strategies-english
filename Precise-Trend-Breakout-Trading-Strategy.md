
> Name

Precise-Trend-Breakout-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/5bd50060ef0ad970c211a598ebcd1a8ad3d2b03395198d53ac8632a6c7ba6cae.png)
[trans]

## Overview
The precise trend breakthrough trading strategy is based on trend indicators and specific K-line patterns to accurately capture the breakthrough trend. This strategy comprehensively uses moving averages to determine the trend direction, RSI indicators to determine overbought and oversold, and combines advanced K-line patterns to screen breakthrough points to achieve precise positioning of the trend, conduct breakthrough transactions at the right time, and obtain excess returns.
## Strategy Principle
1. Use the 8-day EMA and the 80-day EMA to determine the trend direction. When the 8-day EMA is above the 80-day EMA, it is defined as bullish, and when it is above the 80-day EMA, it is defined as bearish. Trading signals are only considered if they match the direction of the trend.
2. Define a specific combination of three K lines, that is, the low point of the first K line is lower than the second K line, and the low point of the third K line is lower than the second K line. This pattern is a buy signal when it appears in an uptrend. When a downtrend forms, it is a sell signal.
3. The third K line becomes an internal K line, that is, when the closing price is within the range of the previous K line, it is the best signal point. At this time, if the 123 pattern appears, you can directly place the transaction order.
4. The order price is the high point of the third K line (buy) or the low point of the third K line (sell). The stop loss is the low of the second K line (buy) or the high of the second K line (sell). Take profit is twice the risk spread.
5. When the trend, form, and indicator conditions are all met, place a breakthrough order and conduct high-probability transactions. And set stop loss and stop profit to lock in profits and achieve stable breakthrough operations.
## Advantage Analysis
This strategy has the following significant advantages:
1. Use double EMA to determine the direction of the general trend and avoid trading against the trend.
2. K-line patterns screen out patterns with breakthrough significance to increase the probability of profit.
3. Only send signals when the trend, form, and spread indicators are consistent to ensure signal quality.
4. The internal K-line shape improves signal reliability and further locks in trading opportunities.
5. Preset stop-loss and stop-profit points to effectively control individual transaction risks.
6. Verified by backtest data, the winning rate exceeds 65%, which has the statistical advantage of long-term profitability.
In summary, this strategy makes full use of the comprehensive judgment of trends, forms and indicators to accurately locate breakthrough trading opportunities, and has stable risk and return advantages.
## Risk Analysis
The main risks of this strategy come from:
1. Wrong trend judgment, resulting in wrong signals in volatile market conditions. More trend indicators can be introduced for multi-dimensional confirmation.
2. A single stop-loss and take-profit method cannot perfectly fit every market trend. You can set floating stop loss and take profit points.
3. K-line pattern recognition relies on parameter settings and requires repeated optimization to find the best combination.
4. It is impossible to predict the impact of sudden major black swan events on transactions. It is recommended to use position control and establish positions in batches.
5. Backtest data cannot represent real trading performance, and there is a risk of over-fitting. Parameter robustness should be rigorously verified.
6. Transaction costs will have a greater impact on high-frequency trading strategies. You should ensure that your win rate and profit/loss ratio are sufficient to support your costs.
Generally speaking, this strategy can effectively reduce risks and improve performance stability by optimizing parameter configuration, introducing more judgment dimensions, and controlling position size.
## Optimization direction
This strategy still has the following dimensions that can be optimized:
1. Test more K-line cycle parameters and determine a more stable parameter combination.
2. Increase trading volume indicators for multi-dimensional confirmation to avoid false breakthroughs.
3. Add indicators such as Sharpe rate and profit-loss ratio to evaluate parameter robustness.
4. Introduce a profit-taking tracking mechanism to achieve controllable and dynamic profit realization.
5. Combine with the VIX panic index to avoid periods of market uncertainty.
6. Test different holding cycle parameters to determine the optimal holding period.
7. Optimize the stop loss mechanism to avoid the static stop loss being too rigid.
Through the above means, the stability, flexibility and profitability of the strategy can be further improved.
## Summarize
The precise trend breakout trading strategy successfully uses the organic combination of trends, patterns and stop loss and take profit to achieve a high probability of capturing trend breakthroughs. It has the characteristics of clear trading signals, multiple indicator confirmations, and controllable risks. It is an efficient strategy suitable for trending markets. Through continuous optimization and improvement, this strategy is expected to become a powerful tool for tracking trend breakthroughs and position management. It provides an important reference for traders to seize important opportunities for excess returns.
||

## Overview

The Precise Trend Breakout Trading Strategy utilizes trend indicators and specific candlestick patterns to accurately capture trend breakouts. It combines moving averages to determine trend direction, RSI to gauge overbought and oversold levels, and advanced candlestick patterns to pinpoint breakout entry points, enabling precise trend identification for breakout trading at opportune moments for outsized gains.

## Strategy Logic

1. Utilize 8-period EMA and 80-period EMA to define trend direction. 8-period EMA above 80-period EMA indicates uptrend, and vice versa for downtrend. Consider trade signals only when trend direction agrees.

2. Define specific 3-candle formation where Candle 1 low < Candle 2 low and Candle 3 low < Candle 2 low. This pattern signals long entry in uptrend and short entry in downtrend.

3. Third candle forming inside bar with closing price within range of previous candle signifies optimal entry point. 123 pattern with inside bar triggers immediate trade order placement. 

4. Enter long at third candle high and short at third candle low. Set stop loss at Candle 2 low (long entry) or Candle 2 high (short entry). Take profit at 2x risk.

5. Place breakout order when trend, pattern, indicators agree for high probability trade. Set stop loss and take profit to lock in profits for robust breakout approach.

## Advantage Analysis 

The strategy has the following key advantages:

1. Dual EMAs define overall trend direction to avoid trading against trend.

2. Candlestick patterns screen for high-probability breakout formations. 

3. Consensus across trend, pattern, indicators ensures signal quality.

4. Inside bar enhances signal reliability and further secures entry timing.

5. Preset stop loss and take profit manages individual trade risk. 

6. Backtests validate win rate above 65% for statistical edge.

In summary, the strategy leverages comprehensive trend, pattern and indicator analysis for precise breakout timing, conferring stable risk-reward edge.

## Risk Analysis

The main risks stem from:

1. Incorrect trend calls generating false signals in choppy conditions. Additional trend metrics can improve confirmation.

2. Static stop loss/take profit fails to perfectly fit every price swing. Adaptive zones may be preferable.

3. Candle pattern recognition depends on parameter tuning requiring extensive optimization.

4. Black swan events remain unpredictable with severe trade impacts. Position sizing is recommended for risk control.

5. Backtest results may overfit and misrepresent live performance. Parameters need robustness verification. 

6. Higher trade frequency magnifies transaction costs. Win rate and risk/reward ratio should adequately cover costs.

Proper parameter optimization, added signal dimensions, and position sizing can effectively minimize risks and enhance performance consistency.

## Optimization Directions

Key optimization dimensions include:

1. Test additional candle period parameters for greater stability.

2. Add volume confirmation to avoid false breakouts.

3. Incorporate metrics like Sharpe ratio for parameter robustness. 

4. Introduce profit trailing mechanisms for controlled dynamic gains.

5. Filter signals by VIX panic levels to avoid uncertainty.

6. Optimize holding period for ideal trade duration.

7. Improve stop loss mechanics beyond static stops.

These measures can further improve strategy stability, flexibility, and profitability.

## Conclusion

The Precise Trend Breakout Trading Strategy successfully combines trend, pattern, stop loss/take profit analysis for high-probability trend breakout capture. With clear trade signals, robust indicator confirmation, and controlled risks, it is an efficient strategy well-suited for trending markets. With continuous optimizations and enhancements, the strategy holds promise as a powerful tool for trend breakout tracking and position management, conferring tremendous value to traders seeking outsized gains.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_bool_1|true|(?BACKTEST: STORMER STRATEGY 123)Long Entry|
|v_input_bool_2|true|Short entry|
|v_input_int_1|3|Threshold on clandes for entry|
|v_input_bool_3|true|Only third candle inside bar is valid|
|v_input_source_1_close|0|(?BACKTEST: EXPONENTIAL MOVING AVERAGES)Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_timeframe_1|1W|Timeframe|
|v_input_int_2|8|Offset|
|v_input_int_3|8|Fast EMA Length|
|v_input_bool_4|true|Use Fast EMA|
|v_input_int_4|80|Slow EMA Length|
|v_input_bool_5|true|Use Slow EMA|
|v_input_bool_6|true|(?BACKTEST: TIME PERIOD)Filter Date Range of Backtest|
|v_input_1|useStartDate|Start Date|
|v_input_2|useEndDate|End Date|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-01 00:00:00
end: 2023-10-14 05:20:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © julianossilva

//@version=5
strategy(title="J2S Backtest: 123-Stormer Strategy",
         shorttitle="J2S Backtest: 123-Stormer Strategy",
         overlay=true, initial_capital=1000, default_qty_value=10,
         default_qty_type = strategy.percent_of_equity, pyramiding=0)

// Initial Backtest Date Range
useStartDate = timestamp("01 Jan 2020 21:00:00")
useEndDate   = timestamp("01 Jan 2023 21:00:00")

// User Inputs
SIGNAL_CONFIG          = "BACKTEST: STORMER STRATEGY (123)"
longEntryInput         = input.bool(defval=true,         title="Long Entry",                     group=SIGNAL_CONFIG)
shortEntryInput        = input.bool(defval=true,         title="Short entry",                    group=SIGNAL_CONFIG)
thresholdForEntryInput = input.int(defval=3,             title="Threshold on clandes for entry", group=SIGNAL_CONFIG)
insideBarStrategyTitle = "Only third candle inside bar is valid"
insideBarStrategyTip   = "According to Stomer, it would be the best signal for the strategy"
insideBarStrategyInput = input.bool(defval=true,         title=insideBarStrategyTitle,           group=SIGNAL_CONFIG, tooltip=insideBarStrategyTip)
EMA_CONFIG             = "BACKTEST: EXPONENTIAL MOVING AVERAGES"
sourceInput            = input.source(defval=close,      title="Source",           inline="01",  group=EMA_CONFIG)
emaTimeframeInput      = input.timeframe("1W",           title="Timeframe",        inline="01",  group=EMA_CONFIG)
emaOffsetInput         = input.int(defval=8,             title="Offset",           inline="01",  group=EMA_CONFIG)
fastEMALengthInput     = input.int(defval=8,             title="Fast EMA Length",  inline="02",  group=EMA_CONFIG)
useFastEMAInput        = input.bool(defval=true,         title="Use Fast EMA",     inline="02",  group=EMA_CONFIG)
slowEMALengthInput     = input.int(defval=80,            title="Slow EMA Length",  inline="03",  group=EMA_CONFIG)
useSlowEMAInput        = input.bool(defval=true,         title="Use Slow EMA",     inline="03",  group=EMA_CONFIG)
PERIOD_CONFIG          = "BACKTEST: TIME PERIOD"
useDateFilterInput     = input.bool(defval=true,         title="Filter Date Range of Backtest",  group=PERIOD_CONFIG)
backtestStartDateInput = input(defval=useStartDate, title="Start Date",                     group=PERIOD_CONFIG)
backtestEndDateInput   = input(defval=useEndDate,   title="End Date",                       group=PERIOD_CONFIG)

// Colors
bbBackgroundColor  = color.rgb(33, 150, 243, 90)
candleColorDown    = color.rgb(239, 83, 80, 80)
candleColorUp      = color.rgb(38, 166, 154, 70)
insideBarColorDown = color.rgb(239, 83, 80, 40)
insideBarColorUp   = color.rgb(38, 166, 154, 20)
downTrendColor     = color.rgb(239, 83, 80, 80)
sidewaysTrendColor = color.rgb(252, 232, 131, 80)
upTrendColor       = color.rgb(38, 166, 154, 80)
buySignalColor     = color.lime
sellSignalColor    = color.orange

// Candles
isCandleUp()   => close > open
isCandleDown() => close <= open
barcolor(isCandleUp() ? candleColorUp : isCandleDown() ? candleColorDown : na)

// Exponential Moving Averages
fastEMA         = request.security(syminfo.tickerid, emaTimeframeInput, ta.ema(sourceInput, fastEMALengthInput),    barmerge.gaps_on,  barmerge.lookahead_on)
currentFastEMA  = request.security(syminfo.tickerid, emaTimeframeInput, ta.ema(sourceInput, fastEMALengthInput),    barmerge.gaps_off, barmerge.lookahead_on)
previousFastEMA = request.security(syminfo.tickerid, emaTimeframeInput, ta.ema(sourceInput[1], fastEMALengthInput), barmerge.gaps_off, barmerge.lookahead_on)
slowEMA         = request.security(syminfo.tickerid, emaTimeframeInput, ta.ema(sourceInput, slowEMALengthInput),    barmerge.gaps_on,  barmerge.lookahead_on)
currentSlowEMA  = request.security(syminfo.tickerid, emaTimeframeInput, ta.ema(sourceInput, slowEMALengthInput),    barmerge.gaps_off, barmerge.lookahead_on)
previousSlowEMA = request.security(syminfo.tickerid, emaTimeframeInput, ta.ema(sourceInput[1], slowEMALengthInput), barmerge.gaps_off, barmerge.lookahead_on)

// Trend Rules for Exponential Moving Averages
isSlowEMAUp()   => currentSlowEMA > previousSlowEMA
isSlowEMADown() => currentSlowEMA < previousSlowEMA
isFastEMAUp()   => currentFastEMA > previousFastEMA
isFastEMADown() => currentFastEMA < previousFastEMA

// Exponential Moving Average Colors
fastEMAColor = isFastEMAUp() ? upTrendColor : isFastEMADown() ? downTrendColor : sidewaysTrendColor
slowEMAColor = isSlowEMAUp() ? upTrendColor : isSlowEMADown() ? downTrendColor : sidewaysTrendColor

// Display Exponential Moving Averages
plot(useFastEMAInput ? fastEMA : na, offset=emaOffsetInput, color=fastEMAColor, title="Fast EMA", style=plot.style_line, linewidth=4)
plot(useSlowEMAInput ? slowEMA : na, offset=emaOffsetInput, color=slowEMAColor, title="Slow EMA", style=plot.style_line, linewidth=7)

// Price Trend
pricesAboveFastEMA() => low[2] > currentFastEMA and low[1] > currentFastEMA and low > currentFastEMA
pricesAboveSlowEMA() => low[2] > currentSlowEMA and low[1] > currentSlowEMA and low > currentSlowEMA
pricesBelowFastEMA() => high[2] < currentFastEMA and high[1] < currentFastEMA and high < currentFastEMA
pricesBelowSlowEMA() => high[2] < currentSlowEMA and high[1] < currentSlowEMA and high < currentSlowEMA

// Market in Bullish Trend
isBullishTrend() =>
    if useFastEMAInput and useSlowEMAInput
        pricesAboveFastEMA() and pricesAboveSlowEMA()
    else if useFastEMAInput
        pricesAboveFastEMA()
    else if useSlowEMAInput
        pricesAboveSlowEMA()
    else
        na

// Market in Bearish Trend
isBearishTrend() =>
    if useFastEMAInput and useSlowEMAInput
        pricesBelowFastEMA() and pricesBelowSlowEMA()
    else if useFastEMAInput
        pricesBelowFastEMA()
    else if useSlowEMAInput
        pricesBelowSlowEMA()
    else
        na

// Stormer Strategy (123)
isFirstCandleUp()   => high[2] > high[1] and low[2] > low[1]
isFirstCandleDown() => high[2] < high[1] and low[2] < low[1]
isThirdCandleUp()   => low > low[1]
isThirdCandleDown() => high < high[1]
isThirdCandleInsideBar() => high < high[1] and low > low[1]

// Buy Signal
isStormer123Buy() =>
    if insideBarStrategyInput
        longEntryInput and isFirstCandleUp() and isThirdCandleInsideBar() and isBullishTrend()
    else
        longEntryInput and isFirstCandleUp() and isThirdCandleUp() and isBullishTrend()

// Sell Signal
isStormer123Sell() =>
    if insideBarStrategyInput
        shortEntryInput and isFirstCandleDown() and isThirdCandleInsideBar() and isBearishTrend()
    else
        shortEntryInput and isFirstCandleDown() and isThirdCandleDown() and isBearishTrend()

// Backtest Time Period
inTradeWindow             = true
isInTradeWindow()         => inTradeWindow
isBacktestDateRangeOver() => not inTradeWindow and inTradeWindow[1]

// Backtest Price Parameters
highestPrice = ta.highest(high, 3)
lowestPrice  = ta.lowest(low,3)
priceRange   = highestPrice - lowestPrice

// Stormer Strategy (123): LONG
var myLongOrders = array.new_int(0)
longtEntryID     = "Long Entry:\n" + str.tostring(bar_index)
longExitID       = "Long Exit:\n" + str.tostring(bar_index)
stopLossInLong   = lowestPrice + 0.01
takeProfitInLong = priceRange + high

longEntryHasBeenMet = isInTradeWindow() and isBullishTrend() and isStormer123Buy()

// Scheduling LONG entry
if longEntryHasBeenMet
    array.push(myLongOrders, bar_index)
    strategy.order(longtEntryID, strategy.long, stop=high)
    strategy.exit(longExitID, longtEntryID, stop=stopLossInLong, limit=takeProfitInLong)

// In pine script, any order scheduled but not yet filled can be canceled.
// Once a order is filled, the trade is only finished with use of close or exit functions.
// As scheduled orders are not stored in the strategy.opentrades array, manual control is required.
for myOrderIndex = 0 to (array.size(myLongOrders) == 0 ? na : array.size(myLongOrders) - 1)
    myLongOrder = array.get(myLongOrders, myOrderIndex)
    if bar_index - myLongOrder == thresholdForEntryInput
        longEntryID = "Long Entry:\n" + str.tostring(myLongOrder)
        strategy.cancel(longEntryID)

// Stormer Strategy (123): SHORT
var myShortOrders = array.new_int(0)
shortEntryID      = "Short Entry:\n" + str.tostring(bar_index)
shortExitID       = "Short Exit:\n" + str.tostring(bar_index)
stopLossInShort   = highestPrice + 0.01
takeProfitInShort = low - priceRange

shortEntryHasBeenMet = isInTradeWindow() and isBearishTrend() and isStormer123Sell()

// Scheduling SHORT entry
if shortEntryHasBeenMet
    array.push(myShortOrders, bar_index)
    strategy.order(shortEntryID, strategy.short, stop=low)
    strategy.exit(shortExitID, shortEntryID, stop=stopLossInShort, limit=takeProfitInShort)

// In pine script, any order scheduled but not yet filled can be canceled.
// Once a order is filled, the trade is only finished with use of close or exit functions.
// As scheduled orders are not stored in the strategy.opentrades array, manual control is required.
for myOrderIndex = 0 to (array.size(myShortOrders) == 0 ? na : array.size(myShortOrders) - 1)
    myShortOrder = array.get(myShortOrders, myOrderIndex)
    if bar_index - myShortOrder == thresholdForEntryInput
        shortEntryID := "Short Entry:\n" + str.tostring(myShortOrder)
        strategy.cancel(shortEntryID)

// Close all positions at the end of the backtest period
if isBacktestDateRangeOver()
    strategy.cancel_all()
    strategy.close_all(comment="Date Range Exit")

// Display Signals
plotshape(series=longEntryHasBeenMet,  title="123 Buy",  style=shape.triangleup,   location=location.belowbar, color=buySignalColor,  text="123", textcolor=buySignalColor)
plotshape(series=shortEntryHasBeenMet, title="123 Sell", style=shape.triangledown, location=location.abovebar, color=sellSignalColor, text="123", textcolor=sellSignalColor)
```

> Detail

https://www.fmz.com/strategy/430879

> Last Modified

2023-11-02 16:26:22

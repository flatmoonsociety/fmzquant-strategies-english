
> Name

Trend reversal trading strategy based on Ichimoku Balance Sheet Ichimoku-and-MACD-Trend-Reversal-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


## Overview
This strategy integrates the Ichimoku Balance Sheet indicator and the MACD indicator, and enters the market after confirming the trend reversal. It is a trend reversal trading strategy.
## Strategy Principle
1. Calculate the turning line of the Ichimoku Balance Sheet as an indicator to determine the trend direction. When the price is above the turning line, it is a long market, and when the price is below it, it is a short market.
2. The MACD indicator generates a sell signal when a dead cross forms in the bull market; it generates a buy signal when a golden cross forms in the bear market.
3. Combine the trend judgment of Ichimoku Balance Sheet and the reversal signal of MACD to conduct reverse trading at the trend reversal point.
4. Trading time control can be set, such as ending trading at night, no trading on weekends, etc., to avoid risks in specific time periods.
5. Adopt appropriate stop-loss and take-profit strategies to lock in profits and control risks.
## Advantage Analysis
1. The Ichimoku Balance Sheet indicator intuitively displays trends and support pressure levels.
2. The MACD indicator is more sensitive to capturing trend reversal.
3. Combined with trend judgment and reversal signals, false signals can be filtered out.
4. The trading time period can be customized to avoid risks at important time points.
5. Setting up stop-loss and take-profit strategies can effectively manage capital risks.
## Risk Analysis
1. The Ichimoku Balance Sheet and MACD indicator may misjudge signals.
2. It is impossible to judge the strength of the reversal, and there is a risk of chasing the top and chasing the bottom.
3. Trading time control may miss some trading opportunities.
4. Improper stop loss and take profit settings may result in premature stop loss or take profit.
5. Parameter optimization may be over-optimized and result in poor results.
## Optimization direction
1. Test the parameters of the Ichimoku Balance Table and MACD to find the optimal parameter combination.
2. Add other indicators to confirm trading signals.
3. Optimize stop-loss and take-profit strategies to balance risks and returns.
4. Evaluate the necessity of trading time control and relax it appropriately.
5. Add trend filter to avoid reversal trading losses.
6. Study how to judge the strength of a reversal and the height of a potential retracement.
## Summarize
This strategy integrates the trend judgment of Ichimoku Balance Sheet and the reversal trading signal of MACD, and makes trading decisions after confirming the trend reversal. By further optimizing parameters and strategies, the risk of signal misjudgment can be reduced and a stable and efficient trend reversal trading system can be built.
||

## Overview

This strategy combines Ichimoku and MACD indicators, entering trades after confirming trend reversal. It belongs to trend reversal trading strategies.

## Strategy Logic 

1. Calculate Ichimoku Tenkan line to gauge trend direction. Price above it indicates uptrend, and below downtrend.

2. MACD death cross generates sell signal in uptrend; golden cross buy signal in downtrend.

3. Combine Ichimoku trend bias and MACD reversal signals to trade trend reversals. 

4. Option to set trading hour control, like no trading at night or weekends, to avoid risks associated with certain times.

5. Employ proper stop loss and take profit for profit locking and risk control.

## Advantages

1. Ichimoku intuitively displays trends and support/resistance levels.

2. MACD sensitively captures trend reversals.

3. Combining trend bias and reversal improves signal quality. 

4. Customizable trading hours avoid risks around major news events.

5. Stop loss and take profit effectively manages capital risks.

## Risks

1. Ichimoku and MACD may generate false signals.

2. Reversal strength unknown, risks of chasing tops and bottoms.

3. Trading hour control may miss some opportunities. 

4. Improper stop loss and take profit settings lead to premature exit. 

5. Parameter optimization may lead to overfitting.

## Enhancement

1. Test Ichimoku and MACD parameters for optimal combinations.

2. Add other indicators to confirm trading signals.

3. Optimize stops and profits to balance risks and returns.

4. Evaluate necessity of trading hour control and relax if appropriate.

5. Incorporate trend filter to avoid losses from reversal trades. 

6. Research ways to gauge reversal strength and potential pullback height.

## Conclusion

This strategy combines Ichimoku's trend bias and MACD's reversal signals to trade after trend reversals. Further optimization and enhancements can reduce signal errors and improve stability and efficiency as a robust trend reversal system.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|9|IchimokuTenkanPeriod|
|v_input_2|190|IchimokuKijunPeriod|
|v_input_3|52|IchimokuSenkouPeriod|
|v_input_4|3|MACDMainFast|
|v_input_5|10|MACDMainSlow|
|v_input_6|9|MACDMainSmooth|
|v_input_7|2|ExitAfterBars|
|v_input_8|135|ProfitTarget|
|v_input_9|70|StopLoss|
|v_input_10|true|DontTradeOnWeekends|
|v_input_11|true|ExitAtEndOfDay|
|v_input_12|23|DayExitTimeHour|
|v_input_13|4|DayExitTimeMinute|
|v_input_14|true|ExitOnFriday|
|v_input_15|20|FridayExitTimeHour|
|v_input_16|40|FridayExitTimeMinute|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-09-13 00:00:00
end: 2023-09-19 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © Revazi

//@version=5
strategy("The Impeccable by zyberal", overlay = true)

// Inputs {
// Strategy variables
IchimokuTenkanPeriod = input(9)
IchimokuKijunPeriod = input(190)
IchimokuSenkouPeriod = input(52)
MACDMainFast = input(3)
MACDMainSlow = input(10)
MACDMainSmooth = input(9)
ExitAfterBars = input(2)
ProfitTarget = input(135)
StopLoss = input(70)

// Trading Options
DontTradeOnWeekends = input(true)
ExitAtEndOfDay = input(true)
DayExitTimeHour   = input(23)
DayExitTimeMinute = input(04)

ExitOnFriday = input(true)
FridayExitTimeHour   = input(20)
FridayExitTimeMinute = input(40)

// }



// TRADING OPTIONS LOGIC {
OpenOrdersAllowed = true

// Dont trade on weekends {
if DontTradeOnWeekends
    if dayofweek == dayofweek.saturday or
       dayofweek == dayofweek.sunday
        OpenOrdersAllowed := false
// }

// Exit on close (end of day) {
if ExitAtEndOfDay
    if timeframe.isintraday and
       time >= timestamp(year(timenow), month(timenow), dayofmonth(timenow), DayExitTimeHour, DayExitTimeMinute)
        OpenOrdersAllowed := false
// }

// Exit on Friday {
if ExitOnFriday
    if timeframe.isintraday and
       time >= timestamp(year(timenow), month(timenow), dayofmonth(timenow), FridayExitTimeHour, FridayExitTimeMinute)
        OpenOrdersAllowed := false
// }


// Rule: Trading signals {
openW3 = request.security(syminfo.tickerid, "W", open)[3]

middleDonchian(Length) => math.avg(ta.highest(Length), ta.lowest(Length))
Tenkan = middleDonchian(IchimokuTenkanPeriod)[2]

[macdLine, signalLine, _] = ta.macd(close, MACDMainFast, MACDMainSlow, MACDMainSmooth)

LongEntrySignal = openW3 > Tenkan and ta.crossunder(macdLine, signalLine)[3] //macdLine[3] < signalLine[3]
ShortEntrySignal = openW3 < Tenkan and ta.crossover(macdLine, signalLine)[3] //macdLine[3] > signalLine[3]
// }



// Calculate conditions {
IsFlat() => strategy.position_size == 0
IsLong() => strategy.position_size > 0
IsShort() => strategy.position_size < 0

longCondition  = OpenOrdersAllowed and not IsLong() and LongEntrySignal
shortCondition = OpenOrdersAllowed and not IsShort() and ShortEntrySignal

// }

// Open positions based on conditions {
strategy.order(id = "buy", direction = strategy.long, qty = 1, when = longCondition)
strategy.order(id = "sell", direction = strategy.short, qty = 1, when = shortCondition)
// }


```

> Detail

https://www.fmz.com/strategy/427385

> Last Modified

2023-09-20 15:44:13

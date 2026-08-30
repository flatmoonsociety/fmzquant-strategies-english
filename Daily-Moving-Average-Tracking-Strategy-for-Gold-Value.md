
> Name

Daily-Moving-Average-Tracking-Strategy-for-Gold-Value
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/b4411c94be124c189c9674515afcc3060fb6bda2b39557a861d233c4e9fd844a.png)
[trans]

## Overview
This strategy uses the previous day's opening and closing prices, as well as the combination of fast EMA and slow EMA, to determine the value direction of the market within a user-defined trading time period and make corresponding buy or sell operations. Also, strategies use trailing stops to lock in profits or limit losses.
## Strategy Principle
This strategy determines the value direction of the gold standard mainly based on two points:
1. The increase or decrease of the previous day's closing price relative to the opening price. If the closing price is higher than the opening price, it means that the overall value of the day has increased; if the closing price is lower than the opening price, it means that the overall value of the day has decreased.
2. The positional relationship between the 50-period fast EMA and the 200-period slow EMA. If the fast line is above the slow line, it means that the short-term value rises faster than the long-term trend; if the fast line is below the slow line, it means that the short-term value rises faster than the long-term trend.
When the long conditions are met, if the previous day's closing price is higher than the opening price, the current price is higher than the previous day's opening price, and the fast EMA is higher than the slow EMA, and within the user-defined trading time, the strategy will go long on the gold standard.
When the short selling conditions are met, if the closing price of the previous day is lower than the opening price, the current price is lower than the opening price of the previous day, and the fast EMA is lower than the slow EMA, and within the user-defined trading time, the strategy will short the gold standard.
Additionally, the strategy uses trailing stops to lock in profits or limit losses. The trailing stop distance is adjusted according to the initial distance and moving step set by the user.
## Advantage Analysis
This strategy has the following advantages:
1. Use multiple indicators to judge the value direction of the gold standard, reducing the probability of wrong transactions.
2. Trailing stop loss can effectively lock in profits, stop losses in time when the market reverses, and reduce risks.
3. Users can choose the appropriate trading range according to their own trading time to avoid being stuck during institutional operation periods.
4. The period value of EMA can be adjusted and optimized according to market changes, making the strategy more flexible.
## Risk Analysis
This strategy also has certain risks:
1. When unexpected events occur, the strategy may cause large losses. This requires manual intervention or setting a more relaxed stop loss distance.
2. EMA cannot completely filter out market noise. When EMA generates false signals, it can trigger unnecessary trades. You can appropriately optimize EMA parameters or add other filtering indicators.
3. Improper setting of trailing stop loss distance will also increase risks. If the distance is too close, it is easy to be stopped out; if the distance is too far, the loss cannot be effectively controlled. Testing is required to determine optimal parameters.
## Optimization direction
This strategy can also be optimized from the following aspects:
1. Add other technical indicators to filter signals, such as MACD, Bollinger Bands, etc., to reduce the probability of EMA false signals.
2. Change the trailing stop loss to an adaptive stop loss, and intelligently adjust the stop loss distance according to the degree of market fluctuations.
3. Add a position management module to allow risk control by dividing positions to reduce the impact of a single loss.
4. Add a machine learning model to determine the trend direction, and use more historical data to improve the accuracy of judgment.
5. Optimize the selection of trading time periods and select trading ranges with higher strategic participation based on normal distribution.
## Summarize
Overall, this strategy is a typical trend following strategy. It combines a variety of indicators to determine the trend direction of rising and falling values, and is a relatively robust strategy type. The application of trailing stop loss also makes it possible to effectively control losses. Through continuous optimization of indicators and stop-loss rules, the strategy can achieve a better balance between return and risk control. It is suitable for investors who have a certain quantitative investment foundation and want to participate in digital currency transactions.
|| 

## Overview

This strategy uses a combination of the previous day’s open and close prices, fast EMA line and slow EMA line to determine the direction of market value within the user-defined trading time period, and makes corresponding long or short entries. Meanwhile, the strategy uses trailing stop loss to lock in profits or limit losses. 

## Strategy Logic

The strategy mainly bases its judgment of gold value direction on two aspects:

1. The rise and fall of previous day’s close price relative to open price. If close price is higher than open price, it indicates that the overall value rose during that day. If close price is lower than open price, it indicates that the overall value dropped during that day.

2. The position relationship between the 50-period fast EMA line and 200-period slow EMA line. If the fast line is above slow line, it means short-term value rising speed is greater than long-term trend. If fast line is below slow line, it means short-term value rising speed is less than long-term trend.

When the long condition triggers, if previous day’s close is higher than open, current price is above previous day’s open, fast EMA is above slow EMA, and it is within user-defined trading hours, the strategy will go long gold.

When the short condition triggers, if previous day’s close is lower than open, current price is below previous day’s open, fast EMA is below slow EMA, and it is within user-defined trading hours, the strategy will go short gold.

In addition, the strategy uses trailing stop loss to lock in profits or limit losses. The trailing stop distance adjusts based on initial user setting and move step.

## Advantage Analysis 

The advantages of this strategy are:

1. Using multiple indicators to determine gold value direction reduces the probability of bad trades.

2. Trailing stop can effectively lock in profits, and exit in a timely manner when trend reverses, lowering risks.

3. Users can choose suitable trading windows based on their own trading time to avoid being trapped during institutional operations.

4. The EMA period values can be adjusted and optimized according to market changes, making the strategy more flexible.

## Risk Analysis

There are also some risks with this strategy:

1. Sudden events may incur large losses that need manual intervention or more relaxed stop loss distance. 

2. EMA cannot fully filter market noise. Erroneous signals can trigger unnecessary trades. Parameters can be optimized or more filters added.

3. Improper trailing stop distance settings also increase risks - too tight tends to get stopped out prematurely while too wide fails to control losses effectively. Extensive testing is needed to determine optimal values.

## Optimization Directions

The strategy can also be optimized in the following aspects:

1. Add other technical indicators for signal filtering, like MACD, Bollinger Bands etc. to reduce erroneous EMA signals.

2. Change to adaptive stops that adjust stop distance intelligently based on market volatility. 

3. Add position sizing rules to allow partial exits for better risk control and lower impact of single trade losses.

4. Add machine learning models to determine trend direction, improving accuracy using more historical data.

5. Optimize trading time window selection using Gaussian distribution to target higher strategy participation intervals.

## Conclusion

In summary, this is a typical trend following strategy. It combines multiple indicators to determine upward or downward value trends and is considered robust. The trailing stop application also allows effective loss control. Further optimizations to the indicators and stop loss rules can achieve an improved balance between returns and risk management. It suits investors with some quant investing knowledge who wish to participate in cryptocurrency trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|11|Start Hour|
|v_input_2|16|End Hour|
|v_input_3|100|Trailing Stop Start (pips)|
|v_input_4|10|Trailing Step (pips)|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-04 00:00:00
end: 2024-01-11 00:00:00
period: 45m
basePeriod: 5m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("My Strategy", overlay=true)

// Inputs for user to modify
startHour = input(11, title="Start Hour")
endHour = input(16, title="End Hour")
trailingStop = input(100, title="Trailing Stop Start (pips)")
trailingStep = input(10, title="Trailing Step (pips)")

// Define the EMAs
longEma = ema(close, 200)
shortEma = ema(close, 50)

// Calculate daily open, high, low, close
daily_open = security(syminfo.tickerid, "D", open[1])
daily_close = security(syminfo.tickerid, "D", close[1])

// Time conditions
timeAllowed = (hour >= startHour) and (hour <= endHour)

// Define long condition based on your criteria
longCondition = (daily_close > daily_open) and (close > daily_open) and (shortEma > longEma) and timeAllowed

// Define short condition based on your criteria
shortCondition = (daily_close < daily_open) and (close < daily_open) and (shortEma < longEma) and timeAllowed

// Enter the trade
if (longCondition)
    strategy.entry("Long", strategy.long)

if (shortCondition)
    strategy.entry("Short", strategy.short)

// Trailing Stop Loss
strategy.exit("Exit Long", "Long", trail_points = trailingStop / syminfo.mintick, trail_offset = trailingStep / syminfo.mintick)
strategy.exit("Exit Short", "Short", trail_points = trailingStop / syminfo.mintick, trail_offset = trailingStep / syminfo.mintick)

// Plotting
plot(daily_open, color=color.red, title="Daily Open")
plot(longEma, color=color.blue, title="200 EMA")
plot(shortEma, color=color.orange, title="50 EMA")

```

> Detail

https://www.fmz.com/strategy/438466

> Last Modified

2024-01-12 11:54:21

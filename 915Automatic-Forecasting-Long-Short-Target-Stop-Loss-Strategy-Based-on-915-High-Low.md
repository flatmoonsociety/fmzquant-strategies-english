
> Name

Automatic-Forecasting-Long-Short-Target-Stop-Loss-Strategy-Based-on-915-High-Low
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/177c2d01e2d3c06a88d.png)
[trans]

## Overview
This strategy automatically calculates the target price and stop loss price in the long and short direction based on the high and low points of the 9:15 minute K line. Use the RSI indicator to determine the overbought and oversold conditions of the current market, and open a position when the price breaks through the 9:15 high and low point and the RSI meets the conditions. This strategy can automatically predict the target price and stop loss price in the long and short directions, simplifying the traders' operation process.
## Strategy Principle
1. Determine the high and low points of the K-line at 9:15 minutes, respectively, as the key prices for the long and short directions.
2. Long direction: The target price is 9:15 high + 200 points, and the stop loss price is 9:15 low.
3. Short direction: The target price is 9:15 low -200 points, and the stop loss price is 9:15 high.
4. Calculate the RSI indicator. The default parameter is 14, the overbought line is 60, and the oversold line is 40.
5. Conditions for opening a long position: the closing price breaks through the 9:15 high, and the RSI is greater than the overbought line.
6. Short position opening conditions: the closing price breaks through the 9:15 low, and the RSI is less than the oversold line.
7. When the conditions for opening a position are met, execute the corresponding long or short position opening operation.
8. Draw the 9:15 high and low points, long and short target prices and stop loss prices, and opening signals on the chart.
This strategy uses the high and low points of the 9:15 minute K-line as the key price to automatically calculate the target and stop loss in the long and short directions, simplifying the traders' operations. At the same time, the RSI indicator is introduced as a filtering condition, which can avoid frequent openings and false breakthroughs to a certain extent.
## Advantage Analysis
1. Automatically calculate the long and short target and stop loss: This strategy automatically calculates the target price and stop loss price in the long and short direction based on the high and low points of the 9:15 minute K line. Traders do not need to set up manually, which simplifies the operation process and improves transaction efficiency.
2. RSI indicator filtering: The strategy introduces the RSI indicator as a filtering condition for opening a position. When the price breaks through a key position, the RSI indicator also needs to reach an overbought or oversold state to trigger a position opening signal. This can help traders avoid frequent trading and false breakthrough traps to a certain extent.
3. Intuitive chart display: This strategy draws the 9:15 high and low points, long and short target prices, stop loss prices and opening signals on the chart. Traders can intuitively see key price levels and trading signals to facilitate making trading decisions.
4. Suitable for short-term trading: This strategy is based on the high and low points of 9:15 minutes, and the target price and stop loss price are set relatively close. Therefore, this strategy is more suitable for short-term trading operations, which can quickly enter and exit and capture short-term price fluctuations.
## Risk Analysis
1. Intraday fluctuation risk: This strategy uses the high and low points of the 9:15 minute K line as the key position, but intraday prices may fluctuate significantly. If the price reverses quickly after triggering a position opening, it may cause traders to lose more than expected.
2. Stop loss position risk: The stop loss position in the strategy is fixed, that is, the stop loss position for long positions is the low point of 9:15, and the stop loss position for short positions is the high point of 9:15. If the price continues to move sharply after breaking through the 9:15 high and low points, the fixed stop loss position may lead to larger losses.
3. RSI indicator parameter risk: This strategy uses the default RSI parameters, that is, the length is 14, the overbought line is 60, and the oversold line is 40. However, in different market environments and targets, these parameters may not be applicable. Fixed parameter settings may affect the effectiveness of the strategy.
4. Profit-loss ratio risk: The fixed target price and stop-loss price in the strategy determine the profit-loss ratio of each transaction. If the profit-loss ratio is set improperly, it may lead to poor profitability of the strategy in the long term.
Solution:
1. For intraday fluctuation risks, you can consider introducing more filtering conditions, such as adding trading volume indicators, or narrowing the stop loss range.
2. For stop loss position risks, you can consider using trailing stop loss or conditional stop loss, and dynamically adjust the stop loss position according to market conditions.
3. For RSI indicator parameter risk, parameters can be optimized for different markets and targets to find a more suitable parameter combination.
4. Regarding the profit-loss ratio risk, you can test different target price and stop-loss price combinations based on historical data to find a better profit-loss ratio setting.
## Optimization direction
1. Dynamic stop loss: The current strategy uses a fixed stop loss position. You can consider introducing a dynamic stop loss mechanism, such as trailing stop loss or conditional stop loss. This allows timely control of risks when prices fluctuate beyond expectations.
2. Introduce more filtering conditions: The strategy currently mainly relies on price breakthroughs and RSI indicators. You can consider introducing more filtering conditions, such as trading volume indicators, volatility indicators, etc. Through the joint confirmation of multiple conditions, the effectiveness of the position opening signal can be improved.
3. Parameter optimization: The parameter settings of the RSI indicator can be optimized for different markets and targets. Through testing historical data, we can find a parameter combination that is more suitable for the current trading target and improve the stability of the strategy.
4. Profit-loss ratio optimization: The profit-loss ratio of the strategy has an important impact on long-term returns. You can backtest historical data and test different target price and stop-loss price combinations to find profit-loss ratio settings that can bring higher returns.
5. Add trend judgment: This strategy currently mainly relies on the breakthrough of intraday high and low points, which is a counter-trend transaction. You can consider adding trend judgment and trading in the direction of the general trend to improve your winning rate and profit-loss ratio.
## Summarize
This strategy automatically calculates the long and short target price and stop loss price based on the high and low points of the 9:15 minute K-line, and uses the RSI indicator as a filter condition to simplify the trader's operation process. The advantage of the strategy is that it has a high degree of automation, is intuitive and easy to use, and is suitable for short-term trading operations. But there are also some risks, such as intraday fluctuation risk, stop loss position risk, indicator parameter risk and profit-loss ratio risk. To address these risks, strategy improvements can be made from dynamic stop loss, introducing more filtering conditions, parameter optimization, profit-loss ratio optimization and trend judgment. Through continuous optimization and improvement, the stability and profitability of this strategy can be improved and better adapted to different market environments.
|| 

## Overview

This strategy automatically calculates long and short target prices and stop loss levels based on the high and low of the 9:15 minute candle. It uses the RSI indicator to determine the current overbought or oversold state of the market and triggers a long or short entry when the price breaks the 9:15 high/low and the RSI condition is met. The strategy simplifies the trading process by automatically predicting target prices and stop loss levels for long and short directions.

## Strategy Principle

1. Determine the high and low of the 9:15 minute candle as key levels for long and short directions.
2. Long direction: target price is 9:15 high + 200 points, stop loss is 9:15 low.
3. Short direction: target price is 9:15 low - 200 points, stop loss is 9:15 high.
4. Calculate the RSI indicator with default parameters of 14, overbought line at 60, and oversold line at 40.
5. Long entry condition: close price breaks above 9:15 high and RSI is greater than the overbought line.
6. Short entry condition: close price breaks below 9:15 low and RSI is less than the oversold line.
7. Execute the corresponding long or short entry when the entry conditions are met.
8. Plot the 9:15 high/low, long/short target prices, stop loss levels, and entry signals on the chart.

The strategy utilizes the high and low of the 9:15 minute candle as key levels and automatically calculates the target prices and stop losses for long and short directions, simplifying the trader's operation. Additionally, it introduces the RSI indicator as a filter condition, which can help avoid frequent entries and false breakouts to a certain extent.

## Advantage Analysis

1. Automatic calculation of long/short targets and stop losses: The strategy automatically calculates the target prices and stop loss levels for long and short directions based on the 9:15 high/low. Traders do not need to set them manually, simplifying the operation process and improving trading efficiency.

2. RSI indicator filter: The strategy introduces the RSI indicator as a filter condition for entry. When the price breaks a key level, the RSI needs to reach the overbought or oversold state to trigger an entry signal. This can help traders avoid frequent trading and false breakout traps to a certain extent.

3. Intuitive chart display: The strategy plots the 9:15 high/low, long/short target prices, stop loss levels, and entry signals on the chart. Traders can intuitively see the key levels and trading signals, facilitating their decision-making.

4. Suitable for short-term trading: The strategy is based on the high and low of the 9:15 minute candle, and the target prices and stop losses are set relatively close. Therefore, it is more suitable for short-term trading operations, allowing for quick entries and exits to capture short-term price movements.

## Risk Analysis

1. Intraday volatility risk: The strategy uses the 9:15 high/low as key levels, but prices may experience significant fluctuations during the trading day. If the price quickly reverses after triggering an entry, it may cause the trader's loss to exceed expectations.

2. Stop loss level risk: The stop loss levels in the strategy are fixed, with the long stop loss at the 9:15 low and the short stop loss at the 9:15 high. If the price continues to move significantly after breaking the 9:15 high/low, the fixed stop loss levels may result in larger losses.

3. RSI indicator parameter risk: The strategy uses default RSI parameters, with a length of 14, overbought line at 60, and oversold line at 40. However, these parameters may not be suitable for different market environments and instruments. Fixed parameter settings may affect the effectiveness of the strategy.

4. Risk-reward ratio risk: The fixed target prices and stop loss levels in the strategy determine the risk-reward ratio of each trade. If the risk-reward ratio is not set appropriately, it may lead to poor long-term profitability of the strategy.

Solutions:
1. For intraday volatility risk, consider introducing more filter conditions, such as volume indicators or narrowing the stop loss range.
2. For stop loss level risk, consider using trailing stop losses or conditional stop losses to dynamically adjust the stop loss levels based on market conditions.
3. For RSI indicator parameter risk, optimize the parameters for different markets and instruments to find more suitable combinations.
4. For risk-reward ratio risk, test different target price and stop loss combinations based on historical data to find more optimal risk-reward ratio settings.

## Optimization Directions

1. Dynamic stop loss: The current strategy uses fixed stop loss levels. Consider introducing dynamic stop loss mechanisms, such as trailing stop losses or conditional stop losses. This allows for timely risk control when prices experience unexpected volatility.

2. Introducing more filter conditions: The strategy currently relies mainly on price breakouts and the RSI indicator. Consider adding more filter conditions, such as volume indicators or volatility indicators. By confirming entry signals through multiple conditions, the effectiveness of the signals can be improved.

3. Parameter optimization: Optimize the RSI indicator parameters for different markets and instruments. By testing historical data, find parameter combinations that are more suitable for the current trading instrument to improve the stability of the strategy.

4. Risk-reward ratio optimization: The risk-reward ratio has a significant impact on long-term profitability. By backtesting historical data, test different target price and stop loss combinations to find risk-reward ratio settings that can generate higher returns.

5. Incorporating trend analysis: The current strategy mainly relies on intraday high/low breakouts, which is a counter-trend approach. Consider incorporating trend analysis to trade in the direction of the larger trend, improving the win rate and risk-reward ratio.

## Conclusion

This strategy automatically calculates long and short target prices and stop loss levels based on the 9:15 high/low, while using the RSI indicator as a filter condition, simplifying the trader's operation process. The advantages of the strategy lie in its high degree of automation, intuitive usability, and suitability for short-term trading operations. However, it also involves certain risks, such as intraday volatility risk, stop loss level risk, indicator parameter risk, and risk-reward ratio risk. To address these risks, the strategy can be improved through dynamic stop losses, introducing more filter conditions, parameter optimization, risk-reward ratio optimization, and trend analysis. By continuously optimizing and improving the strategy, its stability and profitability can be enhanced to better adapt to different market environments.
[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Show Signals|
|v_input_2|9|Session Start Hour|
|v_input_3|false|Session Start Minute|
|v_input_4|9|Session End Hour|
|v_input_5|15|Session End Minute|
|v_input_6|14|RSI Length|
|v_input_7|60|Overbought Level|
|v_input_8|40|Oversold Level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-01 00:00:00
end: 2024-02-29 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("9:15 AM High/Low with Automatic Forecasting", overlay=true)

// Parameters
showSignals = input(true, title="Show Signals")

// Define session time
sessionStartHour = input(9, title="Session Start Hour")
sessionStartMinute = input(0, title="Session Start Minute")
sessionEndHour = input(9, title="Session End Hour")
sessionEndMinute = input(15, title="Session End Minute")

// Calculate session high and low
var float sessionHigh = na
var float sessionLow = na
if (hour == sessionStartHour and minute == sessionStartMinute)
    sessionHigh := high
    sessionLow := low

// Update session high and low if within session time
if (hour == sessionStartHour and minute >= sessionStartMinute and minute < sessionEndMinute)
    sessionHigh := high > sessionHigh or na(sessionHigh) ? high : sessionHigh
    sessionLow := low < sessionLow or na(sessionLow) ? low : sessionLow

// Plot horizontal lines for session high and low
plot(sessionHigh, color=color.green, title="9:00 AM High", style=plot.style_stepline, linewidth=1)
plot(sessionLow, color=color.red, title="9:00 AM Low", style=plot.style_stepline, linewidth=1)

// Calculate targets and stop loss
longTarget = sessionHigh + 200
longStopLoss = sessionLow
shortTarget = sessionLow - 200
shortStopLoss = sessionHigh

// Plot targets and stop loss
plot(longTarget, color=color.blue, title="Long Target", style=plot.style_cross, linewidth=1)
plot(longStopLoss, color=color.red, title="Long Stop Loss", style=plot.style_cross, linewidth=1)
plot(shortTarget, color=color.blue, title="Short Target", style=plot.style_cross, linewidth=1)
plot(shortStopLoss, color=color.red, title="Short Stop Loss", style=plot.style_cross, linewidth=1)

// RSI
rsiLength = input(14, title="RSI Length")
overboughtLevel = input(60, title="Overbought Level")
oversoldLevel = input(40, title="Oversold Level")
rsi = ta.rsi(close, rsiLength)

// Entry conditions
longCondition = close > sessionHigh and rsi > overboughtLevel
shortCondition = close < sessionLow and rsi < oversoldLevel

// Long entry
if (showSignals and longCondition)
    strategy.entry("Long", strategy.long)

// Short entry
if (showSignals and shortCondition)
    strategy.entry("Short", strategy.short)

```

> Detail

https://www.fmz.com/strategy/445477

> Last Modified

2024-03-19 18:37:37

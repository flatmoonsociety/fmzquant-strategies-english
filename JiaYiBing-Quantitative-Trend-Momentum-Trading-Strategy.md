
> Name

JiaYiBing-Quantitative-Trend-Momentum-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/8f51bd3a61fa03de16.png)
[trans]
## Overview
Jia Yibing's quantitative trend momentum trading strategy is a long and short quantitative trading strategy that combines trend tracking, momentum indicators and Bollinger Bands channels. This strategy uses the intersection of fast and slow moving averages to determine the direction of the trend, while combining Bollinger Bands channels and momentum indicators to confirm entry signals. This strategy also has risk control measures such as stop-profit and stop-loss, trailing stop-profit and stop-loss, and position management.
## Strategy Principle
The core principle of this strategy is to use price trends and momentum effects to capture market opportunities. Specifically, this strategy uses two moving averages of different periods (fast line and slow line) to determine the direction of the price trend. When the fast line crosses the slow line from bottom to top, it represents an upward trend, and the strategy will generate a long signal; conversely, when the fast line crosses the slow line from top to bottom, it represents a downward trend, and the strategy will generate a short signal.
For further confirmation of trends and entry timing, this strategy also incorporates Bollinger Bands Channels and Momentum indicators. Bollinger Bands are composed of three lines: the middle track is a moving average, and the upper track and lower track add or subtract a certain standard deviation on the basis of the middle track. When the price breaks through the upper Bollinger Band, it means there is strong upward momentum, and the strategy will be long; when the price breaks through the lower Bollinger Band, it means there is strong downward momentum, and the strategy will be short.
In addition, this strategy also introduces the momentum indicator, which measures the speed of price rise and fall by comparing the current price with the price a certain period ago. Momentum indicators can be used to determine the strength of a trend, thereby providing additional confirmation for entry.
In terms of position management, this strategy allows position size to be set based on account funds and risk appetite. At the same time, the strategy also has stop-profit and stop-loss and trailing stop-profit and stop-loss mechanisms to control the risk exposure of a single transaction.
In general, Jia Yibing's quantitative trend momentum trading strategy strives to capture market trend opportunities while strictly controlling risks and achieving stable investment returns through multiple dimensions such as trend tracking, momentum confirmation and risk management.
## Advantage Analysis
1. Trend following: The strategy uses the intersection of fast and slow moving averages to capture price trend opportunities. It can be long on the upward trend or short on the downward trend to adapt to different market conditions.
2. Momentum confirmation: The introduction of momentum indicators as a secondary confirmation of the trend can help eliminate false signals and improve the quality of entry.
3. Bollinger Bands assist decision-making: Bollinger Bands can reflect the fluctuation range of prices. Breaking through Bollinger Bands can be regarded as a signal of trend acceleration or abnormal price fluctuations, providing a reference for entry.
4. Position management: The strategy adopts a position management method based on account capital ratio and limit, which can flexibly control the capital occupation of each transaction, making full use of funds without being overly exposed to risks.
5. Stop-profit and stop-loss: Set up stop-profit and trailing stop-loss, which can protect profits when the price develops in the expected direction, and decisively stop the loss when the price reverses, effectively controlling the maximum loss of a single transaction.
6. Multi-parameter optimization: The strategy contains multiple adjustable parameters, such as moving average periods, Bollinger Band parameters, take-profit and stop-loss ratios, etc. The adaptability and robustness of the strategy can be improved through parameter optimization.
## Risk Analysis
1. Frequent trading: This strategy generates entry signals based on moving average crossovers and Bollinger Band breakthroughs. When the market fluctuates greatly, trading signals may be generated frequently, resulting in too many transactions and increased handling fee costs and slippage costs.
2. Parameter sensitivity: The strategy contains multiple parameters, such as moving average period, momentum period, Bollinger Band parameters, etc. The selection of different parameters may have a greater impact on the strategy effect. If parameters are chosen improperly, it may result in poor performance of the strategy.
3. Lagging in trend identification: The moving average is a lagging indicator. Especially when the moving average period is long, the speed of identifying trend turning will be slower, and the best entry opportunity may be missed.
4. Stop loss risk: Although the strategy sets stop loss measures, under extreme market conditions (such as rapid short jumps), the price may directly cross the stop loss price, causing actual losses to exceed expectations.
5. Position concentration risk: If the strategy continuously generates signals in the same direction during a certain period, it may cause positions to be excessively concentrated in a certain direction and face greater position risks.
6. Liquidity risk: The backtesting and actual results of the strategy may be affected by market liquidity. Especially when operating large amounts of funds, you may face slippage and insufficient trading volume.
## Optimization direction
1. Introduce more technical indicators: Based on the current moving average, momentum and Bollinger Bands, you can try to introduce more technical indicators, such as RSI, MACD, etc., to improve the reliability of the signal through the joint confirmation of multiple indicators.
2. Optimize the entry and exit mechanism: You can consider introducing more conditions into the judgment of entry and exit. For example, certain trading volume requirements must be met before the price breaks through. When exiting, use batch closing or moving take profit to enhance the flexibility and profitability of the strategy.
3. Dynamically adjust parameters: For moving average periods, momentum periods, Bollinger Band parameters, etc., a set of parameter adaptive mechanisms can be designed to dynamically adjust parameter values ​​according to different market conditions and volatility levels to improve the adaptability of the strategy.
4. Improve position management: On the basis of current position management, more advanced fund management methods can be introduced, such as Kelly formula, fixed ratio, dynamic equity, etc., to better balance returns and risks.
5. Combined with fundamental analysis: Pure technical analysis strategies may face the risk of market inefficiency or failure. If it can be combined with some fundamental factors, such as macroeconomic data, industry trends, etc., to filter and confirm technical signals, the strategy effect may be improved.
6. Enhance the consistency between backtesting and real offer: There may be differences in the performance of strategies in backtesting and real offer. It is necessary to focus on the execution quality of backtest and real offer, including transaction price, slippage, delay and other factors, to ensure the consistency between real offer performance and backtest results.
## Summarize
Jia Yibing's quantitative trend momentum trading strategy is a quantitative trading strategy that combines a variety of technical analysis methods. It uses moving average crossovers to capture trends, Bollinger Band breakthroughs to confirm trends, momentum indicators to reflect speed, stop-profit and stop-loss to control risks, and position management to optimize capital utilization, forming a complete trading decision-making and management system.
The advantage of this strategy is the combination of trend tracking and momentum, Bollinger Bands to assist judgment, position management and stop-profit and stop-loss considerations, and to seize market opportunities through multi-dimensional analysis and decision-making. But at the same time, this strategy also faces potential risks such as frequent trading, sensitive parameters, lagging trend recognition, and stop loss that cannot cover extreme market conditions. This requires continuous improvement and improvement of the strategy by introducing more technical indicators, optimizing signal judgment logic, dynamically adjusting parameters, improving fund management and other measures.
In addition, there may be differences between the backtest results and actual performance of quantitative trading strategies, which requires focusing on execution-level issues such as transaction price, slippage, and delays to improve the feasibility and stability of the strategy. At the same time, quantitative strategies should not be limited to technical analysis. Appropriate combination of fundamental factors will help improve the comprehensiveness and effectiveness of decision-making.
In general, Jia Yibing's quantitative trend momentum trading strategy provides a relatively complete and feasible idea for quantitative trading practice, but the final effect of the strategy also depends on the weighing of various opportunities and risks and the optimization of details. In practical applications, you need to make appropriate adjustments and improvements to the strategy based on your risk preference, capital size, trading market and other specific conditions, and continue to monitor and optimize during real-time operations to pursue more robust and ideal strategy performance.
|| 

## Overview

The JiaYiBing Quantitative Trend Momentum Trading Strategy is a long-short quantitative trading strategy that combines trend tracking, momentum indicators, and Bollinger Bands channels. The strategy uses the crossover of fast and slow moving averages to determine the trend direction, and confirms entry signals based on Bollinger Bands channels and momentum indicators. The strategy also includes risk control measures such as take profit, stop loss, trailing stop, and position sizing.

## Strategy Principles

The core principle of this strategy is to capture market opportunities by leveraging price trends and momentum effects. Specifically, the strategy uses two moving averages with different periods (fast and slow) to determine the direction of the price trend. When the fast moving average crosses above the slow moving average, it indicates an upward trend and the strategy generates a long signal; conversely, when the fast moving average crosses below the slow moving average, it indicates a downward trend and the strategy generates a short signal.

To further confirm the trend and entry timing, the strategy also incorporates Bollinger Bands and momentum indicators. Bollinger Bands consist of three lines: the middle line is the moving average, while the upper and lower bands are a certain number of standard deviations above and below the middle line. When the price breaks above the upper Bollinger Band, it indicates strong upward momentum and the strategy will go long; when the price breaks below the lower Bollinger Band, it indicates strong downward momentum and the strategy will go short.

In addition, the strategy also introduces a momentum indicator, which measures the speed of price changes by comparing the current price with the price a certain period ago. The momentum indicator can be used to judge the strength of the trend and provide additional confirmation for entry.

In terms of position sizing, the strategy allows for setting the position size based on account equity and risk preference. At the same time, the strategy also includes take profit, stop loss, and trailing stop mechanisms to control the risk exposure of each trade.

Overall, the JiaYiBing Quantitative Trend Momentum Trading Strategy seeks to capture trending market opportunities while strictly controlling risk through multiple dimensions such as trend tracking, momentum confirmation, and risk management, in order to achieve stable investment returns.

## Advantage Analysis

1. Trend Tracking: The strategy uses the crossover of fast and slow moving averages to capture trending price opportunities, allowing it to go long in uptrends and short in downtrends, adapting to different market conditions.

2. Momentum Confirmation: The introduction of the momentum indicator as a secondary confirmation of the trend helps to filter out false signals and improve entry quality.

3. Bollinger Bands Assisted Decision-Making: Bollinger Bands can reflect the price volatility range, and breakouts of Bollinger Bands can be seen as signals of trend acceleration or abnormal price fluctuations, providing a reference for entry.

4. Position Sizing: The strategy employs a position sizing method based on a percentage of account equity and a maximum limit, allowing for flexible control of the capital employed in each trade, both fully utilizing funds and avoiding excessive risk exposure.

5. Take Profit and Stop Loss: The strategy sets take profit, stop loss, and trailing stop loss levels, which can protect profits when the price moves in the expected direction, and decisively cut losses when the price reverses, effectively controlling the maximum loss of each trade.

6. Multi-Parameter Optimization: The strategy includes multiple adjustable parameters, such as moving average periods, Bollinger Bands parameters, take profit and stop loss percentages, etc., which can be optimized to improve the adaptability and robustness of the strategy.

## Risk Analysis

1. Frequent Trading: The strategy generates entry signals based on moving average crossovers and Bollinger Band breakouts. When market volatility is high, it may frequently generate trading signals, leading to excessive trading frequency and increasing commission and slippage costs.

2. Parameter Sensitivity: The strategy includes multiple parameters, such as moving average periods, momentum periods, Bollinger Bands parameters, etc. The choice of different parameters can have a significant impact on the performance of the strategy. If the parameters are not properly selected, it may lead to poor strategy performance.

3. Lagging Trend Recognition: Moving averages are lagging indicators, especially when the moving average period is long, the speed of identifying trend reversals will be slower, and the best entry timing may be missed.

4. Stop Loss Risk: Although the strategy sets stop loss measures, in extreme market conditions (such as rapid gaps), the price may directly cross the stop loss level, resulting in actual losses exceeding expectations.

5. Concentrated Position Risk: If the strategy continuously generates signals in the same direction during a certain period, it may lead to excessive concentration of positions in one direction, facing greater position risk.

6. Liquidity Risk: The performance of the strategy in backtesting and live trading may be affected by market liquidity, especially when dealing with large funds, which may face issues of slippage and insufficient trading volume.

## Optimization Directions

1. Introduce More Technical Indicators: On the basis of the current moving averages, momentum, and Bollinger Bands, more technical indicators such as RSI and MACD can be introduced to improve the reliability of signals through multi-indicator confirmation.

2. Optimize Entry and Exit Mechanisms: More conditions can be introduced in the judgment of entry and exit, such as requiring a certain trading volume before price breakouts, using staged position closing or trailing take profit for exits, to enhance the flexibility and profitability of the strategy.

3. Dynamic Parameter Adjustment: For moving average periods, momentum periods, Bollinger Bands parameters, etc., a set of parameter adaptive mechanisms can be designed to dynamically adjust parameter values based on different market states and volatility levels, improving the adaptability of the strategy.

4. Improve Position Sizing: On the basis of current position sizing, more advanced money management methods such as Kelly Criterion, fixed ratio, dynamic equity, etc. can be introduced to better balance returns and risks.

5. Combine with Fundamental Analysis: Pure technical analysis strategies may face the risk of market inefficiency or failure. If some fundamental factors, such as macroeconomic data and industry trends, can be combined to filter and confirm technical signals, it may improve the performance of the strategy.

6. Enhance the Consistency of Backtesting and Live Trading: The performance of the strategy in backtesting and live trading may differ. It is necessary to focus on the execution quality of backtesting and live trading, including factors such as execution price, slippage, and latency, to ensure the consistency of live performance with backtesting results.

## Summary

The JiaYiBing Quantitative Trend Momentum Trading Strategy is a quantitative trading strategy that integrates multiple technical analysis methods. It uses moving average crossovers to capture trends

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|50|Trend Period|
|v_input_2|14|Momentum Period|
|v_input_3|20|Bollinger Bands Period|
|v_input_4|2|Bollinger Bands Deviation|
|v_input_5|23|Fast SMA Length|
|v_input_6|50|Slow SMA Length|
|v_input_float_1|0.5|Long Take Profit %|
|v_input_float_2|0.5|Short Take Profit %|
|v_input_float_3|0.5|Stop Loss %|
|v_input_bool_1|true|Enable Trailing|
|v_input_float_4|0.01|Trailing Take Profit %|
|v_input_float_5|0.5|Trailing Stop Loss %|
|v_input_int_1|20|Position Size %|
|v_input_int_2|10000|Max Position Size|
|v_input_bool_2|false|Beast Mode|
|v_input_bool_3|true|Cap Position Size|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-01 00:00:00
end: 2024-02-29 23:59:59
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('甲易炳', overlay=true)

// Parameters
trendPeriod = input(50, 'Trend Period')
momentumPeriod = input(14, 'Momentum Period')
bbPeriod = input(20, 'Bollinger Bands Period')
bbDeviation = input(2, 'Bollinger Bands Deviation')
fastMALen = input(23, 'Fast SMA Length')
slowMALen = input(50, 'Slow SMA Length')
longTakeProfitPerc = input.float(0.5, 'Long Take Profit %', minval=0.05, step=0.05) * 0.01
shortTakeProfitPerc = input.float(0.5, 'Short Take Profit %', minval=0.05, step=0.05) * 0.01
stopLossPerc = input.float(0.5, 'Stop Loss %', minval=0.05, step=0.05) * 0.01
enableTrailing = input.bool(true, 'Enable Trailing')
trailingTakeProfitPerc = input.float(0.01, 'Trailing Take Profit %', minval=0.01, maxval=100, step=0.01) * 0.01
trailingStopLossPerc = input.float(0.5, 'Trailing Stop Loss %', minval=0.05, step=0.05) * 0.01
qty_percent = input.int(20, 'Position Size %', step=1)
qty_cap = input.int(10000, 'Max Position Size', step=1000)
beast_mode = input.bool(false, 'Beast Mode')
set_cap = input.bool(true, 'Cap Position Size')
strategy.initial_capital = 50000
// Calculate position size
qty1 = (strategy.initial_capital + strategy.netprofit) * qty_percent / 10 / close
qty = (set_cap and qty1 > qty_cap) ? qty_cap : qty1

// Calculate moving averages
fastMA = ta.sma(close, fastMALen)
slowMA = ta.sma(close, slowMALen)

// Bollinger Bands
[upperBB, middleBB, lowerBB] = ta.bb(close, bbPeriod, bbDeviation)

// Entry conditions
buySignal = ta.crossover(close, fastMA) and close > upperBB
sellSignal = ta.crossunder(close, fastMA) and close < lowerBB

// Rampage mode entry conditions
if beast_mode
    buySignal := buySignal and fastMA > fastMA[2]
    sellSignal := sellSignal and fastMA < fastMA[2]

// Active positions
longIsActive = buySignal or strategy.position_size > 0
shortIsActive = sellSignal or strategy.position_size < 0

// Declare take profit and stop loss variables
var float longTakeProfitPrice = na
var float shortTakeProfitPrice = na

// Take profit and stop loss calculation
if longIsActive
    if buySignal and not (strategy.position_size > 0)
        longTakeProfitPrice := close * (1 + longTakeProfitPerc)
    else
        longTakeProfitPrice := nz(longTakeProfitPrice[1], close * (1 + longTakeProfitPerc))
if shortIsActive
    if sellSignal and not (strategy.position_size < 0)
        shortTakeProfitPrice := close * (1 - shortTakeProfitPerc)
    else
        shortTakeProfitPrice := nz(shortTakeProfitPrice[1], close * (1 - shortTakeProfitPerc))

longTrailingTakeProfitStepTicks = longTakeProfitPrice * trailingTakeProfitPerc / syminfo.mintick
shortTrailingTakeProfitStepTicks = shortTakeProfitPrice * trailingTakeProfitPerc / syminfo.mintick
longTrailingStopLossPrice = close * (1 - trailingStopLossPerc)
shortTrailingStopLossPrice = close * (1 + trailingStopLossPerc)

// Entries and exits
if strategy.position_size == 0
    strategy.entry('Long Entry', qty=qty, direction=strategy.long, when=buySignal, alert_message='Long Entry')
    strategy.entry('Short Entry', qty=qty, direction=strategy.short, when=sellSignal, alert_message='Short Entry')
    strategy.exit('Long Take Profit', 'Long Entry', loss=close * stopLossPerc / syminfo.mintick, limit=enableTrailing ? na : longTakeProfitPrice, trail_price=enableTrailing ? longTakeProfitPrice : na, trail_offset=enableTrailing ? longTrailingTakeProfitStepTicks : na, when=longIsActive, alert_message='Long Take Profit')
    strategy.exit('Short Take Profit', 'Short Entry', loss=close * stopLossPerc / syminfo.mintick, limit=enableTrailing ? na : shortTakeProfitPrice, trail_price=enableTrailing ? shortTakeProfitPrice : na, trail_offset=enableTrailing ? shortTrailingTakeProfitStepTicks : na, when=shortIsActive, alert_message='Short Take Profit')
else
    if longIsActive
        strategy.exit('Long Stop Loss', 'Long Entry', stop=longTrailingStopLossPrice, when=longIsActive)
    if shortIsActive
        strategy.exit('Short Stop Loss', 'Short Entry', stop=shortTrailingStopLossPrice, when=shortIsActive)

// Plotting
plot(fastMA, 'Fast SMA', color=color.blue, linewidth=1, style=plot.style_line)
plot(slowMA, 'Slow SMA', color=color.orange, linewidth=1, style=plot.style_line)
plot(upperBB, 'Upper BB', color=color.green, linewidth=1, style=plot.style_line)
plot(lowerBB, 'Lower BB', color=color.red, linewidth=1, style=plot.style_line)

```

> Detail

https://www.fmz.com/strategy/444013

> Last Modified

2024-03-08 15:40:05

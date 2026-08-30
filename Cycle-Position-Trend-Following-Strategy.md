
> Name

Cycle-Position-Trend-Following-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/8d1363fff3375e5405bd886b9f32ffa15bdd78258ca337197ed7850efe901070.png)
[trans]


## Overview
The trend-based cycle trading strategy is a quantitative trading strategy that relies on the 200-day simple moving average to determine the direction of the trend. The strategy offers two modes "Follow the Uptrend" and "Follow the Downtrend" that can be selected according to the trader's preference. The strategy allows traders to customize stop loss and take profit levels, providing greater flexibility.
## Strategy Principle
The core indicator of this strategy is the 200-day simple moving average. The strategy is divided into two modes:
1. Follow the uptrend pattern: go long when the closing price is above the 200-day moving average; close the position when stop loss or take profit is triggered.
2. Follow the downtrend pattern: go long when the closing price is below the 200-day moving average; close the position when stop loss or take profit is triggered.
The long condition is defined by the `longCondition` variable, based on the relationship between the closing price and the 200-day moving average. The closing conditions are defined by the `closeCondition` variable, based on the relationship between stop loss, take profit price and moving average.
Specifically, if the long conditions are met, open a long position through `strategy.entry`; if the closing conditions are met, close the position through `strategy.exit`.
## Strategic Advantages
This strategy has the following advantages:
1. Simple and clear transaction logic, easy to understand and implement.
2. Two optional modes are provided, and the appropriate mode can be selected according to different market environments.
3. The risk-return characteristics of the strategy can be adjusted by customizing the stop-loss and take-profit levels.
4. Use a well-known technical indicator - the 200-day moving average - to determine the direction of the trend.
5. Automatically generate trading signals without manual intervention, reducing operational risks.
## Strategy Risk
This strategy also has the following risks:
1. Relying too much on a single technical indicator can easily produce false signals. You can consider adding other indicators for verification, such as MACD, KDJ, etc.
2. If the stop loss and take profit are too small, the loss will be easily stopped by market fluctuations; if they are too large, the ideal exit point may be missed. Parameters should be properly tested and optimized.
3. Using the method of judging signals based on the closing price, there is a bullish/bearish bias. You can consider changing to judging based on the K-line entity or confirming on the next K-line after the signal is generated.
4. The impact of transaction costs is not considered. A certain amount of room for transaction fees needs to be reserved when placing a firm offer.
## Strategy optimization
This strategy can be optimized from the following directions:
1. Add other technical indicators to verify signals to avoid false signals. For example, MACD indicator.
2. Optimize stop loss and take profit parameters and find the best parameter combination. Comparisons can be made by backtesting multiple sets of parameters.
3. Add trend filtering and only trade when the trend is clear. For example, introduce the ADX indicator.
4. Improve the entry method, consider the K-line entity relationship or add a confirmation mechanism.
5. Consider the impact of trading volume. Verify signal reliability in large numbers.
6. Test different moving average parameters and find the optimal parameters.
## Summarize
To sum up, the overall idea of ​​this strategy is clear and easy to understand, and has certain practical value. However, there are certain blind spots in relying only on a single indicator. More judgment conditions need to be added for verification, and parameters need to be tested and optimized to achieve better results in real trading. In addition, we also need to pay attention to the impact of transaction costs such as slippage and handling fees in the real offer.
|| 


## Overview

The Cycle Position Trend Following Strategy is a quantitative trading strategy that determines the trend direction based on the 200-day Simple Moving Average (SMA). It provides two modes - "Follow Uptrend" and "Follow Downtrend" for traders to choose from according to their preferences. The strategy allows traders to customize stop loss and take profit levels for greater flexibility.

## How The Strategy Works 

The core indicator of this strategy is the 200-day SMA. The strategy has two modes:

1. Follow Uptrend Mode: Go long when close is above 200-day SMA; close position when stop loss or take profit is triggered.

2. Follow Downtrend Mode: Go long when close is below 200-day SMA; close position when stop loss or take profit is triggered.

The long condition is defined in `longCondition` variable based on the close price's relation to the 200-day SMA. The close condition is defined in `closeCondition` variable based on stop loss, take profit and SMA.

Specifically, `strategy.entry` is used to open long positions when the long condition is met. `strategy.exit` is used to close positions when the close condition is triggered.

## Advantages of The Strategy

The advantages of this strategy include:

1. Simple and clear logic that is easy to understand. 

2. Provides two optional modes to suit different market environments.

3. Customizable stop loss and take profit allows tuning of risk-reward profile.

4. Uses the well-known 200-day SMA indicator to determine trend direction. 

5. Generates automated trading signals without manual intervention.

## Risks of The Strategy

The risks of this strategy include:

1. Overly reliant on a single indicator, prone to false signals. Adding other indicators like MACD, KDJ for confirmation could help.

2. Stop loss and take profit levels too tight or too wide could lead to premature stop out or missing ideal exit points. Parameters need proper testing and optimization.

3. Using close price for signals has closing price biases. Consider using candle body or add signal confirmation. 

4. Does not account for trading costs. Need to reserve costs when going live.

## Ways to Improve The Strategy

Some ways to improve the strategy:

1. Add other indicators to confirm signals and avoid false signals, e.g. MACD.

2. Optimize stop loss and take profit parameters to find optimal combination through backtesting.

3. Add trend filter to only trade in well-defined trends, e.g. ADX. 

4. Improve entry method by considering candle body or adding confirmation.

5. Consider trading volume to validate signal reliability. 

6. Test different SMA periods to find the optimal parameter.

## Conclusion

In conclusion, the strategy has clear and understandable logic with practical value. But reliance on a single indicator has limitations. More conditions should be added for confirmation. Parameters also need testing and optimization for better live performance. Furthermore, trading costs like slippage and commissions require consideration in live trading.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_string_1|0|mode: Buy Uptrend|Buy Downtrend|
|v_input_float_1|0.9|Stop Loss (SL) level|
|v_input_float_2|1.1|Take Profit (TP) level|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-10 00:00:00
end: 2023-11-16 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/
// © I11L

//@version=5
strategy("Cycle Position Trading", overlay=true, pyramiding=1, default_qty_value=100000, initial_capital=100000, default_qty_type=strategy.cash, process_orders_on_close=false, calc_on_every_tick=false)

// Input for selecting the mode
mode = input.string("Buy Uptrend", options = ["Buy Uptrend", "Buy Downtrend"])

// Input for customizing stop loss and take profit levels
stopLoss = input.float(0.9, title="Stop Loss (SL) level", step=0.01)
takeProfit = input.float(1.1, title="Take Profit (TP) level", step=0.01)

// Calculate the 200-day Simple Moving Average (SMA)
sma = ta.sma(close, 200)

// Plot the SMA on the chart
plot(sma)

// Define the conditions for entering a long position based on the selected mode
longCondition = mode == "Buy Uptrend" ? close > sma and close[5] > sma : close < sma

// Define the conditions for closing a position based on the selected mode
closeCondition = mode == "Buy Uptrend" ? (strategy.position_avg_price * stopLoss > close or strategy.position_avg_price * takeProfit < close or close < sma * 0.95) : (strategy.position_avg_price * stopLoss > close or strategy.position_avg_price * takeProfit < close or close > sma * 1.05)

// Execute a long position if the longCondition is met
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

// Close the position if the closeCondition is met
if (closeCondition)
    strategy.exit("Exit", limit = close)

```

> Detail

https://www.fmz.com/strategy/432420

> Last Modified

2023-11-17 17:05:11

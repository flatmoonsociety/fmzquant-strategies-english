
> Name

Exponential-Moving-Average-Crossover-Leverage-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/252b9991a2b45dc4f94a63b4482c2e5023cb4cf40dd0027db1d8a49b5476a463.png)

[trans]

#### Overview
This strategy uses the intersection of the 20-day and 55-day exponential moving averages (EMA) to determine trading signals. When the short-term EMA crosses the long-term EMA, a buy signal is issued, and vice versa, a sell signal is issued. The strategy also introduces leveraged trading, which magnifies returns through leverage and also magnifies risks. In addition, the strategy also adds conditional restrictions. A position will only be opened when the price touches the short-term moving average after the two moving averages cross to reduce the risk of false signals. Finally, users can also choose to use a simple moving average (MA) instead of EMA.
#### Strategy Principle
1. Calculate the 20-day and 55-day EMA (or MA).
2. Determine whether the short-term EMA crosses the long-term EMA. If so, set the readyToEnter variable to true, indicating that you are ready to enter the market.
3. If readyToEnter is true and the price touches the short-term EMA, the buy is executed and readyToEnter is reset to false.
4. If the short-term EMA crosses the long-term EMA, close the position.
5. Set the position size according to the leverage parameters.
6. Only execute the strategy within the backtest interval set by the user.
#### Strategic Advantages
1. Moving average crossover is a simple and easy-to-use trend judgment method, suitable for most markets.
2. Introducing leverage trading can amplify profits.
3. Add conditional restrictions to reduce the risk of false signals.
4. Provide two moving average options, EMA and MA, to adapt to different user preferences.
5. The code structure is clear and easy to understand and modify.
#### Strategy Risk
1. Leverage trading will amplify risks and may lead to large losses if judgment is made incorrectly.
2. There is a lag in the moving average crossover, and the best entry opportunity may be missed.
3. Only applicable to markets with obvious trends. If the market fluctuates, frequent transactions may occur, resulting in high handling fees.
#### Strategy optimization direction
1. You can try to optimize the moving average cycle and find the parameters that are most suitable for the current market.
2. You can introduce other indicators, such as RSI, MACD, etc., to comprehensively judge the trend and improve the winning rate.
3. You can set stop loss and take profit to control the risk of a single transaction.
4. The leverage size can be dynamically adjusted according to market volatility, increasing the leverage when the volatility is small and reducing the leverage when the volatility is large.
5. Machine learning algorithms can be introduced to adaptively optimize parameters.
#### Summarize
This strategy combines moving average crossover and leverage trading to amplify returns while grasping market trends. However, leverage also brings high risks and needs to be used with caution. In addition, the strategy still has room for optimization, and the strategy performance can be improved by introducing more indicators and dynamically adjusting parameters. In general, this strategy is suitable for traders who pursue high returns and are able to bear high risks.
||

#### Overview

This strategy uses the crossover of the 20-day and 55-day exponential moving averages (EMAs) to generate trading signals. A buy signal is triggered when the short-term EMA crosses above the long-term EMA, and a sell signal is triggered when the opposite occurs. The strategy also introduces leverage trading, which amplifies both potential returns and risks. Additionally, the strategy includes a conditional restriction that only allows entering a position when the price touches the short-term EMA after the crossover, to reduce the risk of false signals. Finally, users have the option to use simple moving averages (SMAs) instead of EMAs.

#### Strategy Principle

1. Calculate the 20-day and 55-day EMAs (or SMAs).
2. Determine if the short-term EMA crosses above the long-term EMA. If true, set the readyToEnter variable to true, indicating readiness to enter a position.
3. If readyToEnter is true and the price touches the short-term EMA, execute a buy order and reset readyToEnter to false.
4. If the short-term EMA crosses below the long-term EMA, close the position.
5. Set the position size based on the leverage parameter.
6. Execute the strategy only within the user-defined backtesting period.

#### Strategy Advantages

1. The moving average crossover is a simple and easy-to-use method for determining trends, suitable for most markets.
2. Introducing leverage trading can amplify returns.
3. Adding conditional restrictions reduces the risk of false signals.
4. Providing the choice between EMA and SMA suits different user preferences.
5. The code structure is clear and easy to understand and modify.

#### Strategy Risks

1. Leverage trading amplifies risks. If the judgment is wrong, it may lead to significant losses.
2. Moving average crossovers have a lag effect and may miss the best entry opportunities.
3. Only suitable for markets with clear trends. If the market is volatile, frequent trading may occur, resulting in high transaction fees.

#### Strategy Optimization Directions

1. Try optimizing the moving average periods to find the most suitable parameters for the current market.
2. Introduce other indicators, such as RSI and MACD, to comprehensively judge trends and improve the win rate.
3. Set stop-loss and take-profit levels to control single-trade risk.
4. Dynamically adjust leverage size based on market volatility, increasing leverage when volatility is low and decreasing leverage when volatility is high.
5. Introduce machine learning algorithms to adaptively optimize parameters.

#### Summary

This strategy combines moving average crossovers and leverage trading to capture market trends while amplifying returns. However, leverage also brings high risks and needs to be used with caution. In addition, there is room for optimization in this strategy, which can be achieved by introducing more indicators, dynamically adjusting parameters, etc. Overall, this strategy is suitable for traders who pursue high returns and can bear high risks.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|timestamp(2023-01-01)|Start Date|
|v_input_2|timestamp(2024-04-028)|End Date|
|v_input_float_1|3|Leverage Multiplier|
|v_input_bool_1|true|Use EMA (true) or MA (false)?|
|v_input_int_1|20|EMA/MA-1 Length|
|v_input_int_2|55|EMA/MA-2 Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-03-01 00:00:00
end: 2024-03-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA Crossover Strategy with Leverage, Conditional Entry, and MA Option", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=100)

// Inputs for backtesting period
startDate = input(defval=timestamp("2023-01-01"), title="Start Date")
endDate = input(defval=timestamp("2024-04-028"), title="End Date")

// Input for leverage multiplier
leverage = input.float(3.0, title="Leverage Multiplier", minval=1.0, maxval=10.0, step=0.1)

// Input for choosing between EMA and MA
useEMA = input.bool(true, title="Use EMA (true) or MA (false)?")

// Input source and lengths for MAs
src = close
ema1_length = input.int(20, title='EMA/MA-1 Length')
ema2_length = input.int(55, title='EMA/MA-2 Length')

// Calculate the MAs based on user selection
pema1 = useEMA ? ta.ema(src, ema1_length) : ta.sma(src, ema1_length)
pema2 = useEMA ? ta.ema(src, ema2_length) : ta.sma(src, ema2_length)

// Tracking the crossover condition for strategy entry
crossedAbove = ta.crossover(pema1, pema2)

// Define a variable to track if a valid entry condition has been met
var bool readyToEnter = false

// Check for MA crossover and update readyToEnter
if (crossedAbove)
    readyToEnter := true

// Entry condition: Enter when price touches MA-1 after the crossover // and (low <= pema1 and high >= pema1)
entryCondition = readyToEnter

// Reset readyToEnter after entry
if (entryCondition)
    readyToEnter := false

// Exit condition: Price crosses under MA-1
exitCondition = ta.crossunder(pema1, pema2)

// Check if the current bar's time is within the specified period
inBacktestPeriod = true

// Execute trade logic only within the specified date range and apply leverage to position sizing
if (inBacktestPeriod)
    if (entryCondition)
        strategy.entry("Long", strategy.long, qty=strategy.equity * leverage / close)
    if (exitCondition)
        strategy.close("Long")


// Plotting the MAs for visual reference
ema1_color = pema1 > pema2 ? color.red : color.green
ema2_color = pema1 > pema2 ? color.red : color.green
plot(pema1, color=ema1_color, style=plot.style_line, linewidth=1, title='EMA/MA-1')
plot(pema2, color=ema2_color, style=plot.style_line, linewidth=1, title='EMA/MA-2')

```

> Detail

https://www.fmz.com/strategy/449954

> Last Modified

2024-04-30 16:26:37

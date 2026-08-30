
> Name

EMA-Crossover-Strategy-with-Dynamic-Trailing-Stop-Loss
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d941a2e772f625502ae9.png)
![IMG](https://www.fmz.com/upload/asset/2d87196ff768d91869125.png)



[trans]
#### Overview
This strategy is a trend following trading system based on the 68-period exponential moving average (EMA), combined with a dynamic stop loss mechanism. This strategy identifies market trends through the intersection of price and EMA, while using initial stop loss and trailing stop loss to manage risk and achieve robust trading in trending markets.
#### Strategy Principle
The strategy uses the 68-period EMA as the core indicator to determine market trends. When the price crosses the EMA upwards, the system opens a long position; when the price crosses the EMA downwards, the system opens a short position. In order to effectively manage risk, the strategy sets up two layers of stop loss protection mechanisms: initial stop loss and trailing stop loss. The initial stop loss is 20 points from the entry price. When the price moves in a favorable direction and exceeds the initial stop loss distance, the stop loss price will be adjusted by 10 points accordingly, thereby locking in part of the profit.
#### Strategic Advantages
1. Strong trend tracking ability: The 68-period EMA can effectively filter market noise and capture mid- to long-term trends.
2. Perfect risk control: The double stop-loss mechanism not only protects the principal but also locks in profits.
3. Highly adjustable parameters: EMA cycle, stop loss points and other parameters can be flexibly adjusted according to different market characteristics.
4. The strategy logic is clear: the entry and exit conditions are clear, which facilitates real-time operation and monitoring.
5. High degree of automation: The strategy can fully realize programmed trading and reduce human intervention.
#### Strategy Risk
1. Risk of volatile market: Stop loss may be triggered frequently in a volatile market.
Recommended measures: Add trend confirmation indicators, such as ADX, etc.
2. Gap risk: A large gap in the market may cause the actual stop loss price to deviate from expectations.
Recommended actions: Consider using options to hedge or adjust position size.
3. Parameter optimization risk: Over-optimizing parameters may lead to strategy failure.
Recommended measures: Use sample out-of-sample testing to ensure parameter stability.
#### Strategy optimization direction
1. Trend confirmation mechanism: It is recommended to introduce trend strength indicators (such as ADX, MACD, etc.) to improve the accuracy of trend judgment.
2. Dynamic parameter adjustment: EMA cycle and stop loss parameters can be automatically adjusted according to market volatility.
3. Position management optimization: Introduce a dynamic position management system based on volatility.
4. Multi-period collaboration: combined with longer-period trend judgment to improve the accuracy of trading directions.
#### Summary
This strategy builds a complete trading system by combining EMA trend tracking and dynamic stop loss management. The core advantage of the strategy lies in its clear trading logic and complete risk control mechanism. Through the suggested optimization direction, the stability and profitability of the strategy are expected to be further improved. The strategy is suitable for medium and long-term investors who pursue stable returns. ||
#### Overview
This strategy is a trend-following trading system based on the 68-period Exponential Moving Average (EMA) combined with a dynamic stop-loss mechanism. It identifies market trends through price-EMA crossovers while employing initial and trailing stop-losses for risk management, enabling robust trading in trending markets.

#### Strategy Principles
The strategy utilizes a 68-period EMA as its core indicator for trend determination. Long positions are initiated when price crosses above the EMA, while short positions are taken when price crosses below. Risk management is implemented through a dual stop-loss mechanism: an initial stop-loss and a trailing stop-loss. The initial stop-loss is set at 20 points from the entry price, and when price moves favorably beyond the initial stop-loss distance, the stop-loss price adjusts by 10 points to lock in partial profits.

#### Strategy Advantages
1. Strong trend-following capability: 68-period EMA effectively filters market noise and captures medium to long-term trends.
2. Comprehensive risk control: Dual stop-loss mechanism protects capital while securing profits.
3. Flexible parameters: EMA period and stop-loss points can be adjusted according to different market characteristics.
4. Clear strategy logic: Well-defined entry and exit conditions facilitate live trading and monitoring.
5. High automation level: Strategy can be fully automated, reducing manual intervention.

#### Strategy Risks
1. Sideways market risk: Frequent stop-losses may be triggered in range-bound markets.
Recommended solution: Add trend confirmation indicators like ADX.

2. Gap risk: Large market gaps may cause actual stop-loss prices to deviate from expected levels.
Recommended solution: Consider options hedging or position size adjustment.

3. Parameter optimization risk: Over-optimization may lead to strategy failure.
Recommended solution: Implement out-of-sample testing to ensure parameter stability.

#### Strategy Optimization Directions
1. Trend confirmation mechanism: Suggest incorporating trend strength indicators (such as ADX, MACD) to improve trend identification accuracy.

2. Dynamic parameter adjustment: Automatically adjust EMA period and stop-loss parameters based on market volatility.

3. Position management optimization: Introduce volatility-based dynamic position sizing system.

4. Multi-timeframe correlation: Incorporate longer-term trend analysis to improve trade direction accuracy.

#### Summary
This strategy builds a complete trading system by combining EMA trend following with dynamic stop-loss management. Its core strengths lie in clear trading logic and comprehensive risk control mechanisms. Through the suggested optimization directions, the strategy's stability and profitability can be further enhanced. The strategy is suitable for medium to long-term investors seeking steady returns.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-10-01 00:00:00
end: 2025-02-18 08:00:00
period: 2d
basePeriod: 2d
exchanges: [{"eid":"Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA 68 with Trailing Stop-Loss", overlay=true)

// Inputs for customization
length_ema = input(68, title="EMA Length")
initial_stop_loss_points = input(20, title="Initial Stop Loss in Points")
trail_distance = input(10, title="Trailing Stop Adjustment in Points")

ema68 = ta.ema(close, length_ema)

// Plot EMA
plot(ema68, color=color.blue, title="68-Day EMA")

var float entry_price = na // Store entry price
var bool is_long = false // Track if we are in a long trade
var bool is_short = false // Track if we are in a short trade

// Buy Condition: Close above 68-day EMA
if ta.crossover(close, ema68)
    strategy.entry("Long", strategy.long)
    entry_price := close
    is_long := true
    is_short := false

// Sell Condition: Close below 68-day EMA
if ta.crossunder(close, ema68)
    strategy.entry("Short", strategy.short)
    entry_price := close
    is_long := false
    is_short := true

// Long Exit Conditions
if is_long
    stop_loss = entry_price - initial_stop_loss_points
    trail_price = entry_price + initial_stop_loss_points
    if close >= trail_price
        stop_loss := entry_price + trail_distance
    strategy.exit("LongExit", "Long", stop=stop_loss, when=close < ema68)

// Short Exit Conditions
if is_short
    stop_loss = entry_price + initial_stop_loss_points
    trail_price = entry_price - initial_stop_loss_points
    if close <= trail_price
        stop_loss := entry_price - trail_distance
    strategy.exit("ShortExit", "Short", stop=stop_loss, when=close > ema68)

```

> Detail

https://www.fmz.com/strategy/482840

> Last Modified

2025-02-20 14:17:56

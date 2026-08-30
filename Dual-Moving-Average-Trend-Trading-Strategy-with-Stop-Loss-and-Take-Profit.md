
> Name

Dual-Moving-Average-Trend-Trading-Strategy-with-Stop-Loss-and-Take-Profit
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d81537746204e81aaf28.png)
![IMG](https://www.fmz.com/upload/asset/2d8ab7f2e7caee8082576.png)




[trans]
#### Overview
This strategy is a trend following trading system based on double moving average crossover, combined with a risk management mechanism. The strategy uses 9-period and 21-period simple moving averages (SMA) to capture market trends, while setting a 1% stop loss and take profit to control risk. The system enters long positions when the short-term moving average crosses the long-term moving average, and exits when the short-term moving average crosses below the long-term moving average.
#### Strategy Principle
The core logic of the strategy is based on the continuity characteristics of market trends. Determine trend switching points by observing the intersection of the short-term (9-period) and long-term (21-period) moving averages. When the short-term moving average crosses the long-term moving average, a "golden cross" is formed, indicating that the upward trend has begun, and the system sends a long signal; when the short-term moving average crosses below the long-term moving average, a "death cross" is formed, indicating that the upward trend may end, and the system closes the position. At the same time, the strategy introduces a 1% stop-loss and take-profit mechanism to stop losses in time when the market goes unfavorable, or to lock in profits when expected returns are obtained.
#### Strategic Advantages
1. Strong trend grasping ability: By capturing the trend transition point through the intersection of double moving averages, the main trend of the market can be better grasped.
2. Improved risk control: A fixed ratio of stop loss and take profit is set to effectively control the risk of a single transaction.
3. High degree of automation: The system operates completely automatically without manual intervention.
4. Good visualization effect: trading signals and risk control ranges are clearly displayed through the graphical interface.
5. Flexible parameter optimization: the moving average period and stop-loss and take-profit ratio can be adjusted according to different market characteristics.
#### Strategy Risk
1. Risk of volatile markets: In a volatile market, frequent moving average crossovers may lead to false signals.
2. Slippage risk: When the market fluctuates violently, the actual transaction price may deviate greatly from the signal price.
3. Trend reversal risk: When a strong trend suddenly reverses, fixed stop loss may not be enough to cope with large fluctuations.
4. Parameter dependence: Strategy performance is more sensitive to the moving average cycle and stop-loss and take-profit parameter settings.
#### Strategy optimization direction
1. Introduce trend filter: you can add trend strength indicators such as ADX, and only open positions when the trend is clear.
2. Dynamic stop loss mechanism: ATR or volatility can be used to dynamically adjust the stop loss range.
3. Increase trading volume confirmation: Use trading volume as an auxiliary confirmation indicator for trading signals.
4. Optimization parameter adaptation: dynamically adjust the moving average period according to market fluctuation characteristics.
5. Added trend strength filtering: The trend strength can be judged by combining indicators such as RSI.
#### Summary
This strategy captures the trend through the crossover of double moving averages and combines the stop-loss and take-profit mechanisms for risk control. It is a relatively complete trend-following trading system. Although false signals may be generated in a volatile market, the stability and profitability of the strategy can be further improved through reasonable parameter optimization and the addition of auxiliary indicators. The core advantages of the strategy lie in its high degree of automation and complete risk control, making it suitable as a basic strategy framework for mid- to long-term trend tracking. ||
#### Overview
This strategy is a trend-following trading system based on dual moving average crossovers combined with risk management mechanisms. The strategy uses 9-period and 21-period Simple Moving Averages (SMA) to capture market trends, with 1% stop-loss and take-profit levels for risk control. The system enters long positions when the short-term MA crosses above the long-term MA and exits when the short-term MA crosses below the long-term MA.

#### Strategy Principles
The core logic is based on market trend continuity characteristics. By observing crossovers between short-term (9-period) and long-term (21-period) moving averages, the strategy identifies trend reversal points. A "Golden Cross" occurs when the short-term MA crosses above the long-term MA, signaling an uptrend and generating a long entry signal. A "Death Cross" occurs when the short-term MA crosses below the long-term MA, indicating potential trend reversal and triggering position closure. The strategy incorporates 1% stop-loss and take-profit mechanisms to limit losses during adverse market movements and secure profits at target levels.

#### Strategy Advantages
1. Strong trend capture capability: Effectively identifies trend reversal points through dual MA crossovers.
2. Comprehensive risk control: Fixed percentage stop-loss and take-profit levels effectively control per-trade risk.
3. High automation level: System runs fully automatically without manual intervention.
4. Good visualization: Clear graphical interface displaying trade signals and risk control zones.
5. Flexible parameter optimization: MA periods and risk management levels can be adjusted for different market characteristics.

#### Strategy Risks
1. Sideways market risk: Frequent MA crossovers in ranging markets may generate false signals.
2. Slippage risk: Actual execution prices may significantly deviate from signal prices during high volatility.
3. Trend reversal risk: Fixed stop-loss may be insufficient for sudden strong trend reversals.
4. Parameter dependency: Strategy performance is sensitive to MA periods and risk management parameter settings.

#### Optimization Directions
1. Implement trend filters: Add indicators like ADX to trade only in strong trends.
2. Dynamic stop-loss mechanism: Use ATR or volatility to adjust stop-loss levels dynamically.
3. Volume confirmation: Include volume as a confirmatory indicator for trade signals.
4. Adaptive parameter optimization: Dynamically adjust MA periods based on market volatility characteristics.
5. Add trend strength filtering: Incorporate RSI or similar indicators to assess trend strength.

#### Summary
This strategy captures trends through dual MA crossovers while incorporating risk management mechanisms, forming a comprehensive trend-following trading system. While it may generate false signals in ranging markets, the strategy's stability and profitability can be enhanced through proper parameter optimization and additional confirmatory indicators. Its core strengths lie in high automation and robust risk control, making it suitable as a foundation for medium to long-term trend-following strategies.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-21 00:00:00
end: 2024-12-13 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=6
strategy("Moving Average Crossover with Stop Loss and Take Profit", overlay=true)

// Parameters for moving averages
short_length = input.int(9, title="Short Moving Average Length")  // Optimized for 15-minute time frame
long_length = input.int(21, title="Long Moving Average Length")   // Optimized for 15-minute time frame

// Parameters for risk management
stop_loss_percent = input.float(1.0, title="Stop Loss (%)") / 100  // 1% stop loss
take_profit_percent = input.float(1.0, title="Take Profit (%)") / 100  // 1% take profit

// Calculate moving averages
short_ma = ta.sma(close, short_length)
long_ma = ta.sma(close, long_length)

// Plot moving averages
plot(short_ma, color=color.blue, title="Short MA")
plot(long_ma, color=color.orange, title="Long MA")

// Entry and exit conditions
long_condition = ta.crossover(short_ma, long_ma)  // Golden Cross
short_condition = ta.crossunder(short_ma, long_ma)  // Death Cross

// Execute strategy with stop loss and take profit
if (long_condition)
    strategy.entry("Long", strategy.long)
    strategy.exit("Take Profit/Stop Loss", "Long", stop=strategy.position_avg_price * (1 - stop_loss_percent), limit=strategy.position_avg_price * (1 + take_profit_percent)  )

if (short_condition)
    strategy.close("Long")  // Close long position on Death Cross

// Plot Buy/Sell Signals
plotshape(series=long_condition, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=short_condition, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")

// Draw 1% stop loss level as a transparent red rectangle
var float stop_loss_level = na
var float entry_price = na
if (strategy.position_size > 0)  // Only update when in a trade
    stop_loss_level := strategy.position_avg_price * (1 - stop_loss_percent)
    entry_price := strategy.position_avg_price

// Create transparent colors
transparent_red = color.new(color.black, 90)  // 90% transparency
transparent_green = color.new(color.green, 90)  // 90% transparency

// Plot stop loss and entry levels conditionally
plot(strategy.position_size > 0 ? stop_loss_level : na, color=transparent_red, title="Stop Loss Level", linewidth=1)
plot(strategy.position_size > 0 ? entry_price : na, color=transparent_green, title="Entry Price", linewidth=1)

// Fill the area between stop loss and entry price conditionally
fill( plot(strategy.position_size > 0 ? stop_loss_level : na),  plot(strategy.position_size > 0 ? entry_price : na),  color=transparent_red)
```

> Detail

https://www.fmz.com/strategy/482846

> Last Modified

2025-02-27 17:36:23

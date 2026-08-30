
> Name

Multi-Dimensional-Dynamic-ICT-Trading-Strategy-with-Engulfing-Patterns-and-Supply-Demand-Zone-Analysis-System
> Author

ianzeng123

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/2d837364e880e9fd7e94b.png)
![IMG](https://www.fmz.com/upload/asset/2d8b6e8c2eda01a1b6c18.png)




[trans]
#### Overview
This strategy is a comprehensive trading system that incorporates ICT (Internal Trader Concept), engulfing patterns, and supply and demand area analysis. It identifies high-probability trading opportunities by analyzing market structure in multiple dimensions and combining technical indicators and price behavior. The strategy runs on a 15-minute time frame and uses a percentage stop-loss and take-profit approach to manage risk.
#### Strategy Principle
The core logic of the strategy is based on three main components:
1. Use 20 periods of highs and lows to establish supply and demand areas that serve as important support and resistance levels.
2. Identify bullish and bearish engulfing patterns by analyzing the relationship between adjacent candlesticks.
3. When the price breaks through the supply and demand zone and an engulfing pattern appears, the system will execute the transaction taking into account risk management.
The system uses 10% of the capital for each trade and sets a stop loss of 1.5% and a take profit of 3%. This setting provides a risk-to-benefit ratio of 2:1.
#### Strategic Advantages
1. Multi-dimensional analysis improves the reliability of trading signals
2. Combines price action and technical analysis to reduce the impact of false signals
3. Use percentage stop loss and stop profit to adapt to different market conditions
4. The fund management system is reasonable and 10% of the funds used each time reduces the risk.
5. Can adapt to different market environments through parameter adjustment
#### Strategy Risk
1. Frequent stop losses may be triggered in highly volatile markets
2. Identification of supply and demand areas may not be accurate enough under certain market conditions
3. The 15-minute time frame may generate too many trading signals
4. Fixed Stop Loss and Take Profit percentages may not be suitable for all market conditions
Risk control suggestions:
- Recommend adjusting parameters under different market conditions
- Consider adding confirmation indicators
- Stop loss and take profit levels can be dynamically adjusted based on volatility
#### Strategy optimization direction
1. Introduce volatility indicators to dynamically adjust stop-loss and take-profit levels
2. Add volume analysis to confirm signal strength
3. Consider adding a trend filter to reduce counter-trend trades
4. To optimize the identification algorithm of supply and demand areas, consider using multiple time frame analysis
5. Add market status recognition function and use different parameter settings under different market conditions.
#### Summary
This is a well-structured comprehensive trading system that provides reliable trading signals through multi-dimensional analysis. The risk management of the system is reasonable, but there is still room for optimization. It is recommended that traders conduct sufficient backtesting before using it in real markets and adjust parameters according to specific market conditions. The modular design of the strategy makes it highly scalable, and new analysis dimensions can be added as needed. ||
#### Overview
This strategy is a comprehensive trading system that combines ICT (Internal Trader Concepts), engulfing patterns, and supply-demand zone analysis. It identifies high-probability trading opportunities through multi-dimensional market structure analysis, integrating technical indicators and price action. The strategy operates on a 15-minute timeframe and uses percentage-based stop-loss and take-profit levels for risk management.

#### Strategy Principles
The core logic is based on three main components:
1. Establishing supply and demand zones using 20-period high and low prices, which serve as significant support and resistance levels.
2. Identifying bullish and bearish engulfing patterns by analyzing the relationship between adjacent candles.
3. Executing trades when price breaks through supply/demand zones and engulfing patterns appear, with consideration for risk management.

The system uses 10% of equity for each trade, with a 1.5% stop-loss and 3% take-profit, providing a 2:1 risk-reward ratio.

#### Strategy Advantages
1. Multi-dimensional analysis improves signal reliability
2. Combination of price action and technical analysis reduces false signals
3. Percentage-based stop-loss and take-profit adapt to different market conditions
4. Reasonable money management system using 10% equity per trade reduces risk
5. Parameters can be adjusted to adapt to different market environments

#### Strategy Risks
1. May trigger frequent stop-losses in highly volatile markets
2. Supply and demand zone identification might be inaccurate in certain market conditions
3. 15-minute timeframe might generate too many trading signals
4. Fixed percentage stop-loss and take-profit might not suit all market conditions

Risk Control Suggestions:
- Adjust parameters under different market conditions
- Consider adding confirmation indicators
- Dynamic adjustment of stop-loss and take-profit levels based on volatility

#### Strategy Optimization Directions
1. Introduce volatility indicators for dynamic stop-loss and take-profit adjustment
2. Add volume analysis to confirm signal strength
3. Consider adding trend filters to reduce counter-trend trades
4. Optimize supply and demand zone identification algorithm, possibly using multiple timeframe analysis
5. Add market state recognition functionality to use different parameter sets under different market conditions

#### Summary
This is a well-structured comprehensive trading system that provides reliable trading signals through multi-dimensional analysis. The system's risk management is reasonable but has room for optimization. Traders are advised to thoroughly backtest before live trading and adjust parameters according to specific market conditions. The strategy's modular design provides good scalability, allowing for the addition of new analysis dimensions as needed.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-21 00:00:00
end: 2025-02-18 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("ICT + Engulfing + Supply & Demand", overlay=true, default_qty_type=strategy.percent_of_equity, default_qty_value=10)

// Input settings
timeframe = input.timeframe("15", title="Backtest Timeframe")
use_snd = input(true, title="Enable Supply & Demand Zones")
stopLossPerc = input(1.5, title="Stop Loss %")
takeProfitPerc = input(3, title="Take Profit %")

// Identify Engulfing Patterns
bullishEngulfing = (close[1] < open[1]) and (close > open) and (close > open[1]) and (open < close[1])
bearishEngulfing = (close[1] > open[1]) and (close < open) and (close < open[1]) and (open > close[1])

// Supply & Demand Zones (basic identification)
highestHigh = ta.highest(high, 20)
lowestLow = ta.lowest(low, 20)
supplyZone = use_snd ? highestHigh : na
demandZone = use_snd ? lowestLow : na

// Entry & Exit Conditions
longCondition = bullishEngulfing and close > demandZone
shortCondition = bearishEngulfing and close < supplyZone

// Stop-Loss & Take-Profit Calculation
longSL = close * (1 - stopLossPerc / 100)
longTP = close * (1 + takeProfitPerc / 100)
shortSL = close * (1 + stopLossPerc / 100)
shortTP = close * (1 - takeProfitPerc / 100)

// Execute trades
if (longCondition)
    strategy.entry("Long", strategy.long)
    strategy.exit("Long Exit", from_entry="Long", stop=longSL, limit=longTP)

if (shortCondition)
    strategy.entry("Short", strategy.short)
    strategy.exit("Short Exit", from_entry="Short", stop=shortSL, limit=shortTP)

// Plot Supply & Demand Zones
plot(use_snd ? supplyZone : na, color=color.red, title="Supply Zone")
plot(use_snd ? demandZone : na, color=color.green, title="Demand Zone")
```

> Detail

https://www.fmz.com/strategy/482861

> Last Modified

2025-02-20 15:44:25

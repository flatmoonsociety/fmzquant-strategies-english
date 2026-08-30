
> Name

Moving-Average-Based-Supply-Demand-Zone-Trading-System-with-Dynamic-Risk-Management
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/e6b4b2a7143b4a02eeb013576e7c32bb7de0c045e3a9376afc60ec4be9941fd9.png)
![IMG](assets/images/8bccc1d5fc68fea2431056b0f79eeb6859bf8e5165aee1d0e7058b64523b454b.png)



[trans]
#### Overview
This is a comprehensive trading strategy that combines moving average crossovers, supply and demand zone identification, and dynamic stop loss and take profit. This strategy determines the trading direction through the intersection of short-term and long-term moving averages, while using supply and demand areas as important price support and resistance levels, and working with percentage stop-loss and take-profit to manage risk. The core of the strategy is to only open positions near specific supply and demand areas, thereby increasing the winning rate of the transaction.
#### Strategy Principle
The strategy uses 9-period and 21-period simple moving averages (SMA) to determine trend direction. When the price is within 1% of the demand area (support level), and the short-term moving average crosses the long-term moving average upward, the system sends a long signal; when the price is within 1% of the supply area (resistance level), and the short-term moving average crosses the long-term moving average downward, the system sends a short signal. The identification of supply and demand areas is based on significant highs and lows within 50 periods, and requires at least 2 confirmation candles at this point. The system will automatically set dynamic stop loss levels (default 1%) and take profit levels (default 2%) based on the entry price.
#### Strategic Advantages
1. Multiple confirmation mechanism: combines technical indicators (moving average crossover) and price structure (supply and demand area) to reduce the risk of false breakthroughs
2. Dynamic risk management: Stop loss and take profit are set based on the percentage of the entry price, adapting to different market environments
3. Visualized trading signals: Clearly mark supply and demand areas and trading signals on the chart to facilitate analysis and verification.
4. Parameters are flexible and adjustable: moving average cycles, supply and demand area confirmation conditions, stop loss and take profit ratios, etc. can all be adjusted according to different market characteristics.
5. Clear strategy logic: clear entry and exit conditions, easy for backtesting and optimization
#### Strategy Risk
1. Shock market risk: Frequent moving average crossovers may lead to too many false signals
2. Slippage risk: Transactions near the supply and demand area may face greater slippage
3. Parameter sensitivity: The optimal parameters may vary greatly under different market environments.
4. Stop loss width risk: Fixed percentage stop loss may not be suitable for all market environments
5. Fund management risk: The strategy does not include position size management function
#### Strategy optimization direction
1. Introducing trading volume confirmation: adding trading volume indicators to the analysis of moving average crossovers and supply and demand areas to improve signal reliability
2. Dynamic parameter optimization: automatically adjust the stop-loss and take-profit ratios and supply and demand area ranges according to market volatility
3. Add trend filtering: Add longer period trend judgment to avoid trading in the opposite direction of the general trend.
4. Improve fund management: Add volatility-based position size calculation
5. Enhance the identification of supply and demand areas: Introduce more technical indicators to confirm the effectiveness of supply and demand areas
#### Summary
This is a strategy system that combines classic technical analysis methods with modern risk management concepts. By trading near important price areas, combined with moving average crossover signals, the strategy provides a relatively reliable trading framework. The design of dynamic stop-loss and take-profit can help adapt to different market environments, but the actual application of the strategy needs to be optimized according to specific market characteristics. It is recommended to conduct sufficient parameter optimization and backtest verification before real trading.
|| 

#### Overview
This is a comprehensive trading strategy that combines moving average crossovers, supply/demand zone identification, and dynamic risk management. The strategy determines trade direction through short-term and long-term moving average crossovers, utilizes supply/demand zones as key support and resistance levels, and manages risk with percentage-based stop-loss and take-profit levels. The strategy's core principle is to only enter trades near specific supply/demand zones to improve win rate.

#### Strategy Principles
The strategy employs 9-period and 21-period Simple Moving Averages (SMA) to determine trend direction. Buy signals are generated when price is within 1% of a demand zone (support) and the short-term MA crosses above the long-term MA; sell signals occur when price is within 1% of a supply zone (resistance) and the short-term MA crosses below the long-term MA. Supply/demand zones are identified based on significant highs/lows within 50 periods, requiring at least 2 confirmation candles. The system automatically sets dynamic stop-loss (default 1%) and take-profit (default 2%) levels based on entry price.

#### Strategy Advantages
1. Multiple confirmation mechanism: Combines technical indicators (MA crossover) and price structure (supply/demand zones) to reduce false breakout risks
2. Dynamic risk management: Stop-loss and take-profit levels based on entry price percentages, adapting to different market conditions
3. Visual trade signals: Clear visualization of supply/demand zones and trade signals for analysis and verification
4. Flexible parameters: MA periods, supply/demand zone confirmation conditions, and risk management levels can be adjusted for different markets
5. Clear strategy logic: Well-defined entry and exit conditions for backtesting and optimization

#### Strategy Risks
1. Choppy market risk: Frequent MA crossovers may generate excessive false signals
2. Slippage risk: Trading near supply/demand zones may face significant slippage
3. Parameter sensitivity: Optimal parameters may vary significantly across different market conditions
4. Fixed stop-loss risk: Percentage-based stops may not suit all market environments
5. Money management risk: Strategy lacks position sizing functionality

#### Optimization Directions
1. Volume confirmation: Incorporate volume indicators in MA crossover and supply/demand zone analysis to improve signal reliability
2. Dynamic parameter optimization: Automatically adjust stop-loss/take-profit percentages and zone ranges based on market volatility
3. Trend filtering: Add longer-term trend analysis to avoid trading against major trends
4. Enhanced money management: Include volatility-based position sizing calculations
5. Improved zone identification: Introduce additional technical indicators to confirm supply/demand zone validity

#### Summary
This strategy system combines classical technical analysis methods with modern risk management concepts. By trading near significant price zones and incorporating moving average crossover signals, the strategy provides a relatively reliable trading framework. The dynamic stop-loss and take-profit design helps adapt to different market conditions, but practical application requires optimization based on specific market characteristics. Thorough parameter optimization and backtesting are recommended before live trading.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-12-01 00:00:00
end: 2025-02-01 00:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Binance","currency":"ETH_USDT"}]
*/

//@version=5
strategy("MA Crossover with Demand/Supply Zones + Stop Loss/Take Profit", overlay=true)

// Input parameters for Moving Averages
shortLength = input.int(9, title="Short MA Length", minval=1)
longLength = input.int(21, title="Long MA Length", minval=1)

// Input parameters for Demand/Supply Zones
zoneLookback = input.int(50, title="Zone Lookback Period", minval=10)
zoneStrength = input.int(2, title="Zone Strength (Candles)", minval=1)

// Input parameters for Stop Loss and Take Profit
stopLossPerc = input.float(1.0, title="Stop Loss (%)", minval=0.1) / 100
takeProfitPerc = input.float(2.0, title="Take Profit (%)", minval=0.1) / 100

// Calculate moving averages
shortMA = ta.sma(close, shortLength)
longMA = ta.sma(close, longLength)

// Plot moving averages
plot(shortMA, color=color.blue, title="Short MA")
plot(longMA, color=color.red, title="Long MA")

// Identify Demand and Supply Zones
var float demandZone = na
var float supplyZone = na

// Detect Demand Zones (Price makes a significant low and bounces up)
if (ta.lowest(low, zoneLookback) == low[zoneStrength] and close[zoneStrength] > open[zoneStrength])
    demandZone := low[zoneStrength]

// Detect Supply Zones (Price makes a significant high and drops down)
if (ta.highest(high, zoneLookback) == high[zoneStrength] and close[zoneStrength] < open[zoneStrength])
    supplyZone := high[zoneStrength]

// Draw Demand and Supply Zones using lines
var line demandLine = na
var line supplyLine = na


// Trade Logic: Only open trades near Demand/Supply Zones
isNearDemand = demandZone > 0 and close <= demandZone * 1.01  // Within 1% of demand zone
isNearSupply = supplyZone > 0 and close >= supplyZone * 0.99  // Within 1% of supply zone

// Calculate Stop Loss and Take Profit levels
stopLossLevel = strategy.position_avg_price * (1 - stopLossPerc)  // Stop loss for long positions
takeProfitLevel = strategy.position_avg_price * (1 + takeProfitPerc)  // Take profit for long positions

stopLossLevelShort = strategy.position_avg_price * (1 + stopLossPerc)  // Stop loss for short positions
takeProfitLevelShort = strategy.position_avg_price * (1 - takeProfitPerc)  // Take profit for short positions

// Generate buy/sell signals based on MA crossover and zones
if (ta.crossover(shortMA, longMA) and isNearDemand)
    strategy.entry("Buy", strategy.long)
    strategy.exit("Take Profit/Stop Loss", from_entry="Buy", stop=stopLossLevel, limit=takeProfitLevel)

if (ta.crossunder(shortMA, longMA) and isNearSupply)
    strategy.entry("Sell", strategy.short)
    strategy.exit("Take Profit/Stop Loss", from_entry="Sell", stop=stopLossLevelShort, limit=takeProfitLevelShort)

// Optional: Plot buy/sell signals on the chart
plotshape(series=ta.crossover(shortMA, longMA) and isNearDemand, title="Buy Signal", location=location.belowbar, color=color.green, style=shape.labelup, text="BUY")
plotshape(series=ta.crossunder(shortMA, longMA) and isNearSupply, title="Sell Signal", location=location.abovebar, color=color.red, style=shape.labeldown, text="SELL")
```

> Detail

https://www.fmz.com/strategy/482859

> Last Modified

2025-02-20 15:39:27

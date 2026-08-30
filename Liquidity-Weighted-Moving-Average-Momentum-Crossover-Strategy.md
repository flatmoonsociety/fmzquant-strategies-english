
> Name

Momentum Crossover Strategy Based on Liquidity Weighted Index Moving Average-Liquidity-Weighted-Moving-Average-Momentum-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c93d927fa51a492764.png)

[trans]
#### Overview
This strategy is a trading system based on a liquidity-weighted moving average, which measures market liquidity by monitoring the relationship between price fluctuations and trading volume, and builds fast and slow moving averages on this basis. When the fast line crosses the slow line, a buy signal is generated, and when it crosses below, a sell signal is generated. The strategy pays special attention to abnormal liquidity events and records key price points through arrays to provide more precise trading opportunities.
#### Strategy Principle
The core of the strategy is to measure market liquidity through the ratio of trading volume to price changes. The specific implementation steps are as follows:
1. Calculate liquidity indicators: use trading volume divided by the absolute value of the difference between the closing price and the opening price
2. Set liquidity boundaries: identify abnormal liquidity through EMA and standard deviation
3. Maintain the price array: record the price when the liquidity boundary is broken
4. Construct moving averages: Calculate fast and slow EMA based on liquidity events
5. Generate trading signals: determine buying and selling points through moving average crossovers
#### Strategic Advantages
1. Liquidity perception: By combining trading volume with price changes, market activity can be captured more accurately
2. Abnormal event tracking: record key price points through arrays to avoid missing important market opportunities
3. Dynamic adaptation: The decreasing weight characteristic of EMA enables the strategy to better adapt to market changes.
4. Risk control: Provide clear entry and exit signals through moving average crossovers
5. Customizability: multiple parameters can be adjusted to adapt to different market environments
#### Strategy Risk
1. Parameter sensitivity: The strategy effect strongly depends on parameter settings and requires continuous optimization.
2. Hysteresis: Systems based on moving averages have inherent hysteresis.
3. Market dependence: unstable performance in certain time periods and markets
4. False Breakouts: May produce false signals during periods of high volatility
5. Transaction costs: Frequent transactions may bring higher costs
#### Strategy optimization direction
1. Introduce filters:
- Added trend confirmation indicators such as ADX
- Use the volatility indicator to filter out false signals
2. Improve entry timing:
- Incorporate support and resistance levels
- Consider volume breakout confirmation
3. Optimize parameter selection:
- Implement adaptive parameters
- Dynamically adjust according to market conditions
4. Enhance risk management:
- Add stop loss and take profit mechanism
- Implement warehouse management system
#### Summary
This is an innovative strategy that integrates liquidity analysis and technical indicators to optimize the traditional moving average crossover system by monitoring market liquidity abnormalities. Although it performs well in specific market environments, it still needs further optimization to improve stability and applicability. It is recommended that traders conduct sufficient testing before using it in real trading, and combine it with other indicators to build a more complete trading system.
||

#### Overview
This strategy is a trading system based on liquidity-weighted moving averages, measuring market liquidity through the relationship between price movement and trading volume. It constructs fast and slow moving averages to generate buy signals when the fast line crosses above the slow line and sell signals when it crosses below. The strategy particularly focuses on abnormal liquidity events, recording key price levels in an array for more precise trading opportunities.

#### Strategy Principles
The core mechanism relies on measuring market liquidity through the ratio of volume to price movement. The implementation follows these steps:
1. Calculate liquidity indicator: Volume divided by absolute difference between close and open prices
2. Set liquidity boundary: Identify abnormal liquidity using EMA and standard deviation
3. Maintain price array: Record prices when liquidity boundary is breached
4. Construct moving averages: Calculate fast and slow EMAs based on liquidity events
5. Generate trading signals: Determine entry and exit points through moving average crossovers

#### Strategy Advantages
1. Liquidity awareness: More accurately captures market activity by combining volume and price movement
2. Event tracking: Records key price levels through array implementation, preventing missed opportunities
3. Dynamic adaptation: EMA's decreasing weights allow better market adjustment
4. Risk control: Provides clear entry and exit signals through crossovers
5. Customizability: Multiple adjustable parameters for different market conditions

#### Strategy Risks
1. Parameter sensitivity: Strategy effectiveness heavily depends on parameter settings
2. Lag: Inherent delay in moving average-based systems
3. Market dependence: Unstable performance in certain timeframes and markets
4. False breakouts: May generate incorrect signals during high volatility
5. Transaction costs: Frequent trading may incur significant costs

#### Optimization Directions
1. Implement filters:
- Add trend confirmation indicators like ADX
- Use volatility indicators to filter false signals
2. Improve entry timing:
- Incorporate support and resistance levels
- Consider volume breakout confirmation
3. Optimize parameter selection:
- Implement adaptive parameters
- Adjust dynamically based on market conditions
4. Enhance risk management:
- Add stop-loss and take-profit mechanisms
- Implement position sizing system

#### Summary
This innovative strategy combines liquidity analysis with technical indicators, optimizing traditional moving average crossover systems by monitoring market liquidity anomalies. While it shows promising results in specific market conditions, further optimization is needed to improve stability and applicability. Traders should thoroughly test before live implementation and consider combining with other indicators for a more robust trading system.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2019-12-23 08:00:00
end: 2025-01-16 00:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT","balance":49999}]
*/

//Liquidity ignoring price location

//@version=6
strategy("Liquidity Weighted Moving Averages [AlgoAlpha]", overlay=true, commission_type=strategy.commission.percent, commission_value=0.1, slippage=3)

// Inputs
outlierThreshold = input.int(10, "Outlier Threshold Length")
fastMovingAverageLength = input.int(50, "Fast MA Length")
slowMovingAverageLength = input.int(100, "Slow MA Length")
start_date = input(timestamp("2018-01-01 00:00"), title="Start Date")
end_date = input(timestamp("2069-12-31 23:59"), title="End Date")

// Define liquidity based on volume and price movement
priceMovementLiquidity = volume / math.abs(close - open)

// Calculate the boundary for liquidity to identify outliers
liquidityBoundary = ta.ema(priceMovementLiquidity, outlierThreshold) + ta.stdev(priceMovementLiquidity, outlierThreshold)

// Initialize an array to store liquidity values when they cross the boundary
var liquidityValues = array.new_float(5)

// Check if the liquidity crosses above the boundary and update the array
if ta.crossover(priceMovementLiquidity, liquidityBoundary)
    array.insert(liquidityValues, 0, close)
    if array.size(liquidityValues) > 5
        array.pop(liquidityValues)

// Calculate the Exponential Moving Averages for the close price at the last liquidity crossover
fastEMA = ta.ema(array.size(liquidityValues) > 0 ? array.get(liquidityValues, 0) : na, fastMovingAverageLength)
slowEMA = ta.ema(array.size(liquidityValues) > 0 ? array.get(liquidityValues, 0) : na, slowMovingAverageLength)

// Trading Logic
in_date_range = true
buy_signal = ta.crossover(fastEMA, slowEMA) and in_date_range
sell_signal = ta.crossunder(fastEMA, slowEMA) and in_date_range

// Strategy Entry and Exit
if (buy_signal)
    strategy.entry("Buy", strategy.long)

if (sell_signal)
    strategy.close("Buy")

// Plotting
fastPlot = plot(fastEMA, color=fastEMA > slowEMA ? color.new(#00ffbb, 50) : color.new(#ff1100, 50), title="Fast EMA")
slowPlot = plot(slowEMA, color=fastEMA > slowEMA ? color.new(#00ffbb, 50) : color.new(#ff1100, 50), title="Slow EMA")

// Create a fill between the fast and slow EMA plots with appropriate color based on crossover
fill(fastPlot, slowPlot, fastEMA > slowEMA ? color.new(#00ffbb, 50) : color.new(#ff1100, 50))

```

> Detail

https://www.fmz.com/strategy/478717

> Last Modified

2025-01-17 15:45:55

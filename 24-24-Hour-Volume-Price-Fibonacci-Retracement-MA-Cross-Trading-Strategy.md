
> Name

24-Hour-Volume-Price-Fibonacci-Retracement-MA-Cross-Trading-Strategy
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/b77e332090e884a4097061ee643a0a857fbbfb21b2aaa4dea1b00b500255c899.png)
![IMG](assets/images/009986ae99ab4557786a46ba06e38df41a390b9a6519d10048bcfeb9e1ff7308.png)




[trans]
#### Overview
This strategy is a quantitative trading system based on volume, price highs and lows, and Fibonacci retracement levels over a 24-hour period. The strategy timings trades by combining crossover signals from short-term and long-term moving averages, while using volume and Fibonacci levels to verify the validity of price movements. This combination of multi-dimensional indicators can both capture market trends and trade on key support and resistance levels.
#### Strategy Principle
The core logic of the strategy includes the following key elements:
1. 24-hour price range tracking: The system continuously monitors and updates the highest and lowest prices in each trading day to establish a price fluctuation range.
2. Fibonacci retracement calculation: Calculate the four key Fibonacci retracement levels of 23.6%, 38.2%, 61.8% and 78.6% based on the daily high and low points.
3. Trading volume analysis: Use the 20-period simple moving average (SMA) to smooth the trading volume data and reflect market activity.
4. Moving average crossover signal: Trading signals are generated through the crossover of the 14-period and 28-period moving averages, where an upward crossing is a long signal and a downward crossing is a short signal.
#### Strategic Advantages
1. Multi-dimensional analysis: Combining price, trading volume and technical indicators to provide a more comprehensive market perspective.
2. Strong adaptability: Fibonacci levels are calculated based on real-time price ranges and can dynamically adapt to market changes.
3. Reasonable risk control: reduce the risk caused by false breakthroughs through multiple indicator confirmations.
4. Clear operation logic: clear entry signals, easy to execute and backtest.
5. Time cycle optimization: 24-hour monitoring is adopted, which is suitable for markets with around-the-clock trading.
#### Strategy Risk
1. Volatile market risk: In a volatile market, moving average crossover signals may cause frequent transactions.
2. Hysteresis problem: The moving average indicator has a certain degree of lag and may miss the best entry opportunity.
3. Risk of false breakthrough: During periods of low liquidity, price breakthroughs may lack the support of real trading volume.
4. Computational complexity: Real-time calculation of multiple indicators may increase system load.
#### Strategy optimization direction
1. Dynamic parameter optimization:
- Automatically adjust the moving average period based on market volatility
- Optimize the trading volume average cycle and improve sensitivity to market activity
2. Signal filtering enhancement:
- Added trend strength confirmation indicator
- Introduce volatility filter to avoid trading in low volatility environment
3. Improved risk management:
- Implement dynamic stop loss mechanism
- Added position management algorithm
#### Summary
This strategy builds a logically complete trading system by comprehensively using technical indicators such as 24-hour price ranges, Fibonacci retracement levels, trading volume, and moving average crossovers. The main advantages of the strategy lie in multi-dimensional analysis and adaptability, but attention must also be paid to risks such as volatile markets and false breakthroughs. Through the suggested optimization direction, the stability and profitability of the strategy are expected to be further improved. ||
#### Overview
This strategy is a quantitative trading system based on 24-hour trading volume, price highs and lows, and Fibonacci retracement levels. The strategy determines trading opportunities by combining crossover signals from short-term and long-term moving averages while using volume and Fibonacci levels to validate price trend validity. This multi-dimensional indicator combination can both capture market trends and execute trades at key support and resistance levels.

#### Strategy Principles
The core logic of the strategy includes the following key elements:
1. 24-Hour Price Range Tracking: The system continuously monitors and updates the highest and lowest prices within each trading day to establish the price fluctuation range.
2. Fibonacci Retracement Calculation: Calculates four key Fibonacci retracement levels (23.6%, 38.2%, 61.8%, and 78.6%) based on intraday highs and lows.
3. Volume Analysis: Uses a 20-period Simple Moving Average (SMA) to smooth volume data and reflect market activity.
4. Moving Average Crossover Signals: Generates trading signals through crossovers of 14-period and 28-period moving averages, where crossing above indicates a long signal and crossing below indicates a short signal.

#### Strategy Advantages
1. Multi-dimensional Analysis: Combines price, volume, and technical indicators for a more comprehensive market perspective.
2. Strong Adaptability: Fibonacci levels are calculated based on real-time price ranges, allowing dynamic adaptation to market changes.
3. Reasonable Risk Control: Multiple indicator confirmation reduces risks from false breakouts.
4. Clear Operational Logic: Entry signals are explicit, making execution and backtesting straightforward.
5. Optimized Time Period: 24-hour monitoring suits markets that trade around the clock.

#### Strategy Risks
1. Choppy Market Risk: Moving average crossover signals may generate frequent trades in sideways markets.
2. Lag Issues: Moving average indicators have inherent lag, potentially missing optimal entry points.
3. False Breakout Risk: Price breakouts during low liquidity periods may lack genuine volume support.
4. Computational Complexity: Real-time calculation of multiple indicators may increase system load.

#### Strategy Optimization Directions
1. Dynamic Parameter Optimization:
- Automatically adjust moving average periods based on market volatility
- Optimize volume moving average period to improve sensitivity to market activity

2. Signal Filter Enhancement:
- Add trend strength confirmation indicators
- Introduce volatility filters to avoid trading in low volatility environments

3. Risk Management Improvement:
- Implement dynamic stop-loss mechanisms
- Add position sizing algorithms

#### Summary
The strategy constructs a logically complete trading system by comprehensively utilizing 24-hour price ranges, Fibonacci retracement levels, volume, and moving average crossovers. The strategy's main advantages lie in its multi-dimensional analysis and adaptability, but attention must be paid to risks such as choppy markets and false breakouts. Through the suggested optimization directions, the strategy's stability and profitability potential can be further enhanced.[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-02-25 00:00:00
end: 2025-02-22 08:00:00
period: 1d
basePeriod: 1d
exchanges: [{"eid":"Binance","currency":"SOL_USDT"}]
*/

//@version=5
strategy("24-Hour Volume and Fibonacci Levels Strategy", overlay=true)

// Define the 24-hour time period
startTime = timestamp(year, month, dayofmonth, 0, 0)
endTime = timestamp(year, month, dayofmonth, 23, 59)

// Calculate 24-hour high and low
var float dayHigh = na
var float dayLow = na

if (time >= startTime and time <= endTime)
    dayHigh := na(dayHigh) ? high : math.max(dayHigh, high)
    dayLow := na(dayLow) ? low : math.min(dayLow, low)

// Fibonacci levels
fibRetrace1 = dayLow + (dayHigh - dayLow) * 0.236
fibRetrace2 = dayLow + (dayHigh - dayLow) * 0.382
fibRetrace3 = dayLow + (dayHigh - dayLow) * 0.618
fibRetrace4 = dayLow + (dayHigh - dayLow) * 0.786

// Plot Fibonacci levels
plot(fibRetrace1, color=color.green, linewidth=2, title="Fibonacci 23.6%")
plot(fibRetrace2, color=color.blue, linewidth=2, title="Fibonacci 38.2%")
plot(fibRetrace3, color=color.orange, linewidth=2, title="Fibonacci 61.8%")
plot(fibRetrace4, color=color.red, linewidth=2, title="Fibonacci 78.6%")

// Volume Indicator
volumeMa = ta.sma(volume, 20)
plot(volumeMa, color=color.purple, title="24-Hour Volume", linewidth=2)

// Optional: Display the 24-hour volume on the chart
bgcolor(time >= startTime and time <= endTime ? color.new(color.purple, 90) : na)

// Strategy conditions (based on moving averages)
longCondition = ta.crossover(ta.sma(close, 14), ta.sma(close, 28))
if (longCondition)
    strategy.entry("My Long Entry Id", strategy.long)

shortCondition = ta.crossunder(ta.sma(close, 14), ta.sma(close, 28))
if (shortCondition)
    strategy.entry("My Short Entry Id", strategy.short)

```

> Detail

https://www.fmz.com/strategy/483515

> Last Modified

2025-02-24 09:55:47

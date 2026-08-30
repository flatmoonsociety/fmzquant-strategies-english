
> Name

Dual-Moving-Average-Crossover-Trading-System-A-Quantitative-Strategy-Based-on-Short-term-and-Medium-term-MA-Breakthrough
> Author

ianzeng123

> Strategy Description

![IMG](assets/images/b905c215588a89268638d5dd7b0b44843259cea57cd994727adcbd4bd1444e97.png)
![IMG](assets/images/dad090a5d477b6abfc2a169f1bd3e389d5ad8443e50793c6663c104154d41f0d.png)


[trans]
#### Overview
The double moving average crossover quantitative trading strategy is a trend tracking system based on technical analysis. The core mechanism is to use the cross relationship between the short-term moving average (MA7) and the medium-term moving average (MA10) to generate buy and sell signals. This strategy also incorporates long-term moving averages (MA100 and MA200) as reference indicators for market trends, but the main trading signals rely on the crossover behavior of short-term and medium-term moving averages. When the short-term moving average breaks through the mid-term moving average from below, a buy signal is generated; conversely, when the short-term moving average falls below the mid-term moving average from above, a sell signal is generated. This trading method is simple, intuitive, easy to implement, and suitable for capturing short- and medium-term price trend changes.
#### Strategy Principle
The core principle of this strategy is based on the crossover signal of the moving average, and the specific implementation logic is as follows:
1. Calculate four moving averages: 7-day simple moving average (MA7), 10-day simple moving average (MA10), 100-day simple moving average (MA100) and 200-day simple moving average (MA200).
2. Generate trading signals:
   - Buy signal (buySignal): when MA7 breaks through MA10 from below (ta.crossover function).
   - Sell signal (sellSignal): when MA7 falls below MA10 from above (ta.crossunder function).
3. Transaction execution logic:
   - When a buy signal appears, the system opens a long position (strategy.entry).
   - When a sell signal occurs, the system closes the long position (strategy.close).
4. Mark trading signals on the chart: buy signals are displayed below the K-line, and sell signals are displayed above the K-line for easy visual confirmation.
This strategy relies on moving average crossovers to capture changes in price momentum. In an uptrend, the short-term moving average is above the medium-term moving average, indicating increased short-term buying pressure; in a downtrend, the short-term moving average is located below the medium-term moving average, indicating increased short-term selling pressure. When two moving averages cross, it means a change in market momentum and may signal a trend reversal.
#### Strategic Advantages
1. Simple and easy to understand: The strategy is based on classic technical analysis concepts, with clear logic, easy to understand and implement, and is suitable for beginners to get started with quantitative trading.
2. Trend capturing ability: The double moving average crossover system can effectively capture changes in short- and medium-term price trends and avoid frequent trading when the market is sideways.
3. High degree of automation: Strategies can be executed automatically without subjective judgment, reducing the interference of emotional factors.
4. Adaptability: By adjusting the period of the moving average, the strategy can adapt to different market environments and trading varieties.
5. Visually intuitive: The buying and selling signals are clearly marked on the chart to facilitate traders' backtest analysis and real-time monitoring.
6. Clear risk management: There are clear entry and exit rules, which is conducive to fund management and risk control.
7. High calculation efficiency: Using simple moving average (SMA) calculation, the calculation burden is small, and it is suitable for real-time trading systems.
#### Strategy Risk
1. Lagging problem: The moving average is essentially a lagging indicator. The signal generation may have missed the best entry point, which may lead to losses in a rapidly changing market.
2. False signals in a volatile market: In a volatile market, frequent moving average crossings will generate a large number of false signals, leading to frequent transactions and commission erosion.
3. Lack of stop-loss mechanism: There is no clear stop-loss strategy in the code, and you may face large losses when the trend reverses strongly.
4. Parameter fixed risk: The fixed moving average period (7, 10, 100, 200) may not be suitable for all market environments and lacks adaptability.
5. Reliance on a single indicator: Relying only on moving average crossovers may lack a comprehensive market perspective and ignore information from fundamentals and other technical indicators.
6. No trading volume confirmation: The strategy does not combine trading volume analysis, which may lead to false breakthrough signals under low trading volume.
7. Lack of dynamic position management: The strategy uses fixed positions for entry and does not adjust the position size according to market volatility.
#### Strategy optimization direction
1. Introduce a stop-loss mechanism: add fixed stop-loss or ATR dynamic stop-loss to protect the safety of funds, such as `strategy.exit("止损", "Buy", stop=close * 0.95)`.
2. Add trend filter conditions: You can add MA100 and MA200 as trend filters, and only trade in the main trend direction indicated by the long-term moving average, for example, only go long when the price is above MA200.
3. Increase trading volume confirmation: Verify the validity of signals by combining trading volume indicators to avoid false breakthroughs under low trading volume.
4. Optimize moving average parameters: You can find the optimal parameters under a specific market environment by backtesting different moving average cycle combinations, or consider using adaptive moving averages.
5. Add other technical indicators: combine RSI, MACD and other indicators to form a multiple confirmation system to improve signal quality.
6. Realize dynamic position management: dynamically adjust the position size according to volatility (such as ATR), reduce the position when the volatility is high, and increase the position when the volatility is low.
7. Add market environment judgment: distinguish between trending markets and volatile markets, and adopt different trading strategies or parameters in different environments.
8. Improved position closing logic: More sophisticated position closing conditions can be designed, such as partial take profit or trailing stop loss, to optimize the profit structure.
#### Summarize
The double moving average crossover quantitative trading strategy is a classic trend following system based on technical analysis. It captures market momentum changes and executes transactions through the cross relationship of MA7 and MA10. The advantage of this strategy is that it has simple logic, is easy to understand and implement, and can effectively capture short- and medium-term trend changes. However, it also faces risks such as the lag of the moving average, many false signals in the volatile market, and the lack of a stop-loss mechanism.
In order to improve the performance of the strategy, we can improve it by adding stop loss mechanism, trend filtering, transaction volume confirmation, parameter optimization and combining with other technical indicators. In addition, implementing dynamic position management and trading logic that differentiates market environments are also potential optimization directions.
In short, the double moving average crossover strategy provides traders with a good starting point for quantitative trading, and through reasonable optimization and risk management, it can be developed into a more robust and efficient trading system. It is suitable as the first strategy for beginners to get started with quantitative trading, and can also be used as part of the strategy portfolio of experienced traders.
 ||
#### Overview
The Dual Moving Average Crossover Trading System is a trend-following strategy based on technical analysis. Its core mechanism utilizes the crossover relationship between short-term moving average (MA7) and medium-term moving average (MA10) to generate buy and sell signals. The strategy also incorporates long-term moving averages (MA100 and MA200) as reference indicators for market trends, although the primary trading signals rely on the crossover behavior of the short and medium-term moving averages. A buy signal is generated when the short-term MA crosses above the medium-term MA, while a sell signal occurs when the short-term MA crosses below the medium-term MA. This trading approach is simple, intuitive, easy to implement, and suitable for capturing medium to short-term price trend changes.

#### Strategy Principles

The core principle of this strategy is based on moving average crossover signals, with the following implementation logic:

1. Calculate four moving averages: 7-day simple moving average (MA7), 10-day simple moving average (MA10), 100-day simple moving average (MA100), and 200-day simple moving average (MA200).

2. Generate trading signals:
   - Buy signal (buySignal): When MA7 crosses above MA10 (ta.crossover function).
   - Sell signal (sellSignal): When MA7 crosses below MA10 (ta.crossunder function).

3. Trading execution logic:
   - When a buy signal appears, the system enters a long position (strategy.entry).
   - When a sell signal appears, the system closes the long position (strategy.close).

4. Mark trading signals on the chart: Buy signals are displayed below the candles, and sell signals are displayed above the candles for visual confirmation.

The strategy relies on moving average crossovers to capture price momentum changes. In an uptrend, the short-term MA is positioned above the medium-term MA, indicating strengthened buying pressure in the short term; in a downtrend, the short-term MA is positioned below the medium-term MA, indicating strengthened selling pressure. When the two moving averages cross, it suggests a change in market momentum, potentially signaling a trend reversal.

#### Strategy Advantages

1. Simplicity: The strategy is based on classic technical analysis concepts, with clear logic that is easy to understand and implement, making it suitable for beginners entering quantitative trading.

2. Trend-capturing ability: The dual moving average crossover system effectively captures medium to short-term price trend changes, avoiding frequent trading during sideways markets.

3. High degree of automation: The strategy can be fully automated, requiring no subjective judgment, thus reducing emotional interference.

4. Adaptability: By adjusting the moving average periods, the strategy can adapt to different market environments and trading instruments.

5. Visual intuitiveness: Trading signals are clearly marked on the chart, facilitating backtesting analysis and real-time monitoring.

6. Clear risk management: With well-defined entry and exit rules, it supports effective capital management and risk control.

7. Computational efficiency: Using simple moving averages (SMA) for calculations reduces computational burden, making it suitable for real-time trading systems.

#### Strategy Risks

1. Lag issues: Moving averages are inherently lagging indicators, and signals may be generated after missing the optimal entry point, potentially leading to losses in rapidly changing markets.

2. False signals in oscillating markets: In sideways, oscillating markets, frequent moving average crossovers can generate numerous false signals, resulting in frequent trading and commission erosion.

3. Lack of stop-loss mechanism: The code does not include a clear stop-loss strategy, which could lead to significant losses during strong trend reversals.

4. Fixed parameter risk: The fixed moving average periods (7, 10, 100, 200) may not be suitable for all market environments, lacking adaptability.

5. Single indicator dependence: Relying solely on moving average crossovers may lack a comprehensive market perspective, ignoring information from fundamentals and other technical indicators.

6. No volume confirmation: The strategy does not incorporate volume analysis, potentially leading to false breakout signals in low-volume situations.

7. Lack of dynamic position sizing: The strategy uses fixed position sizing for entry, without adjusting position size based on market volatility.

#### Strategy Optimization Directions

1. Introduce stop-loss mechanisms: Add fixed stop-loss or ATR-based dynamic stop-loss to protect capital, such as `strategy.exit("StopLoss", "Buy", stop=close * 0.95)`.

2. Add trend filtering conditions: Utilize MA100 and MA200 as trend filters, trading only in the direction of the main trend indicated by the long-term moving averages, such as only going long when price is above MA200.

3. Incorporate volume confirmation: Combine volume indicators to verify signal validity, avoiding false breakouts during low-volume periods.

4. Optimize moving average parameters: Backtest different combinations of moving average periods to find optimal parameters for specific market environments, or consider using adaptive moving averages.

5. Add additional technical indicators: Combine RSI, MACD, or other indicators to form a multi-confirmation system, improving signal quality.

6. Implement dynamic position sizing: Adjust position size dynamically based on volatility (such as ATR), reducing position size during high volatility and increasing it during low volatility.

7. Add market environment assessment: Differentiate between trending and oscillating markets, applying different trading strategies or parameters in different environments.

8. Improve exit logic: Design more sophisticated exit conditions, such as partial profit-taking or trailing stops, to optimize profit structure.

#### Summary

The Dual Moving Average Crossover Trading System is a classic trend-following system based on technical analysis that captures market momentum changes and executes trades through the crossover relationship between MA7 and MA10. The strategy's advantages lie in its simple logic, ease of understanding and implementation, and effective capture of medium to short-term trend changes. However, it also faces risks such as moving average lag, multiple false signals in oscillating markets, and lack of stop-loss mechanisms.

To enhance strategy performance, we can make improvements by adding stop-loss mechanisms, trend filtering, volume confirmation, parameter optimization, and combining other technical indicators. Additionally, implementing dynamic position sizing and market environment-specific trading logic are potential optimization directions.

In conclusion, the dual moving average crossover strategy provides traders with a good starting point for quantitative trading. Through reasonable optimization and risk management, it can be developed into a more robust and efficient trading system. It is suitable as a first strategy for beginners entering quantitative trading, and can also serve as part of an experienced trader's strategy portfolio.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2025-01-18 19:45:00
end: 2025-03-12 08:00:00
period: 1h
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"TRUMP_USDT"}]
*/

//@version=5
strategy("Backtest Buy and Sell Signals with MA 7 and MA 10", overlay=true)

// Calculate Moving Averages
ma7 = ta.sma(close, 7)
ma10 = ta.sma(close, 10)
ma100 = ta.sma(close, 100)
ma200 = ta.sma(close, 200)

// Plot MAs
plot(ma7, color=color.blue, title="MA 7")
plot(ma10, color=color.red, title="MA 10")
plot(ma100, color=#512ca8, title="MA 100")
plot(ma200, color=color.rgb(152, 139, 20), title="MA 200")

// Buy and Sell Signals
buySignal = ta.crossover(ma7, ma10)
sellSignal = ta.crossunder(ma7, ma10)

// Display signals on the chart
plotshape(buySignal, style=shape.labelup, location=location.belowbar, color=color.rgb(231, 241, 232), size=size.small, title="Buy Signal", text="buy")
plotshape(sellSignal, style=shape.labeldown, location=location.abovebar, color=color.rgb(237, 221, 221), size=size.small, title="Sell Signal", text="sell")

// Entry and Exit Logic
if (buySignal)
    strategy.entry("Buy", strategy.long)

if (sellSignal)
    strategy.close("Buy")

```

> Detail

https://www.fmz.com/strategy/486564

> Last Modified

2025-03-14 09:27:34

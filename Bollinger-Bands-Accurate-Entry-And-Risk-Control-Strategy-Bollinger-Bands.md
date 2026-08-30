
> Name

Bollinger-Bands-Accurate-Entry-And-Risk-Control-Strategy-Bollinger-Bands Accurate Entry and Risk Control Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1cdae69a3fca17dccf7.png)

[trans]
#### Overview
This strategy uses Bollinger Bands as the main indicator and trades under specific conditions by analyzing the relationship between price and the upper and lower rails. The main idea of ​​the strategy is: go long when the closing price breaks through the upper track, go short when it breaks through the lower track, and use opposite signals to close positions to capture price fluctuations.
#### Strategy Principle
1. Calculate the middle track, upper track and lower track of Bollinger Bands. The middle rail is a simple moving average of the closing price, and the upper and lower rails are the standard deviation plus or minus a certain multiple of the middle rail.
2. When the closing price breaks through the upper track, the long condition is triggered and a long position is opened.
3. When the closing price breaks through the lower track, the short selling condition is triggered and a short position is opened.
4. When holding a long position, if short selling conditions occur, the long position will be closed.
5. When holding a short position, if long conditions appear, the short position will be closed.
#### Strategic Advantages
1. Bollinger Bands can effectively reflect price fluctuations, and its use as a trading signal has a certain degree of reliability.
2. The strategy logic is clear and easy to understand and implement.
3. In trending markets, this strategy can capture price fluctuations well and obtain better returns.
4. strategyya5 a4. This number y does not use too many indicators, which reduces noise interference and improves the effectiveness of the signal.
#### Strategy Risk
1. In volatile market conditions, this strategy may result in frequent transactions, resulting in higher transaction costs.
2. The selection of Bollinger Band parameters has a great impact on the performance of the strategy. Inappropriate parameters may cause the strategy to fail.
3. This strategy does not set a stop loss and may face greater risks when the market reverses sharply.
4. The strategy does not take into account the characteristics of the trading varieties, and parameters may need to be adjusted for different trading varieties.
#### Strategy optimization direction
1. Introduce other indicators, such as trend indicators or oscillators, to confirm Bollinger Band signals and improve trading accuracy.
2. Optimize parameters, such as the Bollinger Band cycle and standard deviation multiples, to adapt to different market conditions.
3. Set reasonable stop loss and stop profit to control the risk of a single transaction.
4. Adjust the strategy according to the characteristics of the trading product, such as volatility, liquidity, etc.
5. Consider introducing position management, dynamically adjusting positions according to market conditions, and improving the return-to-risk ratio.
#### Summary
This strategy takes Bollinger Bands as the core and conducts transactions under specific conditions by analyzing the relationship between price and Bollinger Bands. The strategy logic is clear, easy to understand and implement, and you can get better returns in the trend market. But there are also some risks, such as frequent transactions, improper parameter selection, etc. By introducing other indicators, optimizing parameters, setting stop loss and profit, etc., the performance of the strategy can be further improved and better adapted to different market environments.
|| 

#### Overview
This strategy uses Bollinger Bands as the main indicator. By analyzing the relationship between price and the upper and lower bands, it enters trades under specific conditions. The main idea of the strategy is: when the closing price breaks above the upper band, it goes long; when it breaks below the lower band, it goes short. At the same time, it uses opposite signals to close positions, thereby capturing price fluctuations.

#### Strategy Principle
1. Calculate the middle, upper, and lower bands of the Bollinger Bands. The middle band is the simple moving average of the closing price, and the upper and lower bands are the middle band plus or minus a certain multiple of standard deviations.
2. When the closing price breaks above the upper band, it triggers the long condition and opens a long position.
3. When the closing price breaks below the lower band, it triggers the short condition and opens a short position.
4. When holding a long position, if the short condition appears, the long position is closed.
5. When holding a short position, if the long condition appears, the short position is closed.

#### Strategy Advantages
1. Bollinger Bands can effectively reflect price fluctuations, and using them as trading signals has a certain degree of reliability.
2. The strategy logic is clear and easy to understand and implement.
3. In trending markets, this strategy can capture price fluctuations well and obtain good returns.
4. The strategy does not use too many indicators, reducing noise interference and improving the effectiveness of signals.

#### Strategy Risks
1. In range-bound markets, this strategy may experience frequent trading, leading to high transaction costs.
2. The selection of Bollinger Band parameters has a significant impact on strategy performance, and inappropriate parameters may cause the strategy to fail.
3. The strategy does not set a stop loss, which may face greater risks when the market reverses sharply.
4. The strategy does not consider the characteristics of different trading instruments, and parameters may need to be adjusted for different instruments.

#### Strategy Optimization Directions
1. Introduce other indicators, such as trend or oscillator indicators, to confirm Bollinger Band signals and improve trading accuracy.
2. Optimize parameters, such as the period and standard deviation multiple of Bollinger Bands, to adapt to different market conditions.
3. Set reasonable stop losses and take profits to control single transaction risk.
4. Adjust the strategy according to the characteristics of trading instruments, such as volatility and liquidity.
5. Consider introducing position management to dynamically adjust positions according to market conditions and improve the risk-return ratio.

#### Summary
This strategy uses Bollinger Bands as the core and conducts trades under specific conditions by analyzing the relationship between price and Bollinger Bands. The strategy logic is clear and easy to understand and implement. It can obtain good returns in trending markets. However, it also has some risks, such as frequent trading and improper parameter selection. By introducing other indicators, optimizing parameters, setting stop losses and take profits, and other methods, the performance of the strategy can be further improved to better adapt to different market environments.
[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2023-05-28 00:00:00
end: 2024-06-02 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Bollinger Bands Strategy", overlay=true)

src = input(close)
length = input.int(34, minval=1)
mult = input.float(2.0, minval=0.001, maxval=50)

basis = ta.sma(src, length)
dev = ta.stdev(src, length)
dev2 = mult * dev

upper1 = basis + dev
lower1 = basis - dev
upper2 = basis + dev2
lower2 = basis - dev2

// Long Condition: Close above Upper Bollinger Band
longCondition = close > upper1

// Short Condition: Close below Lower Bollinger Band
shortCondition = close < lower1

// Strategy Entry and Exit
strategy.entry("Long", strategy.long, when = longCondition)
strategy.entry("Short", strategy.short, when = shortCondition)

// Close Long Position when Short Condition is Met
strategy.close("Long", when = shortCondition)

// Close Short Position when Long Condition is Met
strategy.close("Short", when = longCondition)

// Plotting Bollinger Bands
plot(basis, color=color.blue)
plot(upper1, color=color.new(color.blue, 80))
plot(lower1, color=color.new(color.orange, 80))

```

> Detail

https://www.fmz.com/strategy/453232

> Last Modified

2024-06-03 10:53:56

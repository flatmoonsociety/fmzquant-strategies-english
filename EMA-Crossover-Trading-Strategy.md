
> Name

Moving average crossover trading strategy EMA-Crossover-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/1b49cf84fd4505078f0.png)
[trans]

## Overview
The moving average crossover trading strategy is a simple and effective quantitative trading strategy. This strategy uses exponential moving averages (EMA) and moving average crossover signals to identify price movements and determine when to buy and sell. Compared with other more complex strategies, it is simpler to use, easier to understand and implement.
## Strategy Principle
The key to this strategy is to use two EMAs with different parameters. EMA1 is set to 25 days and EMA2 is set to 100 days. When the short-term EMA crosses above the longer-term EMA from below, it is a buy signal; when the short-term EMA crosses below the longer-term EMA from above, it is a sell signal. In this way, the short-term EMA reflects the short-term trend and momentum of the price, and the longer-term EMA reflects the long-term trend of the price. When two EMAs form a "golden cross" and a "death cross", they are buying and selling signals.
In order to filter error signals, the strategy also sets some additional conditions. For example, the positive line of the column is required to be negative, and the crossover is required to occur when the RSI is greater than 50, etc. This avoids erroneous trades caused by short-term noise.
## Advantage Analysis
The biggest advantage of this strategy is that it is simple and easy to understand and use. Compared with many strategies with numerous parameters and complex logic, it is more friendly to traders.
Secondly, this strategy captures short-term and long-term trend changes in prices, and uses the classic technical indicators of the moving average "golden cross" and "dead cross" to identify price reversals, thereby determining the timing of buying and selling. This method is effective and allows you to follow the trend and avoid blind trading when there is no clear signal.
Finally, the policy also sets appropriate filter conditions. This can reduce the probability of mistaken transactions and avoid being deceived by market noise. This allows the strategy to achieve stable performance in complex and volatile markets.
## Risk Analysis
The biggest risk with this strategy is the potential for divergence between short-term and long-term trends. Prices fluctuated wildly in the short term, triggering moving average crossover signals, but the long-term trend did not reverse. This can lead to losses on erroneous trades. In addition, in long-term sideways market conditions, frequent false signals are likely to occur.
EMA parameter settings also affect strategy performance. If the EMA period is set improperly, the short-term and long-term EMA will lose their representativeness and cannot effectively identify trends and trend reversals. This also increases false signals and trading risk.
Finally, additional filtering conditions may be too strict and miss valid trading opportunities. This results in a decrease in strategy profitability.
## Optimization suggestions
This strategy can be optimized in combination with other indicators, such as KDJ, MACD, etc., and use more factors to judge buying and selling opportunities to reduce false signals.
Additionally, different parameters can be tested to find the best EMA period combination. Filter parameters can also be adjusted to take into account transaction frequency and stability.
Dynamically adjusting positions is also an important direction for improving strategies. For example, when the two EMAs are farther apart, increase the position; when the two EMAs are closer, decrease the position. This allows for flexible risk adjustment based on market trends.
## Summarize
The moving average crossover strategy is a simple and practical quantitative trading strategy. It uses EMA cross buying and selling signals to comply with short-term and long-term price trend changes to determine trading opportunities. This strategy is easy to understand and implement, minimizes complexity, and is a good choice for beginners to get started with quantitative trading. But we cannot ignore its possible risks and need to optimize parameters and filtering conditions so that they can adapt to a more complex market environment.
|| 

## Overview  

The EMA crossover trading strategy is a simple yet effective quantitative trading strategy. It utilizes exponential moving averages (EMA) and crossover signals to identify price trends and determine entry and exit points. Compared to more complex strategies, it is simpler to understand and implement.  

## Strategy Logic

The key lies in using two EMAs with different parameters. EMA1 is set to 25 days and EMA2 is set to 100 days. When the shorter-term EMA crosses above the longer-term EMA, it is a buy signal. When the shorter EMA crosses below the longer EMA, it is a sell signal. Thus, the shorter EMA captures short-term price trends and momentum, while the longer EMA reflects long-term trends. The “golden cross” and “death cross” formed by the two EMAs generate trading signals.  

To filter out false signals, the strategy also sets some additional criteria. For example, requiring a bullish candlestick pattern or crossover happening above 50 RSI level. This avoids erroneous trades due to short-term noise.

## Advantages

The biggest advantage is the simplicity and intuitiveness of this strategy. Compared to strategies with numerous parameters and complex logic, it is much more user-friendly.  

Also, it captures trend changes in both short-term and long-term timeframes, utilizing the classic technical indicator of EMA crosses to identify trend reversals and determine entries and exits, thus trading with the trend.  

Lastly, appropriate filters are set to reduce false signals and avoid being misguided by market noise. This allows stable performance of the strategy in volatile markets.  

## Risks

The main risk is the divergence between short and long term trends. Dramatic price swings may trigger crossover signals but the longer-term trend remains unchanged, resulting in losing trades. Also, whipsaws often emerge in range-bound markets.  

Inappropriate EMA period settings could also jeopardize strategy performance, as the representative power of the EMAs would diminish, rendering them ineffective in capturing trends and reversals. This introduces higher risks.

In addition, excessively strict filters may cause missing out potential trading opportunities, thus undermining profitability.

## Enhancement  

Combining with other indicators like KDJ, MACD etc. could help confirm trading signals and avoid false signals. 

Testing different parameter sets to find optimal EMA periods, and adjusting filter criteria to balance trading frequency and reliability.

Dynamic position sizing is also important. For example, larger position when the two EMAs are further apart, smaller when closer. This adapts to changing market conditions.  

## Conclusion  

The EMA crossover strategy is a simple yet practical quantitative trading strategy. It capitalizes on EMA crossover signals to trade along with short-term and long-term trends. Easy to understand and implement, it minimizes complexity and suits novice traders. However, its risks should not be neglected. Further optimization on parameters and filters can make the strategy more robust across varying markets.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|true|Position Size (%)|
|v_input_int_1|25|EMA 1|
|v_input_2_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_int_2|100|EMA 2|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_4|14|RSI length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-11-11 00:00:00
end: 2023-12-11 00:00:00
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy('EMA Crossover Signal', shorttitle='EMA Crossover Signal', overlay=true)
// Define input for position size as a percentage of equity
position_size_pct = input(1, title='Position Size (%)') / 100

//Input EMA
len1 = input.int(25, minval=1, title='EMA 1')
src1 = input(close, title='Source')
ema1 = ta.ema(src1, len1)
len2 = input.int(100, minval=1, title='EMA 2')
src2 = input(close, title='Source')
ema2 = ta.ema(src2, len2)
//End of format

//Format RSI
lenrsi = input(14, title='RSI length')
outrsi = ta.rsi(close,lenrsi)

bodybar1 = math.abs(close - open)
bodybar2 = math.abs(close[1] - open[1])
// Plot the EMAs
plot(ema1, color=color.new(color.blue, 0), title='EMA 1')
plot(ema2, color=color.new(color.red, 0), title='EMA 2')

// EMA Crossover conditions
emaCrossoverUp = ta.crossover(ema1, ema2)
emaCrossoverDown = ta.crossunder(ema1, ema2)
var entrybar = close  // Initialize entrybar with the current close

// Calculate crossovers outside of the if statements
emaCrossoverUpOccured = ta.crossover(close, ema1) and ema1 > ema2 and bodybar1 > bodybar2 and close > entrybar
emaCrossoverDownOccured = ta.crossunder(close, ema1) and ema1 < ema2 and bodybar1 > bodybar2 and close < entrybar

plotshape(series=emaCrossoverUpOccured, location=location.abovebar, color=color.new(color.green, 0), style=shape.triangleup, title='New Buy Order', size=size.tiny)
plotshape(series=emaCrossoverDownOccured, location=location.belowbar, color=color.new(color.red, 0), style=shape.triangledown, title='New Sell Order', size=size.tiny)

if emaCrossoverUpOccured
    strategy.entry("Enter Long", strategy.long)
else if emaCrossoverDownOccured
    strategy.entry("Enter Short", strategy.short)
```

> Detail

https://www.fmz.com/strategy/435154

> Last Modified

2023-12-12 17:09:24


> Name

Gods-Bollinger-Bands-RSI-Trading-Strategy Gods-Bollinger-Bands-RSI-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/f781fc6f8091d36a4e.png)
 [trans]
### Overview
Dashen's volatility band RSI trading strategy combines the volatility band indicator and the relative strength index (RSI) indicator to generate a buy signal when the price breaks through the upper track and the RSI indicator shows an oversold signal; when the price falls below the upper track and the RSI indicator shows an overbought signal, a sell signal is generated. This strategy mainly uses the fluctuation band indicator to judge the rhythm changes of market fluctuations, combines the RSI indicator to find overbought and oversold phenomena, and sends trading signals at reversal points.
### Strategy Principles
The core logic of this strategy is based on the following points:
1. Calculate the simple moving average of the closing price on the 20th as the base center track.
2. Calculate the upper and lower rails based on the middle rail. The upper rail is the middle rail + 2 times the standard deviation of the 20-day closing price, and the lower rail is the middle rail - 2 times the standard deviation of the 20-day closing price. form a wave zone.
3. Calculate the 14-day RSI indicator to determine overbought and oversold conditions. An RSI below 20 is oversold, and above 70 is overbought.
4. When the closing price breaks through the upper track from bottom to top and the RSI indicator shows an oversold signal, a buy signal is generated.
5. When the closing price falls below the upper track from top to bottom and the RSI indicator shows an overbought signal, a sell signal is generated.
This strategy uses the volatility band indicator to determine the rhythm and speed of price fluctuations, and combines it with the RSI indicator to find reversal points and send trading signals at possible reversal points.
### Advantage Analysis
1. The volatility zone indicator can determine the rhythm and direction of market fluctuations, and the RSI indicator can determine overbought and oversold phenomena. The combination of the two forms an effective trading signal.
2. The RSI indicator parameters are adjustable, and different overbought and oversold levels can be set according to different markets to avoid false signals.
3. The parameters of the fluctuation zone can also be adjusted. Appropriate parameters can be set according to the range and speed of market fluctuations to increase the probability of profit.
4. Breaking through the upper track will form a buy signal, falling below the upper track will form a sell signal, simple and easy-to-understand trading logic.
5. Can be used in the stock market, foreign exchange and digital currency markets at the same time.
### Risk Analysis
1. When the market continues to rise, it may result in multiple misjudgments of buying signals. The false signal rate can be reduced by optimizing RSI parameters.
2. In a volatile market, the fluctuation band fluctuates frequently between the upper and lower rails, which may lead to frequent trading losses. Breakthrough parameters can be appropriately relaxed to reduce unnecessary transactions.
3. The code assumes that the overbought and oversold standards are fixed. In fact, the parameters should be set according to different levels of market volatility.
4. There is a lag in both the fluctuation band and the RSI indicator. Price trends cannot be predicted in advance, but price changes can only be tracked.
### Optimization direction
1. According to the characteristics of different markets, adjust the fluctuation band parameters, increase the width of the fluctuation band, and reduce the probability of mistaken transactions.
2. RSI parameters also need to be adjusted for different markets, and the overbought and oversold standards should be appropriately raised to avoid triggering false trading signals multiple times.
3. Add other indicator judgments, such as KDJ, MACD, etc., to avoid errors in the judgment of single indicators such as fluctuation bands and RSI.
4. Add a stop-loss strategy and set a reasonable stop-loss point to avoid excessive single losses.
5. Breakout or backtest test parameter optimization can be considered to further improve the stability of the strategy.

### Summarize
The master's volatility band RSI trading strategy uses the volatility band indicator to determine the speed of price fluctuations and the RSI indicator to determine overbought and oversold phenomena, and issue trading signals at possible reversal points. This strategy integrates the advantages of multiple indicators, has simple and clear trading logic, and can be widely applied to the stock market, foreign exchange, digital currency and other trading markets. It is an effective trend trading strategy. However, there is also some room for improvement, which can be optimized from adjusting parameters, adding indicators, stop-loss mechanisms and other aspects to make the strategy more stable and reliable.
||

### Overview

God's Bollinger Bands RSI trading strategy generates buy signals when the price crosses above the upper Bollinger Band and the RSI is showing an oversold signal; it generates sell signals when the price crosses below the upper Bollinger Band and the RSI is showing an overbought signal. This strategy mainly uses the Bollinger Bands indicator to judge changes in market volatility rhythm and combines with the RSI indicator to detect overbought and oversold phenomena to issue trading signals at inflection points.

### Strategy Principle 

The core logic of this strategy is based on the following points:

1. Calculate the 20-period simple moving average of the closing price as the base middle band.

2. Calculate the upper and lower bands on the basis of the middle band. The upper band is the middle band + 2 times the 20-period standard deviation of the closing price, and the lower band is the middle band - 2 times the 20-period standard deviation of the closing price. 

3. Calculate the 14-period RSI indicator to judge overbought and oversold phenomena. RSI below 20 is oversold and above 70 is overbought.

4. When the closing price breaks through the upper rail upward and the RSI indicator shows an oversold signal, a buy signal is generated.

5. When the closing price breaks through the upper rail downward and the RSI indicator shows an overbought signal, a sell signal is generated.

This strategy judges the rhythm and speed of price fluctuations through the Bollinger Bands indicator and detects possible reversal points with the RSI indicator to issue trading signals.

### Advantage Analysis

1. The Bollinger Bands indicator can determine market volatility rhythm and direction, and the RSI indicator judges overbought and oversold phenomena. The combination forms effective trading signals.

2. The RSI indicator parameters are adjustable and can set different overbought and oversold levels for different markets to avoid wrong signals.

3. The Bollinger Bands parameters can also be adjusted according to the market volatility range and speed to set appropriate parameters and improve profitability.

4. Breaking through the upper track forms a buy signal, and breaking through the upper track downward forms a sell signal. The trading logic is simple and easy to understand.

5. Can be used in stock, forex and cryptocurrency markets.

### Risk Analysis

1. In a sustained upside market, it may cause multiple misjudgments of buy signals. The error signal rate can be reduced by optimizing the RSI parameters.

2. In a choppy market, the upper and lower tracks of the Bollinger Bands oscillate frequently, which may lead to frequent unprofitable trades. Appropriately loosen the breakout parameters to reduce unnecessary trades.

3. The code assumes that the criteria for overbought and oversold are fixed, but they should be set according to different market volatility levels. 

4. Both Bollinger Bands and RSI indicators have lags and cannot predict price movements in advance but can only track price changes.

### Optimization

1. According to the characteristics of different markets, adjust the parameters of Bollinger Bands, increase the width of Bollinger Bands, and reduce the probability of erroneous transactions.

2. RSI parameters also need to be adjusted for different markets, appropriately increase the overbought and oversold criteria to avoid triggering multiple erroneous trading signals.

3. Increase other indicators for judgment, such as KDJ and MACD, to avoid errors caused by single Bollinger Bands and RSI indicators. 

4. Increase stop loss strategy and set reasonable stop loss points to avoid excessive losses.

5. Breakout testing or backtesting parameter optimization can be considered to further improve strategy stability.

### Summary

God's Bollinger Bands RSI trading strategy issues trading signals at possible reversal points by judging price volatility speed through Bollinger Bands indicator and overbought and oversold phenomena through RSI indicator. This strategy integrates the advantages of multiple indicators with simple and clear trading logic, and can be widely applied to stock, forex, cryptocurrency and other trading markets as an effective trend trading strategy. But there is also room for improvement, such as adjusting parameters, adding indicators, stop loss mechanism and so on to make the strategy more stable and reliable.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|3|Number of Candles Outside BB|
|v_input_2|3|Number of Candles Outside Upper BB|
|v_input_3|14|RSI Length|
|v_input_4|20|RSI Oversold Level|
|v_input_5|70|RSI Overbought Level|
|v_input_6|20|BB Length|
|v_input_7|2|BB Standard Deviation|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-01-16 00:00:00
end: 2024-01-22 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy("Bollinger Band + RSI Strategy", overlay=true)

// Input variables
numCandlesOutsideBB = input(3, "Number of Candles Outside BB")
numCandlesOutsideUpperBB = input(3, "Number of Candles Outside Upper BB")
rsiLength = input(14, "RSI Length")
rsiOversoldLevel = input(20, "RSI Oversold Level")
rsiOverboughtLevel = input(70, "RSI Overbought Level")

// Bollinger Bands
length = input(20, minval=1, title="BB Length")
mult = input(2.0, minval=0.001, maxval=50, title="BB Standard Deviation")
basis = sma(close, length)
dev = mult * stdev(close, length)
upperBB = basis + dev
lowerBB = basis - dev

// RSI
rsi = rsi(close, rsiLength)

// Buy condition
buyCondition = crossover(close, upperBB) and rsi > rsiOversoldLevel

// Sell condition
sellCondition = crossunder(close, upperBB) and rsi > rsiOverboughtLevel

// Strategy
if buyCondition
    strategy.entry("Buy", strategy.long)
if sellCondition
    strategy.close("Buy")

// Plotting
plot(upperBB, color=color.blue)
plot(lowerBB, color=color.red)
plot(rsi, "RSI", color=color.green)
```

> Detail

https://www.fmz.com/strategy/439744

> Last Modified

2024-01-23 14:33:13

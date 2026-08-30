
> Name

Double-Exponential-Moving-Average-Quant-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/8d049e681aeedaf061.png)
[trans]

### Overview
This strategy generates trading signals by calculating the crossover of the 5-day exponential moving average (EMA) and the 20-day simple moving average (SMA). When the 5-day EMA crosses the 20-day SMA, take a bullish position and enter a long order; when the price changes reaches 5% or -5%, close the position and leave the market. This strategy also combines the trading volume index (TII) as an auxiliary judgment indicator.
### Strategy Principles
The Double Exponential Moving Average is a widely used technical indicator. The 5-day EMA represents the recent price trend, and the 20-day SMA represents the mid-term price trend. When the short-term average crosses the longer-term average, it means that the price trend has turned from falling to rising, and you can enter the market to do long; conversely, when the short-term average crosses below the longer-term moving average, it means that the price has turned from rising to falling, and you should consider leaving the market.
This strategy sets the 5-day EMA and the 20-day SMA as trading signals. Generate a long position signal when the 5-day EMA crosses the 20-day SMA; when the position price change reaches 5% or -5%, it is considered a profit or a stop-loss exit. In addition, the TII indicator is combined as an auxiliary judgment criterion. When TII is greater than 0 and greater than the previous period, it means that the price is currently rising, and the EMA and SMA golden cross signals are more reliable at this time.
The detailed strategic steps are as follows:
1. Calculate 5-day EMA, 20-day SMA and TII indicators
2. When the 5-day EMA crosses the 20-day SMA and the TII is positive and greater than the previous period, a buy signal is generated.
3. Enter a long position
4. When the price changes reaches 5% or -5%, close the position and leave the market
### Strategic Advantages
This strategy utilizes the golden cross trading signal of the moving average and has the following advantages:
1. The strategy signal is simple, clear and easy to implement.
2. The moving average is a mainstream and commonly used technical indicator, and the golden cross is a more classic and reliable trading signal.
3. Combined with the TII indicator, some uncertain signals can be filtered out and the strategy winning rate can be improved.
4. By setting stop loss and take profit standards, single transaction risks can be effectively controlled.
In general, this strategy has clear rules, is easy to understand and implement, uses mature technical indicators such as moving average crossovers, and has relatively comprehensive risk control measures. It is a quantitative trading strategy suitable for novices to learn and use.
### Strategy Risk
This strategy also has certain risks, mainly including:
1. There will be a certain lag in the moving average crossover signal.
2. The TII indicator has a worrying effect in consolidating the market.
3. Fixed stop-loss and take-profit standards may be too arbitrary.
These risks can be improved by:
1. Optimize moving average parameters and reduce signal lag.
2. Add other auxiliary indicators to improve the reliability of the signal.  
3. Set dynamic stop loss and take profit standards.
Therefore, there is room for further optimization of this strategy.
### Strategy optimization direction
This strategy can be optimized from the following aspects:
1. Optimize moving average parameters. You can test shorter-term or longer-term EMA and SMA parameter combinations to find a better parameter pair.
2. Add other indicator filters. For example, the auxiliary judgment of indicators such as MACD and KDJ can avoid some false signals.
3. Apply machine learning algorithms. Use statistical methods or neural networks to model historical data and automatically find better parameters.
4. Set dynamic stop loss and take profit. Adjusting the stop loss range according to the degree of market volatility and individual stock characteristics can better control risks.
5. Expand to other varieties. Apply the same strategy rules to other varieties such as foreign exchange and digital currencies.
Through improvements in the above directions, the stability and profitability of the strategy can be greatly improved.
### Summarize
This strategy overall is a double moving average crossover strategy that is easy to understand and implement. It takes advantage of moving average signals and supplements it with the TII indicator to try to filter out erroneous signals. Control risk by setting stop loss and take profit. This strategy is suitable for beginners to learn, and there is still a lot of room for optimization. If we continue to improve parameter settings, add signal filtering and dynamic stop loss, etc., it can become a very practical quantitative trading strategy.
||

### Overview

This strategy generates trading signals by calculating the crossovers between 5-day exponential moving average (EMA) and 20-day simple moving average (SMA). It goes long when 5-day EMA crosses above 20-day SMA and closes position when price change reaches 5% or -5%. It also incorporates Trading Index Index (TII) as an auxiliary indicator.  

### Strategy Principle

Double exponential moving averages are widely used technical indicators. 5-day EMA represents recent price trends while 20-day SMA shows medium-term price moves. When shorter-term MA crosses above longer-term MA, it signals an upside breakout and upward price trend, indicating good timing to go long. On the contrary, downward crossover implies potential price reversal and should consider exiting positions.

This strategy sets 5-day EMA and 20-day SMA as trading signals. It goes long when 5-day EMA crosses over 20-day SMA and closes position when price change hits 5% or -5%. It also checks if TII is positive and rising to confirm the signal reliability. 

The detailed steps are:

1. Calculate 5-day EMA, 20-day SMA and TII 
2. Generate buy signal when 5-day EMA crosses over 20-day SMA while TII is positive and rising
3. Enter long position 
4. Close position when price change reaches 5% or -5%

### Advantages

This strategy utilizes the golden crossover between two MAs and has following pros:

1. Clear and simple trading signals, easy to implement.  
2. MAs are mainstream and common technical indicators, golden cross signal is classical and reliable.
3. Incorporating TII can filter some uncertain signals and improve win rate.  
4. Predefined stop loss/take profit standards effectively control per trade risk.

In general, this strategy has straightforward rules, utilizes mature technical indicators like MA crossovers, and has relatively comprehensive risk control measurements. It is suitable for beginners to learn and use in quantitative trading field.  

### Risks

There are still some risks within this strategy:

1. MA crossover signals may lag. 
2. TII indicator does not perform well in range-bound markets.
3. Fixed stop loss/take profit standards could be arbitrary.  

Suggested improvements are:

1. Optimize MA parameters to reduce the lag.
2. Add other auxiliary indicators to enhance signal reliability. 
3. Set dynamic stop loss/take profit standards.

So there is room for further optimization.

### Optimization Directions   

This strategy can be improved from the following aspects:

1. Optimize MA parameters by testing shorter/longer EMA and SMA combinations to find the optimal pair.  

2. Add other indicators like MACD, KDJ to filter false signals.  

3. Employ machine learning algorithms to find better parameters through historical data modeling and statistics.

4. Set dynamic stop loss/take profit based on market volatility and instrument characteristics to better control risks.   

5. Expand this strategy to other products like forex, cryptocurrencies.

Through above enhancements, the stability and profitability of this strategy can be substantially improved.  

### Conclusion

In conclusion, this is an easy-to-understand and implement dual MA crossover strategy. It takes advantage of MA signals and uses TII to filter errors. It controls risks by stop loss/take profit. The strategy suits beginners to learn and also has large room for optimizations. Further improvements on parameter tuning, signal filtering and dynamic stop loss can transform it into a practical and powerful trading strategy.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|60|Major Length|
|v_input_2|30|Minor Length|
|v_input_3_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-02 00:00:00
end: 2024-02-01 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("EMA-SMA Crossover Strategy", shorttitle="EMA-SMA Cross", overlay=true)

// Define the moving averages
ema5 = ta.ema(close, 5)
sma20 = ta.sma(close, 20)
smaVolume10 = ta.sma(volume, 50)

majorLength = input(60, title="Major Length")
minorLength = input(30, title="Minor Length")
src = input(close, title="Source")

smaValue = ta.sma(src, majorLength)

positiveSum = 0.0
negativeSum = 0.0

for i = 0 to minorLength - 1
    price = na(src[i]) ? 0 : src[i]
    avg = na(smaValue[i]) ? 0 : smaValue[i]
    positiveSum := positiveSum + (price > avg ? price - avg : 0)
    negativeSum := negativeSum + (price > avg ? 0 : avg - price)

tii = 100 * positiveSum / (positiveSum + negativeSum)

// Buy condition: 5 EMA crosses above 20 SMA
buyCondition = ta.crossover(ema5, sma20) and tii > 0 and tii >= tii[1]

//and volume > smaVolume10 //

// Track entry price
var entryPrice = 0.0
if (buyCondition)
    entryPrice := close

// Calculate percentage change from entry price
priceChange = close / entryPrice - 1

// Plotting the moving averages on the chart
plot(ema5, color=color.blue, title="5 EMA")
plot(sma20, color=color.red, title="20 SMA")

// Highlighting buy signals and exit signals on the chart
// plotshape(series=buyCondition, title="Buy Signal", location=location.belowbar, color=color.green, size=size.small, style=shape.labelup, text="Buy")

// Strategy entry and exit
if (buyCondition)
    strategy.entry("Buy", strategy.long)

// Exit conditions
if (strategy.opentrades > 0)
    if (priceChange >= 0.05 or priceChange <= -0.05)
        strategy.close("Buy")

```

> Detail

https://www.fmz.com/strategy/440813

> Last Modified

2024-02-02 11:41:34

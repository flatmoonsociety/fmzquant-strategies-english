
> Name

Single moving average combination trading strategy Simple-Moving-Average-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/115a9944d892faa0e44.png)
[trans]

## Overview
This strategy is a combination trading strategy based on a simple moving average. It uses the moving average crossover of the 9-day and 21-day lines as buy and sell signals. A buy signal is generated when the short-term moving average crosses above the long-term moving average from below; a sell signal is generated when the short-term moving average crosses below the long-term moving average from above.
## Strategy Principle
The core logic of this strategy is to use two simple moving averages with different parameters, one is the 9-day line representing the short-term trend, and the other is the 21-day line representing the long-term trend. When the short-term trend line crosses the long-term trend line from below, it means that the market has turned from falling to rising, and a buy signal is generated; when the short-term trend line crosses the long-term trend line from above, it means that the market has turned from rising to falling, and a sell signal is generated.
This strategy mainly relies on the "golden cross" and "death cross" signals of the moving average. The so-called "golden cross" is when the short-term moving average breaks through the long-term moving average from bottom to top, indicating that the market may turn from falling to rising; the "death cross" is when the short-term moving average breaks through the long-term moving average from top to bottom, indicating that the market is about to turn from rising to falling. This strategy is to use these two signals to judge the long-term and short-term trend relationship of the market and make buying and selling decisions.
## Strategic Advantages
1. Simple operation, easy to understand and use
2. Few parameters, no need for a lot of testing and optimization
3. Moderate trading frequency and avoid being too aggressive
4. Can relatively accurately capture the turning points of long-term and short-term trends
5. Has certain measurability and stability
## Strategy Risk
1. The dual moving average strategy is prone to generating false signals and frequent switching.
2. The selection of buying and selling points and parameter setting rely on experience and are not systematic enough.
3. The effect is highly related to parameter selection. 9 and 21 antennas are not optimal.
4. Unable to effectively filter out noise trading in volatile market conditions
5. Poor performance in sharp market fluctuations and easy losses
It can be optimized and improved through the following methods:
1. Add a filtering mechanism to avoid false signals
2. Combine with other indicators to determine the reliability of trend signals
3. Test optimization based on different varieties and parameters
4. Set stop loss and take profit logic to control risks
## Summary
Overall, this strategy is a more traditional and simple double moving average combination strategy. It is easy to understand and implement, the parameter selection is relatively simple, and it can effectively track the conversion of long-term and short-term trends. However, this strategy also has some problems, such as the generation of false signals, the selection of PARAMETERS based on experience, and poor performance in sharply volatile market conditions. This requires us to pay attention to risk control when using it, and carry out appropriate optimization, improvement and combination.
||

## Overview
This is a combination trading strategy based on simple moving averages (SMA). It uses a crossover of the 9-day and 21-day SMA lines as buy and sell signals. When the short-term SMA crosses above the long-term SMA from below, a buy signal is generated. When the short-term SMA crosses below the long-term SMA from above, a sell signal is generated.

## Strategy Logic  
The core logic of this strategy is to use two SMA lines with different parameters - a 9-day SMA representing the short-term trend and a 21-day SMA representing the long-term trend. When the short-term trend line crosses above the long-term trend line from below, it indicates the market is changing from downtrend to uptrend, generating a buy signal. When the short-term line crosses below the long-term line from above, it signals a change from uptrend to downtrend, generating a sell signal.

The key signals this strategy relies on are the "golden cross" and "death cross" of the two SMA lines. A golden cross occurs when the short SMA crosses above the long SMA, signaling a possible change from downtrend to uptrend. A death cross occurs when the short SMA crosses below the long SMA, suggesting a downturn from uptrend may start. By utilizing these two signals, the strategy identifies relationships between short-term and long-term trends to make trading decisions.  

## Advantages
1. Simple to understand and implement  
2. Few parameters needing extensive testing/optimization
3. Reasonable trading frequency avoiding overly aggressive trades  
4. Fairly accurate at identifying trend reversal points  
5. Offers measurability and stability to a certain extent

## Risks
1. Prone to generating false signals and whipsaws  
2. Buying/selling point selection relies heavily on experience instead of a systematic approach
3. Performance highly parameter dependent. 9-day/21-day SMA may not be optimal
4. Ineffective at filtering noise trades in choppy/sideways markets
5. Sizable losing trades in high volatility environments  

Possible Enhancements:
1. Add filters to avoid acting on false signals
2. Incorporate other indicators to gauge signal reliability 
3. Test and optimize parameters for different products  
4. Implement stop loss/take profit to control risks

## Conclusion
Overall this is a fairly traditional and simple dual moving average crossover system. It is easy to understand and implement with relatively simple parameter selection. It can effectively track changes between short-term and long-term trends. However, issues like false signals, empirically chosen parameters, mediocre performance in high volatility environments need to be addressed. Appropriate optimizations, enhancements, and combinations should be considered along with solid risk control practices.

[/trans]



> Source (PineScript)

``` pinescript
/*backtest
start: 2024-01-01 00:00:00
end: 2024-01-31 23:59:59
period: 1h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("Bitboy Strategy", overlay=true)

// Define MAs
SlowMA = ta.sma(close, 9)
FastMA = ta.sma(close, 21)

// Plot MAs
plot1 = plot(SlowMA, color=color.new(color.red, 0), title="Slow MA")
plot2 = plot(FastMA, color=color.new(color.green, 0), title="Fast MA")

// Plot MA Ribbon
fill(plot1, plot2, color=FastMA > SlowMA ? color.rgb(233, 21, 21, 50) : color.new(#1de223, 45))

// Define buy/sell conditions
longCondition = ta.crossover(SlowMA, FastMA)
shortCondition = ta.crossunder(SlowMA, FastMA)

// Strategy commands for buy/sell
if longCondition
    strategy.entry("Long", strategy.long)

if shortCondition
    strategy.entry("Short", strategy.short)

// Plot buy/sell signals (for visualization)
plotshape(longCondition, location=location.belowbar, color=color.rgb(18, 230, 25, 37), style=shape.labelup, text="Buy", textcolor=color.white)
plotshape(shortCondition, location=location.abovebar, color=color.rgb(239, 23, 23, 40), style=shape.labeldown, text="Sell", textcolor=color.white)
```

> Detail

https://www.fmz.com/strategy/442388

> Last Modified

2024-02-21 15:11:32

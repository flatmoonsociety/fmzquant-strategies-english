
> Name

Gold-Price-Action-Trading-Algorithm based on price action
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/ab76c0d7f0dd7b9574aa130977e93162902b2cc213747878d136b25fa4d41c37.png)
[trans]

## Overview
This algorithm trades based on the price action of gold. It will calculate the highest and lowest prices of the last 20 K lines to determine the price fluctuation range. When the price breaks through the highest price of the most recent K-line, it will go long; when the price falls below the lowest price of the most recent K-line, it will go short. After long and short positions, take profit and stop loss prices will be set.
## Algorithm principle
The core logic of this algorithm is based on breakthrough theory. It will record the highest and lowest prices of the last 20 K lines to determine the range of price fluctuations. When the price exceeds this range, it is considered a breakout and therefore a trade can be made. Specifically, the algorithm flow is:
1. Calculate the highest prices (highs) and lowest prices (lows) of the last 20 K lines
2. Get the range of price fluctuations (priceRange)
3. Record the highest price of the latest K line as the breakthrough level (breakoutLevel)
4. When the high point of the latest K-line exceeds the breakthrough level and the closing price also exceeds the breakthrough level, go long
5. When the latest K-line low falls below the breakthrough level and the closing price also falls below the breakthrough level, go short
6. Set take-profit and stop-loss prices after going long or short.
It can be seen that the trading signal of this algorithm is based on the judgment of price breakthrough, and the core is to identify the timing of price breakthrough.
## Advantage Analysis
This algorithm has the following advantages:
1. Simple and clear, easy to understand and implement
2. Judgment based on price action, not affected by other indicators
3. The breakthrough signal is clear and entry timing is easy to master.
4. Can significantly filter market noise and avoid being trapped
5. There are stop-profit and stop-loss settings to control single losses.
In general, the core idea of ​​this algorithm is clear, the logic is reasonable, the implementation is simple, the entry timing is easy to master, and the single loss is controllable. It is a highly practical quantitative trading strategy.
## Risk Analysis
This algorithm also has some risks:
1. The probability of breakthrough failure is high, and there is a risk of missing out on profits.
2. If the breakthrough time is not properly grasped, you may enter the market too early or too late.
3. The retracement may be large and requires a certain amount of mental endurance.
4. If the stop-profit and stop-loss settings are unreasonable, you may miss greater profits or suffer greater losses.
To address these risks, the following measures can be taken to control and optimize:
1. Combine with other indicators to confirm breakthroughs to enhance reliability
2. Optimize parameters and improve the accuracy of entry timing
3. Adjust position management to reduce the risk of single loss
4. Dynamically adjust take-profit and stop-loss prices
## Optimization direction
This algorithm can be optimized from the following aspects:
1. **Combined with other indicators**. Indicators such as moving averages and Bollinger Bands can be introduced to confirm breakthroughs twice and improve the reliability of signals.
2. **Parameter optimization**. You can test different parameter combinations, optimize the cycle length of breakthrough judgment, and find parameter settings that make trading signals more reliable.
3. **Optimization of stop profit and stop loss**. It can be combined with indicators such as volatility to dynamically adjust the stop-profit and stop-loss distances in real time.
4. **Position management optimization**. Optimize the position algorithm to reduce the impact of a single loss.
5. **Machine Learning**. Use machine learning algorithms to learn a large amount of historical data and automatically find better parameter combinations.
Through the above optimization, the stability, winning rate and profitability of the algorithm can be further improved.
## Summarize
This gold trading algorithm is based on price action judgment and uses breakout theory to generate trading signals. The idea is simple and clear, easy to implement and highly practical. At the same time, it also carries certain risks and requires further optimization to improve stability and profitability. Generally speaking, this algorithm is suitable for gold trading and is an efficient and practical quantitative strategy. By further combining other indicators, parameter optimization, stop-profit and stop-loss optimization, etc., better strategic effects can be obtained.
||

## Overview   

This algorithm trades gold based on its price action. It calculates the highest and lowest prices of the recent 20 candlesticks to determine the price fluctuation range. It goes long when the price breaks through the highest price of the latest candlestick and goes short when the price breaks through the lowest price of the latest candlestick. After opening long or short positions, it sets take profit and stop loss prices.  

## Principles   

The core logic of this algorithm is based on the breakout theory. It records the highest and lowest prices of the most recent 20 candlesticks to determine the price fluctuation range. When the price exceeds this range, it is considered a breakout and thus a trading signal is triggered. Specifically, the algorithm flow is: 

1. Calculate the highest prices (highs) and lowest prices (lows) of the most recent 20 candlesticks  
2. Get the price fluctuation range (priceRange)
3. Record the highest price of the latest candlestick as the breakout level (breakoutLevel)
4. When the high of the latest candlestick breaks through the breakout level and the close also breaks through the breakout level, go long
5. When the low of the latest candlestick drops below the breakout level and the close also drops below the breakout level, go short  
6. Set take profit and stop loss prices after opening long or short positions  

As can be seen, the trading signals of this algorithm come from price breakout judgements. The key is to identify the timing of price breakouts.  

## Advantages Analysis   

The algorithm has the following advantages:  

1. Simple and clear, easy to understand and implement  
2. Based on price action, not affected by other indicators  
3. Clear breakout signals, easy to grasp entry timing   
4. Can significantly filter market noise and avoid being trapped
5. Take profit and stop loss in place to control single trade loss  

In general, the core idea of this algorithm is clear and logical. It is simple to implement and easy to grasp entry timing. It also allows controlling single trade loss. Thus it is a quantitative trading strategy with strong practicality.   

## Risk Analysis     

The algorithm also has some risks:   

1. High probability of failed breakout, risk of missing profits 
2. Improper grasp of breakout timing, may enter too early or too late  
3. Relatively large drawdowns, need certain psychological endurance  
4. Unreasonable take profit and stop loss settings, may miss larger profits or take higher losses  

To control and optimize against these risks, the following measures can be taken:  

1. Confirm breakout with other indicators to increase reliability  
2. Optimize parameters to improve entry timing accuracy  
3. Adjust position sizing to reduce single trade loss risk 
4. Dynamically adjust take profit and stop loss prices  

## Optimization Directions 

The algorithm can be optimized in the following aspects:   

1. **Combine with other indicators**. Moving averages, Bollinger Bands etc can be introduced to double confirm the breakout signals and increase reliability.  

2. **Parameter optimization**. Different parameter combinations can be tested to optimize the breakout period length and find more reliable parameter settings.   

3. **Take profit and stop loss optimization**. Dynamically adjust take profit and stop loss distance based on volatility etc.  

4. **Position sizing optimization**. Optimize position sizing algorithm to reduce single trade loss impact. 

5. **Machine learning**. Learn from large amount of historical data to automatically find better parameter combinations.   

The above optimizations can further enhance the stability, win rate and profitability of the algorithm.  

## Conclusion   

The gold trading algorithm generates trading signals based on price action and the breakout theory. The idea is simple and clear, easy to implement, and highly practical. Meanwhile, it also has some risks and needs further optimization to improve stability and profitability. Overall speaking, it is suitable for gold trading and an efficient quantitative strategy. By combining other indicators, parameter optimization, take profit/stop loss optimization etc, better strategy performance can be achieved.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|500|Take Profit|
|v_input_2|200|Stop Loss|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-06 00:00:00
end: 2023-12-12 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=5
strategy("XAUUSD Price Action Strategy", overlay=true)

// Define input parameters
takeProfit = input(500, "Take Profit")
stopLoss = input(200, "Stop Loss")

// Calculate price action
highs = ta.highest(high, 20)
lows = ta.lowest(low, 20)
priceRange = highs - lows
breakoutLevel = highs[1]

// Define conditions for long and short trades
longCondition = high > breakoutLevel and close > highs[1]
shortCondition = low < breakoutLevel and close < lows[1]

// Execute long and short trades with take profit and stop loss
if longCondition
    strategy.entry("Long", strategy.long)
    strategy.exit("Long Exit", "Long", limit = close + takeProfit, stop = close - stopLoss)

if shortCondition
    strategy.entry("Short", strategy.short)
    strategy.exit("Short Exit", "Short", limit = close - takeProfit, stop = close + stopLoss)

// Plot breakout level
plot(breakoutLevel, color=color.blue, title="Breakout Level")

// Highlight long and short trade signals on the chart
bgcolor(longCondition ? color.green : na, transp=80)
bgcolor(shortCondition ? color.red : na, transp=80)
```

> Detail

https://www.fmz.com/strategy/435260

> Last Modified

2023-12-13 16:08:12

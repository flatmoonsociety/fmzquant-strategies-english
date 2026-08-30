
> Name

High-Minus-Exponential-Moving-Average-Stock-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/100ccdcc486c163310c.png)
[trans]

## Overview
High Minus Exponential Moving Average Stock Strategy (High Minus Exponential Moving Average Stock Strategy) is a quantitative investment strategy that makes trading decisions based on high points and exponential moving averages. This strategy calculates the 13-period exponential moving average from the high point of the previous period's price minus the closing price of the previous period. If the difference is greater than 0, go long, and if the difference is less than 0, go short. It is a trend-following strategy.
## Strategy Principle
The core indicator of this strategy is the High Minus Exponential Moving Average (HMEMA). Specifically, it takes the highest price of the previous period and subtracts the 13-period exponential moving average of the closing price of the previous period. When the difference is greater than 0, it means that the price of the latest period has reached a new high and entered a bull trend, then go long; when the difference is less than 0, it means that the price is lower than the recent average level, entering a bear trend, then go short.
This strategy believes that when the price reaches a new high, it is the beginning of the bull trend, so go long at that time; when the price falls below the most recent average price, it is the beginning of the short trend, and then go short. Through this method, the strategy can seize the main trend conversion point of price and achieve trend tracking.
## Strategic Advantages
1. This strategy can capture major price trend turning points. Place an order when the price reaches a new high or falls below the moving average, reducing the number of transactions but capturing key points.
2. Using the exponential moving average as a reference can reflect price trends more smoothly and filter out short-term market noise.
3. The strategy logic is simple and clear, easy to understand and modify, and is suitable for beginners to learn.
4. This strategy can be applied to foreign exchange, cryptocurrency and other markets in different time periods and is highly flexible.
## Risk Analysis
1. This strategy cannot determine the specific entry and exit points of the market, and there is a certain risk of drifting with the crowd.
2. When the price is in a volatile range, this strategy will generate false signals and pose the risk of over-trading. You can adjust parameters appropriately or add filter conditions to reduce it.
3. The strategy does not take into account the actual fluctuation range of the stock price, and there is a risk of excessive losses. Stop losses can be set to control risk.
4. The strategy does not determine the long and short direction based on the overall market status, individual stock fundamentals, etc., and there is a risk of poor signal effect.
## Optimization direction
1. You can consider the combined volatility range and only send trading signals when the volatility increases to reduce misleading transactions.
2. You can combine the simple moving average of the stock price, and go long when the high point exceeds the fast line and slow line, and go short when it falls below the fast line and slow line, and set filter conditions.
3. Parameters such as moving average period, comparison series, etc. can be optimized to find the best parameter combination.
4. You can consider switching strategy parameters or using different moving average indicators according to the market status (long, short, shock) to improve the situation adaptability of the strategy.
## Summarize
The Highs Minus Exponential Moving Average strategy designs a simple and effective trend following strategy by comparing price highs to the exponential moving average. This strategy captures the trend turning point when the price reaches a new high or crosses the moving average, which can reduce the number of transactions but capture key points. At the same time, the use of exponential moving averages filters out market noise. This strategy is suitable for tracking the medium and long-term trends of financial products such as foreign exchange or cryptocurrencies. Through further optimization, better strategy performance can be expected.
||


## Overview

The High Minus Exponential Moving Average Stock Strategy is a quantitative investment strategy that makes trading decisions based on the high price of a stock and its exponential moving average (EMA). It calculates the difference between the high price of the previous period and the 13-period EMA of the close price of the previous period. If the difference is greater than 0, it goes long. If the difference is less than 0, it goes short. This strategy belongs to the trend-following type.  

## Strategy Logic

The core indicator of this strategy is the High Minus Exponential Moving Average (HMEMA). Specifically, it takes the high price of the previous period and subtracts the 13-period EMA of the close price of the previous period. When this difference is greater than 0, it means the latest stock price has reached a new high and has entered a bullish trend, so it should go long. When the difference is less than 0, it means the stock price is below its recent average level and has entered a bearish trend, so it should go short.

The logic behind this is when stock price reaches a new high, it signals the start of an uptrend, so a long position should be taken. When the price breaks below its recent average, it signals the start of a downtrend, so a short position should be taken. This way, the strategy is able to capture major turning points in the price trend and follow trends.

## Advantages  

1. This strategy is able to capture major turning points of stock price trends. It enters orders when prices reach new highs or break through moving averages, thus reducing trade frequency while catching key levels.

2. The use of exponential moving averages provides a smoother reflection of price moves, filtering out short-term market noises.

3. The strategy logic is simple and clear, easy to understand and modify, suitable for beginners to learn. 

4. This strategy is flexible enough to be applied to stocks, forex, crypto currencies in different time frames.

## Risks

1. This strategy fails to determine exact entry and exit levels, posing certain risks of trend-chasing.

2. It may generate false signals when prices are ranging, causing over-trading risks. Parameters can be adjusted or filters added to reduce such risks.

3. The strategy does not consider the actual volatility of stock prices, risking oversized losses. Stop loss can be set to control risks.

4. The strategy does not incorporate overall market conditions, fundamentals of individual stocks to determine directions, running the risk of poor signal effects.

## Optimization

1. Consider incorporating price volatility to issue signals only when volatility increases, so as to reduce misleading trades.

2. Adding filters such as a double confirmation from fast and slow simple moving averages may help avoid false signals.  

3. Parameters like moving average periods, price series for comparison can be optimized to find the optimal combination.

4. Consider switching parameters or indicators based on market states to improve adaptability.

## Conclusion

The High Minus Exponential Moving Average Stock Strategy designs a simple but effective way of tracking stock trends by comparing high prices with exponential moving averages. It captures major turning points when prices break to new highs or moving average levels, thus catching key spots with fewer trades. Exponential moving averages also filter out market noises. This strategy suits medium- to long-term trend-following trading of stocks, forex, crypto currencies and more. Further optimizations may lead to improved strategy performance.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|13|Length|
|v_input_2|false|Trade reverse|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-11-27 00:00:00
end: 2023-12-03 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
////////////////////////////////////////////////////////////
//  Copyright by HPotter v1.0 20/16/2016
// This indicator plots the difference between the High (of the previous period)
// and an exponential moving average (13 period) of the Close (of the previous period).
// You can use in the xPrice any series: Open, High, Low, Close, HL2, HLC3, OHLC4 and ect...
// It buy if indicator above 0 and sell if below.
//
// You can change long to short in the Input Settings
// Please, use it only for learning or paper trading. Do not for real trading.
////////////////////////////////////////////////////////////
strategy(title="High - EMA Strategy Backtest", shorttitle="High - EMA Strategy")
Length = input(13, minval=1)
reverse = input(false, title="Trade reverse")
xPrice = close  // You can use any series
hline(0, color=red, linestyle=line)
xEMA = ema(xPrice, Length)
nRes = high[1] - nz(xEMA[1])
pos = iff(nRes > 0, 1,
	   iff(nRes < 0, -1, nz(pos[1], 0))) 
possig = iff(reverse and pos == 1, -1,
          iff(reverse and pos == -1, 1, pos))	   
if (possig == 1) 
    strategy.entry("Long", strategy.long)
if (possig == -1)
    strategy.entry("Short", strategy.short)	   	    
barcolor(possig == -1 ? red: possig == 1 ? green : blue )
plot(nRes, color=blue, title="High - EMA") 
```

> Detail

https://www.fmz.com/strategy/434175

> Last Modified

2023-12-04 14:29:31

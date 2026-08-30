
> Name

Golden Cross and Death Cross Double-Hull-Moving-Average-Crossover-Trading-Strategy
> Author

ChaoZhang

> Strategy Description

[trans]


This strategy mainly uses the intersection of two Hull moving averages in different time periods to determine the market trend and conduct long and short short operations.
### Strategy Principles
This strategy uses two Hull moving averages, one with 60 periods and one with 175 periods. in:
1. Hullma is the 60-period Hull moving average, calculated through the wma function.
2. ahullma is the 175-period Hull moving average, calculated through the wma function.
3. When hullma breaks through ahullma from bottom to top, a golden cross is generated, which is a long signal.
4. When hullma falls below ahullma from top to bottom, a dead cross is generated, which is a short selling signal.
5. longCondition and shortCondition determine the long and short conditions respectively.
6. Use the strategy.entry function to perform long and short operations.
This strategy uses the crossover principle to determine the intersection of the short-term moving average and the long-term moving average to capture changes in the short-term and long-term trends of the market to make profits.
### Advantage Analysis
1. Use Hull moving average to capture price changes faster.
2. The principle of double moving average crossover is simple to understand and easy to operate.
3. The combination of 60-period and 175-period can capture short- and medium-term trends.
4. The cycle parameters can be customized to adapt to different markets and varieties.
5. Can be flexibly used in intraday and position trading.
### Risk Analysis
1. The crossover of double moving averages has a certain lag, and the timing of entry is inaccurate.
2. There may be more false signals at the short-period moving average head.
3. Frequent crossovers may occur in the volatile market, resulting in losses.
4. Improper period setting makes it impossible to capture trend changes.
5. The cycle parameters need to be appropriately optimized, and different varieties need to be adjusted.
Risks can be mitigated by filtering signals in combination with other indicators, optimizing cycle parameters, and appropriately relaxing stop losses.
### Optimization direction
1. Test different moving average combinations to find the best period.
2. Add indicators such as trend index for filtering.
3. Optimize the stop loss strategy and reduce frequent stop losses.
4. The cycle parameters can be adjusted for different varieties.
5. Algorithms such as machine learning can be added to dynamically optimize parameters.
### Summarize
This strategy uses the principles of golden cross and dead cross to judge the market trend through the crossing of double Hull moving averages. It is a typical short-term double moving average trading strategy. The advantage is that the idea is simple, easy to operate, and can capture faster short-term trends. But there is also a higher risk of false signals and lag issues. It can be improved through parameter optimization, indicator filtering and other methods. It is a short-term trading strategy worth learning and studying. This strategy can be flexibly applied to intraday and position trading, and can also be widely used in digital currencies and traditional varieties. Generally speaking, this strategy is suitable for short-term operations and can obtain good returns on investment if used reasonably.
|| 

This strategy mainly uses the crossover of two Hull Moving Averages of different timeframes to determine market trends and make long and short trades.

### Strategy Logic

The strategy uses two Hull Moving Averages, one is 60 periods and the other is 175 periods. Where:

1. hullma is the 60-period Hull Moving Average, calculated by the wma function. 

2. ahullma is the 175-period Hull Moving Average, calculated by the wma function.

3. When hullma crosses ahullma upward, a golden cross occurs, giving a long signal.

4. When hullma crosses ahullma downward, a death cross occurs, giving a short signal.

5. longCondition and shortCondition determine the long and short entry conditions respectively. 

6. The strategy.entry function is used to execute long and short trades.

The strategy utilizes the crossover principle to capture trend changes using the crossovers between short-term and long-term moving averages, for profit.

### Advantage Analysis

1. Hull Moving Average responds faster to price changes.

2. Crossover principle is simple and easy to implement. 

3. The 60- and 175-period combination captures medium-term trends.

4. Customizable period parameters for different markets.

5. Applicable for intraday and position trading.

### Risk Analysis

1. Crossovers have some lag in signals.

2. More false signals from short-term MA. 

3. Frequent crossovers may cause losses in range-bound markets. 

4. Wrong period settings cannot capture trend changes.

5. Need parameter optimization for different symbols.

Risks can be mitigated by adding filters, optimizing parameters, allowing wider stops.

### Optimization Directions

1. Test different MA combinations to find optimal periods.

2. Add trend indicators for signal filtering. 

3. Optimize stop loss strategy to reduce frequent stops.

4. Adjust periods for different symbols. 

5. Add machine learning to dynamically optimize parameters.

### Summary

This strategy utilizes golden cross and death cross principles to determine trends using double Hull Moving Average crossovers. It is a typical short-term dual moving average system. The pros are simple logic and easy implementation, catching fast short-term trends. The cons are high false signals and lagging issues. Improvements can be made via parameter optimization, signal filtering etc. It is a worthwhile short-term trading strategy to study. The strategy can be flexibly applied for intraday and position trading across different markets. Overall, it is suitable for short-term trading and can generate good returns if used properly.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|60|HULL MA 1 LENGTH|
|v_input_2_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_3|175|HULL MA 2 LENGTH|
|v_input_4_close|0|Source: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-10 00:00:00
end: 2023-10-10 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=4
strategy(title = "Hull MA", shorttitle="Junior2", overlay = true)

//HULL MA 1

length = input(60, minval=1,title="HULL MA 1 LENGTH")
src = input(close, title="Source")
hullma = wma(2*wma(src, length/2)-wma(src, length), round(sqrt(length)))

plot(hullma, color=color.green)

//HULLMA 2

alength = input(175, minval=1,title="HULL MA 2 LENGTH")
asrc = input(close, title="Source")
ahullma = wma(2*wma(asrc, alength/2)-wma(asrc, alength), round(sqrt(alength)))

plot(ahullma, color=color.green)

c1up= crossover(hullma,ahullma)
c1down= crossunder(hullma,ahullma)

longCondition = c1up
if longCondition

    strategy.entry("L", strategy.long)


shortCondition = c1down 
if shortCondition

    strategy.entry("S", strategy.short)

plot(close)
```

> Detail

https://www.fmz.com/strategy/428969

> Last Modified

2023-10-11 14:49:54

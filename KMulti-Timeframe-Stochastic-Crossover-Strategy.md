
> Name

Multi-Timeframe-Stochastic-Crossover-Strategy Multi-Timeframe-Stochastic-Crossover-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](https://www.fmz.com/upload/asset/c78a7efdb6101a0a15.png)

[trans]


## Overview
The multi-time period standard deviation K-line crossover strategy is a typical trend following strategy. This strategy calculates the standard deviation values ​​of different time periods (such as daily, weekly, monthly, etc.), constructs multiple sets of K lines and D lines, and then takes the average of these lines to construct a moving average. When the fast line crosses the slow line, it goes long and when it crosses below, it goes short. This strategy makes full use of the predictive ability of standard deviations in different periods. By combining the standard deviation moving averages of multiple periods, it can effectively filter market noise and lock in the main market trends.
## Strategy Principle
The core logic of this strategy is to calculate the standard deviation of multiple time periods and then average it to construct a trading signal.
First, the strategy calculates the standard deviation K value under different parameters through the `stoch()` function. A total of 5 sets of K values ​​are calculated here, and the corresponding time periods are daily, weekly, and monthly levels.
```pine
smoothK = input(55)  
SMAsmoothK = input(13)
k = sma(stoch(price, high, low, smoothK), SMAsmoothK) 

smoothK1 = input(89)
SMAsmoothK1 = input(8)  
k1 = sma(stoch(price, high, low, smoothK1), SMAsmoothK1)

...

smoothK4 = input(377) 
SMAsmoothK4 = input(2)
k4 = sma(stoch(price, high, low, smoothK4), SMAsmoothK4)
```

Then calculate the D line using different parameters:
```pine 
smoothD = input(34)
d = sma(k, smoothD)

...

smoothD4 = input(233)  
d4 = sma(k4, smoothD4)
```

Then, calculate the average value of each group of K lines and D lines to construct the fast line Kavg and the slow line Davg:
```pine
Kavg = avg(k,k1,k2,k3,k4)
Davg = avg(d,d1,d2,d3,d4) 
```

Finally, go long when the fast line crosses the slow line, and go short when it crosses below:
```pine
long = crossover(Kavg, Davg)
short = crossunder(Kavg, Davg)
```

By combining the standard deviation moving averages of multiple time periods, the market noise in larger time periods can be filtered out and the main trend direction can be locked.
## Strategic Advantages
- Utilize the prediction ability of multi-time period standard deviation to effectively filter noise and lock in trends
- By adjusting the cycle parameters, you can freely adjust the holding time of the strategy
- Standard deviation itself has strong trend tracking capabilities
- Using moving average crossover form can avoid being misled by a single fake breakout
- Can easily optimize the moving average period of fast and slow lines to improve stability
## Strategic risks and solutions
- Multi-time period moving average crossovers are prone to produce more false signals, and the moving average period can be appropriately adjusted for optimization
- Standard deviation is easily affected by violent market conditions and produces false signals. Consider adding filter conditions.
- Fixed cycle parameters cannot adapt to market changes, adaptive cycle settings can be used
- It is easy to chase the high and sell the low when holding a long-term position. You can set a trailing stop loss to lock in profits.
- Only considering the KDJ indicator is easily limited, other indicators can be introduced for combined optimization
Solution:
1. Add filter conditions to avoid being misled by short-term false breakthroughs
2. Use adaptive cycle settings to adjust cycle parameters according to market volatility.
3. Set a trailing stop loss to stop the loss in time to avoid chasing the high and killing the low.
4. Optimize the moving average cycle parameters and find the best balance point
5. Combine more indicator signals to improve strategy stability
## Strategy optimization direction
This strategy can be further optimized from the following aspects:
1. Introducing other indicator signals for combination, such as MACD, Bollinger Bands, etc., can improve signal quality
2. Add trend filtering, such as introducing SMA moving average direction, ADX and other indicators to determine the trend and avoid counter-trend trading.
3. Use adaptive cycle settings to dynamically adjust cycle parameters based on market volatility.
4. Add a trailing stop loss strategy, set the stop loss point according to the strategy parameters, and stop the loss in time
5. Optimize the moving average cycle parameters of fast and slow lines and find the best parameter combination
6. Add filter conditions for opening positions to avoid misleading signals by short-term noise
7. Try the Breakout entry strategy and open a position after breaking through the moving average.
8. Test different exit strategies, such as Chandelier Exit, optimize take profit and stop loss
## Summarize
The multi-time period standard deviation K-line crossover strategy integrates the trend tracking ability of the standard deviation indicator and the stability of the moving average strategy. By calculating the K-line and D-line averages of multi-period standard deviations and constructing trading signals, you can effectively utilize the predictive power of standard deviation indicators at different time scales to filter market noise and capture the main trend direction. This strategy has room for parameter tuning, which can be optimized by adjusting cycle parameters and further introducing filter conditions, stop-loss strategies, etc., to obtain better strategy effects. Overall, this strategy combines the advantages of a variety of technical analysis tools and is an efficient trend tracking strategy worth exploring and optimizing.
|| 

## Overview

The Multi Timeframe Stochastic Crossover Strategy is a typical trend following strategy. It calculates the standard deviation values across different timeframes (e.g. daily, weekly, monthly etc.), constructs multiple K and D lines, takes the average of these lines to build moving averages, and goes long when the fast line crosses above the slow line and goes short when the fast line crosses below the slow line. By combining standard deviation lines across multiple timeframes, this strategy can effectively filter out market noise and capture the predominant trend.

## Strategy Logic

The core logic of this strategy is to compute the standard deviation across multiple timeframes and then take the average to generate trading signals.

Firstly, the strategy calculates K values of standard deviation under different parameters across 5 groups, corresponding to daily, weekly and monthly timeframes:

```pine
smoothK = input(55)
SMAsmoothK = input(13)  
k = sma(stoch(price, high, low, smoothK), SMAsmoothK)

smoothK1 = input(89) 
SMAsmoothK1 = input(8)
k1 = sma(stoch(price, high, low, smoothK1), SMAsmoothK1) 

...

smoothK4 = input(377)
SMAsmoothK4 = input(2)
k4 = sma(stoch(price, high, low, smoothK4), SMAsmoothK4)
```

Then it computes D lines with different parameters respectively:

```pine
smoothD = input(34)
d = sma(k, smoothD)  

...

smoothD4 = input(233) 
d4 = sma(k4, smoothD4)
```

Next, it calculates the average of K and D lines to get the fast line Kavg and slow line Davg:

```pine 
Kavg = avg(k,k1,k2,k3,k4)
Davg = avg(d,d1,d2,d3,d4)
```

Finally, it goes long when Kavg crosses above Davg, and goes short when Kavg crosses below Davg:

```pine
long = crossover(Kavg, Davg)  
short = crossunder(Kavg, Davg)
```

By combining standard deviation lines across multiple timeframes, this strategy can filter out market noise in larger timeframes and capture the predominant trend direction.

## Advantages

- Utilizes predictive power of standard deviation across multiple timeframes to filter out noise and capture trends
- Flexibility to adjust holding period by tuning timeframe parameters  
- Standard deviation itself has strong trend following characteristics
- Moving average crossover avoids being misled by single fake breakouts
- Easy to optimize moving average periods for more stability

## Risks and Solutions

- Multiple timeframe moving average crossovers can generate many false signals, optimize moving average periods
- Standard deviation prone to errors from volatile moves, consider adding filters 
- Fixed periods cannot adapt to market changes, adopt adaptive periods
- Long holding periods risk chasing tops and bottoms, use trailing stops to lock in profits
- Reliance on just KDJ indicator is limiting, combine with other indicators

Solutions:

1. Add filters to avoid false breakout signals

2. Use adaptive periods based on market volatility

3. Employ trailing stops to exit trades timely

4. Optimize moving average periods for best balance

5. Incorporate more indicators to improve robustness

## Enhancement Opportunities

This strategy can be further improved in the following areas:

1. Incorporate other indicator signals like MACD, Bollinger Bands to improve signal quality

2. Add trend filters like SMA direction, ADX to avoid counter-trend trades  

3. Utilize adaptive periods based on market volatility

4. Implement trailing stops based on strategy parameters to exit trades

5. Optimize fast and slow moving average periods for best parameters

6. Add entry filters to avoid false signals from short-term noise

7. Test breakout entry after crossover of moving averages

8. Evaluate different exit strategies like Chandelier Exit to optimize exits

## Conclusion

The Multi Timeframe Stochastic Crossover Strategy combines the trend following capability of stochastic indicator and stability of moving average strategies. By taking average of multi-period standard deviation K and D lines to generate signals, it effectively utilizes predictive power of standard deviation across different timeframes, filters out market noise, and captures the predominant trend. This strategy has room for parameter tuning and further enhancements like filters, stops, etc. Overall, it integrates the strengths of multiple technical analysis tools and is an efficient trend following strategy worth exploring and optimizing.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1_close|0|price: close|high|low|open|hl2|hlc3|hlcc4|ohlc4|
|v_input_2|55|smoothK|
|v_input_3|13|SMAsmoothK|
|v_input_4|34|smoothD|
|v_input_5|89|smoothK1|
|v_input_6|8|SMAsmoothK1|
|v_input_7|55|smoothD1|
|v_input_8|144|smoothK2|
|v_input_9|5|SMAsmoothK2|
|v_input_10|89|smoothD2|
|v_input_11|233|smoothK3|
|v_input_12|3|SMAsmoothK3|
|v_input_13|144|smoothD3|
|v_input_14|377|smoothK4|
|v_input_15|2|SMAsmoothK4|
|v_input_16|233|smoothD4|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-09-23 00:00:00
end: 2023-10-23 00:00:00
period: 2h
basePeriod: 15m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=2
strategy(title="Slow Stochastic Multi K&D Average Crossover Strategy", overlay=false, pyramiding=0, calc_on_order_fills=true, initial_capital=100000, default_qty_type=strategy.percent_of_equity, currency="USD", default_qty_value=100)


price = input(close)

///////////////////////////////
smoothK = input(55) 

SMAsmoothK = input(13)
k = sma(stoch(price, high, low, smoothK), SMAsmoothK)



smoothD = input(34)
d = sma(k, smoothD)


///////////////////////////

smoothK1 = input(89) 

SMAsmoothK1 = input(8)
k1 = sma(stoch(price, high, low, smoothK1), SMAsmoothK1)

smoothD1 = input(55)
d1 = sma(k1, smoothD1)

//////////////////////////////////////

smoothK2 = input(144) 

SMAsmoothK2 = input(5)
k2 = sma(stoch(price, high, low, smoothK2), SMAsmoothK2)

smoothD2 = input(89)
d2 = sma(k2, smoothD2)

/////////////////////////////////////

smoothK3 = input(233) 

SMAsmoothK3 = input(3)
k3 = sma(stoch(price, high, low, smoothK3), SMAsmoothK3)

smoothD3 = input(144)
d3 = sma(k3, smoothD3)

////////////////////////////////////////////////

smoothK4 = input(377) 

SMAsmoothK4 = input(2)
k4 = sma(stoch(price, high, low, smoothK4), SMAsmoothK4)

smoothD4 = input(233)
d4 = sma(k4, smoothD4)

/////////////////////////////////////////////////

Kavg = avg(k,k1,k2,k3,k4, k4)
plot(Kavg, color=green)

Davg = avg(d,d1,d2,d3,d4, d4)
plot(Davg, color=red)


///////////////////////////////////////
hline(50, color=gray)


long = crossover(Kavg, Davg)// and d < 50
short = crossunder(Kavg, Davg)// and d > 50


last_long = long ? time : nz(last_long[1])
last_short = short ? time : nz(last_short[1])
long_signal = crossover(last_long, last_short) 
short_signal = crossover(last_short, last_long)



strategy.entry("Long", strategy.long, when=long_signal)
strategy.entry("Short", strategy.short, when=short_signal) 

//len1 = input(3)

//closelong = d[1] < k[len1]
//closeshort = d[1] > k[len1]

//strategy.close("Long", when=closelong)
//strategy.close("Short", when=closeshort)


```

> Detail

https://www.fmz.com/strategy/430042

> Last Modified

2023-10-24 14:44:00

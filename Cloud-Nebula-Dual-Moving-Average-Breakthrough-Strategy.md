
> Name

Cloud-Nebula-Dual-Moving-Average-Breakthrough-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/4c5339646bd0fe475a375e5b2eeebca114675302cf7d611bb780272028e65cf8.png)
[trans]

### Overview
The Yun Ni double moving average breakthrough strategy is a strategy that uses the fast moving average and the slow moving average to form a double cloud for breakthrough trading. This strategy features both trend following and reversal trading.
### Strategy Principles
This strategy calculates the 60-period high and low price EMA as the fast cloud and the 240-period high and low price EMA as the slow cloud. When the fast cloud is completely lower than the slow cloud, go long; when the fast cloud is completely above the slow cloud, go short. The specific entry rules are that you will enter the market when the price breaks through the upper or lower edge of the slow cloud, the stop loss is set at the highest and lowest price within 5 days, and the take profit is set to exit when the price breaks through the upper or lower edge of the fast cloud.
This strategy has both trend following and reversal trading characteristics. When the market is in shock, the fast cloud and the slow cloud fold in half, which is the time to reverse; when the fast cloud and the slow cloud are parallel, follow the trend and do trend trading.
### Advantage Analysis
1. The double cloud structure can effectively judge the market trend, and use the upper and lower crosses between the double clouds to do reversal transactions, greatly improving the winning rate.
2. The separation of fast cloud and slow cloud in the dual cloud structure is a signal of market changes, which provides us with potential opportunities.
3. Utilize crosses between clouds and price breakthroughs on clouds to make the strategy have the characteristics of trend following and reversal trading at the same time, taking into account the operation frequency and winning rate.
4. Using Yunyan as the stop loss and profit point can control risks well.
### Risk Analysis
1. When prices fluctuate violently, fast and slow clouds may cross frequently, resulting in multiple position adjustments and losses.
2. This strategy is more suitable for volatile market environments. In the trend market, there are many parallel situations of fast and slow clouds, and it is easy to get stuck.
3. During the consolidation period, there is a lack of effective methods to follow the trend, and it is impossible to grasp the opportunities for sharp rises and falls that may occur after consolidation.
### Optimization direction
1. The judgment of price channel and trading volume can be added before the cross of Shuangyun occurs to avoid false signals caused by violent price fluctuations.
2. Trend judgment indicators can be added to determine the direction of the general trend and selectively participate in reversal transactions when the fast and slow clouds separate upward and downward.
3. An adaptive algorithm with fast cloud width can be set to find the best parameter combination in both shock and trend market environments.
### Summarize
Yunni's double moving average breakthrough strategy comprehensively uses the advantages of fast moving averages and slow moving averages to build a double cloud system for reversal and trend trading. It has the characteristics of balancing operating frequency and winning rate, and can effectively grasp the changing rhythm of the market. By adding auxiliary judgment indicators and parameter optimization, the strategic advantages can be further expanded and better adapted to the complex and ever-changing market environment.
||


### Overview**

The Cloud Nebula Dual Moving Average Breakthrough Strategy is a strategy that utilizes fast moving averages and slow moving averages to form dual clouds for breakthrough trading. The strategy has the characteristics of both trend tracking and reversal trading.

### Strategy Principle

The strategy calculates the 60-period high-low price EMA as the fast cloud and the 240-period high-low price EMA as the slow cloud. When the fast cloud is completely below the slow cloud, go long; when the fast cloud is completely above the slow cloud, go short. The specific entry rules are that there are opportunities to enter when the price breaks through the upper or lower edges of the slow cloud. The stop loss is set at the highest and lowest prices within 5 days, and the take profit is set when the price breaks through the upper or lower edges of the fast cloud.

The strategy has both the characteristics of trend tracking and reversal trading. When the market is oscillating, the fold-over of the fast and slow clouds is an opportunity to make a reversal; when the fast and slow clouds are parallel, follow the trend to trade the trend.

### Advantage Analysis 

1. The dual cloud structure can effectively judge market trends, using the up and down crossovers between dual clouds to make reversal trades, greatly improving win rate.

2. The separation of the fast and slow clouds in the dual cloud structure is a signal of market change, which provides us with potential opportunities.

3. By using crossovers between clouds and price breakouts against clouds, the strategy has both trend following and reversal trading characteristics, balancing frequency of operation and win rate.

4. Using cloud edges as stop loss and take profit points can effectively control risks.

### Risk Analysis

1. During violent price fluctuations, frequent crossovers may occur between fast and slow clouds, leading to multiple losing positions.

2. This strategy is more suitable for oscillating market environments. In trending markets, there are often many parallel situations between fast and slow clouds, which can easily lead to being trapped.

3. Within consolidation periods, there is a lack of effective methods to follow trends, unable to capture potential major rallies or declines after consolidations.


### Optimization Directions

1. Price channels and trading volumes can be added before cloud crossovers occur to avoid false signals caused by violent price fluctuations.

2. Trend judgment indicators can be added. When separations between fast and slow clouds occur, judge the major trend direction and selectively participate in reversal trading. 

3. Adaptive algorithms for the width of the fast cloud can be set to find the optimal parameter combination in oscillating and trending market environments.


### Conclusion

The Cloud Nebula Dual Moving Average Breakthrough Strategy comprehensively utilizes the advantages of fast moving averages and slow moving averages to construct a dual cloud system for reversal and trend trading. It balances frequency of operation and win rate, and can effectively grasp the rhythm of market changes. By adding auxiliary judgment indicators and parameter optimization, the advantages of the strategy can be further expanded to better adapt to complex and ever-changing market environments.

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|60|Fast Cloud Length|
|v_input_2|240|Slow Cloud Length|


> Source (PineScript)

``` pinescript
/*backtest
start: 2023-12-14 00:00:00
end: 2023-12-19 00:00:00
period: 1m
basePeriod: 1m
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

// High Low Cloud Strategy Backtesting
// © inno14

//@version=4
strategy(title="High Low Cloud Strategy Backtesting", overlay=true, pyramiding=0)
c1=input(60, title="Fast Cloud Length")
c2=input(240, title="Slow Cloud Length")
c1_high=ema(high,c1)
c1_low=ema(low,c1)
highc1=plot(c1_high, title="Fast Cloud - High", color=color.blue, offset=0, transp=50, linewidth=1)
lowc1=plot(c1_low, title="Fast Cloud - Low", color=color.blue, offset=0, transp=50, linewidth=1)
fill(highc1, lowc1, transp=60, color=color.blue, title="Fast Cloud")
c2_high=ema(high,c2)
c2_low=ema(low,c2)
highc2=plot(c2_high, title="Slow Cloud - High", color=color.green, offset=0, transp=50, linewidth=1)
lowc2=plot(c2_low, title="Slow Cloud - Low", color=color.green, offset=0, transp=50, linewidth=1)
fill(highc2, lowc2, transp=40, color=color.green, title="Slow Cloud")
//Backtesting
//Long condition
ycloud_entry=
       c1_high<c2_low
       and crossover(close,c2_high)
       

ycloud_stoploss=
       crossunder(close,valuewhen(ycloud_entry,lowest(close[1],c2),0))

ycloud_takeprofit=
      c1_low>c2_high
      and crossunder(close,c1_low)


strategy.entry("Long", strategy.long, when=ycloud_entry)
strategy.close("Long", when=ycloud_takeprofit or ycloud_stoploss)

//Short condition
xcloud_entry=
       c1_low>c2_high
       and crossunder(close,c2_low)
       
xcloud_stoploss=
       crossover(close,valuewhen(xcloud_entry,highest(close[1],c2),0))

xcloud_takeprofit=
       c1_high<c2_low
       and crossover(close,c1_high)

strategy.entry("Short", strategy.short, when=xcloud_entry)
strategy.close("Short", when=xcloud_takeprofit or xcloud_stoploss)


//EOF
```

> Detail

https://www.fmz.com/strategy/436214

> Last Modified

2023-12-22 11:48:28

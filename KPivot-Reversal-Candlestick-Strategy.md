
> Name

Pivot-Reversal-Candlestick-Strategy
> Author

ChaoZhang

> Strategy Description

![IMG](assets/images/29443c7490fcb3cd741f6377d9ea4fa372c9fd31283059fc155424156bb89d1b.png)
[trans]

### Overview
The pivot reversal K-line strategy is a quantitative trading strategy that generates trading signals based on pivot points. This strategy determines the pivot area by calculating the highest and lowest prices of a certain number of K-lines on the left. When the price breaks through the pivot area, perform long or short operations accordingly.
### Strategy Principles
The core logic of this strategy is to calculate the highest price of the four K lines on the left as the long pivot, and calculate the lowest price of the four K lines on the left as the short pivot. The two K lines on the right are used to confirm that the price has broken through the pivot area. When the price exceeds the long pivot, go long; when the price is below the short pivot, go short.
Specifically, the strategy first calculates the highest price of the four K lines on the left `swh` as the long pivot. At the same time, calculate the lowest price `swl` of the four K lines on the left as the short selling pivot. After the pivot is determined, use the two K lines on the right to determine whether the price breaks through the pivot. If the price exceeds `swh`, go long; if the price is lower than `swl`, go short.
After long and short signals are issued, orders for long or short will be placed, and stop losses will be set outside the pivot area to control risks.
### Advantage Analysis
The biggest advantage of the pivot reversal strategy is its ability to seize the opportunity for price reversal. When prices are trading sideways for a long time, they often fluctuate near the pivot area. At this time, using the pivot breakout strategy can seize the best opportunity for price reversal and make a profit.
Compared with other reversal strategies, the pivot reversal strategy has the advantages of simple operation and controllable risks. The setting of the number of left and right K lines can be adjusted freely to adapt to different varieties and market environments. In addition, the stop loss is set outside the pivot area, which can effectively control risks.
### Risk Analysis
The main risk of the pivot reversal strategy is misjudgment of the pivot area. If the left K-line cannot determine a clear pivot area, the breakthrough of the right K-line may be a false signal. At this time, losses are likely to occur.
In addition, sudden changes in market conditions will also bring risks. Although a stop loss is set, if the market breaks, skips and other abnormal situations, the stop loss may not be able to play a good protective role.
To reduce risks, you can consider adopting a strategy of going long and short at the same time, that is, going long when prices rise and going short when prices fall, thereby hedging some of the risks. In addition, you can also combine other indicators to judge the market situation to avoid missing trading opportunities at possible reversal points.
### Optimization direction
This strategy can be optimized from the following aspects:
1. Optimize the setting of the number of left and right K lines. You can test more left and right K-line combinations to find the best parameters.
2. Add indicator filtering. You can add filters such as MA, MACD and other indicators when entering the market to avoid entering the market under uncertain circumstances.
3. Optimize stop loss setting. You can choose a better stop loss position based on the characteristics of different varieties.
4. Add trailing stop loss. After entering the market, you can use trailing stop loss to lock in profits instead of simply exiting with stop loss.
### Summarize
Pivot reversal strategies trade by timing price reversals in pivot areas. It has the advantages of simple operation and controllable risks. The main risk lies in identifying errors in pivot areas and sudden market changes. Risks can be reduced and strategy stability improved through parameter optimization, adding filters, and improving stop loss strategies. Generally speaking, the pivot reversal strategy is very suitable for capturing short-term trading opportunities in consolidation markets.
||

### Overview

The Pivot Reversal Candlestick Strategy is a quantitative trading strategy that generates trading signals based on pivot points. This strategy calculates the highest price and lowest price of a certain number of candlesticks on the left side to determine the pivot area. When the price breaks through the pivot area, it will initiate corresponding long or short positions.

### Strategy Principle  

The core logic of this strategy is to calculate the highest price of the left 4 candlesticks as the long pivot and the lowest price of the left 4 candlesticks as the short pivot. The right 2 candlesticks are used to determine if the price has broken through the pivot area. When the price exceeds the long pivot, go long. When the price falls below the short pivot, go short.

Specifically, the strategy first calculates the highest price `swh` of the left 4 candlesticks as the long pivot. At the same time, it calculates the lowest price `swl` of the left 4 candlesticks as the short pivot. After determining the pivot, it uses the right 2 candlesticks to judge whether the price breaks through the pivot area. If the price exceeds `swh`, go long. If the price is lower than `swl`, go short. 

After the long and short signals are triggered, it will place long or short orders and set the stop loss outside the pivot area to control risks.

### Advantage Analysis

The biggest advantage of the Pivot Reversal Strategy is that it can capture the timing of price reversals. When the price stays in a range for a long time, it often oscillates around the pivot area. Using the pivot breakout strategy at this time can capture the best timing of price reversals and make profits.

Compared with other reversal strategies, the Pivot Reversal Strategy has the advantages of easy operation, controllable risks, etc. The settings of left and right candlestick numbers can be freely adjusted to adapt to different products and market environments. In addition, with stop loss set outside the pivot area, risks can be effectively controlled. 

### Risk Analysis

The main risk of the Pivot Reversal Strategy is the incorrect judgment of the pivot area. If the left candlesticks cannot determine a clear pivot area, the breakout of the right candlesticks may be a wrong signal, which is likely to cause losses. 

In addition, sudden changes in trends can also bring risks. Although stop loss is set, if abnormal situations such as price gaps or skip happen, the stop loss may not provide good protection.

To reduce risks, we can consider adopting strategies of going both long and short at the same time, that is, go long when price rises and go short when price falls, to hedge some risks. We can also combine other indicators to judge trends and avoid missing trading opportunities at possible reversal points.

### Optimization Directions 

The strategy can be optimized in the following aspects:

1. Optimize left and right candlestick number settings. Test more combinations of left and right candlesticks to find the optimal parameters.  

2. Add indicator filters. Add filters like MA, MACD etc. when taking positions to avoid entering the market in uncertain situations.  

3. Optimize stop loss level settings. Choose better stop loss positions according to the characteristics of different products. 

4. Add trailing stop loss. After taking positions, trailing stop loss can be used to lock in profits, instead of simple stop loss exit.  

### Summary

The Pivot Reversal Strategy makes trades by capturing the timing of price reversals in pivot areas. It has the advantages of easy operation, controllable risks, etc. The main risks lie in the incorrect identification of the pivot area and sudden changes in trends. By methods like parameter optimization, adding filters, improving stop loss strategies, etc., risks can be reduced and the stability of the strategy can be improved. In general, the Pivot Reversal Strategy is very suitable for capturing short-term trading opportunities in range-bound markets.  

[/trans]

> Strategy Arguments



|Argument|Default|Description|
|----|----|----|
|v_input_1|4|leftBars|
|v_input_2|2|rightBars|


> Source (PineScript)

``` pinescript
/*backtest
start: 2022-12-08 00:00:00
end: 2023-12-14 00:00:00
period: 1d
basePeriod: 1h
exchanges: [{"eid":"Futures_Binance","currency":"BTC_USDT"}]
*/

//@version=3
strategy("Pivot Reversal Strategy", overlay=true)

leftBars = input(4)
rightBars = input(2)

swh = pivothigh(leftBars, rightBars)
swl = pivotlow(leftBars, rightBars)

swh_cond = not na(swh)

hprice = 0.0
hprice := swh_cond ? swh : hprice[1]

le = false
le := swh_cond ? true : (le[1] and high > hprice ? false : le[1])

if (le)
    strategy.entry("Long", strategy.long, comment="Long", stop=hprice + syminfo.mintick)

swl_cond = not na(swl)

lprice = 0.0
lprice := swl_cond ? swl : lprice[1]


se = false
se := swl_cond ? true : (se[1] and low < lprice ? false : se[1])

if (se)
    strategy.entry("Short", strategy.short, comment="Short", stop=lprice - syminfo.mintick)

//plot(strategy.equity, title="equity", color=red, linewidth=2, style=areabr)
```

> Detail

https://www.fmz.com/strategy/435465

> Last Modified

2023-12-15 10:17:49
